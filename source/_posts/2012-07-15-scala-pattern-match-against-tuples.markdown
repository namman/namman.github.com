---
comments: true
date: 2012-07-15 09:08:00
layout: post
slug: scala-pattern-match-against-tuples
title: Scala pattern match against tuples
wordpress_id: 20
categories:
- exocortex
---
```scala
 def passed(in : Any) = in match {
case (a,b,c) => true
case _ => false
```
