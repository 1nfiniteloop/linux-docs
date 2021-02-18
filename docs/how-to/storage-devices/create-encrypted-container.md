# Create encrypted container

This document describes how to create an luks-encrypted container for storing
sensitive files and data securely.

## Steps

### Preparation

* Set encrypted container name: `NAME=vault`

### Create container

1. Allocate a 10Mib (count=10) file with random content:
   `dd if=/dev/urandom of=${NAME} bs=1M count=10`.
2. Associate file with loop-device:
   `sudo losetup --show --find ${NAME}`.
3. Initialize LUKS partition and set password:
   `sudo cryptsetup luksFormat /dev/loop<no>`.
4. Unlock:
   `sudo cryptsetup open /dev/loop<no> ${NAME}_crypt`.
5. Format container with a filesystem:
   `sudo mkfs.ext4 /dev/mapper/${NAME}_crypt`.
6. Cleanup, see [Close container](#close-container).

### Open container

Desktop environments requires only to setup a loop device (step 1), remaining
steps can be done from Nautulius file browser.

1. Associate file with loop-device:
   `sudo losetup --show --find ${NAME}`.
2. Unlock:
   `sudo cryptsetup open /dev/loop<no> ${NAME}_crypt`.
3. Mount:
   `sudo mount /dev/mapper/${NAME}_crypt /mnt`.

### Close container

1. Unmount:
   `sudo umount /mnt`.
2. Lock:
   `sudo cryptsetup close ${NAME}_crypt`.
3. Detach loop device:
   `sudo losetup --detach /dev/loop<no>`.
