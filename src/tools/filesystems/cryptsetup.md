# cryptsetup: LUKS and BitLocker volumes

**Package:** `cryptsetup` · **Writes to disks:** not with `--readonly`

Nothing is unlocked at boot. To open an encrypted volume without changing it:

```sh
sudo cryptsetup isLuks -v /dev/sdX2                   # is this a LUKS volume?
sudo cryptsetup luksDump /dev/sdX2                    # header: version, cipher, key slots
sudo cryptsetup open --readonly /dev/sdX2 evidence    # unlock read-only → /dev/mapper/evidence
sudo cryptsetup status evidence                       # check: "mode: readonly"
sudo mount -o ro,noload /dev/mapper/evidence /mnt     # if it holds ext4
sudo umount /mnt && sudo cryptsetup close evidence

sudo cryptsetup luksHeaderBackup /dev/sdX2 --header-backup-file /mnt/target/sdX2.luksheader
```

**BitLocker** (Windows): cryptsetup opens it too, with the user password or
the 48-digit recovery key:

```sh
sudo cryptsetup bitlkDump /dev/sdX3
sudo cryptsetup open --type bitlk --readonly /dev/sdX3 windows
sudo ntfs-3g -o ro /dev/mapper/windows /mnt
```

Verified in a virtual machine for LUKS2: the mapping was read-only, writes
failed and the container's hash did not change. Keep a header backup before
any repair: a damaged LUKS header makes the data unrecoverable.
