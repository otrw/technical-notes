
Simple example of the `.tmux.conf`. This file is typically saved to `$HOME`

```bash
# Re-map the prefix to C-a from C-b  
unbind C-b  
set-option -g prefix C-a  
bind-key C-a send-prefix
```
