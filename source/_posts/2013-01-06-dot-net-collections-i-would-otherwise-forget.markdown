---
layout: post
title: "Junk about .NET collections I would otherwise forget"
date: 2013-01-06 09:19
comments: true
published: false
categories: .NET, c#
---

#SortedSet<T> 

* Reverse() does not mutate collection, but the other methods do.
'''csharp
	var sortedSet = new SortedSet<int>(new []{1,2,3});
			sortedSet.Reverse();
			Console.WriteLine(String.Join(",",sortedSet)); // 1,2,3 
			var reversed = sortedSet.Reverse();
			Console.WriteLine(String.Join(",",reversed));  // 3,2,1
```

todo: complexity of removing from list, show with stopwatch
todo: show diff between sort and orderby
todo: show difference in stability
todo: show covariance of arrays
todo: single dimentional arrays are vectors
rectangular arrays: int[,]
jagged arrays: int[5][10]

int[][] jagged = new int[
show how to access
#


