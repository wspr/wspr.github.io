---
layout: post
title:  "fontspec for LuaTeX"
date:   2010-05-29 13:08:42 +1030
categories: tex
---

As [previously
mentioned](http://latex-alive.tumblr.com/post/637156378/fontspec-in-tex-live-2010),
TeX Live 2010 will contain the first version of `fontspec` to support
LuaTeX.

This has been made possible by a partial port of the ConTeXt OpenType
font handling system by Khaled Hosny and Elie Roux in their `luaotfload`
package (links:
[CTAN](http://www.ctan.org/tex-archive/macros/luatex/generic/luaotfload/),
[Github](http://github.com/khaledhosny/luaotfload)). This package allows
users to load OpenType fonts in plain LuaTeX is much the same way as in
plain XeTeX:

    \font\tenrm="name:Adobe Garamond Pro:+onum" at 10pt
    \tenrm ...

Fonts may also be loaded by filename, as well.

    \font\tenrm="file:AGaramondPro-Regular.otf:+onum" at 10pt
    \tenrm ...

`fontspec` uses these features to provide the same interface in LuaTeX
for loading fonts for LaTeX use:

    \setmainfont[Numbers=OldStyle]{Adobe Garamond Pro} ...

**Important comment \#1:** Before `luaotfload` can load fonts by name as
in the example above, it must first create a database of installed fonts
in the operating system and in the TeX distribution. This performed by
executing the following script included with `luaotfload`

    mkluatexfontdb.lua

(Use the `--help` option for further info.) It will take a couple of
minutes the first time it is run, is quite fast to execute subsequently.
This script must be run whenever a font is added or removed from your
system. Work is ongoing to automate this process, but for now it still
requires manual attention.

------------------------------------------------------------------------

When using `fontspec` with XeLaTeX, it is usually recommended to load
the `xltxtra` package, which addresses some infelicities of LaTeX (and
related packages) to ensure the output using unicode fonts is as good as
it should be (or even working at all).

**Important comment \#2:** For LuaTeX, we’ve decided that there’s no
point requiring a separate package to do these things, so the core of
`xltxtra` has been simplified and included within `fontspec` itself. For
backwards compatibility, XeTeX users should continue to use the
`xltxtra` package, however.

Some parts of `xltxtra` have not been incorporated into `fontspec`
itself. The most important feature that has *not* been included is
automatic access to OpenType superscripts and subscripts. This feature
of `xltxtra` has caused several headaches over the years with problems
related to poor font support and conflicts with other packages that also
redefine sub/superscript commands (especially related to footnotes).
This feature will be released as a separate package in the near future.

------------------------------------------------------------------------

A similar philosophy has been taken with Ross Moore’s `xunicode`
package. This package defines LaTeX interfaces for a wide variety of
accents, accented letters, and symbols for unicode fonts. For example,
writing ’ `\"u` ’ to output ’ u ‘, and so on. This is the function that
is usually performed transparently (for 8-bit TeX fonts) by LaTeX’s
“font encoding” definitions. At the moment, `xunicode` is restricted to
running under XeTeX only. Therefore, for LuaTeX support, we have decided
(for now, at least) to incorporate the functionality of `xunicode`
within the unicode font encoding definition used by `fontspec` to load
its fonts (see the `euenc` package if you’re interested in the details).

This might be a decision we reverse or revisit later. But for now,
**important comment \#3** is to avoid loading the `xunicode` package
when using LuaTeX.

------------------------------------------------------------------------

TeX users are long accustomed to using shorthand ligatures to type
quotes and other punctuation while restricted to ASCII keyboard
characters. For example, writing ’ `---` ’ for an em-dash. In XeLaTeX,
the standard way to achieve this same behaviour was to load the
`tex-text` input mapping:

    \setmainfont[Mapping=tex-text]{...}

**Important comment \#4:** In LuaLaTeX, a different notation is used.
Instead, you must write

    \setmainfont[Ligatures=TeX]{...}

If you use the XeLaTeX syntax in LuaLaTeX, a warning will be issued but
the correct behaviour will still result. The new syntax
(`Ligatures=TeX`) is supported under XeLaTeX as well.

------------------------------------------------------------------------

In summary of the above, when using LuaLaTeX simply load fontspec
without any other packages:

    \usepackage{fontspec}

And remember to run `mkluatexfontdb.lua` to keep the font database in
sync.

------------------------------------------------------------------------

LuaTeX support for fontspec is very new and still undergoing
development. We might change the way some things currently work, and
there might still be rough edges in the current behaviours. Ongoing
development for LuaLaTeX is discussed on the [`lualatex-dev` mailing
list](http://www.tug.org/mailman/listinfo/lualatex-dev). Your feedback
with suggesting improvements and reporting bugs is greatly appreciated.

