# system: adjust swap size

This instruction describes how to adjust swap partition size on the disk.

## Steps

1. Disable swap with `sudo swapoff --all`.
2. Adjust size of swap partition. Example if using LVM:
   `sudo lvresize --size 4G /dev/mapper/samsung--ssd--vg-swap_1`
3. Setup swap partition with `sudo mkswap /dev/mapper/samsung--ssd--vg-swap_1`.
4. If swap partition is referred with `UUID`, make sure to adjust `/etc/fstab`
   accordingly to what `sudo blkid -t TYPE=swap` outputs.
5. Enable swap again with `sudo swapon --all`.
6. Make sure swap is available and working with `cat /proc/swaps`.
