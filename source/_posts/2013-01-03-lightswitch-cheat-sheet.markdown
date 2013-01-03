---
layout: post
title: "lightswitch-cheat-sheet"
date: 2013-01-03 17:33
comments: true
categories: 
---

Order of screen events:
1. InitialiseDataWorkspace.  Has already hydrated the data context from database.
2. Now loads custom controls: ControlAvailable events fire.
3. Created
4. Activated
