# Vim

Vim is a text editor designed for Unix.

Vim = Vi + IMproved

Vi is short for "visual".

Vi has been replaced by Vim.

# Modes

- Normal/Command Mode
- Insert Mode
- Line Mode
- Etc.

Everything you type in normal mode is a command.

To enter insert mode, type `i` while in normal mode.

To leave insert mode, press Escape.

To enter line mode, type `:` while in normal mode.

After a command completes in line mode you are returned to normal mode.

You can also leave command mode by pressing Escape.

# Navigation

`h` left

`l` right

`j` down

`k` up

`w` jump by start of words (punctuation considered words)

`W` jump by words (spaces separate words)

`e` jump to end of words (punctuation considered words)

`E` jump to end of words (no punctuation)

`b` move backward by a word (punctuation considered words)

`B` move backward by a word (no punctuation)

`0` move to the start of the line

`^` move to the first non-blank character of the line

`$` move to the end of the line

`ctrl+f` move down one page

`ctrl+b` move back up one page

`gg` go to the first line in the file

`G` go to the last line in the file

`ctrl+g` print the current file name, the cursor position, and the file status

# Save and Exit

`:w` save file

`:wq` save and quit

`:q!` quit without saving

# Deleting

`d` delete the character under and after the cursor

`D` delete the character before the cursor

`dw` delete from the cursor to the end of the word

`db` delete the part of the word before the cursor

`dd` delete the line

# Undo and Redo

`u` undo

`ctrl+r` redo

# Vim Help System

`:h <command>` or `:help <command>` open the documentation for that command

# Deleting, Yanking, and Putting

`p` paste text after the cursor from register

`P` paste text before the cursor from register

`y` copy text into register

`yy` copy lines into register

`:reg` display the contents of registers

`"ayw` copy one word into register a (overwrite)

`"Ayw` copy one word into register a (append)

`"ap` paste text from register a after the cursor

# Vimrc

- rc = run commands
- System-wide vimrc and personal vimrc
- Unix/Linux/Mac: ~/.vimrc
- Windows: $HOME/_vimrc
- Each line is executed as a command

