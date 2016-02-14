---
layout: post
title:  "A little bit of TLContrib"
date:   2010-10-13 13:08:42 +1030
categories: tex
---

<p>The indefatigable Taco Hoekwater <a href="http://www.bittext.nl/node/7">has released</a> a new project called &ldquo;<a href="http://tlcontrib.metatex.org/">TLContrib</a>&rdquo;, which is an orthogonal package hosting site for TeX Live installations. It does not mirror TeX Live, but consists of a place to distribute material that is otherwise unsuitable for the main TeX Live tree: namely, non-free material, binary updates, and pre-release updates. For example:</p>

<ul><li>Non-free material: <a href="http://www.ntg.nl/maps/34/11.pdf">cowfont</a> (pdf link)</li>
<li>Binary updates: LuaTeX, MetaPost</li>
<li>Pre-releases: siunitx, fontspec</li>
</ul><p>TLContrib is ready to be used by any users of TeX Live 2010; no extra software needs to be installed nor extra configuration performed.</p>

<p>Joseph Wright has already <a href="http://www.texdev.net/2010/10/09/tex-live-packaging-expands/">commented</a> on this new repository and has taken advantage of TLContrib for providing <a href="http://www.texdev.net/2010/10/12/testing-versions-of-siunitx-v2-1-on-tlcontrib/">testing releases</a> for siunitx. I&rsquo;m currently experimenting with the same idea for fontspec.</p>

<p>While users until now have been able to grab pre-release versions of siunitx and fontspec from <a href="http://bitbucket.org/josephwright/siunitx">Bitbucket</a> and <a href="http://github.com/wspr/fontspec/">Github</a>, the nice thing about using TLContrib is that you can use standard TeX Live tools to do the updates.</p>

<h2>TLContrib as a user</h2>

<p>Here&rsquo;s how it&rsquo;s all done as a user. First define an alias to make things easier to remember; put this into your <code>.bash_profile</code> or equivalent:</p>

<pre><code>alias tlc="tlmgr --repository <a href="http://tlcontrib.metatex.org/2010">http://tlcontrib.metatex.org/2010</a>"
</code></pre>

<p>You can now view what is available in the TLContrib repository with standard <code>tlmgr</code> commands such as</p>

<pre><code>tlc list
</code></pre>

<p>to see what is currently available for installation. Packages can be updated to their pre-release versions by typing, say,</p>

<pre><code>tlc update siunitx
</code></pre>

<p>and if an update performed in this way ‘goes bad’ and you&rsquo;d like to revert to the official release, execute</p>

<pre><code>tlmgr install fontspec --reinstall
</code></pre>

<p>and things will be back to normal.</p>

<h2>TLContrib as a package author</h2>

<p>As a package author, what I really like about TLContrib is the automated upload process—it&rsquo;s a very friction-free way to push out quick updates to users. It works by only accepting the very rigid directory structure via which the package is installed into a <code>texmf</code> directory on installation. No human verification of the package contents is performed, so updates are very fast (a delay of at most one hour).</p>

<p>(Updates can even be slurped in from an online SVN repository, but I&rsquo;m not sure how that would typically work for a LaTeX package that would typically not be kept in a <code>texmf</code> directory structure for development.)</p>

<p>In contrast, material submitted to CTAN must be manually processed for addition to TeX Live so that real humans can check to verify correctness and consistency of installation, and to ensure that the material is legally allowed to be included in the distribution, which is free in a very strict sense. It will be great to be able to iterate package development quickly, when necessary, through TLContrib while sending stable releases to CTAN and TeX Live.</p>
