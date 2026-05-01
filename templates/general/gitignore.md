# .gitignore template

## What is this?
Base ignore file for most projects

## When do I use this?
Starting a new repo

## Template

```text
# Secrets / environment
.env
.env.*
secrets*
*.local

# Keys / certificates
*.pem
*.key
*.p12
*.pfx
id_*

# Editor / OS clutter
.DS_Store
Thumbs.db
.vscode/
.idea/
*.swp
*.swo
*~

# Shell history
.zsh_history
.bash_history
```

## Notes

- Always ignore secrets.
- Adjust per project
