---
layout: post
title:  "Elliptic integrals in Matlab"
date:   2011-02-03 13:08:42 +1030
categories: matlab
---

In recent work, I was taking some equations out of a paper and needed to calculate <a href="http://en.wikipedia.org/wiki/Elliptic_integral">elliptic integrals</a> with parameter ranges outside the traditional. I hence stumbled into a world that I was only vaguely aware of and resolved to spend some time writing some Matlab code to help out others in my situation.

I didn't exactly get very far, but I've had a summer research student working on the problem for me—and while we haven't completely solved the problem, I hope what we've written is of some use to some one. The short of it is that if you need to calculate the complete or incomplete elliptic integrals in Matlab, you might find our <code>elliptic123</code> function <a href="http://code.google.com/p/elliptic/">here</a> to be useful.

The usual elliptic integrals you see are the incomplete elliptic integrals of the first, second, and third kinds, respectively, $$ F(\phi\vert m) $$, $$ E(\phi\vert m) $$, and $$ \Pi(n;\phi\vert m) $$. They are referred to as complete when $$ \phi=\pi/2 $$ and denoted as $$K(\phi)$$, $$E(\phi)$$, and $$\Pi(n; m)$$ in turn.

Of these, Matlab can calculate only $$ K(m) $$ and $$ E(m) $$ for parameter range $$ 0\le m\le 1 $$ using its <code>[K,E]=ellipke(m)</code> function.

It turns out that calculating $$\Pi(n;m)$$ is very easy, and it's a trivial task to extend Matlab's <code>ellipke</code> to calculate the third complete elliptic integral using the <a href="http://dlmf.nist.gov/19.8#E7">a faster-than-quadratically converging algorithm</a> involving the arithmetic-geometric mean.

However, calculating the incomplete elliptic integrals is a far more difficult task, and for this purpose we based our work on <a href="http://code.google.com/p/elliptic/">Igor Moiseev's work</a>; again his functions assumed small input ranges with $$ 0\le\phi\le\pi/2 $$, $$ 0\le m\le1 $$ and $$ 0\le n\le 1 $$. Using transformation formulae from the <a href="http://dlmf.nist.gov/19.7">DLMF</a> and other sources, we we able to extend these parameter ranges, in some cases, to be without bound.

The function we have written to do this can be called as

    [K, E] = elliptic123(m)
    [K, E, PI] = elliptic123(m,n)

in the complete case, and

    [F, E] = elliptic123(m,phi)
    [F, E, PI] = elliptic123(m,phi,n)

in the incomplete case.

The idea of this <a href="http://code.google.com/p/elliptic/source/browse/trunk/elliptic123.m"><code>elliptic123</code></a> function is to provide a wrapper around these transformation formulae and the standard methods for calculating the integrals, but we didn't achieve our goal of entirely unrestricting the input parameter ranges, as in Mathematica. (See the help text of the function for the exact ranges where our transformations failed.)

I believe the only way around these limitations is to implement the Carlson symmetry elliptic integrals and use them to calculate the traditional elliptic integrals, as has been done by <a href="http://fredrik-j.blogspot.com/2010/06/incomplete-elliptic-integrals-complete.html">Fredrik Johansson for mpmath</a>. His Python code could be ported to Matlab with too much difficulty, I think. Alas, I am out of time for this project.
