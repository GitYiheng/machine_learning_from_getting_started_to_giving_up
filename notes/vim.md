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

`)` move to the start of the next sentence

`(` move to the start of the previous sentence

`}` move to the start of the next paragraph or block of text

`{` move to the start of the previous paragraph or block of text

`ctrl+f` move down one page

`ctrl+b` move back up one page

`gg` go to the first line in the file

`G` go to the last line in the file

`#` where `#` is the number of a line, this command takes you to the line specified

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

`x` delete a single character

`.` repeat last change, with count replaced with `[count]`

# Inserting

`i` insert text before the cursor
  - `3i` `abc` `esc` will insert `abc` 3 times, that is, `abcabcabc`

`I` insert text before the first non-blank in the line

`a` append text after the cursor

`A` append text at the end of the line

`o` begin a new line below the cursor and insert text

`O` begin a new line above the cursor and insert text

# Substitution

`s` (**s**ubstitute) delete the current character and place the user in insert mode with the cursor between the two surrounding characters. For example, `3s` deletes the next three characters and place the user in insert mode.

`c` (**c**hange) take a vi/vim motion (such as `w`, `j`, `b`, etc.). It deletes the characters from the current cursor position up to the end of the movement. Note that this means that `s` is equivalent to `cl` (vim documentation itself claims these are synonyms).
  - `C` = `c$` change text from cursor position to the end of the line
  - `cc` change the entire line

`r` (**r**eplace) never enter insert mode at all. Instead, it expects another character, which it will then use to replace the character currently under the cursor.

`~` switch case of the character under the cursor and move the cursor to the right
  - `g~{motion}` switch case of `{motion}` text. For example, `g~$` switchs cases from the cursor to the end of the line
  - `g~~` = `g~g~` switch cases for the current line

`gU{motion}` make `{motion}` text uppercase
  - `gUU` make the current line uppercase

`gu{motion}` make `{motion}` text lowercase
  - `guu` make the current line lowercase

`J` joint `[count]` lines, with a minimum of two lines. Remove the indent and insert up to two spaces.

`gJ` joint `[count]` lines, with a minimum of two lines. Don't insert or remove any space.

# Replace Mode

`R` enter replace mode: each character you type replaces an existing character, starting with the character under the cursor

# Undo and Redo

`u` undo

`ctrl+r` redo

# Vim Help System

`:h <command>` or `:help <command>` open the documentation for that command

# Deleting, Yanking, and Putting

cut = delete

copy = yank

paste = put

`p` paste text after the cursor from register

`P` paste text before the cursor from register

`y` copy text into register

`yy` copy lines into register

## Register Types

- Unnamed: `""`
  - `""` holds text from `d`, `c`, `s`, `x`, and `y` operations.
- Numbered: `"0`, `"1`, ..., `"9`
  - `"0` holds last text yanked (`y`)
  - `"1` holds last text deleted (`d`) or changed (`c`)
  - Numbered registers shift with each `d` or `c`
- Named
  - `"a`, `"b`, ..., `"z`
- Black hole register: `"_`
  - Can be used to delete things without affecting normal registers

`:reg` display the contents of registers

`"ayw` copy one word into register a (overwrite)

`"Ayw` copy one word into register a (append)

`"ap` paste text from register a after the cursor

# Searching

`f{char}` to `[count]`th occurrence of `{char}` to the right

`F{char}` to `[count]`th occurrence of `{char}` to the left

`;` repeat last `f`, `t`, `F`, `T` `[count]` times

`,` repeat last `f`, `t`, `F`, `T` in opposite direction `[count]` times

`t` till before `[count]`th occurrence of `{char}` to the right

`T` till after `[count]`th occurrence of `{char}` to the left

`/{pattern}[/]<CR>` search forward for the `[count]`th occurrence of `{pattern}` exclusive

`?{pattern}[?]<CR>` search backward for the `[count]`th occurrence of `{pattern}` exclusive

`n` repeat the last `/` or `?` `[count]` times

`N` repeat the last `/` or `?` `[count]` times in opposite direction

`*` search forward for the `[count]`th occurrence of the word nearest to the cursor

`#` search backward for the `[count]`th occurrence of the word nearest to the cursor

`:set hls` highlight search on

`:set nohls` highlight search of:

# Vimrc

- rc = run commands
- System-wide vimrc and personal vimrc
- Unix/Linux/Mac: ~/.vimrc
- Windows: $HOME/_vimrc
- Each line is executed as a command

