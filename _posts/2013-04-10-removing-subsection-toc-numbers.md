---
layout: post
title:  "Removing subsection numbers in a ToC"
date:   2013-04-10 13:08:42 +1030
categories: tex
---

<p>Very behind on taking care of the <a href="http://www.tug.org/TUGboat/tb30-2/tb95robertson.pdf">Herries Press packages</a> (PDF) which I&rsquo;m maintaining. Apologies to all who have emailed with suggestions, comments, and questions, and to whom I&rsquo;ve unfortunately not been able to respond.</p>

<p>Funny request today: how can I remove subsection <em>numbers</em> from the Table of Contents without removing their entries altogether? LaTeX&rsquo;s <code>tocdepth</code> counter controls which entries will appear in the ToC, but has nothing to say about their formatting. Adjusting LaTeX&rsquo;s ToC formatting yourself is of course possible, but the <code>tocloft</code> package makes things a bit easier.</p>

<p>Still, in this case it doesn&rsquo;t provide an easy interface, since who in their right mind would want to number a subsection but not include that number in the ToC? (You can&rsquo;t fight stylistic decisions like this sometimes—just go with the flow.) Even with <code>tocloft</code>, it&rsquo;s still necessary to write some internal code — and caveat emptor as always in such a case because you never know when the package might change its internal commands behind your back!</p>

<p>In this case, the trick is to read the <code>tocloft</code> documentation and notice that it provides hooks for inserting material before and after the number of a section entry in the ToC. For subsections, these commands, respectively, are <code>\cftsubsecpresnum</code> and <code>\cftsubsecaftersnum</code>. E.g., write</p>

<pre><code>\renewcommand\cftsubsecaftersnum{!}
</code></pre>

<p>to have a bang after every subsection number. (Presumably, a style or spacing change would be more common here.)</p>

<p>Aha! The intrepid LaTeX programmer at this point might suggest something like this:</p>

<pre><code>\def\cftsubsecpresnum#1\cftsubsecaftersnum{}
</code></pre>

<p>That is, when the pre-hook before the number executes, read everything up to and including the after-hook, and do nothing with it. (If the definition was <code>{#1}</code> instead, then it would typeset as usual.)</p>

<p>Well, give it a try like I did, and you&rsquo;ll discover it fails miserably. Back to the drawing board—time to read the package <em>source</em>. The issue stems from the fact that LaTeX uses one command only to typeset each line of a ToC, so this command must be completely general whether it&rsquo;s a chapter or section or subsection that it&rsquo;s dealing with.</p>

<p>Internally, the number in the ToC is typeset using something like</p>

<blockquote>
  <p>&hellip; <code>\@cftbsnum</code> <em>« the number itself »</em> <code>\@cftasnum</code> &hellip;</p>
</blockquote>

<p>where <code>\@cftnbsum</code> and <code>\@cftasnum</code> are <code>\let</code> equal to their appropriate high level definitions <code>\cft…presum</code> and <code>\cft…aftersnum</code> as necessary for the context. Therefore, any look-ahead-and-gobble command must be defined specifically to look ahead for the <em>internal</em> version of the hook rather than the high-level name for it given in the documentation.</p>

<p>Et voila:</p>

<pre><code>\usepackage{tocloft}
\makeatletter
\def\cftsubsecpresnum#1\@cftasnum{}
\makeatother
</code></pre>

<p>I still don&rsquo;t think this is very useful, but it&rsquo;s a nice trick.</p>

<hr><p>Hooks are funny in this way. If you define them to be defined by commands with an argument, such as</p>

<blockquote>
  <p>&hellip; <code>\cftsubsecsnumhook{</code> <em>« the actual number here »</em> <code>}</code> &hellip;</p>
</blockquote>

<p>it&rsquo;s hard to do parsing on it that involves scanning ahead for the contents of the number. On the other hand, in this case where the hook has the form where it&rsquo;s surrounded by a pre-hook and a post-hook, it&rsquo;s hard to grab the whole argument and do something with it since the internal post-hook might not be very user-accessible, as in the example above.</p>

<p>I don&rsquo;t know if there&rsquo;s a way to structure hooks in any better way, however. One possibility I can think of would be to have a generic ‘end hook’ token that could always be read until, such as</p>

<blockquote>
  <p>&hellip; <code>\cftsubsecpresnum</code> <em>« the actual number here »</em> <code>\cftendhook \cftsubsecaftersnum</code> &hellip;</p>
</blockquote>

<p>where <code>\cftendhook</code> was simply a no-op. There would be some subtle issues with nesting that would be somewhat painful to work around.</p>

<p>Maybe it would be better to have the number braced as an argument and instead of having <code>\cftsubsecpresnum</code> be a no-op by default it could be an identity function: (<code>\def\cftsubsecpresnum#1{#1}</code>)</p>

<blockquote>
  <p>&hellip; <code>\cftsubsecpresnum {</code> <em>« the actual number here »</em> <code>} \cftsubsecaftersnum</code> &hellip;</p>
</blockquote>

<p>Does anyone know of any best practices here?</p>
