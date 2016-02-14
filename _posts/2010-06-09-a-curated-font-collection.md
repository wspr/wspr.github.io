---
layout: post
title:  "A curated font collection"
date:   2010-06-09 13:08:42 +1030
categories: tex
---

<p>Here’s an off-the-cuff idea that I’d like to explore when I talk to people at TUG 2010.</p>

<p>Currently TeX Live basically includes any free font that anyone would like to upload to CTAN. There’s some good stuff there, dominated mostly by font designers within the TeX community itself.</p>

<p>With the growing popularity of web fonts using OpenType and the Lua(La)TeX engine able to use them for multilingual typesetting (plus of course Xe(La)TeX which has been doing the same thing for quite a few years now), it would be a great idea to start curating the fonts that CTAN and/or TeX Live carry.</p>

<p>I mean by this that the font collection as a whole could be coherently documented in terms of its OpenType feature coverage, range of designs offered for different alphabets, ability for typesetting languages, and so on. Furthermore, this documentation would be an excellent demonstration of what OpenType features can do (following on from the somewhat anaemic selection in the fontspec manual). In other words, a showcase of modern fonts and how LuaTeX- and XeTeX-based programs can exploit them.</p>

<p>The information used to build this documentation could be contained within a database that could be queried directly; for example:</p>

<pre><code>texfonts --lang=Farsi
</code></pre>

<p>would output a listing of fonts known to TeX Live that supported the Farsi language, and</p>

<pre><code>texfonts --style=sf --feature=onum
</code></pre>

<p>would list sans serif fonts with old-style figures. The extent to which this information would be shared amongst other programs such as <code>mkluatexfontdb</code> and fontspec itself I’ll leave to your imagination.</p>

<p>And obviously a cross-platform graphical interface to browse fonts using this information would be the icing on the cake. (I wonder if it could even be a web app to avoid having to mess around with building binaries.)</p>

<p>I would like to think that this would be good marketing for LaTeX and ConTeXt outside of their traditional roles in largely technical documentation and academic writing.</p>
