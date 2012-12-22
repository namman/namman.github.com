---
comments: false
date: 2012-09-12 13:10:32
layout: post
slug: personal-programming-principles
title: Personal Programming Principles
wordpress_id: 187
categories:
- exocortex
---

Sententious advice abounds.  What has worked for me:

| Principle | Where I first got it| Example |
| Start in the middle. | Daryel Akerlind | For f*&k;'s sake don't start a new module by sketching out interfaces and base classes - a recipe for over engineering. |
| If data structures are likely to change a lot, but the behaviours not so much: use OO.  For the reverse, use FP.  If both, use OO. | "Real World Functional Programming" book. | FP: use C# extension methods for manipulating generated classes from Odata service reference.  Database is not going to change much.  If it does, you're hosed anyway. |
| Use small and cohesive functions and classes. | "Clean Code" book. |
| For tricky and self contained: TDD.  For sprawling and fluid: TAD (test after development). | Personal goddamn experience. |
| Depend on abstractions, not implementations. | Head First Design Patterns book. | Creating simple interfaces for everything that gets constructor injected seems like a hassle at first.  But it will be more of a hassle later when you can't mock the dependencies.  Then you'll have to extract interfaces from classes that are already throughout your code.  So just do it up front.  ReSharper makes it easy. | 
| Just 'pushing through' never bloody works. | Daryel Akerlind | |
| Use contracts and exceptions to flag things you don't expect.  Don't let these cases fall into an 'else' branch or a default value. | Personal goddamned experience. | Slam a contract assertion in before returning from within an else block. |

 

