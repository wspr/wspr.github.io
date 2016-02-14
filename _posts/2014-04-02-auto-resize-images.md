---
layout: post
title:  "Auto-resize images that overfill a page"
date:   2014-04-02 13:08:42 +1030
categories: tex
---

<p>LaTeX&rsquo;s support for graphics through the graphicx package is reliable and works well, but occasionally I find its options somewhat limiting. One thing that often causes me to stop and immediately recompile a document I&rsquo;m working on happens when an image I&rsquo;ve inserted is poorly sized and takes up far more space than it should:</p>

<img src="micycle.png" />

<p>In these sorts of situations I&rsquo;ll immediately chuck in a quick <code>[width=\textwidth]</code> and merrily continue writing my document (or sometimes <code>[height=0.7\textheight]</code> in a <code>beamer</code> document, where vertical space is often compromised instead).</p>

<p>I&rsquo;ve often thought of writing some code that wraps around <code>\includegraphics</code> that would check whether the width or height of an included graphic was too large and shrink down the image if and only if necessary. Note that while it is possible to specify</p>

<pre><code>\usepackage{graphicx}
\setkeys{Gin}{width=\textwidth}
</code></pre>

<p>this has the side-effect of making <strong>all</strong> the graphics the width of the text — often just as disastrous when inserting smaller images. Furthermore, after setting this option globally, trying to write <code>height=&lt;whatever&gt;</code> will have unexpected consequences!</p>

<p>Luckily for me, the TeX community is wide and wonderful, and Martin Scharrer has already implemented what I&rsquo;m after (and more) in the <code>adjustbox</code> package. I&rsquo;ll leave you to digest the rest of the manual on your own, but here&rsquo;s a simple declaration in the preamble:</p>

<pre><code>\usepackage[Export]{adjustbox}
\adjustboxset{max size={\textwidth}{0.7\textheight}}
</code></pre>

<p>This enables the smart resizing that I&rsquo;ve always wanted without any change to the rest of the document — large images are resized down but small images are left as they are. There are also <code>max width</code> and <code>max height</code> options in case you do not wish to set both as in the above example.</p>

<p>This may sound like a small thing but I iterate quickly when writing lectures with <code>beamer</code>, where I often use images that need shrinking. Having such an unobtrusive method to automatically avoid doing this manually each and every time will save me perhaps not appreciably in time but certainly in brain space. Thanks Martin!</p>
