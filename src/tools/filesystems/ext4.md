# ext2, ext3 and ext4: e2fsck, tune2fs, debugfs

**Package:** `e2fsprogs` · **Writes to disks:** `e2fsck` without `-n`

```sh
sudo e2fsck -fn /dev/sdX1      # full check, change nothing (answers "no" to everything)
sudo e2fsck -fp /dev/sdX1      # repair what is safe to repair automatically
sudo e2fsck -fy /dev/sdX1      # repair everything, answering "yes" (last resort, on a copy)
sudo tune2fs -l /dev/sdX1      # superblock: state, last mount, mount count, features
sudo debugfs -R ls /dev/sdX1   # list the root folder without mounting (read-only by default)
```

The file system must not be mounted while `e2fsck` runs. `-f` checks even
when the file system says it is clean.

> **Writes:** `-p` and `-y` repair, and so change the file system. Run them
> on an image when the data matters.
