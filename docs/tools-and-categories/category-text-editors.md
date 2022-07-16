# category: text editors

## Tools

* `aspell` - Interactive spell checker.
* `less` - Read text-files.
* `more` - Page through text, only in downward direction.
* `nano` - Read -and manipulate text-files.
* `vi` - Read -and manipulate text-files.

## Files

* `~/.vimrc` - configuration file for vi and vim.

## Usage

### vi, less

Common flags to `less`:

* `-R` output in ANSI "color". Example used with `grep --color=always |less -R`.
* `-N` output line numbers.

__Navigate:__

Command                      | Description
-----------------------------|----------------------------------------------------------------
`i`                          | Enter text insertion mode (exit with `Esc`)
`:q`                         | Exit editor
`:q!`                        | Exit editor without saving
`:wq`                        | Exit editor and save changes
_line no_ + `G`              | Goto line
`G`                          | Goto last line
`g`                          | Goto first line
`:p`                         | Goto previous file
`:n`                         | Goto next file
`h`                          | Help (`q` to quit help-view)
`:%s/text/replacement/gi`    | Replace on all rows (%) all in row (g), case insensitive (i)
`:10,20s/text/replacement/g` | Replace all (g) occurences on row 10-20
`:s/text/replacement/`       | Replace first occurence on current row
`:set number`                | Show row numbers, use `nonumber` to turn off
`/` + _text_ + `Enter`       | Search forward
`?` + _text_ + `Enter`       | Search backward
`n`                          | Search next forward
`N`                          | Search next backward
`-i`                         | toggle case-insesnitive in searches
`:e <path>`                  | Open file from interactive menu (for vim, might not work in vi)

__Manipulate (only for vi):__

* `y` means yank (copy) content.
* `p` means put (paste) content.
* `d` means delete (cut) content.

Command                  | Description
-------------------------|-----------------------------------------------------------------
`i`                      | Edit text (exit insert-mode with `Esc`)
_number-of-lines_ + `dd` | Cut lines
_number-of-lines_ + `yy` | Copy lines
`yaw`                    | Copy  word, until next whitespace (included)
`yiw`                    | Copy word, until next whitespace (not included)
`y$`                     | Copy content right of the cursor, until end
`y^`                     | Copy content left of the cursor, until beginning
`ytx`                    | Copy until character _x_
`v`                      | Mark text in visual mode, followed by `y` to copy or `d` to cut.
`p` or `P`               | Paste lines before or after cursor.
`Ctrl` + `r`             | Redo
`u`                      | Undo

__Note:__ if `vi` does not work as expected when editing files, install `vim` or
add `set nocompatible` into `~/.vimrc`.

### nano

__Navigate:__

Command                | Description
-----------------------|--------------------
`Ctrl` + `x`           | Exit editor
`Ctrl` + `Shift` + `-` | Goto line
`Alt` + `/`            | Goto last line
`Alt` + `\`            | Goto first line
`Ctrl` + `g`           | Open help section
`Ctrl` + `w` (or `F6`) | Search
`Alt` + `w`            | Search next forward

__Manipulate:__

Command      | Description
-------------|------------
`Ctrl` + `k` | Cut lines
`Alt` + `6`  | Copy lines
`Ctrl` + `u` | Paste lines
`Alt` + `E`  | Redo
`Alt` + `U`  | Undo

__Note:__ In help section:

* `^` = `Ctrl` key
* `M` = `Alt` key

## Reference

* <https://vim.rtorr.com/>