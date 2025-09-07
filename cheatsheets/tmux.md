# Simple `tmux`

## Starting Tmux
- Open terminal.
- Type `tmux` and press Enter to start a new tmux session.

You'll notice the bottom of your terminal now has a green status bar. This indicates you're in a tmux session.

## Prefix Key
The prefix key is used before any tmux command. By default, it's `Ctrl+b` or just `prefix` in the following instructions.

To use a tmux command:
- Press `prefix`
- Release both keys
- Press the command key

**NOTE:**
Many users remap prefix from `Ctrl+b` to `Ctrl+a` for easier reach, this can be done by modifying the `.tmux.conf` in the `$HOME`. A simple example can be founf in the `configs` directory.

## Basic Operations

### Creating Windows

- Press `prefix` then `c` to create a new window.
- Notice the bottom status bar now shows multiple windows.

### Switching Between Windows

- `prefix` then `n` moves to the next window.
- `prefix` then `p` moves to the previous window.
- `prefix` then a number (0-9) jumps to that specific window.

### Splitting Panes

- `prefix` then `%` splits the current pane vertically.
- `prefix` then `"` splits the current pane horizontally.

### Quick Pane Navigation

- `prefix` then `q` shows pane numbers briefly
- `prefix` then `o` to cycle through panes

### Pane Management

- `prefix` then an arrow key moves to the pane in that direction.
- `prefix` then Ctrl+arrow: Resize pane in direction of arrow
- `prefix` then `z`: Toggle zoom on current pane
- `prefix` then `{` or `}`: Swap pane positions

### Closing Panes and Windows

- To close a pane: `prefix` then `x`, then press `y` to confirm.
- To close a window: Close all its panes, or use `prefix` then `&`, then `y` to confirm.

### Session Management

- Create a new name session `tmux new -s session_name` 
- Clean up and close old sessions `tmux kill-session -t name`
- `prefix` then `s` to show session tree (helpful when you have multiple and/or nested sessions)

### Renaming

- Rename the current SESSION: `prefix` then `$`
- Rename the current WINDOW: `prefix` then `,`

### Detaching and Attaching Sessions

- To detach from a session: `prefix` then `d`.
- To reattach to a session:
- List available sessions with `tmux ls`
- Attach to a specific session with `tmux attach -t session_name`

### Copy Mode

- `prefix` then `[`: Enter copy mode
- `Space` (in copy mode): Start selection
- `Enter` (in copy mode): Copy selection
- `prefix` then `]`: Paste copied text
