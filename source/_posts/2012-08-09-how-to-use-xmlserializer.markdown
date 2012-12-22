---
comments: true
date: 2012-08-09 17:26:47
layout: post
slug: how-to-use-xmlserializer
title: How to use XmlSerializer
wordpress_id: 75
categories:
- exocortex
tags:
- C#
- XmlSerializer
---

> XmlSerializer xmlSerializer = new XmlSerializer(typeof(lkif)); 
> 
> var lkifToSerialize = new lkif(); 
> 
> lkifToSerialize.PopulateFromRulebase(this); 
> 
> xmlSerializer.Serialize(xmlWriter,lkifToSerialize);
