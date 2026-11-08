# Download

> **Prototype.** d77orphaned is a proof of concept. It has been tested in
> virtual machines and on a few real computers. Do not rely on it as your
> only way to recover something that matters.

Files are in the [ISO-x86_64 folder on SourceForge](https://sourceforge.net/projects/d77void/files/ISO-x86_64/), next to the d77void
ISOs. Each version has three files, named with its date:

| File | What it is |
|---|---|
| `d77orphaned-live-x86_64-<date>.iso` | the system (about 2 GB, x86_64) |
| `d77orphaned-live-x86_64-<date>.iso.sha256` | the hash, to check the download |
| `d77orphaned-live-x86_64-<date>.SOURCES.txt` | where to get the source of every package |

## Check the download

With the `.iso` and the `.sha256` in the same folder:

```sh
sha256sum -c d77orphaned-live-x86_64-<date>.iso.sha256
```

It must say `OK`.

## Write it to a USB stick

You need a stick of at least 4 GB. Everything on it is **erased**. Find its
name first, by its size and model:

```sh
lsblk -d -o NAME,SIZE,MODEL,TRAN
```

Then, replacing `/dev/sdX` with the **whole stick** (not a partition such as
`/dev/sdX1`):

```sh
sudo dd if=d77orphaned-live-x86_64-<date>.iso of=/dev/sdX bs=4M conv=fsync status=progress
```

Choosing the wrong device overwrites that disk, so check it twice. Then boot
the computer from the stick, and see [The boot menu](boot-menu.md).

If the system where you plug in the stick offers to unlock an encrypted
partition, it is your own automounter seeing a
[persistence](../persistence/index.md) partition; you can cancel it.
