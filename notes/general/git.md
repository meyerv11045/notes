# git reference

## undoing things
- `git commit --ammend` will add any staged changes to previous commit (technically 2nd commit replaces the previous one)
    - only ammend local commits
- `git restore` replaces `git reset`. 
- Unstaging changes:
    - `git reset HEAD <file-name>`
    - `git restore --staged <file-name>`
- Unmodifying an unstaged modified file: `git restore <file>` 
- [source](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)
  
## diff
- unadded changes: `git diff <file/folder-name>`
- added changes: `git diff --cached <file/folder-name>` 
    - also works with `--staged`
- changes from commit 1 to commit 2: `git diff <commit-1-hash> <commit-2-hash>`
    - `--stats` list changed files + insertions/deletions
    - `--name-only` lists name of changed files
    - `--name-status` list status of added/deleted/modified/renamed files
- changes from previous commit to current commit: `git diff HEAD^` (`HEAD^` is previous commit)
- generate output to `.diff` file:
    - `git diff -output=patch.diff`
    - `git diff > patch.diff`
    - `git diff > changes.patch`
- apply a diff/patch:
    - `git apply changes.patch` (only performs the changes-- they still need to be added/commited)
- changes from one branch to another:
    - `git diff main <file-name>` (comparing cur branch to main)
    - adding `~` after branch name will use the previous commit (multiple `~` goes multiple commits back)

## pull vs fetch
- `git fetch` will bring down any changes from remote repo but won't change any of your local branchs 
    - Only updates `.git/` directory with an updated version of the remote repo
    - To integrate the fetched commits, need to run `git merge`
- `git pull` essentially does a fetch followed by a merge into the current branch
- git fetch is the command that says "bring my local copy of the remote repository up to date."
- git pull says "bring the changes in the remote repository to where I keep my own code."

![](static/gitflow.png)

## switch
- new version of checkout
- `git switch <branch-name>`
    - use `-` as branch name to go back to original branch before from before switching
- create and switch to new branch: `git switch -c <new-branch>`
- switch to a remote branch (after fetching): `git switch -c <branch> --track <remote>/<branch>`

## branching
### add branch
- create local branch (doesn't checkout): `git branch <new-branch>`
    - create and automatically checkout a new local-branch: `git checkout -b <new-branch>` 
- add local branch to remote repo: `git push --set-upstream origin <local-branch>`
    - `-u` is shorthand for upstream

### delete branch
- Local: `git branch -d <local-branch>`
    - `-d` refuse to delete unmerged/unpushed changes
    - `-D` force delete
- Remote: `git push origin --delete <remote-branch-name>`

## stash changes
- Stashing can be used to temporaliy store modified, tracked files in order to change branches
- `git stash` saves the modified and staged changes
- `git stash list` lists the stack of stashed file changes
- `git stash pop` writes working from the top of the stash stack
- `git stash drop` discards the changes from the top of the stash stack

## config preferences:
- Stored globally in `~/.gitconfig`
- `git config` to update config settings
    - `--global` for global config updates
    - `--local` for project specific updates 
- `diff.noprefix true` removes a/ and b/ prefixes in diff results
- `credential.helper store` and then type in your username and PAT the next time you login 
    - Will save and use your login credentials for any future remote requests
- can create git aliases `git alias`:
```
[alias]
    unstaged = diff
    staged = diff --cached
    both = diff HEAD 
```
- `help.autocorrect <tenths-of-seconds>` will auto run a mistyped command after specified tenths of a second
- [More Config Settings](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)

## how git works
[how git works from the bottom up](http://ftp.newartisans.com/pub/git.from.bottom.up.pdf)
- index = staging area = cache (all refer to same thing)
- [difference between git restore and git reset](https://stackoverflow.com/questions/58003030/what-is-the-git-restore-command-and-what-is-the-difference-between-git-restor)

## commit hashes
- Git generates a unique SHA-1 hash (40 char string of hex digits) for every commit and refers to commits by this ID (usually only displays first 7 digits)
- SHA-1 has been compromised (can spoof hashes) so they are moving to SHA-256
- Making changes to previous commits in `.git` can be detected b/c each commit's hash is based on the previous commit's hash so the change to a previous commit would be easily detected
    - Simple blockchain of basing commit hashes on previous commits and verifying chains of hashes