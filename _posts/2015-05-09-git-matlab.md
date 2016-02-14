---
layout: post
title:  "Git support in Matlab"
date:   2015-05-09 13:08:42 +1030
categories: matlab
---

I have a love/hate relationship with Matlab, the details of which I probably obliquely mention here from time to time. The biggest reasons that I stick with Matlab are (a) I have to teach my students to use it, and (b) for all its warts, its IDE is quite nice for code authoring/debugging, exploring data sets, and even drawing somewhat sophisticated 3D diagrams.

I've just installed Matlab 2015a on my laptop, and am pretty happy to also see that Matlab now supports Git: (this appears to have been added in 2014b, so I'm a little behind the times)

<img src="matlab-git.png" alt="Screen Shot of Git support in Matlab" />

I usually use a lightweight GUI to perform simple Git operations (GitX on Mac) and the command line for anything more sophisticated. Most common Git operations can be performed from a clunky interface that involves right-clicking on a file, selecting "Source Control" from the menu, and then selecting from a list. Rather like TortoiseGit on Windows, I guess. There are a few impedance mismatches, such as the term "Compare to Ancestor", which is Matlab's version of performing "git diff" to see what you've changed in the current file. I think trying to abstract multiple version control systems under a consistent set of Matlab commands is probably a recipe for disaster, long term, but I can understand the motivation.

I like that the Git status is indicated in the file listing, but I suspect I'll rarely, if ever, use the Matlab interface to actually perform source control. I'm a little disappointed that there isn't a better user interface than delving into contextual menus and receiving little more than plain info in pop-up windows. For example, what I'd like to see would be to double click a "changed" icon (blue square in the above screenshot), which would show the current differences from the last commit, and an integrated text field and nice big button to commit the changes. Not as easy, but more likely to get keep people within Matlab.

What I'm really hoping Git support in Matlab makes it possible to slowly introduce my undergraduate students to Git (engineers learning source control is a subject I hope to discuss another time), and perhaps more importantly I hope it will help facilitate collaboration with research students that work on my code. Fingers crossed.


