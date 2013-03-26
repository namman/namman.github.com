---
layout: post
title: "How to register HTTP handler in web.config in IIS 7"
date: 2013-01-18 15:26
comments: true
categories: .NET, ASP.NET
---
```xml
<system.webServer>
<handlers>
<add path="RelativePathWithoutLeadingOrTrailingBackslashOrAlternativelyAFileNameOrGlobFilePattern"
verb="*" 
type="ClassNameOfHTTPHandlerClassIncludingFullNamspace, AssemblyNameOfHandlerClassIfReferencedAssemblyFromWebProject"
/>
</handlers>
</system.webServer>
```
Full options on MSDN: http://msdn.microsoft.com/en-us/library/ms691481(v=vs.90).aspx

