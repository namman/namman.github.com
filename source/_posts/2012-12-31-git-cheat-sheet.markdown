---
layout: post
title: "git cheat sheet"
date: 2013-04-15 11:49
comments: true
categories: git
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

Revert to particular commit
```bash
git reset <hash of commit you want to revert to>
```
-H to discard changes in working copy.
