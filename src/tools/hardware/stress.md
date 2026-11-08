# stress and fio: load tests

**Packages:** `stress`, `fio` · **Writes to disks:** `fio` only with write tests

```sh
stress -c 4 -t 300                  # 4 CPU workers for 5 minutes (watch "sensors" meanwhile)
stress -m 2 --vm-bytes 1G -t 120    # 2 memory workers of 1 GiB each
sudo fio --name=read --filename=/dev/sdX --rw=read --bs=1M --size=2G --direct=1 --readonly
```

The `fio` line measures sequential reads from a disk without writing to it
(`--readonly`). A machine that shuts down or freezes under `stress` usually
has a cooling or power problem.

> **Writes:** `fio` with `--rw=write` or `randwrite` on a device overwrites
> it. Write tests only on a disk you can wipe.
