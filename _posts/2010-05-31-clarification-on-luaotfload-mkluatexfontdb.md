---
layout: post
title:  "Clarification on luaotfload & mkluatexfontdb"
date:   2010-05-31 13:08:42 +1030
categories: tex
---

<p>I <a href="http://latex-alive.tumblr.com/post/643148677/fontspec-for-luatex">recently covered</a> some of the details for running fontspec under LuaTeX.</p>

<p>As development continues while TeX Live 2010 is still under development, many details are still subject to change. In fact, I overlooked a recent feature of luaotfload that simplifies the whole process significantly.</p>

<p>I mentioned that before typesetting for the first time, and after installing fonts, it was necessary to execute the <code>mkluatexfontdb</code> script to keep the font cache database up to date. This will be configured in TeX Live 2010 to perform transparently by the luaotfload package. When a font is loaded that is not in the font cache, the script will be re-executed to check for added fonts. This brings the behaviour of font loading under LuaTeX much closer to that of how XeTeX functions.</p>

<p>The only downside for this approach is that the very first time that fontspec attempts to load a font, the LuaLaTeX compilation will pause for (up to) several minutes while the font cache is initialised. Subsequent compilations will not be affected.</p>

<p>Finally, users will still be able to execute <code>mkluatexfontdb</code> manually for debugging purposes (e.g., with the <code>-vvv</code> option). In Mac OS X, the LastResort.ttf font causes problems when attempted to be loaded by LuaTeX, and we explicitly ignore it; it&rsquo;s quite plausible there will be other such problematic fonts on other platforms that we need to deal with.</p>
