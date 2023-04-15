## Git command related to branching workflow

- Create a new branch and switch to it

  ```
  git checkout -b new_branch
  ```

- Pushing a local branch to remote branch

  After editing and commiting files from a git branch, to push this branch to remote, do the following from the branch (for the first time),

  ```
  git push -u origin branch_name
  ```
  
  After pushing the branch for the first time successfully, its now tracked remotely too, so after further editing and commiting, you do not need to set the upstream,
  simply push,
  
  ```
  git push
  ```
