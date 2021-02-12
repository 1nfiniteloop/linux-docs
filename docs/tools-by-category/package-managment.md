# Package managment

## Tools

* `apt` - Front-end for apt-* package manager.
* `apt-cache` - Query apt cache.
* `apt-get` - Package manager for Debian (main utility).
* `dpkg` - Package manager for Debian (low-level utility).

## Files

* `/etc/apt/sources.list` - apt mirrors.
* `/var/lib/apt/lists` - apt index files (from apt-get update).
* `/var/cache/apt/archives` - cached installed packages.

## Usage

### Ubuntu

Command                                 | Description
----------------------------------------|---------------------------------------------
`apt-cache search <regex-match>`        | Search for a package candidate to install.
`apt-cache policy libssl-dev`           | Search for available versions to install
`apt-cache show gcc`                    | Show info about a package:
`apt-get install <package>[=<version>]` | Install a specific version
`apt-get autoremove`                    | Remove old packages.
`dpkg --search pwd.h`                   | Which package a program/file comes from
`dpkg --listfiles libcurl4`             | Show which files inside an installed package
`dpkg --contents <package-name>.deb`    | Show which files inside a debian file
`dpkg --list`                           | List packages installed
`dpkg --status make`                    | Report package status (dependencies, etc)
