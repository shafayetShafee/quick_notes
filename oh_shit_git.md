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

