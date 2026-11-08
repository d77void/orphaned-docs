# gpart: guess a lost MBR partition table

**Package:** `gpart` · **Writes to disks:** only with `-W`

Scans a disk for the start of known file systems and proposes an MBR
(msdos) partition table. For GPT disks, use [testdisk](testdisk.md) or
[gdisk](../disks/gdisk.md) instead.

```sh
sudo gpart /dev/sdX         # scan and print the partitions it guesses
sudo gpart -f /dev/sdX      # full scan (slower, finds more)
```

Compare its guess with what you know about the disk before acting on it.

> **Writes:** `-W` writes the guessed table to a device or file. Use
> [testdisk](testdisk.md) for an interactive, safer repair.
