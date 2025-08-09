# **Git Branch Workflow — Quick Reference Guide**

> For solo projects. Keep `main` clean and always working. Do work on a short‑lived branch, merge when done, delete the branch.

Solo flow: branch -> commit -> push -> merge -> delete

## Workflow Reference Guide

### **1. Create a new branch from `main`**

```bash
git switch main           # Go to main branch
git pull --ff-only        # Update from remote
git switch -c <branch>    # Create & switch to new branch
```

Example:

```bash
git switch -c mc-docker-compose-changes
```


### **2. Make changes & commit**

```bash
# Edit your files...
git add -A                       # Stage all changes
git commit -m "Short & clear message"  # Commit staged changes
```

### **3. Push branch to remote (first time)**

```bash
git push -u origin <branch>      # -u sets upstream so later `git push` works without args
```
- Tab completion can be your friend here if working with long names.

### **4. Merge branch into `main` using a local merge**

```bash
git switch main                  # Switch to main branch
git pull                         # Make sure main is current
git merge --no-ff <branch> -m "Merge <branch> into main"
git push
```

- `--no-ff` keeps a merge commit so you can see branch history.


### **5. Clean up branch**

```bash
git branch -d <branch>           # Delete local branch
git push origin --delete <branch> # Delete remote branch
```

### **6. Quick fixes**
```bash
git restore --staged <file>      # unstage
git restore <file>               # discard local changes to file
git commit --amend               # fix last commit (message or staged changes)
git revert <sha>                 # make a new commit that undoes <sha>
```

## **Common Shortcuts**

```bash
# Create and switch in one go
git switch -c <branch>

# Auto-set upstream on first push (do this once)
git config --global push.autoSetupRemote true

# See all branches and where they point
git branch -vv

# View commit history graph
git log --oneline --graph --decorate --all
```

---

**Tips**

* One branch = one task or feature.
* Keep commits small and meaningful.
* Merge often so `main` always benefits from finished work.
* Delete old branches once merged — to keep repo tidy.
