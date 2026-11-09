# flashrom: read and write firmware chips

**Package:** `flashrom` · **Writes:** only with `-w`, to the firmware chip

> **A wrong write can leave the computer unable to start.** Then it only recovers
> with an external programmer (a clip and a CH341A or similar). Have one at hand,
> and know the chip's location, before writing. Never run a write on a laptop on
> battery alone, or on a machine you cannot afford to lose.

The internal programmer needs the **(firmware tools)** entry in the
[boot menu](../../getting-started/boot-menu.md), which adds `iomem=relaxed`. The
other entries keep the kernel's protection of system memory.

## Always read first

```sh
sudo flashrom -p internal                        # find the chip; writes nothing
sudo flashrom -p internal -r backup1.rom         # read it to a file
sudo flashrom -p internal -r backup2.rom         # read it again
sha256sum backup1.rom backup2.rom                # must be identical
```

If the two hashes differ, **stop**: the read is not reliable. Copy the backup off
the stick: anything outside [persistence](../../persistence/index.md) is gone at
the next boot.

## Writing

```sh
sudo flashrom -p internal --wp-status            # is it write-protected?
sudo flashrom -p internal -w new.rom             # write, and verify automatically
sudo flashrom -p internal -v new.rom             # compare the chip with a file
```

On many machines the firmware blocks internal writes, or only some regions can be
written: flashrom says so. Do not force it. Use an external programmer instead.

External programmers use the same commands with another `-p`, for example
`-p ch341a_spi`.

> Not verified yet on real hardware by this project, including whether a
> Libreboot or coreboot machine allows internal access.
