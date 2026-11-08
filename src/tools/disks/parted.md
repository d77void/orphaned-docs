# parted: partition tables

**Package:** `parted` · **Writes to disks:** yes, when changing partitions

```sh
sudo parted -l                       # every disk: table type (gpt/msdos) and partitions
sudo parted /dev/sdX unit s print    # one disk, positions in sectors
sudo parted /dev/sdX print free      # including unallocated space
```

The commands above only read.

> **Writes:** `mklabel`, `mkpart`, `rm`, `resizepart` and the rest change
> the partition table, and parted applies each command at once, without a
> final "write" step. `mklabel` makes every partition on the disk
> unreachable. On a disk you are recovering from, work on a copy instead.
