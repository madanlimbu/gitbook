---
description: Common usage of 'git revert'
---

# Revert

#### Reverting back to a specific commit

Reseting back to specific commit, we need to be careful as this will also remove all local changes.

```text
git reset --hard "commit-hash"
```

#### Keeping few local changes  while reverting

There are times when we want to keep some local changes while reverting. we can use stash to keep the local changes and put those local changes to a commit. 

```text
git stash
git reset --hard "commit-hash"
git stash pop
```

#### Temporary switch to a commit 

There are times when we want to revert to a specific commit and try out the code or add few changes for testing.

```text
# Detach HEAD
git checkout "commit-hash"
```

Then we can temporarily try out code at this specific commit or we can create a new branch from this commit and work on it.

```text
# Create a branch from a specific commit point
git checkout -b "branch-name" "commit-hash"
```



