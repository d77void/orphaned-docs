# xmount: E01 and AFF images as raw disks

**Package:** `xmount` · **Writes to disks:** no (writes go to a cache file, if you allow them)

```sh
sudo mkdir -p /mnt/raw
sudo xmount --in ewf /mnt/target/case1.E01 /mnt/raw     # E01 → a raw .dd file in /mnt/raw
ls /mnt/raw                                              # its name
sudo xmount --in aff image.aff /mnt/raw                  # AFF → raw
sudo losetup -r -P -f --show /mnt/raw/<name>.dd          # then its partitions as /dev/loopNpM
sudo umount /mnt/raw
```

Without `--cache`, the virtual disk is read-only. With `--cache <file>`,
programs that insist on writing (some need it to mount) write into that file
and the image itself stays untouched.
