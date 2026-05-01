# tmux Config

## About

Example of the `.tmux.conf`, typically saved to `$HOME`

```text
# Re-map the prefix to C-a from C-b  
unbind C-b  
set-option -g prefix C-a  
bind-key C-a send-prefix
```
