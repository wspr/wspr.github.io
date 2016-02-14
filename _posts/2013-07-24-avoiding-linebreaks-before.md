---
layout: post
title:  "Avoiding linebreaks before citations and things"
date:   2013-07-24 13:08:42 +1030
categories: tex
---

<p>When using a numerical bibliography style, it&rsquo;s considered bad form (at least by me) to have a linebreak before the citation. You might see suggestions in LaTeX guides to write</p>

<pre><code>... something profound~\cite{robertson2013}.
</code></pre>

<p>to avoid the citation number (‘[72]’, or whatever) ending up on its own at the beginning of a line.</p>

<p>This idea departs slightly from LaTeX&rsquo;s philosophy of separating form and content, since you have to explicitly remember to insert the non-breaking space before each citation. I prefer to do this sort of thing automatically, so that I can write</p>

<pre><code>... something profound \cite{robertson2013}.
</code></pre>

<p>and rest assured in the knowledge that I&rsquo;ll have no lonely citations. Donald Arseneau&rsquo;s <code>cite</code> package will do exactly that if you ask it to, although these days it&rsquo;s unlikely you&rsquo;re not using <code>biblatex</code> or similar which precludes the use of <code>cite</code>.
The method used by <code>cite</code> is nice and general:</p>

    \def\cite@adjust{\begingroup%
      \@tempskipa\lastskip \edef\@tempa{\the\@tempskipa}\unskip
      \ifnum\lastpenalty=\z@ \penalty\citeprepenalty \fi
      \ifx\@tempa\@zero@skip \spacefactor1001 \fi % if no space before, set flag
      \ifnum\spacefactor&gt;\@m \ \else \hskip\@tempskipa \fi
    \endgroup}

<p>(in inimitable Arseneau style). If you can follow this code then feel free to use it for your own documents.
Were I writing a package to automatically insert nonbreaking spaces, I&rsquo;d use something very similar.</p>

<p>But for me in my own documents, things are a little more simple. The easiest solution is</p>

    \let\oldcite\cite
    \renewcommand\cite{\unskip~\cite}

<p>which I can write without even thinking and sometimes do. To be slightly more general, it would be nice if this code didn&rsquo;t add a space if one wasn&rsquo;t already there to begin with.</p>

<p>So here&rsquo;s a command <code>\nobreakbefore</code> that examines whether there&rsquo;s any previous space, and if there is some removes it and re-adds a nonbreaking space. It suits basically all of my needs, which is enough when I&rsquo;m running against a deadline on my thesis:</p>

    \def\nobreakbefore{\relax
      \ifvmode\else
        \ifhmode
          \ifdim\lastskip &gt; 0pt\relax
            \unskip\nobreakspace
          \fi
        \fi
      \fi
    }
    \let\oldcite\cite
    \renewcommand\cite{\nobreakbefore\oldcite}

<p>Being able to automate this sort of thing is one of the reasons that I like LaTeX.</p>
