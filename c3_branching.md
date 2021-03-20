# Branching

## In a nutshell

```
git log --oneline --decorate #where the branch pointers are pointing
git log --oneline --decorate --graph --all #if divergence
```

```
git switch testing-branch
git switch -c new-branch
git switch - #Return to your previously checked out branch
```

## Branching and merging

It’s best to have a clean working state when you switch branches. There are ways to get around this (namely, stashing and commit amending).

```
git switch -c hotfix
git commit -a -m 'Fix broken email address'
git switch main #or switch -
git merge hotfix #fast-forward
git branch -d hotfix #delete
```

*Fast-forward* because the commit from hotfix is directly ahead of the commit from main (first commit's history = no divergence to deal with).

If it's not the case, git will do a *simple three-way merge* and
automatically creates a new commit.

### Basic Merge Conflicts

```
git status
#and edit
```

```
git mergetool #interactive
```

## Branch management

```
git branch -v
git branch --merged #branches already merged into current branch
git branch -d thisbranch #can be deleted
git branch --no-merged
```

### Changing a branch name

**WARNING**: only if nobody is working on it
```
git branch --move bad-branch-name corrected-branch-name
git push --set-upstream origin corrected-branch-name
git branch --all
git push origin --delete bad-branch-name
```

## Branching Workflows

## Remote Branches

## Rebasing

**Do not rebase commits that exist outside your repository and that people may have based work on.**

Alternative to 3-way merge. It will re-apply the patches to the branch.

This will end with the same snapshot. It’s only the history that is different.


```
git checkout experiment
git rebase master
git checkout master
git merge experiment #now fast-forward
```

Rebasing makes for a cleaner history.
Often, you’ll do this to make sure your commits apply cleanly on a remote branch — perhaps in a project to which you’re trying to contribute but that you don’t maintain. In this case, you’d do your work in a branch and then rebase your work onto origin/master when you were ready to submit your patches to the main project.

### More complex

Take the changes in client that aren't on server, and apply them on master...

```
git rebase --onto master server client
```
