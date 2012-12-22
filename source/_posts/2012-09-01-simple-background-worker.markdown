---
comments: false
date: 2012-09-01 22:54:05
layout: post
slug: simple-background-worker
title: Simple background worker
wordpress_id: 151
categories:
- exocortex
tags:
- background worker
- C#
---

[csharp]

var worker = new BackgroundWorker();
            worker.DoWork += worker_DoWork;
            worker.RunWorkerAsync();

void worker_DoWork(object sender, DoWorkEventArgs e)
        {
            // the actual work
        }

[/csharp]
