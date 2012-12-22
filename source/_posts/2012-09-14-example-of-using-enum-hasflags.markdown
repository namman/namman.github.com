---
comments: false
date: 2012-09-14 14:39:40
layout: post
slug: example-of-using-enum-hasflags
title: Example of using Enum.HasFlags
wordpress_id: 323
categories:
- exocortex
tags:
- C#
---

```csharp

public enum Coffees {
	   None = 0,
	   BasicCoffee = 1,
	   WithMilk = 8
	};
	
[Flags]
public enum FlaggedCoffees {
	   None = 0,
	   BasicCoffee = 1,
	   WithMilk = 8
	};
	
void Main()
{
	Coffees plain = Coffees.BasicCoffee;
	Console.WriteLine (plain);  // BasicCoffee
	Coffees plainWithMilk =  Coffees.BasicCoffee | Coffees.WithMilk ; 
	Console.WriteLine (plainWithMilk); // 9 (the result of bitwise OR operation on Coffees.BasicCoffee and Coffees.WithMilk)
	
	var basicPlusMilk =  FlaggedCoffees.BasicCoffee | FlaggedCoffees.WithMilk ;
	Console.WriteLine (basicPlusMilk);  // BasicCoffee, WithMilk
	
	bool hasMilk = basicPlusMilk.HasFlag(FlaggedCoffees.WithMilk);
	Console.WriteLine (hasMilk); // True 
}
```
