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
