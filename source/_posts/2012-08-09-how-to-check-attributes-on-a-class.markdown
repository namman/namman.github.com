---
comments: true
date: 2012-08-09 23:08:02
layout: post
slug: how-to-check-attributes-on-a-class
title: How to check attributes on a class
wordpress_id: 79
categories:
- exocortex
tags:
- attributes
- C#
- reflection
---

```csharp
bool IsEFClass()
{
var typeOfT = typeof (T);
var attributes = System.Attribute.GetCustomAttributes(typeOfT);
if (attributes.Any(a => a is System.Data.Services.Common.EntitySetAttribute))
   return true;
return false;
}
```
