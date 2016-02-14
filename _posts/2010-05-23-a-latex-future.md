---
layout: post
title:  "A LaTeX future"
date:   2010-05-23 13:08:42 +1030
categories: tex
---

I’ve been thinking for a while that it would be a good idea to start
writing about what I'm doing related to my
various LaTeX activities. [Joseph Wright](http://www.texdev.net/) really
provided the inspiration with his cleverly-named website.

Right now, I’m somewhat-actively working in two major areas of LaTeX
development:
[LuaLaTeX](http://www.tug.org/mailman/listinfo/lualatex-dev) and
[LaTeX3](http://www.latex-project.org/). LuaLaTeX has been the great
work so far of Elie Roux, Khaled Hosny, and Manuel Pégourié-Gonnard,
with my contributions being to update my fontspec package sufficiently
for selecting fonts when using the LuaTeX engine. Fontspec was
originally written, of course, for font selection using XeTeX.

The work I’ve been doing with the LaTeX3 project has been rather more
speculative. While we’ve released now the expl3 bundle for
high(er)-level LaTeX programming and Joseph Wright has done a fantastic
effort rewriting and updating the main xpackages that have been released
so far, I see the long-term efforts of the LaTeX3 project as a way to
explore user interfaces for document design and authorship. This can be
seen as being completely orthogonal to the underlying programming
necessary to implement these sorts of ideas, but they obviously need to
be built from something. No-one knows whether that programming will
remain as pure LaTeX in the form of the expl3 bundle or will start
incorporating some Lua programming as well. From my point of view, it
really doesn’t matter, since expl3 is compatible with LuaTeX and whoever
is writing the code can use whatever is most comfortable to them.

The elephant in the room is my almost-finished [PhD
Thesis](http://github.com/wspr/thesis); my LaTeX work and my research
work have been at cross-interests (in terms of using up my time and
attention) for some time now.

My plan for the rest of the year is to finish my thesis and then
continue to earn some money part-time, primarily teaching in the school
of mechanical engineering where I’m currently spending most of my time.
This will give me the opportunity, with any luck, to work a couple of
full days a week on LaTeX activities and get some real work done in the
LaTeX world.

Let’s see how we go.

