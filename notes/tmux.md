# tmux

tmux is a terminal multiplexer: it enables a number of terminals to be created, accessed, and controlled from a single screen. tmux may be detached from a screen and continue running in the background, then later reattached.

## Installation

```
sudo apt install tmux
```

## Starting Your First Tmux Session

To start your first Tmux session, simply type `tmux` in your console:

```
tmux
```

This will open a new session, create a new window, and start a shell in that window.

Once you are in tmux you will notice a status line at the bottom of the screen which shows information about the current session.

You can now run your first tmux command. For example, to get a list of all commands, you would type:

`CTRL+B` then `d`

## Creating Named tmux Sessions

By default, tmux sessions are named numerically. Named sessions are useful when you run multiple tmux sessions. To create a new named session, run the tmux command with the following arguments:

```
tmux new -s session_name
```

It’s always a good idea to choose a descriptive session name.

## Detaching from tmux Session

You can detach from the Tmux session and return to your normal shell by typing:

`CTRL+B` then `d`

The program running in the Tmux session will continue to run after you detach from the session.

## Re-attaching to tmux Session

To attach to a session first, you need to find the name of the session. To get a list of the currently running sessions type:

```
tmux ls
```

The name of the session is the first column of the output.

```
0: 1 windows (created Sat Nov 30 06:42:14 2019) [80x23]
session_name: 1 windows (created Sat Nov 30 06:44:38 2019) [80x23] (attached)
```

As you can see from the output, there are two running tmux sessions. The first one is named `0` and the second one `session_name`.

For example, to attach to session `0`, you would type:

```
tmux attach-session -t 0
```

## Working with tmux Windows and Panes

When you start a new tmux session, by default, it creates a single window with a shell in it.

To create a new window with shell type `CTRL+B` then `c`, the first available number from the range `0...9` will be assigned to it.

A list of all windows is shown on the status line at the bottom of the screen.

Below are some most common commands for managing Tmux windows and panes:

- `CTRL+B` then `c` create a new window (shell)
- `CTRL+B` then `w` choose window from a list
- `CTRL+B` then `0` switch to window `0` (by number)
- `CTRL+B` then `,` rename the current window
- `CTRL+B` then `%` split current pane horizontally into two panes
- `CTRL+B` then `"` split current pane vertically into two panes
- `CTRL+B` then `o` go to the next pane
- `CTRL+B` then `;` toggle between the current and previous pane
- `CTRL+B` then `x` close the current pane

## Resizing Panes

- `CTRL-B` then `:`, followed by `resize-pane -direction number_of_cells`
  - e.g. `resize-pane -U 10`, `resize-pane -D 20`, `resize-pane -L 30`, `resize-pane -R 40`

## Customizing tmux

When tmux is started, it reads its configuration parameters from `~/.tmux.conf` if the file is present.

Here is a sample `~/.tmux.conf` configuration with customized status line and few additional options:

```
# Improve colors
set -g default-terminal 'screen-256color'

# Set scrollback buffer to 10000
set -g history-limit 10000

# Customize the status line
set -g status-fg  green
set -g status-bg  black
```

## Kill a Session

```
tmux kill-session -t target_session
```

## Session Management

`tmux new -s session_name` creates a new tmux session named `session_name`

`tmux attach -t session_name` attaches to an existing tmux session named `session_name`

`tmux switch -t session_name` switches to an existing session named `session_name`

`tmux list-sessions` lists existing tmux sessions

`tmux detach (prefix + d)` detach the currently attached session

## Windows

tmux has a tabbed interface, but it calls its tabs "windows". To stay organized, it is recommended to rename all the windows based on their purposes.

`tmux new-window (prefix + c)` create a new window

`tmux select-window -t :0-9 (prefix + 0-9)` move to the window based on index

`tmux rename-window (prefix + ,)` rename the current window

## Panes

`tmux split-window (prefix + ")` splits the window into two vertical panes

`tmux split-window -h (prefix + %)` splits the window into two horizontal panes

`tmux swap-pane -[UDLR] (prefix + { or })` swaps pane with another in the specified direction

`tmux select-pane -[UDLR]` selects the next pane in the specified direction

`tmux select-pane -t :.+` selects the next pane in numerical order

## Helpful tmux commands

`tmux list-keys` lists out every bound key and the tmux command it runs

`tmux list-commands` lists out every tmux command and its arguments

`tmux info` lists out every session, window, pane, its pid, etc.

`tmux source-file ~/.tmux.conf` reloads the current tmux configuration (based on a default tmux config)

## tmux and Vim

Install the `vim-tmux-navigator` Vim plugin from Chris Toomey. With `vundle`, that’s as simple as adding the following to your `~/.vimrc` file: `Bundle 'christoomey/vim-tmux-navigator'`

Add the following to your `~/.tmux.conf` configuration file to conditionally bind the movement keys depending on the active command:

```
# smart pane switching with awareness of vim splits
bind -n C-h run "(tmux display-message -p '#{pane_current_command}' | grep -iq vim && tmux send-keys C-h) || tmux select-pane -L"
bind -n C-j run "(tmux display-message -p '#{pane_current_command}' | grep -iq vim && tmux send-keys C-j) || tmux select-pane -D"
bind -n C-k run "(tmux display-message -p '#{pane_current_command}' | grep -iq vim && tmux send-keys C-k) || tmux select-pane -U"
bind -n C-l run "(tmux display-message -p '#{pane_current_command}' | grep -iq vim && tmux send-keys C-l) || tmux select-pane -R"
bind -n C-\ run "(tmux display-message -p '#{pane_current_command}' | grep -iq vim && tmux send-keys 'C-\\') || tmux select-pane -l"
```
