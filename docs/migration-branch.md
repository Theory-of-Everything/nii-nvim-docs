---
title: migration to main branch
author: TheoryToE
date: 2022-04-17

---
# Migration to main branch

In recent, much of nii-nvim's commit history has been littered with bad practice, greatly
effecting tracking changes. So a hard rebase was done to the branch, which now lives on
as the `main` branch. If you do attempt to pull changes, you will get odd issues.

## Migrating personal tweaks

nii-nvim is designed to be a base configuration, thus many have modified its core.
There are many ways to migrate based on the state of the repo's $working_directory:

### Uncommitted changes

The easiest way to transfer all of your changes is to stash your local changes.

```bash
git stash
```

Next pull and pop stashed changes

```bash
git checkout main
git stash pop
```

### Committed changes

If you have committed changes, you will have to be a bit more involved with picking out commits.

First of all, do not merge upstream changes if you have recent commits on HEAD, rather, you will
want to create patches of your latest commits, then apply them to `main`. Generally speaking,
if you dont know if you've committed recently, check `git log`.

For this example, I have 3 commits applied to master. 

I will first generate a diff of my changes and save it to a patch file.
You can also make multiple patch files if you have mixed in commits.
Make sure to move this patch file OUTSIDE your working directory, so 
that checkout wont take it.

- [Select revisions with git](https://git-scm.com/book/en/v2/Git-Tools-Revision-Selection)

```bash
git diff -u HEAD~3 > my_commits.patch
```

Next, checkout to the main branch. (make sure to pull it)
```bash
git pull origin main
git checkhout main
```

Finally, apply the patch of your changes.
```bash
git apply my_commits.patch
```

Then commit changes
```bash
git commit -m "chore: Migrated from master"
```

## Post-migration

Pull all changes

```bash
git pull origin master
git pull origin main
```

Remove the master branch

```bash
git branch -D master
```
