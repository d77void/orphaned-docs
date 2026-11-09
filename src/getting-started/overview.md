# What d77orphaned is

d77orphaned is a live ISO built on Void Linux (glibc, x86_64) with runit. You
boot it, use it, and switch it off; nothing is installed. It is meant for:

- **Recovery:** copying data off a failing disk, repairing partition tables
  and file systems, reinstalling the boot loader of a system that no longer
  boots, restoring backups.
- **Diagnostics:** disk health (SMART, NVMe), hardware inventory, memory test,
  network checks.
- **Careful forensics:** imaging disks and examining file systems without
  changing them.
- **Secure erasure:** wiping disks before reuse or disposal, only when you ask
  (see [Secure erasure and sanitization](../tools/erase/index.md)).
- **Authorized security testing:** a few network tools (`nmap`, `tcpdump`,
  `arp-scan`, …), only for networks you are allowed to test.

The full list is in [Tools in the image](../tools/index.md). When something has
gone wrong, start with the [Emergency procedures](../emergency/index.md).

## What it does not do on its own

d77orphaned is careful with the disks of the computer it runs on. Out of the
box, it:

- does not mount any disk;
- does not assemble software RAID (MD) or activate LVM volumes;
- does not unlock encrypted (LUKS) volumes;
- does not use swap partitions it finds;
- has no automounting (no udisks2, udiskie or gvfs);
- runs no SSH server and listens on no network port.

All of this was checked in a virtual machine with test disks holding ext4
and XFS (with unfinished journals), NTFS, LUKS2, MD RAID 1, LVM and swap. The
disks' contents were identical, byte for byte, before and after booting and
using a graphical session.

Reading a disk is still not the same as preserving evidence. See
[Working safely with disks](../disks/index.md) before you mount anything.

## Logging in

| User | Password | Notes |
|---|---|---|
| `anon` | `voidlinux` | the live user; `sudo` without a password |
| `root` | `voidlinux` | |

The passwords are the same on every copy of the ISO. Change them before
connecting to a network you do not trust, and always before turning on SSH
(see [Network](../network/index.md)).

## Nothing is kept, unless you ask

Everything you change while it runs lives in memory and is gone at the next
boot. To keep files and settings on the USB stick, you can add an encrypted
partition: see [Persistence](../persistence/index.md). Otherwise, saving work
means copying it somewhere on purpose.

## Source code

Every ISO comes with a `SOURCES.txt` file, next to it on the download page
and inside the system at `/usr/share/doc/d77orphaned/SOURCES.txt`. It lists
every package in the image, with its version and license, and says where to
get its source:

- Void Linux packages: `https://sources.voidlinux.org/<package>-<version>/`;
- d77void packages: [d77void/srcpkgs-d77](https://github.com/d77void/srcpkgs-d77)
  and each project's own page.

The same file contains a written offer of the source code of every program
in the image. Requests go to the
[d77orphaned issues on GitHub](https://github.com/d77void/d77orphaned/issues).

The image contains one package that is not free software in the strict
sense: `nmap`, under the Nmap Public Source License (Void ships it in its
"nonfree" repository).

## What it is not

- Not a d77void variant to install: there is no installer.
- Not a replacement for Kali, Parrot or BlackArch: it has a short, chosen
  list of tools, not hundreds of offensive ones.
- Not a forensic product with a chain-of-custody workflow. It gives you
  tools that do not write to disks unless told to; the procedure is yours.
