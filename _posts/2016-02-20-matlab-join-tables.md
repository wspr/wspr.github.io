---
layout: post
title:  "Matlab tables: loading and joining"
date:   2016-02-21 00:13:42 +1030
categories: matlab
---

A couple years back, Matlab added *yet another* datatype to its standard kernel.
This new datatype is called `table`, and it's like a cross between a cell and a
structure. It seems quite neat, in that it's easier to store metadata; apparently
this datatype is a spruced up version of something that's been available in the
statistics toolbox for some time. I wouldn't know; I avoid stats.

For some new work I thought it would be a good opportunity to try to learn
`table`. The very first thing that attracted me to it was its `readtable` function
to import CSV files in a sensible way; if you're like me you would have lamented
at various points that Matlab's built-in `csvread` is basically useless since it
only reads numbers.

An example is probably worthwhile. Say we have a CSV file that looks like:

    ,Mass,MassSigma,COM,COMSigma
    headneck,7.13,0.59,87.42,1.8
    trunk,46.49,1.61,69.31,0.7
    pelvis,11.17,0.94,49,5.6
    arm,3.73,0.28,43.8,7
    forearm,1.33,0.09,42.95,9.6
    hand,0.57,0.06,49.67,3.5

In a new-ish version of Matlab, we can now write `T = readtable('example.csv','ReadRowNames',true)` to receive

    T =
                      Mass     MassSigma     COM     COMSigma
                      _____    _________    _____    ________
        headneck       7.13    0.59         87.42     1.8
        trunk         46.49    1.61         69.31     0.7
        pelvis        11.17    0.94            49     5.6
        arm            3.73    0.28          43.8       7
        forearm        1.33    0.09         42.95     9.6
        hand           0.57    0.06         49.67     3.5

Note that the mix of strings and numbers have imported without trouble, and we
even have nice row and column headings. (Okay, I haven't shown a big mix of data types,
but trust me that it's more robust. It does seem like each column must be one data type, however.)
Accessing data in a `table` can be done in various
ways, for example: `T.Mass` gives an array of the mass column; `T{:,{'Mass','COM'}}`
extracts two columns; .`T{{'arm'},{'COM'}}` extracts that one value; and so on.

Having in-built metadata like this allows a number of powerful set-like operations
to be performed on tables, with new functions such as `intersect`, `setdiff`, and
so on. In addition, there's even an Excel-PivotTable-like `summary` command that takes the
data in a `table` and attempts to do some (simple) automatic stats on it.
Nice for data exploration.

Like for any new tool, learning `table` hasn't been without a few wrong turns and
dead-ends for me. Here's one of them.

## Dissimilar tables don't join

I have a number of variables that each contains a value for a set of parameters (`Rows`).
The rows are not (necessarily) the same for each variable, however.
I want to join the variables together so the results are all displayed in a single table.
E.g., I want to join these together: (drawn side by side to save space)

              Var_A                    Var_B
             ________                 _______
        a     0.36744            b    0.88517
        b     0.98798            c    0.91329
        c    0.037739            d    0.79618

Matlab provides three functions for joining tables; `join`, `innerjoin`, and `outerjoin`.
The obvious syntax doesn't work:

    A = table(rand(3,1),'VariableNames',{'Var_A'},'RowNames',{'a','b','c'})
    B = table(rand(3,1),'VariableNames',{'Var_B'},'RowNames',{'b','c','d'})

    try
      C = join(A,B)
    catch e
      disp(e.identifier)
      disp(e.message)
    end

This results in:

    MATLAB:table:join:CantInferKey
    Cannot find a common table variable to use as a key variable.


Okay, so maybe `join` isn't intended for this -- what about `outerjoin`? Its documentation sounds promising:

> *The outer join includes the rows that match between A and B, and also unmatched rows from either A or B, all with respect to the key variables. C contains all variables from both A and B, including the key variables.*

Well, `outerjoin` apparently can't be used with tables with row names!
(I just get nonsense because it needs a common variable to match against in each table.)
This is the closest I've found that does what I want, but seems to be against the idea of the `table` data structure to some degree:

    AA = table({'a';'b';'c'},rand(3,1));
    AA.Properties.VariableNames = {'param','Var_A'}

    BB = table({'b';'c';'d'},rand(3,1));
    BB.Properties.VariableNames = {'param','Var_B'}

    CC = outerjoin(AA,BB,'Keys',1,'MergeKeys',true)

This results in

    param     Var_A      Var_B
    _____    _______    _______

    'a'      0.10676        NaN
    'b'      0.65376    0.77905
    'c'      0.49417    0.71504
    'd'          NaN    0.90372

I.e., the `row` is just stored as a separate variable. This means it can't be indexed using "logical" notation such as `CC{'a',:}`.
But this can be fixed with:

    CCC = CC(:,2:end);
    CCC.Properties.RowNames = CC{:,1}

Which finally results in:

    CCC =

              Var_A      Var_B
             _______    ________

        a     0.4168         NaN
        b    0.65686     0.29198
        c    0.62797     0.43165
        d        NaN    0.015487

But is this really the best way to go about things? This seems like a pretty big edge case.

* * *

The joining of tables by taking their row names and turning them into variables
can be automated with the following function:

    function C = fakejoin(A,B)

    fake = {'FakeRowNames'};

    AT = array2table(A.Properties.RowNames,'VariableNames',fake);
    BT = array2table(B.Properties.RowNames,'VariableNames',fake);

    % these can't be inlined into outerjoin() for some reason!
    AV = [AT, A];
    BV = [BT, B];

    CV = outerjoin(AV,BV,'Keys',1,'MergeKeys',true);

    C = CV(:,2:end);
    C.Properties.RowNames = CV{:,1};

    return

One caveat to all this: I'm currently using Matlab 2015a, so some of this behaviour
may well have already changed and will soon.

I quite like the `table` data structure, but I feel (based on experiences like
this) that it's a little rough around the edges. Or perhaps I simply haven't
internalised its proper use cases yet, and I'm the weird one. Very possible.
