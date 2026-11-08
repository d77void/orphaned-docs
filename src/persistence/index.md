# Persistence

By default d77orphaned keeps nothing: every boot starts clean. If you want to
keep files and settings on the USB stick, `d77-persist` adds an **encrypted**
partition to it. This is optional; without it, the system works exactly the
same.

```sh
d77-persist create            # once: add the encrypted partition to the stick
d77-persist open              # unlock: your files, and your settings come back
d77-persist open --data-only  # unlock: your files only
d77-persist status            # what is there, and what is open
d77-persist close             # lock it; do this before removing the stick
```

The commands ask for `sudo` by themselves, which needs no password on the live
system.

## What is kept

- **Your files**, in `/mnt/d77-data`.
- **Settings**, unless you use `--data-only`:

| What | Where it lives |
|---|---|
| Saved Wi-Fi networks | `/etc/NetworkManager/system-connections` |
| pwm, including the theme and keyboard set in Kantele | `~/.config/pwm` |
| wasp, including what Kantele sets | `~/.config/wasp` |
| Kantele | `~/.config/kantele` |
| Utumno's theme and wallpaper | `~/.config/d77`, `~/.cache/d77`, `~/.cache/quickshell/wallpaper` |
| SSH keys | `~/.ssh` |

The first `open` copies what the session has at that moment; from then on,
changes in those folders are saved on the stick while it is open.

pwm picks up its settings at once. wasp and Utumno read theirs when they
start, so log out and back in for those to apply.

## What is not kept

The system itself: packages installed with `xbps-install`, and anything else
outside the list above, are gone at the next boot, as always. This is on
purpose: the system you boot is always the one in the ISO. The browser's
profile is not kept either; Mullvad Browser is designed to forget.

## Creating it

`d77-persist create` works only on the device the system booted from, and
never on the computer's disks. It shows that device, and writes only after
you type its name. The existing partitions are not changed, and the new one
takes all the free space after them (at least 256 MiB are needed).

The encryption (LUKS2) is not optional. **The passphrase cannot be recovered**:
without it, the data is lost.

## Writing a new ISO erases it

Writing a new ISO to the stick replaces the partition table, so the
persistence partition and its data are lost. **Copy your files elsewhere
first.** Persistence is not a backup: keep copies of anything important.

## Safety

- Nothing happens at boot: the partition stays locked and unmounted until you
  run `d77-persist open`, and the system boots the same with or without it.
- A passphrase is never stored, and nothing is unlocked automatically.
- Other disks are not involved, even if one of them has a partition with the
  same name.

Verified in a virtual machine with a simulated USB stick: creating, closing,
wrong passphrase, reopening after a reboot, and booting with BIOS and UEFI
with the new partition table; another disk's hash did not change.

> Not verified yet on every firmware. If a machine stops booting the stick
> after `create`, write the ISO again (this erases the persistence).
