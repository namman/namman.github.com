---
comments: true
date: 2012-08-10 14:12:09
layout: post
slug: how-to-do-dependency-properties-in-xaml
title: How to do dependency properties in XAML
wordpress_id: 107
categories:
- exocortex
---

```
public class MyStateControl : ButtonBase
{
  public MyStateControl() : base() { }
  public Boolean State
  {
    get { return (Boolean)this.GetValue(StateProperty); }
    set { this.SetValue(StateProperty, value); }
  }
  public static readonly DependencyProperty StateProperty = DependencyProperty.Register(
    "State", typeof(Boolean), typeof(MyStateControl),new PropertyMetadata(false));
}
```

Remember:
	
  * The identifier of the property has to end in "Property": eg "StateProperty".	
  * The name of the property here is "State".
  * Set the property from within the class using the Set on the public property.


