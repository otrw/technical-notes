# Quicklook Bash Operators

- `cmd1 ; cmd2` → run `cmd1`, then run `cmd2` (always, sequential).
- `cmd1 && cmd2` → run `cmd2` **only if** `cmd1` succeeds (exit code 0).
- `cmd1 || cmd2` → run `cmd2` **only if** `cmd1` fails (non-zero exit code).
- `cmd1 && cmd2 || cmd3` → “if success, do cmd2, else cmd3” (be careful: use `(... )` for clarity).
- `cmd1 | cmd2` → pipe: send `stdout` of `cmd1` into `cmd2`’s input.
- `cmd1 &` → run `cmd1` in background, return immediately.
- `(cmd1 ; cmd2)` → run in a subshell (isolated environment).
- `{ cmd1 ; cmd2; }` → run in current shell (grouped commands).

---

**In Bash, “success” = exit code `0`, “failure” = anything non-zero.**


- `&&` means “if success (0) -> then do next.”
    
- `||` means “if failure (≠0) -> then do next.”
    

---

## **Real-world `&&` / `||` examples**:

### Grep


```bash
grep "ERROR" logfile && echo "Errors found"
grep "ERROR" logfile || echo "No errors found"
```

- First one: only prints if grep **found** a match.
- Second one: only prints if grep **didn’t** find anything.

---

### Curl

```bash
curl -s https://example.com && echo "Site is up" || echo "Site is down"
```

- If curl succeeds (exit code 0), it echoes *“Site is up.”*
- If it fails (non-0, e.g. timeout), it echoes *“Site is down.”*

---

### Make

```bash
make && sudo make install
```

- Only installs if the build completed successfully.

---

### Install fallback

```bash
sudo dnf install htop || sudo apt install htop
```

- Try DNF first; if that fails, try apt.
