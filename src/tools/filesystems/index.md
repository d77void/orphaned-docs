# File systems and volumes

Mounting, checking and repairing file systems, and opening encrypted
volumes, LVM and software RAID.

Everything here starts from [Working safely with disks](../../disks/index.md):
nothing is mounted, assembled or unlocked automatically, and on a disk that
matters you mark it read-only first.

**Checking** (`-n`, no changes) is safe. **Repairing** writes to the file
system; on a disk with data you need, image it first ([ddrescue](../recovery/ddrescue.md))
and repair the copy.

| Tool | For |
|---|---|
| [mount](mount.md) | mounting read-only, without replaying journals |
| [ext2/3/4](ext4.md) | `e2fsck`, `tune2fs`, `debugfs` |
| [XFS](xfs.md) | `xfs_repair`, `xfs_info` |
| [Btrfs](btrfs.md) | `btrfs check`, `btrfs restore` |
| [NTFS](ntfs.md) | `ntfs-3g`, `ntfsfix`, `ntfsinfo` |
| [FAT and exFAT](fat.md) | `fsck.vfat`, `fsck.exfat` |
| [cryptsetup](cryptsetup.md) | LUKS and BitLocker volumes |
| [dislocker](dislocker.md) | BitLocker volumes (alternative) |
| [LVM](lvm.md) | logical volumes |
| [mdadm](mdadm.md) | Linux software RAID, and Intel RST (IMSM) sets |
