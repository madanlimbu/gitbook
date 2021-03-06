---
description: Common usage of 'git revert'
---

# Revert/Resting

## Resting back to a specific commit

Reseting back to specific commit, we need to be careful as this will also remove all local changes.

```text
git reset --hard <commit_hash>
```

## Keeping few local changes  while reseting

There are times when we want to keep some local changes while reseting. we can use stash to keep the local changes and put those local changes to a commit.

```text
git stash
git reset --hard <commit_hash>
git stash pop

#or 

#reset but keep the local changes (if ~x is ~2, it will reset 2nd commit from the bottom)
git reset HEAD~x

#or 

#Undo last commit, but keep the changes (--soft)
git reset HEAD~

#or

#Revert last commit and rollback the changes:
git reset --hard HEAD~
```

#### Git reset can be used to reset to any branch / history

```text
#Reset local branch to origin/remote branch
git fetch origin
git reset --hard origin/develop
```

## Temporarily switch to a specific commit

There are times when we want to revert to a specific commit and try out the code or add few changes for testing.

```text
# Detach HEAD
git checkout <commit_hash>
```

## Branch off from a specific commit

We can temporarily try out code at this specific commit or we can create a new branch from this commit and work on it.

```text
# Create a branch from a specific commit point
git checkout -b <branch_name> <commit_hash>
```

## Reverting strategies

There are some few ways to revert in git.

```text
# This will revert last n Number of commits
git revert HEAD~"n"

# Reverting a range of commmits
git revert <start_commit_hash>..<end_commit_hash>

# Revert a merge commit ( -m 1 message tells git to go back to first commit before the merge )
git revert -m 1 <merge_commit_hash>

# Revert some commits at once
git revert <commit_hash_1> <commit_hash_2> <commit_has_3>
```

### Difference Revert vs Reset

**Reset** will clean up the git log history and make it seem like the commit didn't exist. However **Revert** will create a new commit which will undo the commit we want gone. 

It is **best to use Revert** instead of Reset if the changes has already been pushed to remote origin and pulled by someone else. 

## _**References:**_

* [Undo pushed merge](https://www.christianengvall.se/undo-pushed-merge-git/)
* [Git revert Manuals](http://schacon.github.io/git/git-revert.html)

