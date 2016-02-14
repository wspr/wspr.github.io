---
layout: post
title:  "A breqn for punishment"
date:   2014-06-11 13:08:42 +1030
categories: tex
---

<p>As an aside before I start work on belatedly fixing some of <code>unicode-math</code>&rsquo;s more pressing shortcomings, I&rsquo;ve also started work tidying up the <code>breqn</code> package: <a href="https://github.com/wspr/breqn">https://github.com/wspr/breqn</a></p>

<p>The <code>breqn</code> package was the brainchild of Michael J. Downes (of <code>amsmath</code> fame), and later updated by Morten Høgholm as part of his honours thesis. The package is explained in Michael&rsquo;s 1997 <a href="http://tug.org/TUGboat/tb18-3/">TUGboat article ‘Breaking Equations’</a>, and Morten&rsquo;s thesis is available online <a href="https://sites.google.com/site/mortenhoegholm/">if you know where to look</a> (I don&rsquo;t know how long it will be available there).</p>

<p>Since I have so much trouble keeping up with LaTeX work as it is, why would I take another package under my belt? In short, partly because <code>breqn</code> vastly alters the implementation of LaTeX mathematics, so I need to eventually know how to hook into it to properly support <code>unicode-math</code>. But also partly because of its heritage; such a promising piece of work shouldn&rsquo;t be neglected—I used <code>breqn</code> in my own PhD thesis, and while I could have done without it, once you start with <code>breqn</code> it is hard to go back to <code>amsmath</code>.</p>

<p>If you&rsquo;re interested, I need help generating test files; once they&rsquo;re sufficiently comprehensive I&rsquo;ll begin the process of translating the code into LaTeX3. Hopefully I can fix a bug or two along the way.</p>
