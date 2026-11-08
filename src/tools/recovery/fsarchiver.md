# fsarchiver: back up and restore file systems

**Package:** `fsarchiver` · **Writes to disks:** `restfs` overwrites the target

Saves file systems to a compressed archive and restores them to partitions
of any size (as long as the data fits).

```sh
sudo fsarchiver probe                                       # file systems it can see
sudo fsarchiver savefs -j4 /mnt/target/backup.fsa /dev/sdX1 # save one file system (4 threads)
sudo fsarchiver savefs -Z3 /mnt/target/backup.fsa /dev/sdX1 /dev/sdX2   # two, zstd level 3
fsarchiver archinfo /mnt/target/backup.fsa                  # what is in an archive
sudo fsarchiver restfs /mnt/target/backup.fsa id=0,dest=/dev/sdY1   # restore the first one
```

In `restfs`, `id=` is the position of the file system in the archive (0 for
the first), as shown by `archinfo`.

> **Writes:** `restfs` formats and overwrites the destination partition.
