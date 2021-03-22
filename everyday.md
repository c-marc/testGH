# Individual Developer (Standalone)

## log

```
git log A..B #from B but not from A
git log B..A
git log A...B #symmetric difference: useful for merges
```

Filtering:

```
git log -2
git log v2.. <file>
```

## switch & branch

```
git switch -c fixup HEAD~3 #create fixup from HEAD~3 & switch
git switch - #go back
```

```
git switch --detach HEAD~3 #just have a look
git switch -c fixup #and decide to modify
```

```
git branch #local
git branch -r #remote
git branch -a #both
```

```
git branch -d exp #delete a merged branch
git branch -D crazy #delete an unmerged branch
```

## add

```
git add -u #--update already indexed files
```

## diff

Check working tree:

```
git diff #changes in the working tree not yet staged
git diff --cached #btw the index and the last commit
git diff HEAD #changes in the working tree since last commit
```

Comparing commits:

```
git diff test #compare to test branch
git diff HEAD -- ./test  #limit to the file test
git diff HEAD^ HEAD
```

Comparing branches:

```
git diff topic master    #changes between the tips of topic and master
git diff topic..master   #same
git diff topic...master  #changes in master since topic was started off
```

## status

## commit

```
git commit -m "m"
git commit --amend -m "m"
```

## restore

Restore specified paths in the working tree with some contents from a restore source.

```
git restore <pathspec> #restore WT from the index by default
git restore --staged <pathspec> #restore the index from HEAD
git restore --staged --worktree <pathspec> #restore both the index and the WT from HEAD
```

```
git restore --source master~2 Makefile #a file out another commit
```

```
git restore . #all files in the current dir
git restore :/ #all working tree file
```

## merge

Merge between local branches.

**First** get current work clean and committed locally. Then apply outside changes.

```
git merge topic
```


### Fast-forward


Note that fast-forward updates do not create a merge commit.

Typically when you `git pull` an upstream tracked repo, and you've not committed locally. The HEAD is updated to point at the named commit.

### True merge

```
git merge --abort
```

...

## rebase

Reapply commits on top of another base tip

```
git switch topic
git rebase master
```

or

```
git rebase master topic
```

Will reapply topic commits on top master. And rewrite history !

To transplant a topic branch based on one branch to another:

```
git rebase --onto master next topic
```

Will take out topic from next and apply on master.

```
git rebase --continue
git rebase --abort
```


## tag
