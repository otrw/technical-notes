# Set a Git Commit Template

Use a `.gitmessage.txt` to guide consistent commit messages (Can be global or per-repo).

---
## 1. Create the `.gitmessage.txt` file

```bash
cat <<EOF > ~/.gitmessage.txt
# Summary (max ~50 characters)
# Keep it short and descriptive

# Body (optional, wrap lines at ~72 chars)
# Use this space to explain *why* the change was made
# Bullet points work well:
# - Refactored volume paths to be more consistent
# - Added setup steps for new users
#
# Delete any unused lines before committing.
EOF
```

## 2. Configure Git to use it

```bash
git config --global commit.template ~/.gitmessage.txt`
```

When you run `git commit`, this template opens with reminders.
