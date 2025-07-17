# Tmux

[Cheatsheet](https://tmuxcheatsheet.com/)

`B` = `Space` for my config

### Start a session with specified name

```
tmux new -s name
```

### List sessions

```
tmux ls
```

### detach current session

```
ctrl+space d
```

### attach to a session

```
tmux a -t name
```

### Split panel

```
ctrl+alt+q - Horizontal
ctrl+alt+e - Vertical

ctrl+space arrow - Move between split panes
```

### Close Windows

```
ctrl+alt+w
```

### New Window

```
ctrl+t 
```

### Switch Window

```
ctrl+space pane#
```

### Rename Windows

```
ctrl+space ,

tmux rename-window -t <window> <newname>
```
