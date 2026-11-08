# NTFS: ntfs-3g, ntfsfix, ntfsinfo

**Package:** `ntfs-3g` · **Writes to disks:** `ntfsfix` without `-n`

```sh
sudo ntfs-3g -o ro /dev/sdX1 /mnt     # mount read-only
sudo ntfsinfo -m /dev/sdX1            # volume information (unmounted)
sudo ntfsfix -n /dev/sdX1             # what ntfsfix would do, without writing
sudo ntfsfix -d /dev/sdX1             # clear the "dirty" flag so Windows runs chkdsk
```

A Windows that was **hibernated** or shut down with Fast Startup leaves NTFS
in a state that must not be written to; mount it read-only (`-o ro`), as
above. The Windows partitions of a BitLocker-encrypted disk must be opened
first with [cryptsetup](cryptsetup.md) or [dislocker](dislocker.md).

`ntfsfix` is not a full repair tool (that is `chkdsk` on Windows); it fixes
some common problems and schedules a check.
