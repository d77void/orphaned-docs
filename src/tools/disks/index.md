# Disks

Tools to identify disks, read their health and look at their partition
tables. Most of them only read; the pages say clearly when a command writes.

Start with [lsblk](lsblk.md) to see what is there, then
[smartctl](smartctl.md) to see whether a disk is failing. Before anything
else on a disk that matters, make it read-only with [blockdev](blockdev.md)
and read [Working safely with disks](../../disks/index.md).

| Tool | For |
|---|---|
| [lsblk and blkid](lsblk.md) | which disks, partitions and file systems there are |
| [smartctl](smartctl.md) | health of SATA and NVMe drives |
| [nvme](nvme.md) | NVMe drive details and health |
| [hdparm](hdparm.md) | SATA drive identification, ATA password state, read speed |
| [lsscsi and sg_inq](lsscsi.md) | disks behind USB adapters and SAS controllers |
| [blockdev](blockdev.md) | the kernel's read-only flag, device sizes |
| [losetup](losetup.md) | using a disk image as a disk |
| [parted](parted.md), [gdisk and sgdisk](gdisk.md), [fdisk](fdisk.md) | partition tables |
| [gparted](gparted.md) | partitions, in a window |
| [f3](f3.md) | fake-capacity USB sticks and cards |

The commands use `/dev/sdX` for a whole disk and `/dev/sdX1` for a
partition; NVMe drives are `/dev/nvme0n1` and `/dev/nvme0n1p1`.
