---
layout: post
title: Git Practice
description: "Git is the most commonly used version control system today." 
tags: [git]
categories: [TIL]
---

# Managing History

## Git Log

```bash
# options are add to display better
$ git log --oneline --decorate --graph --all -30
```

## Git Show

```bash
# display the commit info and a diff
$ git show 770b1ab6
```

# Undoing

## Amending Commits

```bash
# incorporate "Gemfile.lock" into the previous commit
$ git add Gemfile.lock
$ git commit --amend --no-edit

# edit the commit msg
$ git commit --amend
```

**NOTE**  
`Git` creates a new commit object when use `amend`.

## Unstaging Files

```bash
$ git status --short
 M Gemfile
 M Gemfile.lock
 A TODO.md

# undo the staging file
$ git reset TODO.md
```

## Undoing a Commit

```bash
# remove the commit from the history and revert to the point where the files were staged
$ git reset --soft HEAD^
```

# More

## Git Stash 

`git stash` is a command that it stores all of the changes away. What so great about is that you can come back to the code anytime that you had stashed away. So I recommend to use it when there is an emergency bugfix.

```bash
# use -u flag to grab everything and get back to an empty status 
$ git stash -u
```

