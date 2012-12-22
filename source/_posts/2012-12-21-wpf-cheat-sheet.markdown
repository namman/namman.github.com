---
layout: post
title: "WPF Cheat Sheet"
date: 2012-12-21 06:52
comments: true
categories: 
publish: false
---

IValueConverter:
Convert goes source object -> UI
ConvertBack goes UI -> source object
'paramater is passed in by UI.

```xaml
<ObjectDataProvider x:Key="ZoomOptions"
MethodName="GetNames"
ObjectType="{x:Type sys:Enum}"
>
<ObjectDataProvider.MethodParameters>
<x:Type TypeName="bll:enumZoomOptions"/>
</ObjectDataProvider.MethodParameters>
</ObjectDataProvider>

<ComboBox ItemsSource="{Binding Source={StaticResource ZoomOptions}}" />
```
