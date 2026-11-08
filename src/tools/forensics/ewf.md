# ewfacquire, ewfverify, ewfinfo, ewfmount: EWF (E01) images

**Package:** `libewf` · **Writes to disks:** `ewfacquire` writes the image files

The Expert Witness Format (`.E01`, `.E02`, …) stores the disk compressed,
in segments, with case notes and hashes inside.

```sh
sudo ewfacquire /dev/sdX                       # interactive: asks for target, case number, examiner, …
sudo ewfacquire -u -t /mnt/target/case1 -C 2026-001 -E disk1 -e "J. Doe" -d sha256 /dev/sdX
ewfverify /mnt/target/case1.E01                # recompute and check the stored hashes
ewfinfo /mnt/target/case1.E01                  # case data, acquisition date, hashes
sudo mkdir -p /mnt/ewf && sudo ewfmount /mnt/target/case1.E01 /mnt/ewf   # → /mnt/ewf/ewf1, a raw view
```

- `-u`: unattended (no questions); `-t`: target name without extension;
  `-C` case number, `-E` evidence number, `-e` examiner, `-d sha256` an
  extra hash besides MD5.

`ewfmount` exposes the image as one read-only raw file (`ewf1`), which the
[Sleuth Kit](sleuthkit.md) or [losetup](../disks/losetup.md) can then read.
