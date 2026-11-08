# sha256sum and friends: hashes

**Package:** `coreutils` · **Writes to disks:** no

```sh
sudo sha256sum /dev/sdX                      # hash a whole disk (reads all of it)
sha256sum disk.img > disk.img.sha256         # hash an image and keep the result
sha256sum -c disk.img.sha256                 # later: check the image has not changed
```

`md5sum`, `sha1sum` and `sha512sum` work the same way. Hash the source and
the image: identical hashes mean an exact copy.
