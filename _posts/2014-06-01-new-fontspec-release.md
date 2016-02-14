---
layout: post
title:  "New fontspec release"
date:   2014-06-01 13:08:42 +1030
categories: tex
---

<p>Major releases of fontspec don&rsquo;t happen too often:</p>

<pre><code>v2.1   2010 / 09
v2.2   2011 / 09
v2.2b  2012 / 05 ("TeX Live 2012")
v2.3   2013 / 02
v2.4   2014 / 06
</code></pre>

<p>The new version on its way to CTAN now is the largest in a long time; I&rsquo;m happy to report that a couple of long-standing and significant bugs have been squashed. (Of course, I may well have spawned a few more…)</p>

<p>This release happened because of a one bug in particular, involving the poor (or rather non-existent) interaction between <code>SizeFeatures</code> and the shape options such as <code>ItalicFeatures</code>. I&rsquo;d known about it for years and years, gnawing away in the background, and I knew it wasn&rsquo;t exactly a trivial fix—my code had simply not been written cleanly with these two interacting features in mind.</p>

<p>It shouldn&rsquo;t be a secret that I haven&rsquo;t had much time for LaTeX programming over the last few years now, and fixing up fontspec, the package that got me into this whole mess in the first place, turned out to be a good way to re-engage somewhat with my old flame.</p>

<p>Turns out after reading through the code again, summarising what was going on, and heavily re-factoring, the bug I was trying to fix turned out to be fairly easy to resolve. All it needed was some time and attention. But while looking through my old code and old bugs, I managed to squeeze in a few new features at the same time.</p>

<p>One particular change that I&rsquo;ve made that I want to discuss is the position of the optional arguments. For the last decade, fontspec has asked its users to write</p>

<pre><code>\setmainfont[
  Ligatures = TeX ,
  Extension = .otf ,
  UprightFont = *-regular ,
  ...
]{texgyrepagella}
</code></pre>

<p>to select a font. First of all, <code>Ligatures=TeX</code> is now <em>default</em> when using either <code>\setmainfont</code> or <code>\setsansfont</code>. This is something I&rsquo;ve wanted for a long time.</p>

<p>Secondly, it&rsquo;s always seemed awkward to me to have the mandatory argument hanging on the end of <code>\setmainfont</code> like that—somewhat forgotten, and strangely unbalanced (the most important detail is left &lsquo;til last).</p>

<p>I realised that with xparse, it was trivial to add a new interface to fontspec:</p>

<pre><code>\setmainfont{texgyrepagella}[
  Ligatures = TeX ,
  Extension = .otf ,
  UprightFont = *-regular ,
  ...
]
</code></pre>

<p>I&rsquo;m worried this may cause some minor issues if people have ever written something like:</p>

<pre><code>\newcommand\foofont{\fontspec{foo}}
\foo [uh oh]
</code></pre>

<p>but until people contact me about this particular problem, I&rsquo;m going to assume people <em>haven&rsquo;t</em> been writing this—after all, this is what <code>\newfontfamily</code> is for. I can always revert the change if there is any pain, and for me the new interface is far, far more palatable.</p>

<p>I&rsquo;m not going to spend any more time discussing new features; you can read about them below (transcribed from the readme). Please let me know via the <a href="https://github.com/wspr/fontspec/issues/">Issue Tracker</a> if you come across any problems or have further suggestions to make.</p>

<p>I&rsquo;m aware this doesn&rsquo;t resolve everything on my todo list, but I have some pressing bugs in unicode-math to attend to next.</p>

<h2>Release notes for v2.4</h2>

<ul><li><p>Significant change to the user interface: instead of <code>\setmainfont[features]{font}</code>, you now write <code>\setmainfont{font}[features]</code>.
 Backwards compatibility is of course preserved.</p>

<p>The reason for this change is to improve the visual comprehension of the font loading syntax with large numbers of font features.</p></li>
<li><p>Defaults for symbolic font families like this can now be specified with</p>

<pre><code>    \defaultfontfeatures[\rmfamily]{...}
</code></pre>

<p>or</p>

<pre><code>    \defaultfontfeatures[\headingsfont]{...}
    \setfontfamily\headingsfont{...}
</code></pre></li>
<li><p>New <code>PunctuationSpace=WordSpace</code> and <code>PunctuationSpace=TwiceWordSpace</code> settings, intended for monospaced fonts; these force the space after a period to be exactly one or two spaces wide, respectively, which preserves character alignment across lines.</p></li>
<li><p>The features above now allow changes to the default settings:</p>

<ul><li><code>Ligatures=TeX</code> is enabled by default with <code>\setmainfont</code> and <code>\setsansfont</code>.</li>
<li><code>WordSpace={1,0,0}</code> and <code>PunctuationSpace=WordSpace</code> are now enabled by default for <code>\setmonofont</code> to produce better monospaced results.</li>
<li>(These can be adjusted by created your own <code>fontspec.cfg</code> file.)</li>
</ul></li>
<li><p><code>SizeFeatures</code> can now be nested inside <code>ItalicFeatures</code> (etc.) and behaves correctly. This has been a very long overdue bug!</p></li>
<li><p>New feature <code>NFSSFamily=ABC</code> to set the NFSS family of a font to “<code>ABC</code>”. Useful
 when other packages use the <code>\fontfamily{ABC}\selectfont</code> interface.</p></li>
<li><p>New feature <code>FontFace = {series}{shape}{font}</code> allows a font face to be loaded with a specific NFSS font series and font shape.
 A more verbose syntax allows arbitrary font features as well (and this also plays nicely with <code>SizeFeatures</code>):</p>

<pre><code>    \fontspec{myfont.otf}[
      FontFace = {b}{ui}{Font = myfont-bui.otf, &lt;features&gt;} ,
    ]
</code></pre>

<p>The code above, for example, will allow a bold upright italic font to be selected using the standard NFSS interface:</p>

<pre><code>    \fontseries{b}\fontshape{ui}\selectfont
</code></pre></li>
<li><p><code>\defaultfontfeatures+</code> (note the <code>+</code>) can now be used to append to the default font feature set.</p></li>
<li><p>Setting the <code>SmallCapsFont</code> using the <code>*</code>-replacement notation has been improved/fixed.</p></li>
</ul>
