# testdisk: lost partitions and boot sectors

**Package:** `testdisk` · **Writes to disks:** only when you choose "Write"

Finds lost or deleted partitions, rebuilds partition tables and boot
sectors, and can undelete files on FAT, NTFS and ext2 file systems (for
ext3/ext4, see [extundelete](extundelete.md)).
It is interactive (menus).

```sh
sudo testdisk /list /dev/sdX      # just list the partitions it sees
sudo testdisk /log /dev/sdX       # interactive, keeping testdisk.log
sudo testdisk /log disk.img       # work on an image instead of the disk
```

Typical path for a lost partition: choose the disk → the partition table
type → **Analyse** → **Quick Search** (then **Deeper
Search** if needed). Check the partitions it found with **P** (list files)
before going on.

> **Check the table type.** On a GPT disk left with no partitions, TestDisk
> proposes *Intel* (MBR): choosing it would replace the GPT. Choose **EFI GPT**.
> See [I deleted a partition](../../emergency/deleted-partition.md).

> **Writes:** only at the end, on **Write**. Until then, everything is read
> only. Prefer running it on an image of the disk.

For deleted files: **Advanced** → choose the partition → **Undelete**.
