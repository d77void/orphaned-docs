# hdparm: SATA drive information

**Package:** `hdparm` · **Writes to disks:** only some options (see below)

```sh
sudo hdparm -I /dev/sdX     # identification: model, serial, features, security state
sudo hdparm -t /dev/sdX     # time sequential reads from the disk (read-only)
sudo hdparm -T /dev/sdX     # time reads from the cache, for comparison
sudo hdparm -r /dev/sdX     # show the kernel's read-only flag (0 or 1)
```

`hdparm -I` shows whether the drive has an ATA password set ("Security:
… enabled / locked"), which explains a disk that cannot be read.

> **Writes:** many hdparm options change drive settings or data (for example
> the security and erase options). Use only the read options above unless
> you know exactly what an option does.
