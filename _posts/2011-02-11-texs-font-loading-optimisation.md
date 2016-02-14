---
layout: post
title:  "TeX’s font-loading optimisation"
date:   2011-02-11 13:08:42 +1030
categories: tex
---

<p>A user of Peter Wilson’s <code>fonttable</code> package reported an interesting bug in the interaction between it and the Spanish module (if not others) of <code>babel</code>.</p>

<p>Here’s the problem in a nutshell:</p>

<pre><code>\documentclass{article}
\usepackage[spanish]{babel}
\begin{document}
$\lim x_n$
{\font\x=cmr10\x hello}
$\lim x_n$
\end{document}
</code></pre>

<p>Can you see the problem? It certainly wasn’t immediately obvious to me.</p>

<p>I probably wouldn’t have had time to work through the problem (after all, it’s clearly <code>babel</code>’s problem, not <code>fonttable</code>’s) but the user that reported the problem had also tracked down the root of it already (thanks!). In Spanish, the maths operator <code>\lim</code> is written as ‘lím’, which requires the use (in 8-bit LaTeX) of an acute accent combined with a dotless ‘i’. And inside the definition for <code>\dotlessi</code> in <code>babel</code>’s Spanish module, you’ll find</p>

<pre><code>\expandafter\expandafter\expandafter
\split@name\expandafter\string\the\textfont\mathgroup\@nil
</code></pre>

<p>Note the <code>\split@name</code> command, which  takes an NFSS font name such as <code>OT1/cmr10/m/n/10</code> and split it into its components (resp.: encoding, family, series, shape, size). It’s operating on <code>\the\textfont\mathgroup</code> there, and this is where the problem comes from.</p>

<p>By default in a 10pt LaTeX document, <code>\textfont</code> is defined as <code>OT1/cmr10/m/n/10</code>.
In pseudocode, LaTeX originally calls something like this:</p>

<pre><code>\font \OT1/cmr10/m/n/10 = cmr10 at 10pt
\textfont\fam=\OT1/cmr10/m/n/10
</code></pre>

<p>(This would not execute without ‘<code>/</code>’ having <code>\catcode</code> ‘letter’.) The problem comes in when someone comes along and writes something like</p>

<pre><code>\font\x=cmr10 at 10pt
</code></pre>

<p>Because TeX does not want to load the same font more than once, it optimises its references to font names to point to the last name a specific font was requested with (here ‘font’ means ‘font face + size’).</p>

<p>At this point, the <code>\textfont</code> now points to <code>\x</code> instead of <code>\OT1/cmr10/m/n/10</code>, which causes <code>\split@name</code> to break pretty spectacularly. And this even happens if the font loading happens inside a group:</p>

<pre><code>\font\1=cmr10 at 9pt
{\font\2=cmr10 at 9pt}
\textfont\fam=\1
\showthe\textfont\fam
</code></pre>

<p>The above code returns ‘<code>\2</code>’, quite unintuitively. So what can be done about this problem? Let’s assume for now that we can’t change how <code>babel</code> does things (I don’t know the practicality of that in any event).</p>

<p>One way to avoid this problem occurring might be to dynamically check the current ‘values’ of <code>\textfont</code>, <code>\scriptfont</code>, etc., and then not reload the same font under a different name if it’s the same as the font you would like to load. This could be implemented in a wrapper around <code>\font</code> like <code>\newcommand</code> is around <code>\def</code>, and this might be something we look into for <code>expl3</code>.</p>

<p>A less general solution is to simply load the new font like this:</p>

<pre><code>\font\x=cmr10 at 9.9999pt
</code></pre>

<p>Because the font is technically at a different size (although the difference is imperceptible), TeX considers it a separate font and will no longer replace its old pointer to <code>\OT1/cmr10/m/n/10</code> with <code>\x</code>. (I also perform this trick in <code>unicode-math</code> to load the same font with different <code>\fontdimen</code>s for assigning to different math groups.)</p>

<p>This is certainly less robust than an explicit check, and will not always be an acceptable solution, but it’s simple to implement in <code>fonttable</code> and serves its purpose there quite well.</p>

<p>In conclusion, due to this fragility in <code>babel</code> (I don&rsquo;t know if it&rsquo;s the Spanish module only but it seems likely the problem could occur elsewhere), be careful loading certain fonts with <code>\font</code> unless you are confident it won’t also be used as a maths font. If possible, use the LaTeX font loading interface instead.</p>
