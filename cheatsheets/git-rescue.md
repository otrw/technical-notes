## Git Is Being a Bellend: Rescue Cheatsheet

When Git kicks off and breaks, check the symptom and apply the fix.

Push failed?  
| -- File too big? (100MB+) -> [1](#1-github-rejected-my-push-big-file)
| -- Remote missing? -> [2](#2-remote-disappeared)
| -- "You must pull first"? -> [3](#3-git-says-you-must-pull-first)
| -- Just overwrite remote? -> [4](#4-nuke-it-from-orbit-overwrite-remote)

Want to ignore files? -> [5](#5-ignore-files-from-now-on)
Need cleanup tips? -> [6](#6-final-cleanup-tips)

---
### 1. GitHub rejected my push (big file?)
GitHub blocks:
- >100 MB files (hard fail)  
- >50 MB files (warning)

**Check tracked files:**
```bash
git ls-files | grep data/
````

**Stop tracking large file (keep it on disk):**

```bash
git rm --cached path/to/large_file
git commit -m "Remove large file"
```

---
### 2. Remote disappeared

**Check:**
```bash
git remote -v
```

**Re-add origin:**
```bash
git remote add origin git@github.com:USERNAME/REPO.git
```

---
### 3. Git says “You must pull first”

Remote has changes...you don’t.

**Safe way (preserve remote history):**
```bash
git pull --rebase
git push
```

**If branch not tracking:**
```bash
git branch --set-upstream-to=origin/main main
```

---
### 4. Nuke it from orbit (overwrite remote)

⚠️ **Destructive!** Use only if you really want local to replace remote.
```bash
git push origin main --force
```

---
### 5. Ignore files from now on

Add to `.gitignore`:
```gitignore
**/data/
*.jar
*.zip
*.tar.gz
```

Already tracked files? Remove them:
```bash
git rm --cached path/to/file
```

---
### 6. Final Cleanup Tips

Check what’s staged:
```bash
git status
```

See what’s being ignored:
```bash
git check-ignore -v path/to/file
```
