---
layout: post
title:  "Lucida Math OpenType"
date:   2011-09-05 13:08:42 +1030
categories: tex
---

![](lucida-math.png)

As part of the next incarnation of the Lucida typefaces, I’ve been
testing out the OpenType versions of the maths fonts.

It’s fair to say that most people will have seen a Lucida font in one
form or another. Lucida has been very popular in the past as one of the
very few commercial and unique maths fonts for TeX. It is a super-family
of fonts with more font faces than I’m aware of in any other such
collection, including serif, sans serif, typewriter, script,
blackletter, handwriting, casual, fax (a sturdier serif), and symbols or
wingdings. It has been distributed very widely on various computer
systems, with Lucida Grande used in Mac OS X itself (the menu font,
among other uses), and Java and Windows shipping the standard
serif/sans/mono trio for many years.

For more information about the Lucida fonts and their new release, Ulrik
Vieth and Mojca Miklavec have just published a TUGboat paper with [all
the gossip](https://www.tug.org/members/TUGboat/tb32-2/tb101vieth.pdf).
(Link accessible for TUG members only until it becomes open access in
one year.) Further information can also be found on TUG’s own [site for
the font](http://www.tug.org/store/lucida/designnotes.html) and [an
overview of the
fonts](http://mysite.verizon.net/william_franklin_adams/lucida.txt)
written by the font designers, Charles Bigelow and Kris Holmes.

Due to my particular interest in [Unicode
maths](http://www.ctan.org/pkg/unicode-math), I’m especially excited to
see a new OpenType maths font on the scene. I like to think that we’re
entering into somewhat of a golden age of maths font design, as OpenType
provides a mechanism by which both TeX users and GUI apps such as
Microsoft Word can use them; in times past, it was simply rarely worth
the expense of creating a new TeX maths font and this is evident by the
relative paucity of them.

After the Lucida release later this year, available OpenType maths fonts
will include:

-   Latin Modern Math (1347)
-   XITS Math (2428)
-   Cambria Math v1.0 (1592)
-   Lucida Math (1947)
-   Lucida Math Demibold (877)
-   Asana Math (2240)
-   Neo Euler (411)

shown with approximate symbol counts for each font (based on symbols
defined in `unicode-math`, *not* by literal glyph count). The STIX fonts
are the reference, here, and contain the largest number of symbols; I
believe recent versions of Cambria Math have more than is listed above.
But what is impressive to see is that not only does Lucida have a large
glyph coverage already, but it will also be provided with a ‘bold’
version of the font as well and, as far as I know, will be the first
OpenType maths font to offer this.

To facilitate the use of the bold font, `unicode-math` can now load
multiple maths fonts simultaneously through LaTeX’s `\mathversion`
command (although this new feature hasn’t been widely tested), which is
shown in the image above. Note in the image above the integral sign for
the bold example isn’t scaling yet; this will be rectified of course for
the release version of the fonts.

I’m very pleased to be able to play whatever small role I can in
bringing these fonts to new audiences. Many thanks to Charles Bigelow
and Kris Holmes for working on the new fonts and everyone involved in
the OpenType transition but particularly the seemingly tireless Khaled
Hosny. Great work!

