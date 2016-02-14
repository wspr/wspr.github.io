---
layout: post
title:  "Correct punctuation spaces"
date:   2010-07-18 13:08:42 +1030
categories: tex
---

<p>Who can remember when to use <code>\@</code> in a (La)TeX document? I thought I knew, but an exception caught me by surprise today.</p>

<p>In approximate detail, the idea of <code>\@</code> is to indicate when punctuation is or isn&rsquo;t ending a sentence. Why would you want to do that? By default, Plain TeX and LaTeX both have a feature whereby a little extra space is allowed after a sentence (whether a period or other punctuation mark) to help break the paragraph into lines. If you need a little extra space in this line, better to lump it after the period than add extra space between all the words.</p>

<p>This typesetting approach was very common (often to an exaggerated extent) in the 1800s and early 1900s but nowadays I think is less common. If you don&rsquo;t like it, write <code>\frenchspacing</code> in your preamble and you can forget about whether <code>\@</code> is ever required. However, when writing a LaTeX document for another source, such as a journal, it&rsquo;s polite to follow their style and include such niceties.</p>

<p>The canonical example for using <code>\@</code> is after abbreviations such as ‘<code>Prof.\@ Crumb</code>’. Without the <code>\@</code>, the space after ‘Prof.’ will be mistakenly enlarged—this is a common typographical mistake in (La)TeX documents.</p>

<p>Conversely, <code>\@</code> can also be used to indicate when a punctuation mark <em>should</em> end a sentence. By default, punctuation after a capital letter is assumed not to end a sentence (so you can write ‘<code>M. C. Escher</code>’ without the <code>\@</code>). But if you happened to refer to someone by their initial at the end of a sentence you&rsquo;d need to write, say,</p>

<pre><code>… `So he did', said M\@.  (New sentence) …
</code></pre>

<p>to ensure that the extra spacing <em>was</em> included after that final period.</p>

<p>I should also mention that I often don&rsquo;t use <code>\@</code> after punctuation in favour of typing an explicit space control sequence; that is, I prefer to write <code>Prof.\ Crumb</code>. This is shorter to type and perhaps more memorable.</p>

<p>Well, that&rsquo;s where the limits of my understanding finished until today. And then I wrote something like</p>

<pre><code>depending on the context of `a' and `b' (etc.) where …
</code></pre>

<p>Much to my surprise, the space after the ‘<code>(etc.)</code>’ was too large! Turns out that the space factor (which is the parameter governing when and where this extra space should appear) isn&rsquo;t ‘reset’ by the parenthesis and you need to write <code>(etc.\@)</code> instead.</p>

<p><strong>Update</strong>: Karl Berry gives another example:</p>

<pre><code>… `Et cetera et cetera etc.' said the King …
</code></pre>

<p>Here, there will be extra space after the closing quotes <code>'</code> (or <code>''</code>) that is incorrectly added due to the presence of the period; the closing bracket <code>]</code> is also ‘invisible’ to the space factor. His take on the matter:</p>

<blockquote>
  <p>Fixing end-of-sentence spacing (in one direction or the other) is one of the most common things we have to with TUGboat submissions.</p>
</blockquote>

<p><strong>End update</strong></p>

<p>The best idea in a case like this is to define a macro for inserting it all without your having to remember it; for example,</p>

<pre><code>\makeatletter
\newcommand\etc{etc\@ifnextchar.{}{.\@}}
\makeatother
</code></pre>

<p>where you would write ‘<code>(\etc)</code>’ or ‘<code>…, \etc, …</code>’ but if you wanted to finish a sentence with it, you would explicitly include the period:</p>

<pre><code>… \etc. (New sentence) …
</code></pre>

<p>I&rsquo;m continually learning about small details like this even though I&rsquo;ve been using TeX and friends quite closely for a number of years. It&rsquo;s important to keep one&rsquo;s eyes open.</p>
