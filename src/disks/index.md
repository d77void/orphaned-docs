# Working safely with disks

d77orphaned does not touch the computer's disks by itself (see
[What d77orphaned is](../getting-started/overview.md#what-it-does-not-do-on-its-own)).
This page is about not touching them by accident once **you** start working.

In the commands below, replace `/dev/sdX` (whole disk) and `/dev/sdX1`
(partition) with your devices. `lsblk -f` lists disks, partitions and file
systems without changing anything.

## "Read-only" is not one thing

Mounting a file system with `-o ro` is not enough to leave a disk untouched:

- **ext4 and XFS replay their journal** even when mounted read-only, if it
  was not closed cleanly. That writes to the disk.
- **LVM, RAID and LUKS** have metadata that some commands update.
- **Your own commands** (`fsck`, `testdisk`, a wrong `dd`) can write anywhere.

Two habits cover most of this:

1. Mark the block devices read-only in the kernel before anything else.
2. Whenever you can, work on an **image** of the disk instead of the disk.

## 1. Mark the devices read-only

```sh
sudo blockdev --setro /dev/sdX
sudo blockdev --setro /dev/sdX1      # each partition you will use, too
sudo blockdev --getro /dev/sdX1      # 1 = read-only
```

This flag lasts until the device is removed or the computer reboots.

## 2. Mount without replaying the journal

| File system | Command |
|---|---|
| ext4 (and ext3) | `sudo mount -o ro,noload /dev/sdX1 /mnt` |
| XFS | `sudo mount -o ro,norecovery /dev/sdX1 /mnt` |
| others | `sudo mount -o ro /dev/sdX1 /mnt` |

Verified in a virtual machine: with `blockdev --setro` and these options,
ext4 and XFS disks with unfinished journals were mounted. The journals stayed
unfinished, and the disks' SHA-256 hashes did not change.

## 3. Image the disk instead

For damaged disks, or anything that might become evidence, copy the disk
first and work on the copy. Store the image on another disk that you mount
read-write on purpose:

```sh
# failing or damaged disk: ddrescue keeps a map, so it can be resumed
sudo ddrescue -d /dev/sdX /mnt/target/disk.img /mnt/target/disk.map

# EWF (E01) image with case notes and built-in hashes
sudo ewfacquire /dev/sdX

# raw image with hashes computed while copying
sudo dcfldd if=/dev/sdX of=/mnt/target/disk.img hash=sha256 hashlog=/mnt/target/disk.sha256
```

`losetup --read-only` and the Sleuth Kit (`mmls`, `fls`, …) can then examine
the image.

## Encrypted (LUKS) volumes

Nothing is unlocked at boot. To open a volume read-only:

```sh
sudo cryptsetup open --readonly /dev/sdX2 evidence
sudo mount -o ro,noload /dev/mapper/evidence /mnt   # if it holds ext4
sudo umount /mnt && sudo cryptsetup close evidence
```

Verified in a virtual machine: the mapped device was read-only, writes to it
failed, and the LUKS2 container's hash did not change.

## LVM

d77orphaned never activates LVM volumes on its own. To activate one volume
group **read-only**:

```sh
sudo vgchange -ay --config 'activation { read_only_volume_list = [ "myvg" ] }' myvg
sudo lvs myvg                        # the attributes start with -R: read-only
```

Verified in a virtual machine: the logical volumes were active and read-only,
writes failed, and the disk's hash did not change.

Avoid these two commands, which look right but are not:

- `vgchange -ay --readonly` activates **nothing**: `--readonly` stops the
  command from making any change, activation included.
- `lvchange -pr` (`--permission r`) **writes** the new permission into the
  LVM metadata on the disk. Verified: the disk's hash changed.

## Software RAID (MD)

Arrays are never assembled on their own. To assemble one read-only:

```sh
sudo mdadm --assemble --readonly /dev/md0 /dev/sdX1 /dev/sdY1
```

> Not verified yet in d77orphaned. Prefer imaging each member disk first.

## Swap

Swap partitions found on the disks are not used. Do not run `swapon` on a
disk you are examining: it writes to it.
