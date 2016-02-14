---
layout: post
title:  "fontspec in TeX Live 2010"
date:   2010-05-27 13:08:42 +1030
categories: tex
---

I have just gone through the always-slightly-worrying process of
submitting a new version of fontspec to CTAN. (There’s always more typos
and bugs you wish you could fix before you hit that “Upload” button.)

The new version is a major release, v2.0, representing quite a
significant internal update over the v1.18 release that’s been going
strong since, well, ages. There are quite a few minor problems that have
been squashed (especially related to various combinations of
font-loading features), and the code has been simplified and improved in
several areas. In particular, it now uses the expl3 programming
language, which I’ve been working on with the LaTeX3 project. It’s not a
complete port, however, so the package code is currently a big mish-mash
of TeX, LaTeX, expl3, *and*, yes, Lua code. Don’t look at the sources
unless you’ve got a strong constitution.

Unfortunately, the new v2.0 release has not been targeted towards fixing
all the bugs nor adding the features that have been requested and
discussed. (Interested parties should visit the [Issue
Tracker](http://github.com/wspr/fontspec/issues) for more information.)

So while some things have been fixed in the process of re-writing and
generalising (some of) the code, I haven’t managed to look at
everything. In particular, the documentation is in a significant state
of disrepair. There aren’t even any typeset examples, which I’m not too
happy about. But they’ll come.

The reason fontspec has been released now, specifically, is because TeX
Live 2010 has just gone into testing. Thanks to the efforts of Khaled
Hosny, Elie Roux, and Manuel Pégourié-Gonnard, fontspec is now fully
functional with the LuaTeX engine, which is slated to become the *de
facto* TeX engine in a few years time. Being able to easily select fonts
and OpenType features is a big step toward promoting
[LuaLaTeX](http://www.tug.org/mailman/listinfo/lualatex-dev) (as it’s
called) for more general use.

The new version of fontspec should still be fully functional in XeTeX
running on TeX Live 2009. There has not been a huge amount of testing
for the new release; I’d greatly appreciate any and all XeTeX users
reading this to try out the new package as soon as possible and report
problems back to me.

LuaTeX users, however, require some significant updates before fontspec
will work for them (involving
[luaotfload](http://github.com/khaledhosny/luaotfload) and post-TeX Live
2009 [LuaTeX binaries](http://luatex.org/download.html), specifically).
I recommend waiting for a refreshed testing version of [TeX Live
2010](http://tug.org/texlive/mirmon/) before trying out fontspec with
LuaTeX. I’ll be writing about some of the changes we’ve made for LuaTeX
users in the future.

While TeX Live 2010 is in testing, I’ve given fontspec v2.0 the
designation of “b1” to indicate it’s still under development. I hope
(ha!) that few changes will be required to the code while we’re testing
and the beta status can be dropped before TeX Live 2010 is completed.
After all that I’ll try and fix up the documentation.

In the meantime, I’m also planning to finally release my unicode-math
package as well. Stay tuned.

