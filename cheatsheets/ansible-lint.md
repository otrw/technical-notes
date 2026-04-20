# Ansible lint

Catch mistakes and bad practices in playbooks before running them. Can also be run before commiting playbooks to `git` to help catch syntax errors and bad practices in files not being immediately run.

> This can be installed on MacOS using `brew`

## Usage
```bash
# Check a single playbook
ansible-lint update.yml

# Check all playbooks in current directory
ansible-lint
```

## Common Warnings

* Missing `name:` in tasks
* Deprecated modules/options
* Wrong indentation in YAML
* Commands that should use Ansible modules instead

