# I need the files from a BitLocker disk

**Writes to the disk:** no, with the commands below.

> **Not tested.** This project has no BitLocker disk to test with. This page comes
> from the documentation of `cryptsetup` and `dislocker`. Try it with a copy of the
> disk first, if you can.

## You need the key

Without the password or the 48-digit **recovery key**, there is no way in. Windows
users often have the recovery key in their Microsoft account
(account.microsoft.com/devices/recoverykey), in their company's directory, or on a
printout or USB stick from when BitLocker was turned on.

A Windows computer that "is not encrypted" may be: many turn on device encryption
by themselves. See if the partition is BitLocker:

```sh
lsblk -o NAME,SIZE,FSTYPE          # shows BitLocker
```

## Option 1: cryptsetup

```sh
sudo blockdev --setro /dev/sdXn
sudo mkdir -p /mnt/windows
sudo cryptsetup open --type bitlk --readonly /dev/sdXn windows      # asks for the password or recovery key
sudo ntfs-3g -o ro /dev/mapper/windows /mnt/windows
```

Cleaning up:

```sh
sudo umount /mnt/windows
sudo cryptsetup close windows
```

## Option 2: dislocker

When cryptsetup does not recognise the volume. See
[dislocker](../tools/filesystems/dislocker.md).

```sh
sudo mkdir -p /mnt/bitlocker /mnt/windows
sudo dislocker -r -V /dev/sdXn -p -- /mnt/bitlocker      # asks for the recovery key
sudo ntfs-3g -o ro /mnt/bitlocker/dislocker-file /mnt/windows
```

## If Windows was only hibernated or "fast started"

NTFS is left marked as in use, and read-only mounting is the right thing to do
anyway. Do not force a read-write mount: it can lose data still waiting to be written.

See [NTFS](../tools/filesystems/ntfs.md).
