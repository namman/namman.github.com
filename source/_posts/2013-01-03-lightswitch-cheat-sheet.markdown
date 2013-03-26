---
layout: post
title: Order of Lightswitch screen events
date: 2013-01-03 17:33
comments: true
categories: lightswitch
---

When opening a new screen:

1. Run.  (It's in Application namespace.  Screen paramaters are arguments.)
1. InitialiseDataWorkspace.  Appears to happen BEFORE data context gets hydrated from database.
1. Now loads custom controls. (ControlAvailable events fire when done.)
1. CanRun
1. Created
1. Activated 
1. Validate on all the entity properties.
1. Loaded

When navigating back to an already open screen:

1. Activated
2. Control available events fire.

To do something with a custom control on load (like set its view model or feed it some data), use FindControl in the _Activated hook, then hook into the Control_Available event.  Don't use _Activated - it may appear to work, but this is just dumb luck.
