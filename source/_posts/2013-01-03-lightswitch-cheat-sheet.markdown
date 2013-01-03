---
layout: post
title: Order of Lightswitch screen events
date: 2013-01-03 17:33
comments: true
categories: lightswitch
---

1. InitialiseDataWorkspace.  Has already hydrated the data context from database.
2. Now loads custom controls: ControlAvailable events fire.
3. Created
4. Activated
