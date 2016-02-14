---
layout: post
title:  "Use of § in refstyle"
date:   2013-05-05 13:08:42 +1030
categories: tex
---

<p>I&rsquo;m a big fan of the refstyle package. (Before I knew it existed, I started writing something similar myself. I&rsquo;m glad I found refstyle before it was too late!)</p>

<p>The refstyle package automates the use of cross references; while vanilla LaTeX would have us write <code>Figure~\ref{xyz}</code>, this is written in refstyle as <code>\figref{xyz}</code>. Far more flexible and this syntax lends itself to many clever extensions such as referring to ranges of figures with <code>\figrangeref</code> or multiple individual ones using comma-lists. (And sections, and chapters, and equations, etc.)</p>

<p>From memory, The LaTeX Companion does not mention refstyle; I don&rsquo;t recommend the use of prettyref or fancyref these days, as they&rsquo;re both very limited in comparison. There is a rival to refstyle named cleveref which I have not used; it has been actively developed for a number of years and is worth checking out.</p>

<p>I&rsquo;ll talk about refstyle&rsquo;s syntax vs cleveref another day, perhaps. If we were to chose one of them to emulate for a LaTeX3 package, which would we choose? I do not know. We&rsquo;re not at that stage now, so I&rsquo;ll put off thinking about it.</p>

<p>What I do want to discuss here is the use of the section sign, §. By default,  writing</p>

<pre><code>see \secref{foo} for foo and we know about bar already (\secref*{bar}).
</code></pre>

<p>results in the output</p>

<blockquote>
  <p>see section §1 for foo and we know about bar already (§2).</p>
</blockquote>

<p>In this case, I&rsquo;m (ab)using the default appearance of the section sign to use <code>\secref*</code> as a ‘short reference’ that&rsquo;s nice and tidy within parentheses, while preferring to spell out ‘section’ explicitly in text within a sentence.</p>

<p>My PhD supervisor has pointed out to me, however, that writing ‘section §1’ is like writing ‘section section 1’ — not really the thing to do. Luckily refstyle provides hooks (namely, <code>\ifRSstar</code>) that allow us to define a reference that defaults to ‘section 1’ but shifts to ‘§1’ when the star form is used.</p>

<p>In the configuration file that defines the <code>refcmd</code> for sections, simply write</p>

<pre><code>refcmd  = {\ifRSstar\S\fi\ref{#1}},
</code></pre>

<p>and we&rsquo;re all set.</p>

<p>(At the same time, I switch all of the lowercase alternatives to uppercase so that cross-references are always ‘Section 1’ and so on — this is probably a regional preference.)</p>
