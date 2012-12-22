---
comments: true
date: 2012-08-09 16:42:41
layout: post
slug: syntax-for-paths-in-bashrc
title: Syntax for paths in .bashrc
wordpress_id: 44
categories:
- exocortex
tags:
- .bashrc
- linux
---

To make paths actually work in .bashrc:

```bash
export AKKA_HOME=~/Programs/typesafe-stack 
alias t='todo.sh -d ~/Programs/todo.txt/todo.cfg'
export PATH=$PATH:~/Programs/typesafe-stack/bin
```
