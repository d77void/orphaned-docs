# photorec: recover files by their content

**Package:** `testdisk` · **Writes to disks:** only to the folder where recovered files go

Recovers files (photos, documents, archives, …) by recognising their
content, even when the file system is damaged or reformatted. File names
and folders are not kept.

```sh
sudo photorec /log /d /mnt/target/recovered /dev/sdX   # recover into that folder
sudo photorec /log /d /mnt/target/recovered disk.img   # from an image
```

It is interactive: choose the partition (or the whole disk), the file
system type and the file types to look for (**File Opt**), then
**Search**.

> **Writes:** recovered files go to the folder given with `/d`. It must be
> on **another** disk; recovering onto the disk you are scanning overwrites
> the files you are looking for.
