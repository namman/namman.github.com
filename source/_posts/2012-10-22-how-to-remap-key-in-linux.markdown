---
comments: false
date: 2012-10-22 14:56:52
layout: post
slug: how-to-remap-key-in-linux
title: How to remap key in linux
wordpress_id: 373
categories:
- exocortex
---

Use ##xev## to find the keycode for any key.

To remap the annoying backslash on a British Standard 4822 keyboard to left shift:

```bash
cd ~
xmodmap -e "keycode 94 = Shift_L"
xmodmap -pke > .Xmodmap
echo xmodmap .Xmodmap > .xinitrc
chmod u+x .xinitrc
```
