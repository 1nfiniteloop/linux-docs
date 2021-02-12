# System

## Tools

* `apropos` - Search the manual page for program names and descriptions.
* `date` - Print or set the system date and time.
* `dmesg` - Print or control the kernel ring buffer.
* `free` - Display free & used memory on the system.
* `grub-*` - GRUB bootloader configuration.
* `halt` - Halt machine. Deprecated, use `shutdown`.
* `journalctl` - Query the systemd journal.
* `man` - Show manual for a program.
* `reboot` - Deprecated, use `shutdown`.
* `service` - Main utility for managing *System V* services.
* `sudo` - Execute a command as superuser or another user.
* `sysctl` - Configure kernel parameters at runtime.
* `systemctl` - Main utility for managing *systemd* services.
* `update-grub2` - update grub config after reconfiguration.
* `shutdown` - Restart and shutdown (power off).

## Files

* `/etc/timezone` - Contains a string of the current configured timezone.
* `/etc/localtime` - Symbolic link to current timezone data (Check timezone with `readlink /etc/localtime`).
* `/etc/default/grub` - GRUB Bootloader configuration.

## Usage

### System services

Command                                  | Description
-----------------------------------------|-----------------------------------------------------------------
`systemctl list-units --type service`    | List active services. flag `--all` lists all available services.
`systemctl status <service>`             | Show status of service.
`systemctl start|stop|restart <service>` | Start or stop service.

### Kernel configuration

Set kernel parameters, exampls:

* non-persistent: `sudo sysctl net.ipv4.ip_forward=1`.
* Persistent: create a file in `/etc/sysctl.d/60-*.conf`, see further in `/etc/sysctl.d/README`.

### Logs & Journals

* List journals from a systemd-managed service with `journalctl -u systemd-networkd.service`

### Memory

* Show available RAM memory: `free -h`

### System time

* Configure timezone interactively with `sudo dpkg-reconfigure tzdata`.
