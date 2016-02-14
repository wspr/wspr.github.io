---
layout: post
title:  "Callbacks in LuaTeX"
date:   2010-10-23 13:08:42 +1030
categories: tex
---

<p>You often hear the term “callbacks” bandied about when reading about new functionality offered by LuaTeX. Callbacks offer powerful functionality, but they don’t have pithy explanation that can easily explain why they’re so useful.</p>

<p>Paul Isambert has written a great example of using callbacks on comp.text.tex, his post prompted by Dan Luecking’s plea:</p>

<blockquote>
  <p>What is a callback? And don’t tell me to read the manual:
it has over 100 instances of the word callback and I gave
up trying to find out what they are after examining the
first 50 or so instances. </p>
</blockquote>

<p>Paul’s reply is <a href="http://groups.google.com.au/group/comp.text.tex/msg/62205ab5d302e11f">here</a>; he hints at an upcoming <a href="http://tug.org/TUGboat/">TUGboat</a> article going into more detail (don’t have a TUG subscription? You should: it’s cheap and furthers the development of TeX and friends), but here’s his opening explanation:</p>

<blockquote>
  <p>[A] callback is a point where you can interrupt TeX’s
normal operations, and throw in some (Lua) code of your own. There are
many such points, for many different operations: managing the input
buffer, reading a file, loading a font, building a paragraph, etc. </p>
</blockquote>

<p>His example then shows a short way to do in LuaTeX what requires rather more fragile and tricky code in regular TeX. Good stuff.</p>
