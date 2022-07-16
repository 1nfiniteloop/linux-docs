# system: recovery

This instruction describes some common steps for how to recover Ubuntu system.

## Mount rootfs

This can be done from another system such as Alpine Linux run from ram, or from
Ubuntu Live CD (read more @ <https://help.ubuntu.com/community/LiveCdRecovery>).

1. Find name and type of the root partition.
2. Mount root-partition with `sudo mount /dev/<dev> /mnt` or if using LUKS
   combined with LVM:

        sudo cryptsetup open --type luks /dev/<partition> <name>
        sudo mount /dev/mapper/<name>

3. If boot partition is separated, mount it with `sudo mount /dev/<dev> /mnt/boot`.
4. Mount virtual folders:

        sudo mount --bind /dev /mnt/dev
        sudo mount --bind /proc /mnt/proc
        sudo mount --bind /sys /mnt/sys

5. Change root with `sudo chroot /mnt` and make the changes.

## Reconfigure grub bootloader

1. Open grub configuration with `vi /etc/default/grub`.
2. Disable splash screen to show kernel and systemd boot logs by removing
   `quiet splash` from `GRUB_CMDLINE_LINUX_DEFAULT` as example.
3. Update grub2 with `sudo update-grub2`.

## Reconfigure initramfs

Read more about initramfs @ <https://wiki.ubuntu.com/Initramfs>.

__NOTE:__ If reconfiguration is made from inside chroot:

1. Make sure the name used with `cryptsetup luksOpen <partition> <name>` is the
   same as in `/etc/crypttab`. Else there will be a mismatch during initramfs
   reconfiguration which is difficult to diagnose because as a result luks
   decryption prompt won't show up on boot.
2. The tool `cryptsetup` might not be included when updating initramfs manually.
   Change `/etc/cryptsetup-initramfs/conf-hook` with `CRYPTSETUP=y` to always
   include.

Update initramfs on latest kernel with: `sudo update-initramfs -u`
