## Setting Up

- `git config --global user.name "Your Name"`: Set your name
- `git config --global user.email "your.email@example.com"`: Set your email

## Creating and Cloning Repositories

- `git init`: Initialize a new Git repository in the current directory
- `git clone <repository-url>`: Clone an existing repository

## Basic Workflow

- `git status`: Check the status of your working directory
- `git add <file>`: Add a file to the staging area
- `git add .`: Add all changed files to the staging area
- `git commit -m "Commit message"`: Commit staged changes with a message
- `git push`: Push commits to the remote repository
- `git pull`: Fetch and merge changes from the remote repository

## Branching

- `git branch`: List all local branches
- `git branch <branch-name>`: Create a new branch
- `git checkout <branch-name>`: Switch to a different branch
- `git checkout -b <branch-name>`: Create and switch to a new branch
- `git merge <branch-name>`: Merge a branch into the current branch
- `git mergetool`: Launch configured merge tool to resolve conflicts

## Viewing Changes

- `git log`: View commit history
- `git diff`: View unstaged changes
- `git diff --staged`: View staged changes

## Undoing Changes

- `git restore <file>`: Discard changes in working directory
- `git restore --staged <file>`: Unstage a file
- `git reset HEAD~1`: Undo the last commit, keeping changes
- `git reset --hard HEAD~1`: Undo the last commit, discarding changes
- `git stash`: Save uncommitted changes temporarily
- `git stash pop`: Reapply previously stashed changes
- `git pull --rebase`: Pull changes and rebase local commits on top
## Remote Repositories

- `git remote add origin <repository-url>`: Add a remote repository
- `git remote -v`: List remote repositories
- `git fetch`: Download objects and refs from remote

## File tracking & ignoring

- `git ls-files` - see what Git is actually tracking
- `git check-ignore <path>` - test if a file/dir is being ignored
- `git rm --cached <file>` - stop tracking a file but keep it locally
- `git clean -n` - preview what untracked files would be deleted
- `git clean -f` - actually delete untracked files

## Status & inspection

- `git status --ignored` - show ignored files too
- `git diff --cached` - see staged changes
- `git log --oneline` - compact commit history
- `git show HEAD` - see the latest commit details

## Undoing things

- `git restore <file>` - discard local changes
- `git restore --staged <file>` - unstage a file
- `git reset HEAD~1` - undo last commit but keep changes

## Help

- `git help <command>`: Get help for a specific Git command
- For initial setup using `gh` command, see [[git-terminal-setup]]

**NOTE:**

- Always be careful with commands that can discard changes (like `reset --hard`). When in doubt, make a backup or use safer alternatives.
- Stick to a single workflow when learning. Try not make edits in `vscode` one minute then `vim` the next, same goes for `git commit`. Dealing with `git` errors is not worth the stress 😅
