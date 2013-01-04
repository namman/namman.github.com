---
layout: post
title: Order of Lightswitch screen events
date: 2013-01-03 17:33
comments: true
categories: lightswitch
---

When opening a new screen:
1. InitialiseDataWorkspace.  Appears to happen BEFORE data context gets hydrated from database.
1. Now loads custom controls. (ControlAvailable events fire when done.)
1. CanRun
1. Created
1. Activated
1. Validate on all the entity properties.
1. Loaded

