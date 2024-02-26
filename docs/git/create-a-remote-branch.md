# Create a remote branch

# Create a local branch and switch to it

Start by creating a local branch using `git checkout`

```
git checkout -b <new-branch-name>
```

This will create a new branch from your current branch. If you want to create a branch from a different branch, run the following.

```
git checkout -b <new-branch-name> <from-branch-name>
```

## Push local branch to remote

Run the below once you are ready to push the local branch to remote

```
git push -u origin <branch-name>
```
