---
comments: false
date: 2012-09-21 12:22:06
layout: post
slug: delete-files-older-than-7-days
title: Delete files older than 7 days
wordpress_id: 344
categories:
- exocortex
tags:
- bash
- linux
---


```bash
find . ! -newermt "7 days ago" -delete
```
