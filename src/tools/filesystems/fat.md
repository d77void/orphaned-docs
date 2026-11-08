# FAT and exFAT: fsck.vfat, fsck.exfat

**Packages:** `dosfstools`, `exfatprogs` · **Writes to disks:** without `-n`

```sh
sudo fsck.vfat -n /dev/sdX1    # check a FAT12/16/32 file system, change nothing
sudo fsck.vfat -a /dev/sdX1    # repair automatically
sudo fsck.exfat -n /dev/sdX1   # check exFAT, change nothing
sudo fsck.exfat -y /dev/sdX1   # repair exFAT
```

USB sticks and SD cards are usually FAT32 or exFAT. EFI system partitions
are FAT32.

> **Writes:** `-a` and `-y` repair, and so change the file system.
