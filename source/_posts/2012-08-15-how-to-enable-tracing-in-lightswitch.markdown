---
comments: false
date: 2012-08-15 14:12:28
layout: post
slug: how-to-enable-tracing-in-lightswitch
title: How to enable tracing in Lightswitch
wordpress_id: 53
categories:
- exocortex
tags:
- lightswitch
---

Edit Web.config in server project:

```xml
<add key="Microsoft.LightSwitch.Trace.Enabled" value="true" />
```

Make sure custom errors in web.config is also set to "Off" (sic).

Then check <your app root>/trace.axd in browser.
