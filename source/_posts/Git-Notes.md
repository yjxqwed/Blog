---
title: Git Notes
date: 2020-12-09 17:40:52
tags:
---

This post is to archive some commonly used git commands.

## Clone
```bash
# Just clone a certain branch from repo and name the local directory as dir
$ git clone -b <branch> <repo> [dir]
```

## Merge
```bash
# Go to branch master
$ git checkout master

# Merge branch dev into master
$ git merge dev
# Then handle potential conflicts

# Merge branch dev into master. If conflicted, use master
$ git merge -X ours dev

# Merge branch dev into master. If conflicted, use dev
$ git merge -X theirs dev
```

## Commit
```bash
# Modify the last commit message
$ git commit --amend
```

## Rebase
```bash
# Merge the most recent 2 commits
$ git rebase -i HEAD~2
# Then squash the second and following commits and edit the combined commit message
```


## Checkout
```bash
# Create and checkout a new branch (with current change).
$ git checkout -b <branch>

# Create a new local branch tracking origin/<remote-branch>
$ git checkout -b <local-branch> origin/<remote-branch>

# Clear the changes of a file
$ git checkout -- <file>

# Checkout an existing branch
$ git checkout <branch>
```

## Branch
```bash
# List all local branchs
$ git branch

# Create a new branch
$ git branch <branch>

# Delete a branch
$ git branch -D <branch>

# Delete a fully merged branch
$ git branch -d <branch>
```

## Push
```bash
# Forcefully push
$ git push -f

# Push this branch to origin and as remote-branch
$ git push --set-upstream origin <remote-branch>
```

## Reset
```bash
# Discard all uncommitted changes
$ git reset --hard
```

## Clean
```bash
# Remove all untracked files
$ git clean -fd
```

## Submodule
If you need to put a git repo inside another git repo, treat the inside repo as a git submodule.
```bash
$ git submodule add [OPTIONS] <repo> <path>
```
