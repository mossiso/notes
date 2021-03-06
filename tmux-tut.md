---
layout: page
title:  "Tmux Tutorial"
categories: how-to
---

# tmux configuration

* In your system's keyboard settings, set the Capslock key to be the same as the
Control key
* Put the following at ~/.tmux.conf

```
# Set prefix to Ctrl-j (or Cap-j)
set -g prefix C-j

# use UTF8
set -g utf8
set-window-option -g utf8 on

# make tmux display things in 256 colors
set -g default-terminal "screen-256color"

# set scrollback history to 10000 (10k)
set -g history-limit 10000


# reload ~/.tmux.conf using PREFIX r
bind r source-file ~/.tmux.conf \; display "Reloaded!"

# use PREFIX | to split window horizontally and PREFIX - to split vertically
bind | split-window -h
bind - split-window -v

# map Vi movement keys as pane movement keys
unbind-key h
bind h select-pane -L
unbind-key j
bind j select-pane -D
unbind-key k
bind k select-pane -U
unbind-key l
bind l select-pane -R

# and use C-h and C-l to cycle thru panes
bind -r C-h select-window -t :-
bind -r C-l select-window -t :+



# use vim keybindings in copy mode
setw -g mode-keys vi


# http://zanshin.net/2013/09/05/my-tmux-configuration/
# ----------------------
# set some pretty colors
# ----------------------
# set pane colors - hilight the active pane
set-option -g pane-border-fg colour235 #base02
set-option -g pane-active-border-fg green #colour240 #base01

# colorize messages in the command line
set-option -g message-bg black #base02
set-option -g message-fg brightred #orange

# ----------------------
# Status Bar
# -----------------------
set-option -g status on                # turn the status bar on
set -g status-utf8 on                  # set utf-8 for the status bar
set -g status-interval 5               # set update frequencey (default 15 seconds)
set -g status-justify centre           # center window list for clarity
# set-option -g status-position top    # position the status bar at top of screen

# visual notification of activity in other windows
setw -g monitor-activity on
set -g visual-activity on

# set color for status bar
set-option -g status-bg colour235 #base02
set-option -g status-fg yellow #yellow
set-option -g status-attr dim 

# set window list colors - red for active and cyan for inactive
set-window-option -g window-status-fg brightblue #base0
set-window-option -g window-status-bg colour236 
set-window-option -g window-status-attr dim

set-window-option -g window-status-current-fg brightred #orange
set-window-option -g window-status-current-bg colour236 
set-window-option -g window-status-current-attr bright

# show host name and IP address on left side of status bar
set -g status-left-length 70
set -g status-left "#[fg=green]| #h |"

# show session name, window & pane number, date and time on right side of
# status bar
set -g status-right-length 60
set -g status-right "#[fg=blue]#S #I:#P #[fg=yellow]| %d %b %Y #[fg=green]| %l:%M %p |"
```

# Commands

* Use these keys to start using tmux 

| Session Commands | Definition |
|------------------|------------|
| `tmux ls` | show current sessions |
| `tmux attach -t billy`    | attach to a session named 'billy' |
| `tmux new -s billy`   | create a new session named 'billy' |


* To use the following commands while in tmux, hit the caps lock and 'J' key
first, then the following key.

| In Tmux Commands | Definition |
|------------------|------------|
| `Cap-j d` | detach from session |
| `Cap-j [` | enter copy mode (use vim key bindings to move cursor) |


| Window Commands  | Definition |
|------------------|------------|
| `Cap-j c`     | create a new window |
| `Cap-j ,`     | rename the current window |
| `Cap-j n`     | move to next window |
| `Cap-j p`     | move to previous window |
| `Cap-j [0-9]`     | move to window number [0-9] |
| `Cap-j w`     | list the windows |


|  Pane Commands   | Definition |
|------------------|------------|
| `Cap-j %`     | split vertically |
| `Cap-j o`     | move cursor to next pane |
| `Cap-j ;`     | move cursor to previous pane |


|  Command Commands   | Definition |
|------------------|------------|
| `Cap-j :`     | prompt to enter commands |
