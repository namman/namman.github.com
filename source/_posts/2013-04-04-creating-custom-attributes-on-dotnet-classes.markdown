---
layout: post
title: "Steps to Creating Custom Attributes on .NET classes"
date: 
comments: false
categories: c#, .NET
---

* Attribute usage:
** whether to allow mulitple instances of attribute on same method or class
** what it applies to: class or method
** whether subclasses of the class inherit the attribate attached to the base class
* Create class inheriting from Attrbribute and stick the Attribute usage element on that.
* For attribute parameters, make constructor parameters of the custom attribute class

```csharp
 [AttributeUsage(AttributeTargets.Class, AllowMultiple = false, Inherited = true)]
    public class FileExtensionAttribute : Attribute
    {
        private readonly string _extWithDot;

        public FileExtensionAttribute(string extWithDot)
        {
            Contract.Requires(IsValidExt(extWithDot));
            _extWithDot = extWithDot;
        }

        bool IsValidExt(string extWithDot)
        {
            var regex = new Regex(@"\.????$");
            var machesRegex = regex.IsMatch(extWithDot);
            char[] invalidCharts = Path.GetInvalidFileNameChars();
            var containsInvalidChars = extWithDot.ToCharArray().Any(invalidCharts.Contains);
            return (machesRegex && !containsInvalidChars);
        }
    }
```
