---
comments: false
date: 2012-10-02 00:14:55
layout: post
slug: how-to-check-if-a-sequence-is-ordered-in-a-contract
title: How to check if a sequence is ordered
wordpress_id: 350
categories:
- exocortex
tags:
- C#
---

Extension method {{{SequenceEqual(this IEnumerable, IEqualityComparer)}}}

Eg:
{{{ lang=csharp
Contract.Requires(remainingShares.OrderByDescending(s => s.PurchaseDate).SequenceEqual(remainingShares));
}}}
