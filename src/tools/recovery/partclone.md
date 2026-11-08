# partclone: image a file system

**Package:** `partclone` · **Writes to disks:** to the output; when restoring, to the target partition

Copies only the blocks a file system uses, so images are much smaller than
with `dd`. There is one program per file system: `partclone.ext4`,
`partclone.ntfs`, `partclone.vfat`, `partclone.btrfs`, `partclone.exfat`,
`partclone.f2fs`, … (there is no `partclone.xfs` in Void; use `xfsdump` or
[fsarchiver](fsarchiver.md) for XFS)

```sh
sudo partclone.ext4 -c -s /dev/sdX1 -o /mnt/target/sdX1.img    # save (clone) to an image
sudo partclone.ext4 -r -s /mnt/target/sdX1.img -o /dev/sdY1    # restore the image to a partition
sudo partclone.ntfs -b -s /dev/sdX1 -o /dev/sdY1               # partition to partition
```

- `-c`: clone to partclone's image format; `-r`: restore from it;
  `-b`: device to device.
- `-s`: source; `-o`: output.

partclone needs a readable file system. For a disk with bad sectors, use
[ddrescue](ddrescue.md) instead.

> **Writes:** restoring (`-r`, `-b`) overwrites the target partition.
