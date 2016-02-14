---
layout: post
title:  "Avoid Excel vlookup: use index+match instead"
date:   2014-12-02 13:08:42 +1030
categories: excel
---

This is I'm sure old news to Excel gurus out there (of which I'm reluctantly, seemingly, turning into).

I started having a little more appreciation for Excel when I began using <code>vlookup</code> more seriously; this allows a semi-structured way of dealing with linked data in Excel. E.g., when a list of grades has a different set of students than a class list, you can still sensibly lookup values without manually copy/pasting information from one to the other.

I suppose an actual example is in order:

<img src="vlookup/vlookup1.png" />

I hope this is fairly obvious; we have an extremely basic lookup-style functionality (hence the name) where the function looks up <code>"c"</code> in the first column and outputs the corresponding entry in row <code>2</code>. You'd obviously usually use a reference to another cell rather than hard-code the <code>"c"</code> entry in there.

So this is great, but comes with some problems.

First of all, <code>vlookup</code> of course has the incredibly frustrating default behaviour of not exactly matching entries; in my own experience, things never work out unless you write it in the form <code>vlookup(•,•,•,FALSE)</code> — and if I'm rusty I never remember whether I should be writing true or false as the argument in there. So that's one reason <code>vlookup</code> is dumb.

Second of all, <code>vlookup</code> breaks in a completely transparent manner if you ever alter the columns in your original query. Perhaps I am re-arranging the spreadsheet so that there is a grade column as well:

<img src="vlookup/vlookup2.png" />

Unlike what happens in a lot of other Excel cases, inserting the new column hasn't updated the <code>vlookup</code> equation (not saying it should, though). And our lookup now obviously returns different data. This can bite you pretty bad unless you have stringent error checking somewhere along the line.

On the other hand, the useful replacement for <code>vlookup</code> does NOT have this same problem. This solution is called something like <code>index+match</code> instead, and you should not be intimidated from using it because it's slightly more complex. In fact, I find it easier to use in most cases:

<img src="vlookup/vlookup3.png" />

Translating that formula into prose produces something like this: "index into column D the row that matches "c" in column C". Note again Excel's insistence that you need a dumb suffix to tell <code>match</code> to do its thing properly; don't forget the <code>match(•,•,0)</code>.

Why is <code>index+match</code> better? I'm glad you asked:

<img src="vlookup/vlookup4.png" />

As soon as we inserted the extra column, the <code>match</code> function automatically updated and our formula is still correct. You can argue more tenuous advantages about <code>index+match</code> (e.g., that <code>vlookup</code> can't have a negative column index), but automatic updating is the killer.

