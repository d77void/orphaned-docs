# foremost: carve files out of raw data

**Package:** `foremost` · **Writes to disks:** only to the output folder

Finds files by their headers and footers in an image or device, ignoring
the file system. Like [photorec](../recovery/photorec.md), but configured by
file type.

```sh
foremost -i disk.img -o /mnt/target/carved                  # all built-in types
foremost -t jpg,pdf,doc -i disk.img -o /mnt/target/carved   # only some types
foremost -T -i disk.img -o /mnt/target/carved               # time-stamped output folder
```

The output folder must not exist yet (or use `-T`); a report
(`audit.txt`) is written there too.
