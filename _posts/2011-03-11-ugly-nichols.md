---
layout: post
title:  "Obtaining less ugly printed Nichols plots"
date:   2011-03-11 13:08:42 +1030
categories: matlab
---

<p>I'm unexpectedly teaching a course in system dynamics and PID control at the moment. In this course there is a somewhat complex display called a Nichols Plot, in which the log magnitude of an open loop transfer function (i.e., a complex function) is plotted against its phase, overlaid against contours of magnitude and phase of the closed loop dynamics. It's these contours that cause some grief.</p><p>Using the in-built commands in both Matlab and Mathematica (resp. <code>nichols</code> and <code>NicholsPlot</code>) produces quite useable interactive plots which can be queried and manipulated on-screen. Information can be selected and extracted by clicking and pointing, which is largely the intention of using these sorts of techniques.</p><p>But for generating course material (slides, assignments, exams) neither Matlab nor Mathematica offer sufficient (user-accessible) features to produce print-quality output. Here's the best I can do in Matlab:</p>

<img scr="nichols/matlab-nex.png" />

<p>Actually, disregarding the clipping problem at the bottom of this plot, this is pretty close to what I'd like to get. All I want is a way to control those contour lines — solid light grey looks far better especially near that 6dB contour — but my brief investigation into trying to customise them didn't get me very far.</p><p>And Mathematica is worse: (to be fair, Wolfram only recently added these plots to Mathematica so they're still immature)</p>

<img scr="nichols/mma-nex.png" />

<p>Frankly, the Mathematica output is largely unusable in print; contour labels are only visible on mouse-hover, which obviously is not suitable here; furthermore, these contour lines don't have any customisation options, and digging into Mathematica's internals for customising plots is even less fun than in Matlab. Finally, the tick labels need work so they snap to ±<em>n</em> 90°, which is yet something else that needs manual adjustment.</p><p>Here's my first attempt at something a little better in Mathematica. I'm out of time now to keep playing with it, but I think I'm on the right track; all that's missing is to omit the regions within the 6dB circle, etc. And then do the same thing in Matlab.</p>

<img scr="nichols/better-nex.png" />
