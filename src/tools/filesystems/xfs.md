# XFS: xfs_repair, xfs_info

**Package:** `xfsprogs` · **Writes to disks:** `xfs_repair` without `-n`

```sh
sudo xfs_repair -n /dev/sdX1   # check only, no changes
sudo xfs_repair /dev/sdX1      # repair (the file system must be unmounted)
xfs_info /mnt                  # geometry of a mounted XFS
```

If `xfs_repair` refuses because the log is dirty, first mount and unmount
the file system once so the log is replayed (this writes), or, as a last
resort, `xfs_repair -L`, which **throws the log away** and can lose recent
changes.

To read a damaged XFS without changing it, mount with `-o ro,norecovery`
(see [mount](mount.md)).
