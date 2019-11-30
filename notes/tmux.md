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
