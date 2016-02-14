---
layout: post
title:  "New version of pstool"
date:   2013-02-07 13:08:42 +1030
categories: tex
---


New version of pstool
=====================

<p>Somewhat to my surprise, I have a new version of <code>pstool</code> to release.
This is a LaTeX package I maintain that provide an easy workflow (I hope) for including <code>psfrag</code> graphics into pdfLaTeX documents.
This allows, say, graphs from Matlab or Mathematica to be presented with fonts matching your document and using macros defined in your main preamble.</p>

<p>For context below, here&rsquo;s a brief run-down of how it works.
As a graphic is requested in the main document (using <code>\psfragfig</code> or similar), a check is made whether it has been converted into PDF in a previous compilation (and the source graphic hasn&rsquo;t been updated in the mean time).
If so, it saves some time and simply loads that graphic.
If not, an entirely new LaTeX document is created with the preamble of the main document, but which otherwise contains only the graphic that needs to be processed.
This document is run through the regular (‘old-fashioned’) <code>latex</code> → <code>dvips</code> → <code>ps2pdf</code> compilation workflow, which performs the wanted <code>psfrag</code> substitutions (and any other PostScript-based processing) and the final figure is cropped to size.
Execution returns back in the main document and the PDF graphic can be inserted directly, and the compilation of the main document continues as normal.</p>

<p>The <code>pstool</code> package been invaluable to me in preparation of my PhD thesis, but I haven&rsquo;t had the opportunity to work on the code for a long time.
In fact, I discovered some code I&rsquo;d written for it from 2010 (see below) that I&rsquo;d never released to CTAN.
Why a new package now, then? Because I hate it when my code breaks and wastes people&rsquo;s time.</p>

<p><em>Windows ps2pdf breaking</em></p>

<p>Some time back, the maintainers of <code>ps2pdf</code> changed the way that options were passed on the command line under Windows, so where previously <code>pstool</code> was writing something like</p>

<pre><code>ps2pdf "-dPDFSETTINGS=/prepress" "foo.ps" "foo.pdf"
</code></pre>

<p>to generate the PDF file from the <code>psfrag</code>-generated PostScript file, the default settings were now terribly broken for recent users of MiKTeX, causing their documents to fail to compile. The syntax which now works correctly is</p>

<pre><code>ps2pdf -dPDFSETTINGS#/prepress "foo.ps" "foo.pdf"
</code></pre>

<p>Note <code>#</code> instead of <code>=</code> to set the options.
In order to fix the issue, I decided to separate the fix from the user-level interface to pstool, which can set <code>ps2pdf</code> options with syntax like</p>

<pre><code>\usepackage[
    ps2pdf-options={-dPDFSETTINGS=/prepress}
]{pstool}
</code></pre>

<p>Rather than requiring users to know to replace the <code>=</code> with <code>\#</code> (remembering that <code>#</code> is a special character than needs to be escaped), <code>pstool</code> automatically replaces all equals signs in the <code>ps2pdf</code> options with hash characters.
This provides some level of platform-independence so that documents will compile correctly whether on Windows, Linux, or Mac OS X.
Of course, it will still work correctly for Windows users that write <code>\#</code> anyway.</p>

<p><em>More robust preamble scanning</em></p>

<p>The second feature (and this is the code that was written in 2010 but never released) is a more robust scanning method for copying the main document&rsquo;s preamble into the preamble for each externally processed graphic.
In prior versions of the package, this was achieved by redefining <code>\begin{document}</code> but this method broke whenever a class or package did their own redefinition.
The command <code>\EndPreamble</code> was provided to manually indicate where the preamble should end, but users would usually run across the error and not know where to look to fix the problem.</p>

<p>The changes for this feature are all internal and shouldn&rsquo;t be noticeable if the code is working correctly; <code>\EndPreamble</code> still works for the cases where you don&rsquo;t need the entire document preamble to be replicated for each graphic.</p>

<p><em>Cross-references and citations supported</em></p>

<p>The third major change for the new version of <code>pstool</code> is to support cross-references and citations in externally-processed graphics.
This has been on my wish-list for some time, as I know that some people have used references and citations in their figures and graphs, and have had to use Rolf Niepraschk&rsquo;s <code>pst-pdf</code> (or my wrapper package <code>auto-pst-pdf</code>) in this case.
That solution is fine and perhaps still preferable in many cases, but if it could be done in <code>pstool</code> then I wanted to try and support it if possible.</p>

<p>It wasn&rsquo;t entirely straightforward, but I think it now works.
The short of it is: the main file&rsquo;s <code>.aux</code> and <code>.bbl</code> files are now copied over for each graphic&rsquo;s external compilation; the current page number is passed into the external graphic; and anything written to the <code>.aux</code> file by the external graphic is copied back into the main document&rsquo;s <code>.aux</code> file.
Copying the <code>.bbl</code> file is only necessary to support <code>biblatex</code> use, for reasons I&rsquo;m still not entirely clear on.</p>

<p>What does this allow us to do now?
If you have a document that defines several different equations and plots the results of those equations, it is possible to annotate the figure with the actual equation numbers cross-referenced from the document.
Or even include a citation in the graph for some method that was described in another paper.</p>

<p>However, there&rsquo;s a downside to all of this, which is that <code>pstool</code> graphics require multiple passes to resolve any cross-referencing.
And this is not possible to detect automatically (well, it may be theoretically possible but I don&rsquo;t think it&rsquo;s easy).
So the old approach of <code>pstool</code> to check the PDF and update the graphic only if necessary fails for those which use cross-references; in these cases, it is necessary to force their generation manually until everything resolves.
This can be done on a per-graphic level by using <code>\psfragfig*</code>, or on a document level by loading the package with the <code>[process=all]</code> option.</p>

<hr><p>This new version is still being <a href="https://github.com/wspr/pstool">tested on GitHub</a> (please check it out if you&rsquo;d like to help!) and I hope to upload it to CTAN in the next few days. I hope this release marks the beginning of somewhat of a return to the LaTeX community for me — last year was tumultuous for many reasons and I hope I can now re-dedicate some time every week.</p>

<p>Famous last words.</p>
