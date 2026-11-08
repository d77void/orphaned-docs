# xxd and hexedit: raw bytes

**Packages:** `xxd`, `hexedit` · **Writes to disks:** `hexedit` when saving

```sh
xxd -l 512 disk.img                 # first sector: hex and text side by side
sudo xxd -s 1024 -l 512 /dev/sdX1   # 512 bytes starting at offset 1024 (ext superblock)
hexedit disk.img                    # interactive viewer/editor
```

In `hexedit`, `Ctrl-X` saves and quits, `Ctrl-C` quits **without**
saving. Open evidence only in images, or use `xxd`, which only reads.
