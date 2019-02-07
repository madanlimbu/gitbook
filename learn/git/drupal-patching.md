---
description: Simple process of creating a patch in drupal.
---

# Drupal patching

**Steps:**

1\) Clone the project or checkout the latest `[branch]` i.e `7.x-2.x` 

```text
git clone --branch [branchname] http://git.drupal.org/project/[project_name].git
or
git checkout [branchname]
git pull
```

2\) Locally Create and checkout issue-number branch i.e `123-bug` 

```text
git checkout -b [issue-number]-[short-description]
```

3\) Work on fixing the issue/bug

4\) Commit the changes 

```text
git commit -am "Issue #123 by username: Fixed bug"
```

5\) Next apply changes to latest version of code \([rebase](https://www.youtube.com/watch?v=TymF3DpidJ8)\)

```text
git fetch origin
git rebase origin/[branchname] 
```

6\) Finally, create patch file using `git diff` 

```text
git diff origin/[branchname] > [project-name]-[short-description]-[issue-number]-[comment-number].patch
```

7\) Apply the patch 

```text
git apply patch-name.patch
```

