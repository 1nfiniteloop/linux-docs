
# Boot manually

This document describes how to manualy boot a Linux system. This might be
necessarry to fault-trace faulty systems and fix issues during boot.

## GRUB

Ubuntu uses grub as bootloader.

__Note:__ If no GRUB boot menu appears try press `Shift` after BIOS, or `Esc`
if using UEFI. See more @ <https://help.ubuntu.com/community/Grub2#Hidden>.

### Boot kernel manually from grub

1. Enter grub command line pressing `c` in the grub menu.
2. Check which kernel versions is available in `/boot`
3. Load kernel with `linux /boot/vmlinuz-4.4.0-104-generic root=/dev/sda1`
4. Load ramdisk with `initrd /boot/initrd.img-4.4.0-104-generic`
5. boot by typing `boot`

### Drop into initramfs

1. In grub, press any key to interrup the boot process.
2. Enter boot script by pressing `e` in the grub menu.
3. To interrupt in the initramfs add `break=init` to the kernel cmdline, i.e.
   the row with the "linux" command. Continue boot by presssing `F10`.
4. You've been dropped into a initramfs shell. The kernel has booted and the
   system is just about to start the init process.
5. Continue the boot by typing `exit`.

Ref: <https://wiki.ubuntu.com/DebuggingKernelBoot#Dropped_into_a_initramfs_shell>

### Boot into custom runlevel

1. In grub, press any key to interrup the boot process.
2. Enter boot script by pressing `e` in the grub menu.
3. Append the desired runlevel example `1` for single-user (rescue) mode to the
   kernel cmdline, i.e. the row with the "linux" command. Continue boot by
   presssing `F10`.
4. Continue boot by changing to normal runlevel with
   `systemctl isolate graphical.target` (Ubuntu uses `systemd,` not `init`).
