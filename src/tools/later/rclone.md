# rclone: cloud storage

**Install:** `sudo xbps-install -S rclone` ([about installing](index.md)) · **Writes:**
to the destination you name

Copies files to and from cloud storage (Google Drive, S3, OneDrive and many others),
often the quickest way to get rescued files off a machine.

```sh
rclone config                              # set up a remote, interactively; here called "drive"
rclone lsd drive:                          # its folders
rclone ls drive:Rescue                     # its files
rclone copy -P /mnt/rescue drive:Rescue    # copy, with progress
rclone copy --dry-run /mnt/rescue drive:Rescue    # show what it would do
rclone check /mnt/rescue drive:Rescue      # do both sides match?
```

> **`sync` deletes.** It makes the destination identical to the source, removing
> what is not in the source. Use `copy` unless you mean that.

The configuration holds your access to the account. Without
[persistence](../../persistence/index.md) it vanishes at reboot. Set it up again each time.

> Installed, and its options checked against its help. Not tested with a real
> cloud account.
