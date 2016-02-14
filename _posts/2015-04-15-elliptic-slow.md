---
layout: post
title:  "Elliptic integrals in Matlab: symbolic toolbox is slow"
date:   2015-04-23 13:08:42 +1030
categories: matlab
---
My real work in magnetics involves evaluating sometimes complex integrals that often result in solutions that include the elliptic integrals. These are a funny set of functions that I've <a href="https://wspr.wordpress.com/2011/02/03/elliptic-integrals-in-matlab/">discussed before</a>.

Matlab has historically only included the bare minimum here: in-built function to calculate the first and second complete elliptic integrals. Hence Igor Moiseev’s valuable work in this area (<a href="https://github.com/moiseevigor/elliptic">now moved to Github</a>).

Those with a variety of Matlab toolboxes, however, will usually run into the newish functions provided by the symbolic toolbox <code>ellipticF</code>, <code>ellipticE</code>, and friends. (Quite an impressive collection, actually.) However, if you actually wish to use these functions for something computationally intensive, such as numerical integration, it's a bad idea to use them. Why?

    >> tic; ellipticF(0.5,0.5), toc
    ans =
         0.5105
    Elapsed time is 0.020991 seconds.

That's a small fraction of a second — seems fast! But compare with Igor's native Matlab function:

    >> tic; elliptic12(0.5,0.5), toc
    ans =
         0.5105
    Elapsed time is 0.000705 seconds.

So the symbolic toolbox is fine if you just need to evaluate a value or two. But for anything iterative — and this holds for algorithms in general, not just for my own example of numerically integrating elliptic integral functions — you'll want to avoid the overhead of switching to the symbolic toolbox mid-calculation.

(This is an example of why I find Mathematica a more enjoyable computational environment; no alien toolboxes.)

