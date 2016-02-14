---
layout: post
title:  "Improving documentation through the community"
date:   2010-10-04 13:08:42 +1030
categories: tex
---

<p>While I&rsquo;m technically spending as little time as possible on TeX development at the moment, I&rsquo;m still keeping an eye on things around the place. (In some cases, having to fix bugs comes as a rather time-critical priority now that users are updating very frequently with tools such as <code>tlmgr</code> or MacTeX&rsquo;s ‘TeX Live Utility’.)</p>

<p>Over on the TeX branch of Stack Exchange (still yet to be named, although I favour ‘overfull-hbox.com’), I&rsquo;m currently experimenting with a way to replace my current lack of attention on my documentation with community-contributed material.</p>

<p>The background to this is that LuaTeX&rsquo;s font loading through <code>luaotfload</code> allows OpenType fonts to be augmented at load time with new features and updated information such as kerning. I&rsquo;d love to be able to document this feature properly in fontspec, but the problem is that I don&rsquo;t have time to learn about it and write it up in the detail that it deserves. So I&rsquo;ve opened up a question on StackExchange asking how to do this (<a href="http://tex.stackexchange.com/q/3602/179">‘changing kerning of a font in LuaLaTeX’</a>) with the request that the answer come in the form of a patch to the fontspec manual.</p>

<p>I don&rsquo;t know if anyone&rsquo;s going to reply, but there&rsquo;s a bounty of 400 reputation points going for it if anyone does. (You get 10 reputation points for each upvote on a question or answer you post on the site). The reputation system is an indicator of your participation on the site, so the reward is essentially just good karma — but I hope this can perhaps be a useful way to muster the community so that users who otherwise might not be able to contribute with the code can still help out with the non-technical aspects of putting together a package. You&rsquo;d be surprised how long it takes to write good documentation!</p>
