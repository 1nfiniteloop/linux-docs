# storage: create raw disk image

This instruction describes how to create a raw disk image, without need of root
privileges. I use this when creating customized Alpine Linux installations for
Raspberry Pi as example. It can also be used to create customized virtual
machine disks.

The disk created in this example consists of one boot partition of type _vfat_
and one root partition of type _ext4_.

## Steps

### Preparation

* Set name on image with `prefix_name=alpine-linux`.

### Create image

1. Allocate space for partitions as separate files:

        # "The default start offset for the first partition is 1 MiB", see "man sfdisk"
        truncate -s 1M ${prefix_name}.0.mbr+offset
        truncate -s 128M ${prefix_name}.1.vfat
        truncate -s 128M ${prefix_name}.2.ext4

2. Create folders, holding each partition's content:

        mkdir \
          ${prefix_name}.1.vfat.d \
          ${prefix_name}.2.ext4.d

3. Create filesystem on partitions and copy content from folders:

        mkfs.vfat ${prefix_name}.1.vfat
        mcopy -s -i ${prefix_name}.1.vfat ${prefix_name}.1.vfat.d/* ::/
        mkfs.ext4 -q -d ${prefix_name}.2.ext4.d ${prefix_name}.2.ext4

4. Merge the partitions into one single disk:

        cat > ${prefix_name}.img \
          ${prefix_name}.0.mbr+offset \
          ${prefix_name}.1.vfat \
          ${prefix_name}.2.ext4

5. Create partition table, using a helper function converting MiB to blocks:

        MiB()
        {
          local size_mib=${1}
          local mega=$((2**20))
          local block_size=512
          echo $((${size_mib}*${mega}/${block_size}))
        }

        sfdisk ${prefix_name}.img << EOF
        type=c, size=$(MiB 128), bootable
        type=83, size=$(MiB 128)
        EOF

### Verify image

Note down the offset of each partitions with `fdisk --list ${prefix_name}.img`,
default sector size is 512.

Mount the partitions:

    sudo mount -o offset=$((2048*512)) ${prefix_name}.img /mnt
    sudo umount /mnt
    sudo mount -o offset=$((264192*512)) ${prefix_name}.img /mnt
    sudo umount /mnt

Check filesystem:

    sudo losetup --partscan --show --find ${prefix_name}.img
    sudo fsck.vfat /dev/loop18p1 && echo "ok!"
    sudo fsck.ext4 /dev/loop18p2 && echo "ok!"
    sudo losetup -d /dev/loop18
