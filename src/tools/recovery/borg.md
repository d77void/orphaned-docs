# borg: read and restore backups

**Package:** `borg` · **Writes to disks:** only to the current folder when extracting

Opens BorgBackup repositories. It asks for the passphrase if there is one.

```sh
borg list /mnt/backup/repo                     # the archives
borg list /mnt/backup/repo::2026-11-01         # files in one archive
borg info /mnt/backup/repo::2026-11-01         # its size and date
cd /mnt/target/out && borg extract /mnt/backup/repo::2026-11-01             # everything
cd /mnt/target/out && borg extract /mnt/backup/repo::2026-11-01 home/user/Documents
borg extract --dry-run --list /mnt/backup/repo::2026-11-01     # show, write nothing
borg check /mnt/backup/repo                    # is the repository healthy?
```

`borg extract` writes into the **current folder**: change to a folder on another
disk first. Repositories over SSH need Borg on the other machine too:
`borg list user@host:/backups/repo`.
