# toolset: bash

## Tools

* `clear` - clear the terminal screen.
* `reset` - reset terminal (clear history, etc).
* `stty` - change and print terminal line settings

## Files

* `~/.inputrc` - User configuration for readline.
* `~/.bash_aliases` - User configuration for aliases.
* `/etc/inputrc` - Global system configuration for readline.

## Usage

### Shortcuts

Bash uses library _readline_  for command line editing and shortcuts, see
more @ [References](#references).

Command                  | Description
-------------------------|---------------------------------------------------------------------------------------------------------------------
`Tab`                    | Autocomplete, tap twice to get suggestions.
`Arrow Up/Down`          | Step backward forward in command history.
`Shift`+`Insert`         | Paste text, `Mouse Scroll Wheel` can also be used. _Note:_ Mark text in the terminal emulator is enough for copying.
`Shift` + `Page up/down` | Scroll up and down, comes handy on bare terminals.
`Ctrl` + `A`             | Move to the start of the line (also mapped to `Home`).
`Ctrl` + `E`             | Move to the end of the line (also mapped to `End`).
`Ctrl` + `U`             | Remove all text before cursor.
`Ctrl` + `K`             | Remove all text after cursor.
`Ctrl` + `W`             | Remove/cut the word before cursor.
`Ctrl` + `D`             | Remove/cut the word after cursor*
`Ctrl` + `Y`             | Paste last cut word, then step backwards in buffer with `Alt` + `Y`.
`Alt` + `U`              | Uppercase current word, from cursor until next blankspace.
`Alt` + `L`              | Lowercase current word, from cursor until next blankspace.
`Ctrl` + `Shift` + `-`   | Undo
`Ctrl` + `R`             | Reverse-search through command history, repeat to continue step backwards.
`Ctrl` + `Shift` + `R`   | Step forward in search through command history.

\* __NOTE:__ `Ctrl` + `D` is bound to emit end-of-file in the terminal driver
and has precedence over bash shortcut. This closes the input stream and thus
exit the shell.

### Input and output

Command              | Description
---------------------|---------------------------------------------------------------
`cat <<< "text"`     | Send text to _stdin_
`command 2> log.txt` | Send _stderr_ to file. _stdout_ is still printed onto console.
`command &> log.txt` | Send both _stdout_ and _stderr_ to file.
`program |& less`    | _stderr_ (2) is merged onto _stdout_ (1) stream.
`program 2>&1 |less` | Same as above.

### Jobs & processes

Bash has some built-in keywords for controlling processes (see more with
`help jobs fg bg kill`). Many of the keywords has an equvivalent shortcut,
e.g. `Ctrl` + `Z` for pausing a process. The shortcuts is handled by the
_terminal-driver_ and not through bash, see `stty --all` for available
key-bindings.

Command    | Description
-----------|---------------------------------------------------
`jobs`     | List job(s)
`kill %n`  | Terminate jobs, or use `Ctrl`+`C` if in foreground
`Ctrl`+`Z` | Pause job
`bg %n`    | Resume job and run in background
`fg %n`    | Resume job and run in foreground

\* where _n_ is the job number

### Environment variables

Command                   | Description
--------------------------|------------------------------------------
`export <variable>`       | Allow subprocesses to gain
`${HOME}`                 | User's home directory
`varable="value" command` | Set environment variable to process only.

## References

* [1] <https://www.gnu.org/software/bash/manual/bash.html>
