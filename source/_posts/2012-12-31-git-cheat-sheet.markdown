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

# Checkout a version of a file from a previous commit into working tree
git checkout <hash of previous commit> <path of file>

Revert to particular commit
```bash
git reset <hash of commit you want to revert to>
```
-H to discard changes in working copy.


Pretty log
```
git log --graph --decorate --pretty=oneline --abbrev-commit master origin/master <any other branch names you want in log>
```

Diff between merge and rebase:
* merge does a three way merge between your commit, the remote head and the most recent common ancestor of the two.  Then in commits that to the remote branch.
* rebase compares your branch to the point in master where you diverged, makes a patch, then applies it to master.  Then you need to fastforward the HEAD of master by checkout out master and merging the latest commit (because HEAD of master will point to the second latest commit).

The point is that rebase makes one commit to master with clean history, rather than merging all the commits separately which you made in your topic branch.

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




