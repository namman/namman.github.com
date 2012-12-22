---
comments: false
date: 2012-09-14 16:20:33
layout: post
slug: difference-between-super-set-and-proper-super-set-also-subsets
title: Difference between Super Set and Proper Super Set (also subsets)
wordpress_id: 331
categories:
- exocortex
---

{{{ lang=csharp
var first = new HashSet() {1,2};
var second = new HashSet() {1,2};
var isProperSuperSet = first.IsProperSupersetOf(second);
Console.WriteLine (isProperSuperSet); // false
var isSuperSet = first.IsSupersetOf(second);
Console.WriteLine (isSuperSet); // true
}}}

Duh.
