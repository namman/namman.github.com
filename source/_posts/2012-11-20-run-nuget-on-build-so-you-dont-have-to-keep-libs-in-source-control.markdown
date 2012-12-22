---
comments: false
date: 2012-11-20 09:14:10
layout: post
slug: run-nuget-on-build-so-you-dont-have-to-keep-libs-in-source-control
title: Run NuGet on build so you don't have to keep libs in source control
wordpress_id: 413
categories:
- exocortex
tags:
- nuget
---

* Check 'Allow nuget to download missing packages during build'.  (Tools: Library Package Manager: Package Manager Settings).
* Check in repositories.config (in packages dir) and packages.config files (one for each project).
* Check in .nuget folder from root of solution (yes, even including the .exe)
* Right-click on Solution file -> Enable Nuget Package Restore
