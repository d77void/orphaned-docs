# Archives: tar, zip, 7z, zstd, cabextract, unp

**Packages:** `tar`, `zip`, `unzip`, `p7zip`, `zstd`, `lz4`, `lzop`, `cabextract`, `unp`

```sh
tar -cf - folder | zstd -T0 > folder.tar.zst   # pack and compress with all cores
tar -xf folder.tar.zst                          # unpack (tar detects the compression)
zip -r folder.zip folder                        # zip, readable everywhere
unzip -l file.zip                               # list without extracting
7z x file.7z -o/mnt/target/out                  # extract 7z (also rar, iso, …)
7z t file.7z                                    # test an archive
zstd -d file.zst                                # decompress zstd
cabextract file.cab                             # Windows .cab files
unp file.anything                               # unpack whatever format it is
```
