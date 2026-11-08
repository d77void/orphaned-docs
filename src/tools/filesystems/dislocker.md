# dislocker: BitLocker volumes

**Package:** `dislocker` · **Writes to disks:** not with `-r`

An alternative to [cryptsetup](cryptsetup.md) for BitLocker. It exposes the
decrypted volume as a file, `dislocker-file`, which is then mounted.

```sh
sudo mkdir -p /mnt/bitlocker /mnt/windows
sudo dislocker -r -V /dev/sdX3 -u -- /mnt/bitlocker          # asks for the user password
sudo dislocker -r -V /dev/sdX3 -p -- /mnt/bitlocker          # asks for the recovery key
sudo dislocker -r -V /dev/sdX3 -f /path/key.BEK -- /mnt/bitlocker   # with a .BEK key file
sudo ntfs-3g -o ro /mnt/bitlocker/dislocker-file /mnt/windows
sudo umount /mnt/windows && sudo umount /mnt/bitlocker
```

`-r` keeps the BitLocker volume read-only.
