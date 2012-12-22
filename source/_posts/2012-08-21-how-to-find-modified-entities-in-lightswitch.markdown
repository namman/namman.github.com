---
comments: false
date: 2012-08-21 12:06:20
layout: post
slug: how-to-find-modified-entities-in-lightswitch
title: How to find modified entities in Lightswitch
wordpress_id: 137
categories:
- exocortex
tags:
- C#
- ef
- lightswitich
---

Add to SaveChanges_Executing() hook (runs before EF writes scheduled changes to database):


```csharp
        var remainingChangesToMyEntity =
                from e in this.DataWorkspace.ApplicationData.Details.GetChanges().ModifiedEntities
                 where e is MyEntity
                 select e as MyEntity;
```

