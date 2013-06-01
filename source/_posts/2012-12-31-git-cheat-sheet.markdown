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


Pretty log
```
git log --graph --decorate --pretty=oneline --abbrev-commit master origin/master <any other branch names you want in log>
```

Detached HEAD means the commit that is HEAD can't be referenced by other commits - you can never merge it.
To check if it was caused by a partially completed rebase (which creates a detached HEAD):
See if there is anything in:
```
.git/rebase-merge/
```
To confirm detached head:
```
git branch -a
```

Solution: 
* Make a temp branch from your branch with work you want to push
* Merge that branch into the target branch (eg, master)
* Delete the temp branch
```
git checkout -b temp
# check your work is there
git checkout master
git merge temp
git branch -d temp
```




