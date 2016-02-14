---
layout: post
title:  "Non-textual tabular requirements"
date:   2011-03-29 13:08:42 +1030
categories: tex
---

![](tabular-squares.png)

I [once wrote](http://www.tug.org/pracjourn/2005-2/robertson/) a
procedure for drawing tabulars with square cells; it was one of my
earliest experiences with LaTeX programming, actually. When I’d done so,
I received a comment ‘why doesn’t LaTeX allow this easily’?

Well, I wondered, why not? My feelings at the time (echoed a little
today) were that LaTeX is a tool for writing largely technical
documents, and such specific requirements fall outside its regular
bounds of ways to typeset tabular material. (Forget, for the minute,
that LaTeX’s tables are pretty ugly by default; I’m assuming everybody
uses the booktabs package.)

I still agree with the author of booktabs on this matter: ‘It is not
going too far to say that if you cannot create a table using the
commands in this package, you should redesign it.’ However, I do admit
that things like tables with coloured rows and so on do have their uses.

Just recently [Karl
Berry](http://www.advogato.org/person/karlberry/diary/199.html)
mentioned he wanted to typeset a grid of images with a large image in
the centre. (Not unlike what you see at the top of the page. Just
replace the coloured boxes by real images.) This isn’t something that
LaTeX does out of the box, and I’m not sure, actually, if any third
package can do it either. (I tried but failed with multirow.)

Spurred on by the [requisite ConTeXt
example](http://randomdeterminism.wordpress.com/2011/03/28/would-a-table-by-any-other-name-be-as-useful/)
that ‘just works’, my own attempt to implement this arrangement turned
out to be quite easy but not exactly straightforward. Let me know if
there’s a better way.

First of all, the input syntax:

    \begin{tighttabular}{@{}c@{}c@{}c@{}c@{}c@{}c@{}}
    \1&\1&\1&\1&\1&\1\\
    \1&\1&\1&\1&\1&\1\\
    \1&\1&  &  &\1&\1\\
    \1&\1&\9&  &\1&\1\\
    \1&\1&\1&\1&\1&\1\\
    \1&\1&\1&\1&\1&\1\\
    \end{tighttabular}

Notice that my approach simply puts the material in the lower-left cell
in order to fill in the space taken up by the others. This would not
work if the cells were of unknown and uneven sizes.

The definition of `tighttabular` is easy; just define `\arraystretch` to
zero, locally:

{% raw %}
    \newenvironment{tighttabular}{%
      \def\arraystretch{0}%
      \begin{tabular}%
    }{%
      \end{tabular}%
    }
{% endraw %}

How do we place material in that box `\9` so it comes out with the
correct alignment? Actually, it’s not that bad:

{% raw %}
    \def\9{%
      \rlap{\smash{\largebox}}%
    }
{% endraw %}

The `\rlap` first removes the horizontal width, and the `\smash` removes
the vertical height. This is done so that the cell that holds `\9` takes
up only the same amount of space as the other cells around it.
(Otherwise, they would stretch to fit, distorting the size and alignment
of the tabular.)

Finally, what is `\1` and how do you get the colours to do that?

    \def\1{\smallbox}
    \def\smallbox{\color{blah!!+}\rule{2cm}{2cm}}
    \def\largebox{\scalebox{2}{\smallbox}}

(`\scalebox` requires the graphicx package.) These boxes use the xcolor
package’s very convenient ‘colour series’ feature:

    \usepackage{xcolor}
    \definecolorseries{blah}{hsb}{step}[hsb]{.5,1,1}{.1,-.05,0}
    \resetcolorseries{blah}

And that’s it. Whether you think this whole approach is nice and
straightforward or horribly arcane will be somewhat of a personal
decision. We’re still awaiting the one tabular package to replace all
others in the LaTeX world, although I’m pleased to see recent efforts
moving towards providing a complete interface to the different methods
supported by the various LaTeX third-party packages in this area.

(With my LaTeX3 hat on: no, as far as I know we’ve not even begun
thinking about how this might be dealt with there. I’m not an expert in
this area. Although I will say that I mildly dislike both LaTeX’s `&`
and ConTeXt’s `\bTR`…`\eTR` syntax; for me, the former is too close to
the metal and the latter too verbose.)

