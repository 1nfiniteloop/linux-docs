# Users

## Tools

* `addgroup` - Add new group to system, interactive.
* `adduser` - Add new user to system, interactive.
* `chage` - Manage password change interval.
* `chpasswd` - Change login passsword (batched, suitable in scripts).
* `delgroup` - Remove group from system.
* `deluser` - Remove user from system.
* `groupadd` - Add group to system (low level utility, suitable in scripts).
* `groupdel` - Remove group from system.
* `groupmod` - modify a group definition on the system, example change gid.
* `id` - Print user and group IDs.
* `last` - Show a listing of last logged in users.
* `newgrp` - Start a shell with a new primary group (use exit to change back).
* `passwd` - Change login passsword, interactive.
* `useradd` - Add user to system (low level utility, suitable in scripts).
* `usermod` - Modify a user account.
* `w` - Show who is logged on and what they are doing.
* `who` - show who is logged on.
* `whoami` - Print current user.

## Files

* `/etc/environment` - User's $PATH
* `/etc/passwd` - User database
* `~user` - Home directory of _user_.

## Usage

Command                                      | Description
---------------------------------------------|-----------------------------------------------------------------------------
`getent passwd [<user>]`                     | Show all users (equivalent to `cat /etc/passwd`), or about a specific user.
`getent group [<group>]` or `cat /etc/group` | Show all groups (equivalent to `cat /etc/group`), or about a specific group.
`adduser <username>`                         | Add new user, with default values (password, home-directory, group, etc)
`adduser <existing-user> <existing-group>`   | Add user to group*
`deluser <username>`                         | Remove user from system.
`deluser <existing-user> <existing-group>`   | Remove user from group*
`groupadd <groupname>`                       | Add new group to system.
`groupdel <groupname>`                       | Remove group from system.
`passwd [<user>]`                            | Change password for current user, or for _\<user\>_.

\* User need to logout and login for change to affect.
