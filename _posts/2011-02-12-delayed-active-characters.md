---
layout: post
title:  "Delayed active characters"
date:   2011-02-12 13:08:42 +1030
categories: tex
---

<p>Funny problem in mathtools vs. francais babel. (Only a coincidence that I&rsquo;m debugging two babel problems back-to-back.)</p>

<p>Morten Høgholm&rsquo;s mathtools package has an option to turn the colon into an active character so that writing <code>:=</code> produces a colon-equals sign with a correctly centred colon. (Unicode mathematics provides a specific character for this symbol but the input shorthand is still a convenience.)</p>

<p>But babel&rsquo;s French module also has a feature with an active colon, and although both mathtools and babel can be otherwise used together without problem, these two features cannot both be active simultaneously. This is a documented problem, and a workaround requires changes to babel to allow hooks into its active characters. (Not going to happen any time soon, in other words.)</p>

<p>Despite the documented incompatibility, there was still something breaking when both packages were loaded, and even when the centred-colon feature was never activated. Turns out we were lazy in mathtools. (To be fair, this portion of the code originated in the depths of time on comp.text.tex.)</p>

<p>Active characters are interesting because they can be switched on and off by changing their catcode, and they remember their meaning the whole time. In mathtools, we were taking advantage of this by writing something like</p>

<pre><code>\begingroup
  \catcode`\:=\active
  \gdef:\fancycolon % not the actual defn.
\endgroup
</code></pre>

<p>and in the mathtools option processing, all we had to do to activate the centred-colon feature was to execute</p>

<pre><code>\catcode`\:=\active
</code></pre>

<p>and our previously saved definition automatically takes into effect.</p>

<p>Unfortunately, this is a rather inconsiderate way to do things, because it doesn&rsquo;t take into account the fact that other people (in this case babel) might also want to assign the colon an active meaning. If mathtools is loaded after babel, then the colon is overwritten even though the centred-colon feature is never activated!</p>

<p>There are a few ways that both mathtools and babel could behaviour more sensibly here. But when dealing with catcodes, such clashes are inevitable since there are so few ASCII characters and we always want to simplify the way we write our documents.</p>
