---
layout: post
title:  "The asymptote LaTeX package"
date:   2010-10-18 13:08:42 +1030
categories: tex
---

<p>John Bowman has just announced <a href="http://sourceforge.net/projects/asymptote/forums/forum/409349/topic/3901078">version 2.05 of Asymptote</a>, a 3D programmatic drawing package that uses TeX for typesetting its labels. Asymptote is unique in its ability to generate 3D graphics that can be rotated and zoomed within Adobe Reader, allowing far more interactive graphics for scientific documents.</p>

<p>John has written several TUG papers on Asymptote over the last few years; the latest was for the <a href="http://tug.org/TUGboat/Contents/contents31-2.html">TUG 2010 conference</a> held earlier this year in San Francisco (the video of John&rsquo;s presentation is available on <a href="http://river-valley.tv/interactive-tex-aware-3d-vector-graphics/">River Valley TV</a>). I had the great pleasure of meeting John at the conference; amongst other things we discussed some improvements I had in mind for the LaTeX package for including Asymptote graphics within a document.</p>

<p>After the conference I foolishly went over the package and re-wrote much of it in the DocStrip format to better document the internal behaviour of the code. Unfortunately—hence the ‘foolishly’—many bugs were introduced in the process when my new code smoothed over edge cases that it shouldn&rsquo;t have—but it&rsquo;s now finally working and included in the main Asymptote distribution. The package source is now more modern and better documented (available in the file <code>doc/asy-latex.dtx</code> in the Asymptote distribution), which should help with maintenance in the long run.</p>

<p>The main reason for the re-write was to add the feature to be able to include graphics defined in external files; before, graphics had to be included inline in the form</p>

<p><code>\begin{asy}</code><br/>
    <em>asy graphics code</em><br/><code>\end{asy}</code></p>

<p>The new version of <code>asymptote.sty</code> allows you to write</p>

<p><code>\asyinclude{</code><em>myfig.asy</em><code>}</code></p>

<p>where the <em>asy graphics code</em> is now placed in the file <em>myfig.asy</em>. This can be useful when you wish to re-use an Asymptote graphic between multiple files or if you just like to keep your document source as minimal as possible.</p>

<p>Thanks to John for his patience in testing the packages as bugs were fixed and yet more bugs were discovered. It&rsquo;s been great to work together.</p>
