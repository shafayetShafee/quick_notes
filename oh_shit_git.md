## I have commited some files. How do I uncommit them?
  
If by "uncommit" you meant, 

- all you want to do is undo the act of committing, leaving everything else intact, use,

  ```
  git reset --soft HEAD~1
  ```
  
- you want to undo the act of committing and everything you'd staged, but leave the work tree (your files) intact:

  ```
  git reset HEAD~1
  ```
 
- you actually want to completely undo it, throwing away all uncommitted changes, resetting everything to the previous commit,

  ```
  git reset --hard HEAD~1
  ```

## I have added and pushed some unwanted files to remote repo. How can I resolve this issue?

```
git rm --cached .Rhistory  
```

Use flag `-r` for directory.

```
git rm --cached -r .Rproj.user 
```

`--cached` flag will remove the file/directory from git tree, keep them in the local filesystem.

Then add these files/directory in the `.gitignore` and then git add the `.gitignore`. Then do git commit and push.

## I have a Github Action that only runs on pushing tagged commit. Now I have noticed something wrong on my recent tag, how can rerun the Action again and delete the previous tag and add new release? 

At first delete the recent tag, locally and remotely,

```
git tag --delete v0.3.0
```

```
git push --delete origin v0.3.0
```

then create the tag again and do tag push. On tagged commit push, the workflow will run again,

```
git tag v0.3.0
```

```
git push --tags
```

## I have a few stale refs (refs to deleted remote branches). How can I clean them?

One way is to,

```
git remote prune origin --dry-run
```

This would show, which refs will be pruned if the command runs. If it is okay, then,

```
git remote prune origin
```

This will prune stale refs to origin.

Another way of doing it,

```
git remote prune origin --dry-run
```

or set the global config,

```
git config --global fetch.prune true
```
