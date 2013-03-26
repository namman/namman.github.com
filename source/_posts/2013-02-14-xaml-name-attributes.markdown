---
layout: post
title: "How does x:Name attribute magically pop up in the code behind?"
date: 2013-02-14 11:15
comments: false
categories: xaml, c#, Silverlight
---

"The specified x:Name becomes the name of a field that is created in the underlying code when XAML is processed, and that field holds a reference to the object. In Silverlight, using the managed API, the process of creating this field is performed by the MSBuild target steps, which also are responsible for joining the partial classes for a XAML file and its code-behind. "

The name applies for a XAML namescope.

All the XAML in a single XAML file can be in one namescope.  So the name applies for all the elements in that XAML file. 

So that's why you can access it anywhere in the code behind for that XAML file.

http://msdn.microsoft.com/en-us/library/cc189028(v=vs.95).aspx


