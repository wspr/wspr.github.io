---
layout: post
title:  "fontspec missing font error"
date:   2011-02-27 13:08:42 +1030
categories: tex
---

<p>The latest version of fontspec now returns proper error messages when a font cannot be found:</p>

<pre><code>!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
./small.tex:6:
! fontspec error: "font-not-found"
!
! The font "Ggeorgia" cannot be found.
!
! See the fontspec documentation for further information.
! For immediate help type H &lt;return&gt;.
!...............................................

l.6 \fontspec{Ggeorgia}

? H
|'''''''''''''''''''''''''''''''''''''''''''''''
| A font might not be found for many reasons.
| Check the spelling, where the font is installed etc. etc.
|
| When in doubt, ask someone for help!
|...............................................
</code></pre>

<p>The wording might not be optimal, but having something to explain what&rsquo;s going on here has been missing for a long time!</p>

<p>The ASCII-art ‘design’ of these error messages comes from work we&rsquo;ve been doing in expl3 trying to make the console output a little more attractive. It&rsquo;s not an easy job working around TeX&rsquo;s idiosyncrasies here, but I&rsquo;m quite happy with the final result.</p>
