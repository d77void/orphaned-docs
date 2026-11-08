# binwalk: embedded files and firmware

**Package:** `binwalk` · **Writes to disks:** only with `-e`, to a folder next to the file

```sh
binwalk firmware.bin        # list signatures found inside: archives, file systems, images
binwalk -e firmware.bin     # extract what it recognises
binwalk -E firmware.bin     # entropy: compressed or encrypted areas
```

Useful for router firmware, unknown blobs and files hidden inside other
files.
