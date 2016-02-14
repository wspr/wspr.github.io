---
layout: post
title:  "SplitShow for dual-screen PDF presentations"
date:   2010-05-23 13:08:42 +1030
categories: tex
---

I’ve started lecturing recently in the area of Sports Engineering, which
is slightly outside my area of expertise but tremendous fun to jump
into. I’ve been asked to help out for around a third of the lecture
material which was previously being outsourced to a different course.
(I.e., the students went off and attended someone else’s lectures for a
few weeks.)

While the content I’ve been required to cover has been (roughly)
specified and prepared earlier, I wasn’t happy with using someone else’s
lecture material for my own use—it’s just much harder to work off
another’s slides. Considering my [sometime
pasttime](http://www.latex-project.org/), my tool of choice for creating
lecture material is the [beamer](http://latex-beamer.sourceforge.net/)
package for LaTeX.

Using any tool you’re comfortable with is great and I’ve enjoyed using
beamer, although I haven’t delved too far into making things pretty. I’m
mostly happy with the standard, plain-looking output.

<img src="splitshow/beamer-slide.png" border="1" width="400" />

However, one aspect of presenting from a PDF rather than from Keynote or
Powerpoint is a certain lack of in-presentation features such as a text
notes or a preview of the next slide. My preference when presenting is
to display to the audience a relatively spare amount of information and
use off-screen notes to remind myself what to say. That only works if
the notes can be displayed on a second screen, usually my notebook.

This isn’t really the sort of thing that a presentation based on PDF is
designed to do. But Beamer has a good solution for this problem: create
one double-length PDF page and set up the two displays to span the PDF
page across both displays. The content on the left half will be shown on
the main display viewed by the audience, and the right half is visible
to the presenter.

<img src="splitshow/splitshow1.png" border="1" />

Unfortunately, neither Adobe Reader nor Mac OS X’s Preview application
support a full-screen presentation mode that spans multiple displays. I
was at a bit of a loss until stumbling across the open source
application [SplitShow](http://code.google.com/p/splitshow/), which has
been written with the express purpose of presenting dual-screen PDF
documents from beamer.

![](splitshow/splitshow2.png)

SplitShow is absolutely essential for presenting beamer documents on Mac
OS X, and it works great. Thanks to those who contributed to the
project.

