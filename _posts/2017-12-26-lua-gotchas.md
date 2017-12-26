---
layout: post
title:  "Lua gotchas"
date:   2017-12-26 09:02:23 +0930
---

From the outside Lua is close to the perfect language for scripting.
It is small and understandable, without sacrificing power.
However, there are a few things about it which have stumped me at first.

## Unicode ‘support’ 

Here's an easy one:

    s = "‡"
    print(s:len()) -- returns "3"
    
Pretty-printing non-ASCII documents using `string.format` is basically impossible
without resorting to additional libraries.
And unfortunately it seems that the unicode library in LuaTeX doesn't ‘fix’ the formatting problem:

    s = "‡"
    print(unicode.utf8.len(s))
    -- "1", as expected 
    
    print(unicode.utf8.format("string: [%-4s]",s))
    -- "[‡ ]", only 2 chars, not 4; same as string.format

Oh well. This can be addressed by manually calculating the number of spaces to insert:

    L = 4
    s = "‡"
    Nspaces = L - unicode.utf8.len(s)
    print(string.format("string: [%s]",s .. string.rep(" ",Nspaces)))



## Table variables are pointers

I think I understand this, but it sure took me a while to figure out the first time around:

    pp = {x=2}
    print(pp.x) -- "2"
    local ll = pp
    ll.x=0
    print(pp.x) -- "0" (!)
    
Coming from a Matlab background, this behaviour was unexpected to say the least.
The canonical way to copy a table appears to be:

    local ll = {}
    for k,v in pairs(pp) do 
      ll[k] = v
    end

