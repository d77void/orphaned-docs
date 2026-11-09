# I want to move to another disk

**Writes to the disk:** yes, everything on the **new** disk is replaced. The old
disk is only read.

The simple way: copy the whole disk to a new one at least as big, then use the
extra space. This keeps the partitions, the boot loader and the encryption.

## 1. Identify both disks

```sh
lsblk -d -o NAME,SIZE,MODEL,SERIAL,TRAN
```

Check the **new** one twice. Below, `sdX` is the old disk and `sdY` the new one.

## 2. Copy

```sh
sudo ddrescue -f /dev/sdX /dev/sdY /tmp/move.map
```

**Source first.** `-f` lets it write to a device, so swapping them destroys the old
disk. Nothing on either disk may be mounted.

## 3. Use the extra space (GPT)

```sh
sudo sgdisk -e /dev/sdY                    # move the GPT's backup to the new end
sudo parted /dev/sdY resizepart N 100%     # grow the last partition: number N
sudo partprobe /dev/sdY
sudo e2fsck -f /dev/sdYN                   # check first
sudo resize2fs /dev/sdYN                   # grow ext4 to fill the partition
```

Only the **last** partition can grow this way. Others need moving first, with
[gparted](../tools/disks/gparted.md). For other file systems: XFS uses
`xfs_growfs` once mounted, Btrfs uses `btrfs filesystem resize max` once mounted.
On LUKS or LVM there are more layers to grow, inside to out: `cryptsetup resize`,
then `pvresize`, then `lvextend`, then the file system. That was not tested.

## 4. Do not keep both disks connected

The copy has the same IDs as the original, and systems can pick the wrong one or
get confused. Remove the old disk, and keep it, untouched, until the new one has
proven itself.

If you have to keep both, give the new one its own IDs (ext4):

```sh
sudo sgdisk -G /dev/sdY              # new GUIDs for the disk and partitions
sudo tune2fs -U random /dev/sdYN     # new file system UUID
```

But then the system's `/etc/fstab` and boot configuration may point to the old
IDs. Fix them through [The computer does not boot](no-boot.md).

## Moving to a smaller disk

A whole copy will not fit. Copy the file systems instead, with
[fsarchiver](../tools/recovery/fsarchiver.md) or `rsync -aHAX`, then create
the partitions and [reinstall the boot loader](no-boot.md).

## A new computer

The copy usually boots, but check whether it uses BIOS or UEFI: the new computer
has to support the same one. A system with its disk encrypted by a TPM will not
unlock on another machine without the recovery key.

> Tested in a virtual machine: an ext4 disk moved to a bigger one, with its files
> identical, its file system grown, and new IDs; and an installed Void system moved
> the same way, which then booted with both BIOS and UEFI. `e2fsck` can exit with
> code 1 here: that means it corrected something, which is fine. Not tested: XFS,
> Btrfs, LUKS or LVM growth, smaller disks, a different computer.
