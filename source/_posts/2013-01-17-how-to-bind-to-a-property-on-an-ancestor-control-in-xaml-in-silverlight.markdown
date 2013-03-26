---
layout: post
title: "How to bind to a property on an immediate ancestor (parent) control in XAML in Silverlight?"
date: 2013-01-17 17:20
comments: false
categories:  XAML, silverlight
---
```xml
<ElementYouWantToSetPropertyIn PropertyYouWantToSet={Binding RelativeSource={RelativeSource Mode=FindAncestor, AncestorLevel=1, AncestorType=namespaceOfType:AncestorTypeName} Path=PropertyOnAncestor}">
```
