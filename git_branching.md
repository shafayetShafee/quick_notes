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

- Deleting a branch locally and remotely

  To delete a branch remotely, do the following from that branch,
  
  ```
  git push -d origin branch_name
  ```
  
  Now to delete the branch locally, at first checkout to main branch (if you are not already)
  
  ```
  git checkout main
  ```
  
  and then,
  
  ```
  git branch -d branch_name
  ```
  
  **And do not forget to do a git pull when switched to main if you pushed that deleted local branch to remote and merged to remote main branch.**
  
