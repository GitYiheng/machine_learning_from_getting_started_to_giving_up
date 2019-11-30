# Tree

List contents of directories in a tree-like format.

## Installation

```
sudo apt-get install tree
```

## Usage

```
tree [-adfgilnopqrstuxACDFNS] [-L level [-R]] [-H baseHREF] [-T title] [-o filename]
[–nolinks] [-P pattern] [-I pattern] [–inodes] [–device] [–noreport] [–dirsfirst]
[–version] [–help] [directory …]
```

- `--help` outputs a verbose usage listing.
- `--version` outputs the version of tree.
- `-a` all files are printed. By default, tree does not print hidden files (those beginning with a dot `.`). In no event does tree print the file system constructs `.` (current directory) and `..` (previous directory).
- `-d` list directories only.
- `-f` prints the full path prefix for each file.
- `-i` tree will not print the indentation lines. Useful when used in conjunction with the `-f` option.
- `-l` follows symbolic links to directories as if they were directories. Links that would result in a recursive loop are avoided.
- `-x` stay on the current file system only, as with find `-xdev`.
- `-P {pattern}` list only those files that match the wild-card pattern.
- `-I {pattern}` do not list those files that match the wild-card pattern.
- `--prune` makes tree prune empty directories from the output, useful when used in conjunction with `-P` or `-I`.
- `--filelimit #` do not descend directories that contain more than `#` entries.
- `--timefmt {format}` prints (implies `-D`) and formats the date according to the format string which uses the strftime syntax.
- `--noreport` omits printing of the file and directory report at the end of the tree listing.
- `-p` print the protections for each file (as per `ls -l`).
- `-s` print the size of each file along with the name.
- `-u` print the username, or `UID #` if no username is available, of the file.
- `-g` print the group name, or `GID #` if no group name is available, of the file.
- `-D` print the date of the last modification time for the file listed.
- `--inodes` prints the `inode` number of the file or directory
- `--device` prints the device number to which the file or directory belongs
- `-F` append a `/` for directories, a `=` for socket files, a `*` for executable files and a `|` for FIFO’s, as per `ls -F`
- `-q` print non-printable characters in file names as question marks instead of the default carrot notation.
- `-N` print non-printable characters as is instead of the default carrot notation.
- `-r` sort the output in reverse alphabetic order.
- `-t` sort the output by last modification time instead of alphabetically.
- `--dirsfirst` list directories before files.
- `-n` turn colorization off always, over-ridden by the `-C` option.
- `-C` turn colorization on always, using built-in color defaults if the `LS_COLORS` environment variable is not set. Useful to colorize output to a pipe.
- `-A` turn on ANSI line graphics hack when printing the indentation lines.
- `-S` turn on ASCII line graphics (useful when using linux console mode fonts). This option is now equivalent to `--charset=IBM437` and will eventually be depreciated.
- `-L {level}` max display depth of the directory tree.
- `-R` recursively cross down the tree each level directories (see `-L` option), and at each of them execute tree again adding `-o 00Tree.html` as a new option.
- `-H baseHREF` turn on HTML output, including HTTP references. Useful for ftp sites. baseHREF gives the base ftp location when using HTML output. That is, the local directory may be `/local/ftp/pub`, but it must be referenced as `ftp://host-name.organization.domain/pub` (baseHREF should be `ftp://hostname.organization.domain`). Hint: don’t use ANSI lines with this option, and don’t give more than one directory in the directory list. If you want to use colors via CSS stylesheet, use the `-C` option in addition to this option to force color output.
- `-T title` sets the title and H1 header string in HTML output mode.
- `--charset {charset}` set the character set to use when outputting HTML and for line drawing.
- `--nolinks` turns off hyperlinks in HTML output.
- `-o {file_name}` send output to file name.
