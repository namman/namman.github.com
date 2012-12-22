---
comments: true
date: 2012-07-15 09:25:51
layout: post
slug: scala-reflection
title: Scala reflection
wordpress_id: 30
categories:
- exocortex
---

Call method by reflection in Scala on all instantiated instances of base class:
```scala
val baseClass = "UrBaseClass".getClass 
val urMethod = baseClass.getMethod("urMethod") 
val instances = baseClass.getDeclaredClasses.map(dc => dc.newInstance()) 
val resultsOfMethodCallsOnAllClasses = instances.map(instance => urMethod.invoke(instance)) 
```

