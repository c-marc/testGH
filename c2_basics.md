# Git Basics

## Get a git repo

Create:

```
cd ~/projects/my_project
git init

```

Clone:

```
cd ~/projects
git clone <url> [another_name_dir]
```


## Recording changes

```
git status -s #--short
```

```
git add <file>
git commit -m "blabla"
```

```
git diff #To see what you’ve changed but not yet staged
git diff --staged #what you’ve staged that will go into your next commit
```

Note that `git diff` doesn't show all changes made since last commit ; doesn't show changes that are already staged.

```
git rm <file> #stages the removal
git rm -f #if already modified or staged
git rm --cached #just remove from staging area
```

```
git mv README.md README #move or rename
#or git rm and git add if the move or renaming is done already
```

## History

```
git log -2 #last 2
git log -p -2 #--patch adds diff
git log --stat #abbreviated stats
git log --pretty=format:"%h %s" --graph
```

Various filtering :

```
git log -S function_name #find the last commit that added or removed a reference to
git log -- path/to/file
```

## Undoing Things

Go forward:

```
git commit --amend
```

### Unstaging a Staged File:

```
git restore --staged <file>
#OLD: git reset HEAD <file>
```

### Unmodifying a Modified File

```
git restore <file>
#OLD: git checkout -- <file>
```
**WARNING** : Changes will be gone !
Git just replaced that file with the last staged or committed version !

Stashing and branching are an alternative if you want to keep the changes but temporary get them away.


## Working with Remotes

Implicitly:

```
git clone <>
```

Explicitly:

```
git remote add <shortname> <url>
git remote -v
git fetch <shortname>
git fetch <remote>
git fetch origin #default name if cloned
```

Configuring pulling:

- If you want the default behavior of git (fast-forward if possible, else create a merge commit): `git config --global pull.rebase "false"`

- If you want to rebase when pulling: `git config --global pull.rebase "true"`

```
git push <remote> <branch> #push this branch to the remote
git push origin master
```

### Rename / remove

```
git remote rename pb paul
git remote remove paul
```


## Tagging

```
git tag
git tag -l "v1.*"
```

### Annotated tag

Should be preferred to lightweight

```
git tag -a v1.4 -m "my version 1.4"
git show v1.4
```

### lightweight

Just a pointer.
```
git tag v1.4-lw
```

### Tag an old commit
```
git log --pretty=oneline
git tag -a v1.2 9fceb02 #tag an old commit
```

### Tags must be pushed explicitly

```
git push origin <tagname>
git push origin --tags #all at once (both ann and lightweight)
```

### Delete

```
git tag -d v1.4-lw
git push origin --delete <tagname> #and from remote
```

### Switch

**WARNING**: simply switching to a tag will put us in a *detached HEAD* state (a new commit won't belong to any branch...). If any modification is planned, consider creating a branch:

```
git switch -c version2 v2.0.0
#OLD: git checkout -b version2 v2.0.0
```

## Aliases

```
git config --global alias.last 'log -1 HEAD'
git last
```
