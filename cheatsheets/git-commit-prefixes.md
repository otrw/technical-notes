# Git Commit Prefix Cheatsheet

## Git Commit Prefixes

These prefixes can be used when making a commit.

| Prefix        | Use when…                                                         |
| ------------- | ----------------------------------------------------------------- |
| **feat:**     | Adding a new feature, file, service, or significant functionality |
| **fix:**      | Correcting bugs, mistakes, typos, or broken behaviour             |
| **docs:**     | Updating documentation (README, notes, comments, guides)          |
| **chore:**    | Repo housekeeping — renames, config changes, formatting, deps     |
| **refactor:** | Improving structure or clarity without changing behaviour         |
| **remove:**   | Deleting files, features, or obsolete content                     |
| **wip:**      | Work-in-progress commit (should be squashed or cleaned later)     |

## Template

`<prefix>: <verb> <thing>`

## Examples

```text  
feat: add portainer and dozzle compose files
fix: correct volume path for libation
docs: add section on bind mounts vs volumes
refactor: simplify minecraft container network config
chore: bump alpine base image
remove: delete old docker-compose.backup.yaml
```

