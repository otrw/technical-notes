Quick drill for practicing basic branch workflow. Goal: make branching, editing, and committing muscle memory before pushing.

---
### **Branch Drill (Clone -> Branch -> Edit -> Commit -> Check)**

1. **Clone**
```bash
git clone --depth=1 https://github.com/user/repo.git
cd repo
```

2. **Make branch**
```bash
git checkout -b feature/test-branch
```

3. **Edit something small**
(e.g. update `README.md`with a note and/or example)

4. **Stage & commit**
```bash
git add README.md
git commit -m "docs: <your-change>"
```

5. **Check**
```bash
git status
git log --oneline
```

>**Drill: `clone -> branch -> edit -> commit -> check`**

---
## **Repeat**
### Run this drill on different repos until it feels automatic.

*(Push is optional until you are confident with the process)*
