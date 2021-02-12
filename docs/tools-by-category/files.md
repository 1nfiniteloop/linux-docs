# Files

## Tools

* `basename` - Strip directory from filenames (`/a/b/c.txt` -> `c.txt`).
* `cat` - Concatenate files.
* `chgrp` - Change file ownership (group).
* `chmod` - Change file permissions.
* `chown` - Change file ownership (user and group).
* `cmp` - Compare binary files.
* `cp` - Copy files and directories.
* `diff` - Compare text-files and output diff.
* `dirname` - Get directory of an absolute path (`/a/b/c.txt` -> `/a/b`).
* `du` - Size of files & folders.
* `fuser` - List processes using files or sockets.
* `file` - Get which file type.
* `find` - Find files by name.
* `grep` - Find files by content.
* `head` - Output first part of file.
* `hexdump` - Dump file in ASCII, decimal, hexadecimal, octal (see also `xxd`).
* `install` - Copy files and set attributes.
* `ln` - Make links between files.
* `mv` - Move files and folders.
* `mktemp` - Create a temporary file or directory (with a random suffix).
* `md5sum` - File checksum using md5 algorithm.
* `readlink` - Print value of a symbolic link (or canonical file name).
* `sha1sum` - File checksum using sha1 algorithm.
* `stat` - Get file info (size, type, inode, permissions).
* `touch` - Create empty file (or alter existing file timestamp).
* `truncate` - shrink or extend the size of a file to the specified size.
* `rm` - Remove files and folders.
* `split` - Split file into pieces.
* `tail` - Output last part of file.
* `umask` - Set file mode creation mask in folder.
* `xxd` - Make a hexdump or do the reverse (see also `hexdump`).

## Usage

### Copying

* Copy content of directory into other: `cp -a /source/. /dest`
* Move content of directory into other: `mv /source/* /dest`

### File permissions & ownership

Bit   | Decimal | Name | Description
------|---------|------|-------------------------------------------------------------
`001` | 1       | x    | Execute, allow file to be executed or folder to be examined.
`010` | 2       | w    | Write
`100` | 4       | r    | Read

__Examples:__

Command             | Description
--------------------|--------------------------------------------------------
`chmod 744 <file>`  | Set permissions to: user=7(rwx), group=4(r), other=4(r)
`chmod +x <file>`   | Make file executable for all.
`chmod a+x <file>`  | Make file executable for all.
`chmod go-w <file>` | Remove write-permissions for group and others.

### Search

Common flags to `grep`:

* `[-r|--recursive]`
* `[-n|--line-number]`
* `[-l|--files-with-matches]` List files with matches, instead of the matched line.
* `[-E|--extended-regexp]` Use regular experssions in match string.

Command                                            | Description
---------------------------------------------------|-----------------------------------------------------------------------------------
`find . -type d -name <directory> -prune`          | Find directory by name, don't examine inside  target directory iteself (`-prune`).
`find . -type f -name '*.cc' -o '*.h'`             | find all file by type(s), where `-o` means logical OR.
`grep -r -E '^#include <algorithm>$' <directory>`  | Find files containing match.
`find . -type f -name '*.h' |xargs grep '<match>'` | Find match in all filenames with suffix .h.

### Examine files

Command                       | Description
------------------------------|-----------------------------------------------------
`file <file-name>`            | Determine file type.
`stat <file-name>`            | Display file status and details.
`stat -c "%a %n" <file-name>` | Display file or folder permissions in octal.
`du -sh <file-or-directory>`  | Check total size of file or folder and its content.
`du -hPd 1 / |sort -hr`       | Check total size of folders in root, sorted by size.
`lsof <file-or-directory>`    | Check what process uses this directory or file.
`fuser <file>`                | Identify processes using files (or sockets).

### Compare files

Command                                    | Description
-------------------------------------------|--------------------------------------------
`md5sum <first-file> <second-file>`        | Compare files by checksum
`diff -u first.txt second.txt`             | Compare text files and output diff.
`diff -ruN <first-folder> <second-folder>` | Compare two directories and output diff.
`cmp <first-file> <second-file>`           | Compare binary files and output first diff.
