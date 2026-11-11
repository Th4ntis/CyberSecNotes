# TMUX

**tmux** is a terminal multiplexer: it lets you run multiple terminal sessions, windows, and panes inside a single terminal, and - crucially - keeps them alive in the background. You can **detach** from a session and **re-attach** later (even after disconnecting from an SSH session), with everything still running.

That last point is why tmux is so useful over SSH: start a long job inside tmux on a remote server, detach, close your laptop, and reconnect hours later to find it still running exactly where you left it. A dropped connection no longer kills your work. (It's a modern, more capable\
alternative to the older `screen`.)

* [Cheatsheet](https://tmuxcheatsheet.com/)

### Key concepts

* **Session** - a collection of windows; the thing you attach to and detach from.\
  Survives in the background.
* **Window** - like a tab, filling the whole terminal.
* **Pane** - a split within a window (multiple shells side by side).
* **Prefix** - the key combo you press _before_ a tmux command, so tmux knows the\
  next keystroke is for it and not the shell. The default prefix is `Ctrl+b`;\
  **in my config it's remapped to `Ctrl+Space`** (configured in the\
  config below).

> **A note on the keybindings in this note:** the shortcuts below reflect _my_ custom config, not tmux's defaults. On a stock tmux you'd press the prefix and then a key (e.g. `Ctrl+b` then `%` to split), whereas my config binds many actions to direct combos like `Ctrl+Alt+Q`. If you're on a fresh install, either load my config or translate accordingly.

### Attach, or create if missing

A common line to put in your shell startup (e.g. `.zshrc`) to auto-attach to a session named `base`, creating it if it doesn't exist - so every terminal you open drops straight into tmux:

```bash
tmux attach -t base || tmux new -s base
```

The `||` runs the second command only if the first fails - see Common Commands > Redirection, pipes, and wildcards.

### PuTTY note

For PuTTY, add this to `.tmux.conf` to make `Ctrl+Arrow` work:

```bash
# Disable smkx/rmkx to enable CTRL+arrow
set -g terminal-overrides "xterm*:kLFT5=\\eOD:kRIT5=\\eOC:kUP5=\\eOA:kDN5=\\eOB:smkx@:rmkx@"
```

### Plugins

Managed with [TPM](https://github.com/tmux-plugins/tpm) (the Tmux Plugin Manager). Clone TPM and the plugins used in my config:

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
git clone https://github.com/tmux-plugins/tmux-cpu ~/.tmux/plugins/tmux-cpu
git clone https://github.com/tmux-plugins/tmux-battery ~/.tmux/plugins/tmux-battery
git clone https://github.com/tmux-plugins/tmux-yank ~/.tmux/plugins/tmux-yank
```

With TPM configured (see the config below), you can also install the plugins\
listed in `.tmux.conf` from inside tmux by pressing `prefix` + `I`.

### Quick reference (my bindings)

| Action             | Key                   |
| ------------------ | --------------------- |
| Prefix             | `Ctrl+Space`          |
| New window         | `Ctrl+T`              |
| Split horizontally | `Ctrl+Alt+Q`          |
| Split vertically   | `Ctrl+Alt+E`          |
| Move between panes | `Ctrl+Space` + arrow  |
| Resize pane        | `Ctrl+Alt` + arrow    |
| Close pane         | `Ctrl+Alt+W`          |
| Switch to window N | `Ctrl+Space` + number |
| Rename window      | `Ctrl+Space` + `,`    |
| Detach session     | `Ctrl+Space` + `d`    |
| Reload config      | `Ctrl+Space` + `r`    |
| Install plugins    | `Ctrl+Space` + `I`    |

### Sessions

Start a session with a specified name:

```bash
tmux new -s name
```

List sessions:

```bash
tmux ls
```

Detach the current session (keybinding):

```
ctrl+space d
```

Attach to a session:

```bash
tmux a -t name
```

### Panes

> The split/navigation keys below reflect my custom config.

Split a pane:

```
ctrl+alt+q   # Horizontal split
ctrl+alt+e   # Vertical split
```

Move between panes:

```
ctrl+space arrow
```

Close the current pane:

```
ctrl+alt+w
```

### Windows

New window:

```
ctrl+t
```

Switch to a window by number:

```
ctrl+space pane#
```

Rename a window:

```
ctrl+space ,                              # interactive rename
tmux rename-window -t <window> <newname>  # from the command line
```

### Config (with descriptions)

My full `~/.tmux.conf`. It remaps the prefix to `Ctrl+Space`, sets up custom split/navigation/resize bindings, enables the mouse and vi-style copy mode, builds a custom status bar (user, memory, CPU, temperature, battery, clock, date), and loads the plugins via TPM. Being a dotfile, it's a prime candidate for version control - see Linux General > Dotfiles.

```bash
### Remap prefix from 'C-b' to 'C-space' ###
unbind C-b
set-option -g prefix C-space
bind-key C-space send-prefix

### Split panes using Ctrl+Alt+Q/E ###
bind -n C-m-q split-window -v -c "#{pane_current_path}"
bind -n C-m-e split-window -h -c "#{pane_current_path}"
unbind '"'
unbind %

### Switch panes using Ctrl+alt+arrow without prefix ###
bind -n C-Left select-pane -L
bind -n C-Right select-pane -R
bind -n C-Up select-pane -U
bind -n C-Down select-pane -D
bind -n C-m-W kill-pane

### Resize Panes with Ctrl+arrow ###
bind -n C-m-Left resize-pane -L 2
bind -n C-m-Right resize-pane -R 2
bind -n C-m-Down resize-pane -D 2
bind -n C-m-Up resize-pane -U 2

### Changes History limit ###
set -g history-limit 10000

### Enable mouse mode configs ###
set -g mouse on
set -g @yank_with_mouse on
set -g @yank_selection_mouse 'clipboard'

### Enables Copy Mode ###
setw -g mode-keys vi

#### Reload config file ###
unbind r
bind r source-file ~/.tmux.conf \\; display "Reloaded ~/.tmux.conf"

### Windows(tabs) ###
unbind t
bind -n C-t new-window -c "#{pane_current_path}"
set -g base-index 1
set-window-option -g pane-base-index 1
set -g pane-border-format "#P: #{pane_current_command}"

### Status Bar Config ###
set-window-option -g window-status-style fg=colour244
set-window-option -g window-status-style bg=default
set-window-option -g window-status-current-style fg=#00cc00
set-option -g status on
set-option -g status-interval 1
set-option -g status-style fg=colour136,bg=colour235
set-option -g status-left "#[fg=#00cc00]#(whoami) #[fg=white]Φ "
set-option -g status-right-length 165
set-option -g status-right "#[fg=#00cc00,bg=default,bright]MEM:#{ram_percentage} | CPU:#{cpu_percentage} | CPU Temp:#{cpu_temp} | Batt:#{battery_percentage} |%l:%M:%S %p | %a-%m-%d-%Y"

### Plugins ###
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-battery'
set -g @plugin 'tmux-plugins/tmux-yank'
set -g @plugin 'tmux-plugins/tmux-cpu'

### End of File Stuff ###
run -b '~/.tmux/plugins/tpm/tpm'
run-shell '~/.tmux/plugins/tmux-yank/yank.tmux'
run-shell '~/.tmux/plugins/tmux-cpu/cpu.tmux'
```

> After editing `.tmux.conf`, reload it with `prefix` + `r` (configured above), or run `tmux source-file ~/.tmux.conf`.
