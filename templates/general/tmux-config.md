# tmux config template

## What is this?
Basic `~/.tmux.conf` setup

## When do I use this?
Setting up tmux on a new system

# Usage

```text
unbind C-b  
set-option -g prefix C-a  
bind-key C-a send-prefix
```
## Notes

- Above changes prefix from `ctrl+b` -> `ctrl+a`
- Reload using `tmux source-file ~/.tmux.conf` 