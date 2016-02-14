---
layout: post
title:  "Upright pi with mathpazo"
date:   2010-06-15 13:08:42 +1030
categories: tex
---

<p>A friend of mine asked if it were possible to define an upright pi to use to represent the constant number pi. ISO standards recommend this as well as upright i and e for their respective mathematical constants, but it’s not common to see the upright pi due to the constraints of most maths fonts.</p>

<p>I’m not aware of a general solution to accessing an upright pi (until <a href="http://latex-alive.tumblr.com/post/665558008/unicode-math-in-a-picture">unicode-math</a> becomes more widespread), but luckily in this case we were working with the Palatino-based mathpazo fonts. Palatino was designed by Hermann Zapf, who also designed the upright maths font Euler; like most of HZ’s fonts, these two harmonise very well together. So we can take Euler’s upright pi to use in our otherwise Palatino-based Greek alphabet.</p>

<p>(Disclaimer: I actually don’t know the origins of the Greek mathpazo letters; they may in fact not be based on any font designed by HZ himself but simply drawn to match the Palatino clone used in the mathpazo package.)</p>

<p>This is performed in LaTeX with the following invocation:</p>

<pre><code>\usepackage{mathpazo}
\DeclareSymbolFont{euler}{U}{eur}{m}{n}
\DeclareMathSymbol \uppi \mathalpha {euler} {"19}
</code></pre>

<p>You may then use <code>\uppi</code> to obtain an upright pi symbol:</p>

<p><img src="uppi.png" border="1" /></p>

<p>If you would prefer to replace the original definition of <code>\pi</code>, write instead </p>

<pre><code>\DeclareMathSymbol \pi \mathalpha {euler} {"19}
</code></pre>

<p>and all pi symbols in the document will be typeset with the upright glyph. I wouldn’t anticipate most readers being able to distinguish the difference between these pi glyphs, so I suggest using discretion in mixing the two.</p>

<hr><p>If you would also like to replace the default e and i glyphs by their upright shapes from the Euler font, write as well </p>

<pre><code>\DeclareMathSymbol {e} \mathalpha {euler} {`\e}
\DeclareMathSymbol {i} \mathalpha {euler} {`\i}
</code></pre>

<p>and you will receive:</p>

<p><img src="upeipi.png" border="1" /></p>

<p>Disregarding the nonsense maths, I like it.</p>
