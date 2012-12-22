---
comments: false
date: 2012-10-21 14:20:19
layout: post
slug: simple-linq-group
title: Simple LINQ group
wordpress_id: 367
categories:
- exocortex
tags:
- C#
- group
- linq
---
```csharp

 int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 }; 
      
        var numberGroups = 
            from n in numbers 
            group n by n % 5 into g 
            select new { Remainder = g.Key, Numbers = g }; 

```
