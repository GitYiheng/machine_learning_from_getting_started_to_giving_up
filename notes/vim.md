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

`:[range]s/{pattern}/{string}/[flags] [count]` for each line in `[range]` replace a match of `{pattern}` with `{string}`
  - `:s/old/new/g` replace old with new in the current line
  - `:1s/is/isn't/` replace `is` with `isn't` in the 1st line
  - `:1,5s/for/FOR/g` replace all `for` with `FOR` from line 1 to line 5
  - `$` represents last line
  - `.` represents current line
  - `.,$` represents from current line to last line
  - `%` represents all lines, that is entire file
  - `:%s/{pattern}/{string}/g` global substitution

# Line Number

`:set nu` turn on line number

`:set nonu` turn off line number

`:set nu!` toggle line number

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

# Window Split

`:[N]sp [++opt] [+cmd] [file]` or `CTRL+W s` split current window in two. The result is two viewports on the same file. Make the new window `N` high (default is to use half the height of the current window). Reduces the current window height to create room. If `[file]` is given it will be edited in the new window. If it is not loaded in any buffer, it will be read. Else the new window will use the already loaded buffer. **sp**lit

`:[N]vs [++opt] [+cmd] [file]` or `CTRL+W v` like `:split`, but split vertically. **v**ertical**sp**lit

`:[N]new [++opt] [+cmd]` or `CTRL+W n` create a new window and start editing an empty file in it. Make new window `N` high (default is to use half the existing height). Reduces the current window height to create room.

`:[N]vne [++opt] [+cmd] [file]` like `:new`, but split vertically.

`:[N]sp [++opt] [+cmd] {file}` create a new window and start editing file `{file}` in it. This behaves like a `:split` first, and then an `:e` command. If `[+cmd]` is given, execute the command when the file has been loaded `+cmd`.

`:[N]sv [++opt] [+cmd] {file}` same as `:split`, but set `readonly` option for this buffer. **s**plit**v**iew

`:[N]sf [++opt] [+cmd] {file}` same as `:split`, but search for `{file}` in `path` like in `:find`. Doesn't split if `{file}` is not found.

`:{count}on[!]` or `CTRL+W o` make the current window the only one on the screen. All other windows are closed.

`CTRL+W` + `h` or `j` or `k` or `l` switch among splitted windows.

`CTRL+W` + `H` or `J` or `K` or `L` move splitted windows to the designated position.

`CTRL+W` + `+` or `-` or `<` or `>` or `=` adjust height and width of current window split.

`CTRL+W` + `r` or `R` rotate windows.

# Text Objects

`{operator}{a}{object}`
  - `daw` delete a word
  - `das` delete a sentence
  - `dap` delete a paragraph
  - `da[` or `da]` delete content in `[...]` including the square brackets
  - `da(` = `da)`, `da<` = `da>`, `da{` = `da}` = `daB`, `da"`, `da'` work in the same way
  - `dat` delete content within a tag including the tag, `<p>...</p>` &rarr; ` `

`{operator}{a}{object}`
  - `ciw` change inner word
  - `dis` delete inner sentence
  - `dip` delete inner paragraph
  - `di[` or `di]` delete content in `[...]` but the square brackets are untouched
  - `di(` = `di)`, `di<` = `di>,``di{` = `di}` = `diB`, `di"`, `di'` work in the same way
  - `dit` delete content within a tag but the tag is untouched, `<p>...</p>` &rarr; `<p></p>`

# Macros

Recording a macro is a great way to perform a one-time task, or to get things done quickly when you don't want to mess with Vim script or mappings, or if you do not yet know how to do it more elegantly.

Each register is identified by a letter `a` to `z`.

To enter a macro, type:

`q<letter><commands>q`

To execute the macro <number> times (once by default), type:

`<number>@<letter>`

In plain language, to record a macro, use the `q` command followed by a register name. To stop, type `q` again. There is no special macro register. There is only one `a` register, for example. To replay the macro use `@` followed by the register name. To repeat the most recent macro, use `@@`.

`:{range}norm[!] {commands}` execute normal commands `{commands}` for each line in the `{range}`. Before executing the `{commands}`, the cursor is positioned in the first column of the range, for each line.

For example, `:27,35norm @d` applys the macro in register `d` from line 27 to line 35.

You also can edit macros. For example, use `"ap` to paste content in register `a` and edit it. Then `0"ay$` to save the modified content into register `a`.

Notes: `CTRL-V + esc` represent escape

`q{register}` overwrite the register

`q{CAPITAL_REGISTER}` append to the register

Save macros in `vimrc` file:

`let @{register} = 'keystrokes'`

# Visual Mode

When editing text with Vim, visual mode can be extremely useful for identifying chunks of text to be manipulated.

Vim's visual mode has three versions: character, line, and block. The keystrokes to enter each mode are:

- Character mode: `v`
- Line mode: `V`
- Block mode: `CTRL+V`

While in (any of the three) Visual mode(s), pressing `o` will move the cursor to the opposite end of the selection. In Visual Block mode, you can also press `O`, allowing you to position the cursor in any of the four corners.

`iw` in visual mode selects the inner word.

`ap` in visual mode selects the paragraph.

`gv` start visual mode with the same area as the previous area and the same mode. In visual mode the current and the previous visual area are exchanged. After using `p` or `P` in visual mode the text that was put will be selected.

You can use `>>` and `<<` to indent and unindent. `>{text_object}` and `>{text_object}` work as well.

`:set shiftwidth=4`

`:set list`

`:set list!`

`:set expandtab`

Use visual mode to select target content and press `:` enters the command mode `:'<,'>`. Type `ce 80` (i.e. `:'<'>center 80`) to center selected text based on 80-character width. Similarly, `le` for left aligned, `ri` for right aligned.

# Vimrc

- rc = run commands
- System-wide vimrc and personal vimrc
- Unix/Linux/Mac: ~/.vimrc
- Windows: $HOME/_vimrc
- Each line is executed as a command
  - `set ruler` = `:set ruler`

Key mapping refers to creating a shortcut for repeating a sequence of keys or commands. You can map keys to execute frequently used key sequences or to invoke an Ex command or to invoke a Vim function or to invoke external commands. Using key maps you can define your own Vim commands.

`:map {lhs} {rhs}` map the key sequence `{lhs}` to `{rhs}` for the modes where the map command applies. The result, including `{rhs}`, is then further scanned for mappings. This allows for nested and recursive use of mappings.

For example, `:map <F2> i# Author:<CR># Date Created:<CR># Description:<CR># Date Modified:<CR><CR>`

- `<BS>` backspace
- `<CR>` enter
- `<Enter>` enter
- `<Return>` enter
- `<Esc>` escape
- `<Space>` space
- `<Up>` up arrow
- `<Down>` down arrow
- `<Left>` left arrow
- `<Right>` right arrow
- `<Insert>` insert
- `<Del>` delete
- `<Home>` home
- `<End>` end
- `<PageUp>` page-up
- `<PageDown>` page-down
- `<Tab>` tab
- `<bar>` `|`
- `<C-X>` CTRL-X
- `<F1>-<F12>` function keys

# Buffers

`:e [++opt] [+cmd] {file}` edit `{file}`. This fails when changes have been made to the current buffer, unless `:set hidden`.

- `%` means that this line corresponds to the buffer in the current window.
- `a` means that it is an active buffer which is loaded and visible
- `h` means that it is now a hidden buffer
- `#` means that it is the alternate buffer

`:ls[!] [flag]` show all buffers.

`:[N]b[!] [+cmd] [N]` edit buffer `[N]` from the buffer list. If `[N]` is not given, the current buffer remains being edited.

`:[N]bn[!] [+cmd] [N]` go to `[N]`th next buffer list. `[N]` defaults to one. Wraps around the end of the buffer list.

`:[N]bp[!] [+cmd] [N]` go to `[N]`th previous buffer list. `[N]` defaults to one. Wraps around the end of the buffer list.

`:bf [+cmd]` go to first buffer in buffer list. If the buffer list is empty, go to the first unlisted buffer.

`:bl[!] [+cmd]` go to last buffer in buffer list. If the buffer list is empty, go to the last unlisted buffer.

`:bad [+lnum] {fname}` add file name `{fname}` to the buffer list, without loading it. If `lnum` is specified, the cursor will be positioned at that line when the buffer is first entered.

`:bd[!] [N]` unload buffer `[N]` (default: current buffer) and delete it from the buffer list. If the buffer was changed, this fails, unless when `[!]` is specified, in which case changes are lost. The file remains unaffected. Any windows for this buffer are closed. If buffer `[N]` is the current buffer, another buffer will be displayed instead. This is the most recent entry in the jump list that points into a loaded buffer.

`:bdelete[!] {bufname}` delete buffer given by name.

`:bdelete[!] N1 N2` delete buffer for given number.

`[range]bufdo[!] {cmd}` execute `{cmd}` in each buffer in the buffer list or if `[range]` is given only for buffers for which their buffer number is in the `[range]`. For example, `:bufdo %s/#/@/g | w`.

`:wa` write all changed buffers.

`:[N]Explore[!] [dir]...` explore directory of current file. Will open the local-directory browser on the current file's directory (or on directory `[dir]` if specified). The window will be split only if the file has been modified and `hidden` is not set, otherwise the browser window will take over the window. Normally the splitting is taken horizontally.
