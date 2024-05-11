---
layout: post
title:  “Howto Python with forked sankey package"
date:   2024-05-11 20:21:23 +0930
categories: python 
---

Over summer (a few months back) I finally started to learn Python in more detail. What started as a few bits and pieces to play around with my bank’s REST API ended up as a fork of a popular visualisation library that I built more features into:

https://github.com/AUMAG/ausankey

This package draws so-called Stanley diagrams like this:

<img src=“../img/ausankey.png” />

Compared to what I’m familiar with (mostly Matlab and Lua), it’s been interesting to see what is similar and what is different. I like the OOP approach and the broad set of datatypes that Python and modules like NumPy and Pandas provides. On the hand, there is a lot to wrap your head around in the Python ecosystem, and the complexity of having different approaches (and even competing approaches) adds some mental overhead for a beginner. 

Anyway, back to the visualisation package itself. My changes were intended to modularise the code, add (many) more configuration options, and wrap it up nicely so I could also get some experience with the Python packaging ecosystem. This involved a lot of fun getting ruff to like me. 

To do this the main elements of the repo that I set up were:

* Hatch as the build system (in hindsight I wonder if a build system with more critical mass would have been safer — I believe Hatch is newer and only maintained by a solo/small team)
* GitHub actions for lint/CI/release to PyPi (I had previously set up Travis and this went well)
* Documentation with mkdocs and Github Pages (I miss LaTeX for authoring but can’t argue with the accessibility of the online docs)
* (Some) unit tests — these are a bit challenging because a lot of the code is focused around visual output

I’m particularly happy with the documentation approach, as the GitHub action generates the images dynamically. Good package documentation is something I feel very strongly about, coming from the TeX ecosystem. 

Finally, another key element of this whole project was that I did all of it on iOS, mainly on iPhone. Once the pain of setting up the GitHub actions was out of the way, this has worked surprisingly well. I jump between Textastic as my main code editor, Pythonista as my main Python IDE for running examples/test scripts, Working Copy for version control and light editing tasks, and the GitHub app for monitoring actions. 

This makes Python by far the easiest language I know of for teaching and playing around with — even someone without a PC can jump right in and do quite a lot. I wouldn’t want to tackle a larger programming exercise in the same way, but I managed to take this much further than I expected. Okay, part of that was just proof of concept — is it possible? Turns out yes — but the other part was that I have my phone on me most times. I could grab a coffee and fix a bug in my code. Sitting down at a computer feels more like a chore these days (blame work!!) and this brought back a lot of the fun of tinkering on a computing device. 

Now I wish I had similar workflows set up for my LaTeX code.