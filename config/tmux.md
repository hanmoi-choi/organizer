<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">Default Key Bindings</a>
<ul>
<li><a href="#sec-1-1">remap prefix from 'C-b' to 'C-a'</a></li>
<li><a href="#sec-1-2">Setting the delay b/w prefix and command</a></li>
<li><a href="#sec-1-3">Set the base index for windows to 1</a></li>
</ul>
</li>
<li><a href="#sec-2">Pane Management</a>
<ul>
<li><a href="#sec-2-1">Set the base index for panes to 1</a></li>
<li><a href="#sec-2-2">Reload the config file - &lt;S&gt;</a></li>
<li><a href="#sec-2-3">Splitting Panes</a></li>
<li><a href="#sec-2-4">Moving b/w panes</a></li>
<li><a href="#sec-2-5">Pane resizing</a></li>
<li><a href="#sec-2-6">Cycle Panes</a></li>
<li><a href="#sec-2-7">Kill Pane, if last pane, kill window</a></li>
<li><a href="#sec-2-8">Zoom Panes</a></li>
<li><a href="#sec-2-9">Copy Current Pane's Path</a></li>
</ul>
</li>
<li><a href="#sec-3">Window Management</a>
<ul>
<li><a href="#sec-3-1">Create new Window and rename it</a></li>
<li><a href="#sec-3-2">List Windows</a></li>
<li><a href="#sec-3-3">Swap Windows</a></li>
<li><a href="#sec-3-4">Kill Window</a></li>
<li><a href="#sec-3-5">Switch to another window by name</a></li>
<li><a href="#sec-3-6">Forward &amp; Backward b/w windows</a></li>
</ul>
</li>
<li><a href="#sec-4">Session Management</a>
<ul>
<li><a href="#sec-4-1">Rename Session</a></li>
<li><a href="#sec-4-2">Switch to previously selected session</a></li>
<li><a href="#sec-4-3">Switch to another session by name</a></li>
</ul>
</li>
<li><a href="#sec-5">Mouse</a>
<ul>
<li><a href="#sec-5-1">Mouse On</a></li>
</ul>
</li>
<li><a href="#sec-6">Status Bar</a>
<ul>
<li><a href="#sec-6-1">Message Text</a></li>
<li><a href="#sec-6-2">Mode</a></li>
<li><a href="#sec-6-3">Pane</a></li>
<li><a href="#sec-6-4">Status Bar</a></li>
</ul>
</li>
<li><a href="#sec-7">Terminal Window</a>
<ul>
<li><a href="#sec-7-1">Title</a></li>
</ul>
</li>
<li><a href="#sec-8">Etc</a>
<ul>
<li><a href="#sec-8-1">Copy and Paste</a></li>
<li><a href="#sec-8-2">Execute Tmux Command</a></li>
<li><a href="#sec-8-3">Visual Bell</a></li>
<li><a href="#sec-8-4">Miscellaneous</a></li>
<li><a href="#sec-8-5">Tmux plugin</a></li>
</ul>
</li>
</ul>
</div>
</div>

# Default Key Bindings<a id="sec-1" name="sec-1"></a>

## remap prefix from 'C-b' to 'C-a'<a id="sec-1-1" name="sec-1-1"></a>

    unbind C-b
    set-option -g prefix `
    bind-key ` send-prefix

## Setting the delay b/w prefix and command<a id="sec-1-2" name="sec-1-2"></a>

    set -s escape-time 1

## Set the base index for windows to 1<a id="sec-1-3" name="sec-1-3"></a>

    set -g base-index 1

# Pane Management<a id="sec-2" name="sec-2"></a>

## Set the base index for panes to 1<a id="sec-2-1" name="sec-2-1"></a>

    setw -g pane-base-index 1

## Reload the config file - <S><a id="sec-2-2" name="sec-2-2"></a>

    unbind !
    bind ! source-file ~/.tmux.conf \; display "Reloaded!"

## Splitting Panes<a id="sec-2-3" name="sec-2-3"></a>

    bind | split-window -h
    bind \ split-window -h
    bind - split-window -v

## Moving b/w panes<a id="sec-2-4" name="sec-2-4"></a>

    unbind l # unbind default binding for `last-window`
    bind h select-pane -L
    bind j select-pane -D
    bind k select-pane -U
    bind l select-pane -R

## Pane resizing<a id="sec-2-5" name="sec-2-5"></a>

    bind -r C-h resize-pane -L 5
    bind -r C-j resize-pane -D 5
    bind -r C-k resize-pane -U 5
    bind -r C-l resize-pane -R 5

## Cycle Panes<a id="sec-2-6" name="sec-2-6"></a>

    unbind Space
    bind   Space select-pane -t :.+  # cycle panes
    bind   C-Space select-pane -t :.-  # cycle panes in reverse

## Kill Pane, if last pane, kill window<a id="sec-2-7" name="sec-2-7"></a>

    bind   x if "tmux display -p \"#{window_panes}\" | grep ^1\$" "confirm-before -p \"Kill the only pane in window? It will kill this window too! (y/n)\" kill-pane" "kill-pane"

## Zoom Panes<a id="sec-2-8" name="sec-2-8"></a>

    bind   z resize-pane -Z

## Copy Current Pane's Path<a id="sec-2-9" name="sec-2-9"></a>

    unbind C-p
    bind   C-p run -b "tmux display -p -F '#{pane_current_path}' | xclip -i" \; display "Copied current path '#{pane_current_path}' to the clipboard."

# Window Management<a id="sec-3" name="sec-3"></a>

## Create new Window and rename it<a id="sec-3-1" name="sec-3-1"></a>

    unbind c
    bind C-n command-prompt -p "New window:" "new-window -c '#{pane_current_path}' -n %1"
    unbind  , # unbind default binding for `rename-window`
    bind r command-prompt -p "New name for this window:" "rename-window '%%'"

## List Windows<a id="sec-3-2" name="sec-3-2"></a>

    bind   ? list-windows -F '#{window_index}:#{window_name}: #{?pane_dead, (dead), (not dead)}'﻿

## Swap Windows<a id="sec-3-3" name="sec-3-3"></a>

    unbind  , # unbind default binding for `rename-window`
    bind -r , swap-window -t -1 # move window one position to the left
    bind -r < swap-window -t -1 # move window one position to the left
    unbind  . # unbind default binding to move window to user provided index
    bind -r . swap-window -t +1 # move window one position to the right
    bind -r > swap-window -t +1 # move window one position to the right

## Kill Window<a id="sec-3-4" name="sec-3-4"></a>

    unbind & # unbind default binding for `kill-window`
    bind C-c confirm-before -p "Kill this window? (y/n)" kill-window

## Switch to another window by name<a id="sec-3-5" name="sec-3-5"></a>

    bind   w split-window "tmux lsw | percol --initial-index `tmux lsw | awk '/active.$/ {print NR-1}'` | cut -d':' -f 1 | xargs tmux select-window -t"

## Forward & Backward b/w windows<a id="sec-3-6" name="sec-3-6"></a>

    bind -r   p previous-window
    bind -r   n next-window

# Session Management<a id="sec-4" name="sec-4"></a>

## Rename Session<a id="sec-4-1" name="sec-4-1"></a>

    bind R command-prompt -p "New name for this session:" "rename-session '%%'"

## Switch to previously selected session<a id="sec-4-2" name="sec-4-2"></a>

    unbind L # unbind default binding for `switch-client -l`
    bind   b switch-client -l # switch to previously selected session

## Switch to another session by name<a id="sec-4-3" name="sec-4-3"></a>

    bind   S split-window "tmux ls | percol --initial-index `tmux ls | awk '/attached.$/ {print NR-1}'` | cut -d':' -f 1 | xargs tmux switch-client -t"

# Mouse<a id="sec-5" name="sec-5"></a>

## Mouse On<a id="sec-5-1" name="sec-5-1"></a>

    setw -g mode-mouse on
    set -g mouse-select-pane on
    set -g mouse-resize-pane on
    set -g mouse-select-window on

# Status Bar<a id="sec-6" name="sec-6"></a>

## Message Text<a id="sec-6-1" name="sec-6-1"></a>

    set -g message-fg black
    set -g message-bg Magenta
    set -g message-command-fg blue
    set -g message-command-bg black

## Mode<a id="sec-6-2" name="sec-6-2"></a>

    setw -g clock-mode-colour colour135
    setw -g mode-attr bold
    setw -g mode-fg colour196
    setw -g mode-bg colour238

## Pane<a id="sec-6-3" name="sec-6-3"></a>

    set -g pane-border-fg black
    set -g pane-active-border-fg brightred

    set -g status-justify centre
    set -g status-bg default
    set -g status-fg colour12
    set -g status-interval 2
    setw -g mode-bg colour6
    setw -g mode-fg colour0

    setw -g window-status-format " #F#I:#W#F "
    setw -g window-status-current-format " #F#I:#W#F "
    setw -g window-status-format "#[fg=magenta]#[bg=black] #I #[bg=cyan]#[fg=colour8] #W "
    setw -g window-status-current-format "#[bg=brightmagenta]#[fg=colour8] #I #[fg=colour8]#[bg=colour14] #W "
    setw -g window-status-current-bg colour0
    setw -g window-status-current-fg colour11
    setw -g window-status-current-attr dim
    setw -g window-status-bg green
    setw -g window-status-fg black
    setw -g window-status-attr reverse

## Status Bar<a id="sec-6-4" name="sec-6-4"></a>

    set -g status-position bottom
    set -g status-bg colour234
    set -g status-fg colour137
    set -g status-attr dim
    set -g status-left "#[fg=colour233,bg=colour241,bold][#S] #[default]"
    set -g status-right '#[fg=colour233,bg=colour241,bold] %a%l:%M:%S #[fg=colour233,bg=colour245,bold] %Y-%m-%d '
    set -g status-right-length 50
    set -g status-left-length 30

    setw -g window-status-current-fg colour81
    setw -g window-status-current-bg colour238
    setw -g window-status-current-attr bold
    setw -g window-status-current-format ' #I#[fg=colour250]:#[fg=colour255]#W#[fg=colour50]#F '

    setw -g window-status-fg colour138
    setw -g window-status-bg colour235
    setw -g window-status-attr none
    setw -g window-status-format ' #I#[fg=colour237]:#[fg=colour250]#W#[fg=colour244]#F '

    setw -g window-status-bell-attr bold
    setw -g window-status-bell-fg colour255
    setw -g window-status-bell-bg colour1

# Terminal Window<a id="sec-7" name="sec-7"></a>

## Title<a id="sec-7-1" name="sec-7-1"></a>

    set   -g set-titles on
    set   -g set-titles-string '#h :: #S :: #W W#I/#{session_windows} :: P#P/#{window_panes}'

# Etc<a id="sec-8" name="sec-8"></a>

## Copy and Paste<a id="sec-8-1" name="sec-8-1"></a>

    bind C-w run -b "tmux show-buffer | pbcopy"
    bind C-y run -b "exec </dev/null; pbpaste | awk 1 ORS=' ' | tmux load-buffer - ; tmux paste-buffer"

## Execute Tmux Command<a id="sec-8-2" name="sec-8-2"></a>

    bind C-x command-prompt # default command-prompt binding "PREFIX :" also works

## Visual Bell<a id="sec-8-3" name="sec-8-3"></a>

    set   -g bell-action any
    set   -g bell-on-alert off
    set   -g visual-bell on

## Miscellaneous<a id="sec-8-4" name="sec-8-4"></a>

    setw  -g aggressive-resize on
    set   -g default-terminal "xterm-256color"
    setw  -g mode-keys         vi
    setw  -g status-keys       vi
    set   -s escape-time       0 # Allows for faster key repetition
    set   -g history-limit     100000
    set   -g display-time      1000 # Duration of tmux display messages in milliseconds

## Tmux plugin<a id="sec-8-5" name="sec-8-5"></a>
