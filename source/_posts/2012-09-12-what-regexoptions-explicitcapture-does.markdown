---
comments: false
date: 2012-09-12 10:40:23
layout: post
slug: what-regexoptions-explicitcapture-does
title: What RegexOptions.ExplicitCapture does
wordpress_id: 310
categories:
- exocortex
tags:
- C#
- regex
---

public static RegexOptions ExplicitCapture = RegexOptions.ExplicitCapture 
in enum RegexOptions

Summary:
Specifies that the only valid captures are explicitly named or numbered groups of the form (?…). This allows unnamed parentheses to act as noncapturing groups without the syntactic clumsiness of the expression (?:…).

Eg, this only captures the first letter of a the string, and the period at the end:

``` csharp
 var r = new Regex(@"(^[a-z])|\.\s+(.)", RegexOptions.ExplicitCapture);
```


