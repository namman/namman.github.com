---
comments: true
date: 2012-08-09 16:44:58
layout: post
slug: how-to-use-scala-pattern-matching-against-tuples
title: How to use scala pattern matching against tuples
wordpress_id: 47
categories:
- exocortex
tags:
- pattern matching
- scala
- tuples
---

pattern matching against tuples: 

def passed(in : Any) = in match {  
case (a,b,c) => true  
case _ => false  
}
