---
comments: true
date: 2012-07-15 09:27:45
layout: post
slug: run-scala-tests-in-idea-using-junit-runner
title: Run scala tests in IDEA using JUnit runner
wordpress_id: 32
categories:
- exocortex
---
```scala
import org.scalatest.junit.JUnitRunner  
import org.scalatest.FlatSpec  
import org.junit.runner.RunWith 
 
@RunWith(classOf[JUnitRunner])
```
