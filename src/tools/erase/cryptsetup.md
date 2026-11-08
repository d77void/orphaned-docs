# Destroying encryption keys

**Package:** `cryptsetup` · **Writes to disks:** yes, the key material

A LUKS volume is unreadable without its keys, so destroying them makes the data
unrecoverable in seconds, whatever the size of the disk.

```sh
sudo cryptsetup isLuks -v /dev/sdX2     # is it LUKS?
sudo cryptsetup erase /dev/sdX2         # destroy all key slots
sudo cryptsetup luksDump /dev/sdX2      # the slots are now empty
```

This is only as good as the encryption was: copies of the LUKS header, kept
elsewhere, could still open the volume with an old passphrase. If the disk was
ever used unencrypted, old data may remain outside the volume, so follow with a
method from [the chapter's table](index.md) when that matters.

The [persistence partition](../../persistence/index.md) of a d77orphaned stick
can be destroyed this way too.
