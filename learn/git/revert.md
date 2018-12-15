---
description: Common usage of 'git revert'
---

# Revert

#### Reverting back to a specific commit

Reseting back to specific commit, we need to be careful as this will also remove all local changes.

```text
git reset --hard <commit_hash>
```

#### Keeping few local changes  while reverting

There are times when we want to keep some local changes while reverting. we can use stash to keep the local changes and put those local changes to a commit. 

```text
git stash
git reset --hard <commit_hash>
git stash pop
```

#### Temporarily switch to a specific commit 

There are times when we want to revert to a specific commit and try out the code or add few changes for testing.

```text
# Detach HEAD
git checkout <commit_hash>
```

#### Branch off from a specific commit

We can temporarily try out code at this specific commit or we can create a new branch from this commit and work on it.

```text
# Create a branch from a specific commit point
git checkout -b <branch_name> <commit_hash>
```

#### Reverting strategies

There are some few ways to revert in git.

```text
# This will revert last n Number of commits
git revert HEAD~"n"

# Reverting a range of commmits
git revert <start_commit_hash>..<end_commit_hash>

# Revert a merge commit
git revert -m 1 <merge_commit_hash>

# Revert some commits at once
git revert <commit_hash_1> <commit_hash_2> <commit_has_3>
```

#### _**References:**_

* [Undo pushed merge](https://www.christianengvall.se/undo-pushed-merge-git/)
* [Git revert Manuals](http://schacon.github.io/git/git-revert.html)

