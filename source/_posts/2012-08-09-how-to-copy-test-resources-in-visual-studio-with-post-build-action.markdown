---
comments: true
date: 2012-08-09 17:25:30
layout: post
slug: how-to-copy-test-resources-in-visual-studio-with-post-build-action
title: How to copy test resources to output dir in Visual Studio with post-build action
wordpress_id: 73
categories:
- exocortex
---

```
xcopy.exe $(ProjectDir)\TestResources . /E /Y
```
