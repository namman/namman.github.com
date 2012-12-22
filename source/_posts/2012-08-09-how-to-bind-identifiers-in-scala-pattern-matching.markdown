---
comments: true
date: 2012-08-09 16:46:39
layout: post
slug: how-to-bind-identifiers-in-scala-pattern-matching
title: How to bind identifiers in Scala pattern matching
wordpress_id: 49
categories:
- exocortex
tags:
- identifiers
- pattern matching
- scala
---

```scala
def commit[T](p: => Parser[T]) = Parser{ in =>
p(in) match{ 
case s @ Success(_, _) => s
case e @ Error(_, _) => e
case f @ Failure(msg, next) => Error(msg, next)
} 
```


