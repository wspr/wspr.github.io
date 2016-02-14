---
layout: post
title:  "KenKen in LaTeX etc."
date:   2011-02-23 13:08:42 +1030
categories: tex
---

<p>The latest issue of the PracTeX Journal (discl.: I used to be a production editor there some years back) contains a set of interesting challenges: typeset and <a href="http://tug.org/pracjourn/2010-2/distract.html">solve a KenKen puzzle</a>. I haven&rsquo;t seen this puzzle before; it looks fun for those of you who like this sort of thing. I encourage all with the time to attempt at least some of the problem—it looks fun!</p>

<p>In 2008 TPJ issued a similar challenge <a href="http://tug.org/pracjourn/2008-2/distract/">for Sudoku</a>. At the time I didn&rsquo;t think anyone would implement a complete Sudoku solution in TeX but I was astonished and happily surprised when <em>two</em> solutions were forthcoming.</p>

<p>It&rsquo;s good to remember that almost anything can be done in TeX macros if one tries hard enough. In this theme, my favourite example of ‘why not?’ when it comes to theoretically-possible but rather-quite-difficult problem solving in TeX is from the late Michael Downes&rsquo; series of ‘<a href="http://www.ctan.org/tex-archive/info/challenges/AroBend/">Around the Bend</a>’ problems. (Peter Wilson created a wonderfully typeset version available, in a TeX Live distribution at least, via ‘<code>texdoc AroundTheBend</code>’.) See chapters 10 and 11:</p>

<blockquote>
  <p>Using as few lines of TeX code as possible, set up an Around the Bend post containing a typical exercise so that it can be processed by plain TeX to (a) skip over the exercise text and (b) decode an embedded encoded answer.</p>
</blockquote>

<p>It&rsquo;s a fascinating idea to encode and decode text in TeX itself (of course with LuaTeX around now such ‘problems’ are little more than academic); as far as I know, however, such tools were never exploited for robust text passing to/from other formats. (E.g., inside PDF metadata where data should be encoded correctly.)</p>

<p>And surely everyone reading this has seen David Carlisle&rsquo;s <a href="http://www.tug.org/TUGboat/Articles/tb19-4/tb61carl.pdf"><code>xii.tex</code></a> before, right?</p>
