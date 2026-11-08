# mount: mount without changing the disk

**Package:** `util-linux` · **Writes to disks:** not with the options below

```sh
sudo blockdev --setro /dev/sdX /dev/sdX1        # first: make the devices read-only
sudo mount -o ro,noload /dev/sdX1 /mnt           # ext3/ext4: no journal replay
sudo mount -o ro,norecovery /dev/sdX1 /mnt       # XFS: no log recovery
sudo mount -o ro /dev/sdX1 /mnt                  # other file systems
findmnt /mnt                                     # check: options must include "ro"
sudo umount /mnt
```

Without `noload` (ext4) or `norecovery` (XFS), the kernel replays an
unfinished journal **even with `-o ro`**, which writes to the disk.

For NTFS, see [NTFS](ntfs.md); for encrypted volumes, open them first with
[cryptsetup](cryptsetup.md).
