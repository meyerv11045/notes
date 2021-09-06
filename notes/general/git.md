# Git Cheat Sheet

## Setup Repo
- `git init` initializes an existing directory as a git repo
- `git clone <url>` retrieves an entire remote repository 

## Add Branch
- Local: `git branch <new-branch>` will create a new local branch from the branch you are currently located on but will not automatically check it out 
    - `git checkout -b <new-branch>` will create and automatically checkout a new local-branch
- Remote: `git push --set-upstream origin <local-branch>` will add your new local branch to the remote repo
    - `git push -u origin <local-branch>` uses the `-u` flag as shorthand 

## Delete Branch
- Local: `git branch -d <local-branch>`
    - `-d` flag will refuse to delete the branch when it contains commits not merged into other local branches or pushed to a remote repo
    - `-D` flag will delete such a branch regardless (force deletion)
- Remote: `git push origin --delete <remote-branch-name>`

## Stash Changes
- Stashing can be used to temporaliy store modified, tracked files in order to change branches
- `git stash` saves the modified and staged changes
- `git stash list` lists the stack of stashed file changes
- `git stash pop` writes working from the top of the stash stack
- `git stash drop` discards the changes from the top of the stash stack


## Commit Hashes
- Git generates a unique SHA-1 hash (40 char string of hex digits) for every commit and refers to commits by this ID (usually only displays first 7 digits)
- SHA-1 has been compromised (can spoof hashes) so they are moving to SHA-256
- Making changes to previous commits in `.git` can be detected b/c each commit's hash is based on the previous commit's hash so the change to a previous commit would be easily detected
    - Simple blockchain of basing commit hashes on previous commits and verifying chains of hashes