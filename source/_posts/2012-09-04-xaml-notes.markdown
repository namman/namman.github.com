---
comments: false
date: 2012-09-04 17:49:45
layout: post
slug: xaml-notes
title: XAML notes
wordpress_id: 173
categories:
- cheat-sheets
---

Every XAML element corresponds to a .NET class.  
This creates a new class 'Window1' inheriting from 'Window':
```xml
<Window x:class="MyNamespace.Window1"/>
```
The XAML XML namespaces map to collections of .NET namespaces.  The main ones are:

  * xmlns="...presentation"  - all the .NET WPF namespaces
  * xmlns:x="... xaml" - all the XAML .NET namespaces

To reference classes outside the WPF or XAML namespaces, you need to map the .NET namespace to a XAML namespace:
xmlns:myPrefix="clr-namespace:myDotNetNamespace;assembly=myDotNetAssembly"

Several types of XAML properties:

  * Simple properties, eg align="center".  Type converters change the string to the type of the property.
  * Complex properties, eg .  This represents a property on the Grid class.

Markup extensions in curly brackets {}: DSL for bindings and the like.

Attached properties, eg <Grid.Row=0/>, appear in child element but are properties of parent element.

Two ways to find elements in XAML:

  * LogicalTreeHelper
  * FrameworkElement.FindName(...)

How to refer to another XAML element without binding: x:Reference="nameOfElement".

How to bind DataContext to viewmodel:
```xml
<UserControl ... DataContext="{Binding RelativeSource={RelativeSource Self}, Path=UrViewModelPropertyInCodeBehind}">
```

