---
description: Day to day git flow usages
---

# Gitflow

## Git Flow Usual Work Flow

### Features

We have master, develop and feature branch. We use master for production ready code, develop should always be up to date with master and hold stuff ready in development environment. Finally, feature branch off of develop for each individual feature and merge back into develop once feature is completed.

```text
#Basic Work flow of feature

git checkout develop 

git flow feature start MY_FEATURE

#work on feature and commit stuff...

git flow feature finish MY_FEATURE

git push origin develop
```

### Release

Next, we will look into making a release using gitflow. Usually, once we have our collection of feature finished and merged back to develop, we create a release branch with release tag as the release branch name to release into master/production.

```text
#Basic release from develop

git checkout develop

git flow release start RELEASE_TAG(1.0.3)

git flow release finish RELEASE_TAG(1.0.3)

git push origin master:master develop:develop --tags
```

### Hotfix

Sometimes, there are some urgent bugs or security release we want out into production as soon as possible or we might want some patches out to production/master but develop branch has stuff that we don't want to release. This is when hotfix are used. Only while releasing hotfix we create a branch derived from master/production.

```text
#Basic hotfix from master

git checkout master
git pull

git flow hotfix start HOTFIX_TAG(1.0.4)

#apply fixes and commit them

git flow hotfix finish HOTFIX_TAG(1.0.4)

git push origin master:master develop:develop --tags
```

