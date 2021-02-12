# Processes

## Tools

* `/bin/kill` - send a signal to a process (kill exists as a bash built-in
  command also).
* `pgrep` - look up processes based on name.
* `pkill` - signal processes based on name.
* `pmap` - Report memory map of a process.
* `ps` - report snapshot info about a processes.
* `top` - Display various info continuous about processes.
* `watch` - Periodically execute a program.
* `time` - Run program and summarize system resource usage.

## Files

_None_

## Usage

### top

* Sort by memory usage: `Shift` + `m`.
* Sort by CPU usage: `Shift` + `t`.

### Process info

Command                   | Description
--------------------------|----------------------------------------------------
`sudo pmap <pid>`         | Show memory usage for process.
`echo $$`                 | Get current procees PID.
`cat /proc/<pid>/cmdline` | Get commandline arguments provided from start
`ps -ef`                  | Get all processes (optional flags: `[f|--forest]`).

### Process signals

See more @ `kill --list` and `man signal 7` for all existing signals. Note:
`kill` is also a bash built-in command, which is why `/bin/kill` is used below.

Command                         | Description
--------------------------------|----------------------------------------------
`/bin/kill --signal STOP <pid>` | Pause process, equivalent to `Ctrl` + `Z`.
`/bin/kill --signal INT <pid>`  | Terminate process, equivalent to `Ctrl`+`C`.
`/bin/kill --signal CONT <pid>` | Resume process, equivalent to `fg %<job-no>`.
`/bin/kill --signal KILL <pid>` | Terminate process, forced.
