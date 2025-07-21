# Git Worktree: A Safer, Cleaner Workflow for Testing Changes

## Overview
`git worktree` allows you to create multiple working directories from a single Git repository. It's ideal for testing, temporary changes, or working on multiple branches without switching or cloning.

---

## Use Case: Testing Docker or Config Changes

Instead of cloning your repo into a temp folder, you can:
- Create a new branch
- Attach a separate working directory
- Make changes and test in isolation
- Merge back when happy

---

## Step-by-Step Guide

### 1. Ensure your repo is clean
```bash
cd ~/projects/docker-projects/project1
git status  # Should show a clean working tree
```

### 2. Create a test branch
```bash
git checkout -b test-config-change
```

### 3. Add a worktree for that branch
```bash
git worktree add ~/temp/project1-test test-config-change
```

This creates a new working directory at `~/temp/project1-test`, checked out to the new branch.

### 4. Work in the test directory
```bash
cd ~/temp/project1-test
code .  # or use any editor
```
Make changes, test with Docker, etc.

### 5. (Optional) Commit your changes
```bash
git add .
git commit -m "Test new config for project1"
```

### 6. Merge changes back to `main`
```bash
cd ~/projects/docker-projects/project1
git checkout main
git merge test-config-change
```

### 7. Clean up
```bash
git worktree remove ~/temp/project1-test # removes the workflow directory
git branch -d test-config-change # deletes the test branch
```

### 8. Push to remote (optional)
```bash
git push origin main
```

---

## Why This Workflow Works
| Benefit                   | Explanation                              |
| ------------------------- | ---------------------------------------- |
| Isolated testing          | Keeps main branch untouched              |
| No need to stash/checkout | Work simultaneously on multiple branches |
| Clean merges              | Use Git’s built-in merge when ready      |
| Low overhead              | More efficient than cloning full repos   |

---

## Alias Automation
To speed things up, add these to `.zshrc` or `.bashrc`:

```bash
# Paths
export project1_PATH=~/projects/docker-projects/project1

# Set up test worktree
alias project1-test='\
  cd $project1_PATH && \
  git checkout -b test-env-change && \
  git worktree add ~/temp/project1-test test-env-change && \
  cd ~/temp/project1-test && code .'

# Clean up test worktree
alias project1-clean='\
  git worktree remove ~/temp/project1-test && \
  cd $project1_PATH && git branch -D test-env-change'
```

---

## Commands Reference
```bash
git worktree list             # Show all active worktrees
git worktree add <path> <branch>   # Add a new worktree
git worktree remove <path>   # Remove a worktree
git branch -d <branch>        # Delete the test branch
```

---

## When to Use
| Situation                                 | Use Worktree? |
|------------------------------------------|---------------|
| Testing Docker configs/scripts           | ✅ Yes         |
| Developing a feature in isolation        | ✅ Yes         |
| Need quick throwaway sandbox             | ✅ Yes         |
| Want to clone and forget Git\*             | ❌ No          |
\*Using  `cp` to another directory is enough here.

---

