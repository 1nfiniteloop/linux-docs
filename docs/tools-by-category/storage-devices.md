# Storage devices

## Tools

* `dd` - File/block copy utility.
* `fdisk` - Partition tool, menu-driven.
* `gparted` - Graphical version of parted.
* `lsblk` - List block devices.
* `lshw` - List hardware details of the machine.
* `parted` - Partition tool, GNU partiton manipulation program.
* `resize2fs` - Resize file systems (ext2, ext3, ext4).
* `sfdisk` - Partition tool, non-interactive.
* `sync` - Synchronize cached writes to persistent storage.

## Files

* `/etc/fstab` - Configuration file containing filesystems to mount on boot (
  see `man fstab`).
* `/etc/mtab` - Contains current mounted file systems.
* `/sys/block/*` - Block devices.

## Usage

### Block devices

Command                                                       | Description
--------------------------------------------------------------|----------------------------------------------------------------
`lsblk -o NAME,TYPE,FSTYPE,MOUNTPOINT,SIZE,UUID`              | List available block devices, detailed.
`sudo lshw -class disk`                                       | Show details about storage hardware.
`cat /sys/block/<dev>/device/{model,vendor}`                  | Show details about storage hardware, manually.
`sudo su -c "/sys/block/<dev>/device/delete <<< 1"`           | Unregister storage device before detach disk (hot-swap).
`dd if=<img> of=/dev/mmcblk0 bs=1M status='progress' && sync` | Copy image to memory card and show progress.
`sfdisk --list <img|dev>`                                     | List partition table of image or block device.
`mount -o offset=$((2848*512)) <img> /mnt`                    | Mount partition of image where offset=2048 and sector-size=512.

## Notes

### Block device names

Block device names as `/dev/sda`, `/dev/sdb` are not stable across reboots,
or across machines in a cluster. The names are assigned on a first come, first
served basis by the kernel. It is prefereed to always refeer the disks from
`/dev/disk/by-path` or `/dev/disk/by-uuid` in configurations instead.
