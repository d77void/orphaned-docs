# Install when you need them

These tools are large, and most people never need them, so they are not in the
image. They install in a few minutes on the running system, with a network.

| Tool | For | Memory it takes |
|---|---|---|
| [rclone](rclone.md) | cloud storage: copying files to and from it | about 140 MB |
| [tshark and termshark](tshark.md) | analysing network captures | about 220 MB |
| [john](john.md) | testing and recovering passwords | about 80 MB |
| [clamav](clamav.md) | scanning for malware | about 220 MB, plus its signatures |

```sh
sudo xbps-install -S rclone
```

## What you should know

- **They live in memory, and vanish at reboot.** The running system is held in RAM,
  and [persistence](../../persistence/index.md) keeps files and settings, not
  packages. So you reinstall each time.
- **Make sure you have the memory.** The numbers above were measured in a virtual
  machine, and include the downloaded package. All of them, with ClamAV's signatures,
  took about 770 MB. On a machine with little RAM, install only what you need, and
  `sudo xbps-remove -O` afterwards frees the downloaded packages.
- **They need the network** (see [Network](../../network/index.md)), unless you
  built your own image containing them (see [Building](../../building/index.md)).

> All installed and run in a virtual machine from this image, except as each page
> notes.
