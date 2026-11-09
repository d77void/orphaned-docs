# I deleted a partition

**Writes to the disk:** yes, the partition table, at the very end and only when you
say so. Your files are usually still there: deleting a partition removes its entry
in the table, not the data.

**Do not create new partitions, format, or install anything** on that disk. That is
what really destroys the data.

## 1. Work on a copy, if you can

```sh
sudo ddrescue /dev/sdX /mnt/target/disk.img /mnt/target/disk.map
```

Repair the copy, confirm your files are there, and only then repeat on the real
disk. If you have nowhere to copy it, you can run TestDisk on the disk directly,
as it writes only at the end.

## 2. Find it with TestDisk

```sh
cd /mnt/target                     # it leaves testdisk.log here
sudo testdisk /log disk.img        # or /dev/sdX
```

1. Choose the disk, and **Proceed**.
2. **Choose the partition table type yourself.**

   > **On a GPT disk left with no partitions, TestDisk proposes *Intel*. Choosing
   > that would replace your GPT with an MBR.** Choose **EFI GPT**. If you are not
   > sure which the disk had, `sudo gdisk -l /dev/sdX` says whether a GPT is present.

3. **Analyse**, then **Quick Search**.
4. Your partition appears in the list. Press **P** to list its files. If you see
   them, you have the right one. Press **q** to go back.
5. With the arrows **← →**, change its status: on GPT, from `D` (deleted) to `P`
   (primary); on MBR, `*` (bootable) or `P`. Then **Enter**.
6. **Write**, then **Y** to confirm. Nothing has been written before this.
7. Leave with **Quit**, and reboot if you repaired the real disk.

If Quick Search does not find it, try **Deeper Search**.

## 3. Check it

On an image:

```sh
sudo losetup -Pf --show disk.img       # prints /dev/loopN
sudo mount -o ro,noload /dev/loopNp1 /mnt/check
```

On the real disk, after rebooting:

```sh
sudo mount -o ro,noload /dev/sdXn /mnt/check
```

`noload` is for ext4; for XFS use `norecovery`, and for others simply `ro`.

## If it was formatted, or TestDisk finds nothing

The partition's file system is gone or overwritten. [photorec](../tools/recovery/photorec.md)
recovers files by their contents, without their names or folders, to another disk.

> Tested in a virtual machine, through TestDisk's menus, on copies of a GPT disk
> and an MBR disk, each with an ext4 partition deleted: the partition came back
> with its files identical. Not tested: NTFS, or partitions overlapping others.
