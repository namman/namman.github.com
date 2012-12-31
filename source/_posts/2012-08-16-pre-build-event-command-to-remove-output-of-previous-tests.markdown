---
comments: false
date: 2012-08-16 14:23:43
layout: post
slug: pre-build-event-command-to-remove-output-of-previous-tests
title: Pre-build event command to remove output of previous tests
wordpress_id: 132
categories:
- exocortex
tags:
- visual studio
---

Remove any junk previous test runs may have written to TestOutput directory:
``` 
del /Q $(ProjectDir)\TestOutput
```
