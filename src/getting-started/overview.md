# What D77orphaned is

D77orphaned is a live ISO built on Void Linux (glibc, x86_64) with runit. You
boot it, use it, and switch it off; nothing is installed. It is meant for:

- **Recovery:** copying data off a failing disk, repairing partition tables
  and file systems, rescuing a system that no longer boots.
- **Diagnostics:** disk health (SMART, NVMe), hardware inventory, memory test,
  network checks.
- **Careful forensics:** imaging disks and examining file systems without
  changing them.
- **Authorized security testing:** a few network tools (`nmap`, `tcpdump`,
  `arp-scan`, …), only for networks you are allowed to test.

The full list is in [Tools in the image](../tools/index.md).

## What it does not do on its own

D77orphaned is careful with the disks of the computer it runs on. Out of the
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

## Nothing is kept

Everything you change while it runs lives in memory and is gone at the next
boot. Saving work means copying it somewhere on purpose, for example to a USB
stick you mount yourself. A separate, optional data partition is planned but
not part of the prototype.

## What it is not

- Not a d77void variant to install: there is no installer.
- Not a replacement for Kali, Parrot or BlackArch: it has a short, chosen
  list of tools, not hundreds of offensive ones.
- Not a forensic product with a chain-of-custody workflow. It gives you
  tools that do not write to disks unless told to; the procedure is yours.
