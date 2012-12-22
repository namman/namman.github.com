---
comments: true
date: 2012-08-09 17:01:51
layout: post
slug: difference-between-ref-and-out-in-c
title: Difference between ref and out in C#
wordpress_id: 58
categories:
- exocortex
tags:
- C#
---

Difference between ref and out: 
```csharp
int x;
Foo(out x); // OK
int y;
Foo(ref y); // Error
```
ref has to be initialised before passed in, out has to be initialised before passed out.
