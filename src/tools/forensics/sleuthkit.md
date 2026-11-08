# Sleuth Kit: mmls, fsstat, fls, icat, istat, tsk_recover

**Package:** `sleuthkit` · **Writes to disks:** no (`tsk_recover` writes to its output folder)

Reads partitions and file systems inside an image (or a device) without
mounting it, including deleted entries. It works on raw images, and on E01
directly.

```sh
mmls disk.img                       # partitions, with their start sector
fsstat -o 2048 disk.img             # file system at sector 2048: type, size, dates
fls -o 2048 -r -p disk.img          # every file, with full paths (deleted ones marked *)
fls -o 2048 -r -d -p disk.img       # deleted entries only
istat -o 2048 disk.img 1234         # metadata of inode/MFT entry 1234
icat -o 2048 disk.img 1234 > out    # the contents of inode 1234
tsk_recover -o 2048 -e disk.img /mnt/target/recovered   # extract every file, deleted ones included
```

`-o` is the partition's start sector, from `mmls`. `fls -m / -r` prints a
"body file" for building a timeline with `mactime`.
