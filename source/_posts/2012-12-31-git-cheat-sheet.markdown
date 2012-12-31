---
layout: post
title: "git cheat sheet"
date: 2012-12-31 08:51
comments: true
categories: 
---
Dredge up files deleted by previous lameness:
```bash
#Change to location where files deleted
cd wherever
# Find last commit that affected this dir
git log -- .
# diff commits to find where deleted
git diff [commit 1 hash] [commit 2 hash]
# checkout files you deleted from last good commit
git checkout [hash of commit with files you want] -- .\**
# short log of last five commits
git log --oneline -5
```
