# restic: read and restore backups

**Package:** `restic` · **Writes to disks:** only to the folder you restore into

Opens restic repositories, local or remote, to recover files from them. It asks
for the repository's password.

```sh
restic -r /mnt/backup/repo snapshots                     # list the snapshots
restic -r /mnt/backup/repo ls latest                     # files in the newest one
restic -r /mnt/backup/repo find report.odt               # which snapshots have this file
restic -r /mnt/backup/repo restore latest --target /mnt/target/out
restic -r /mnt/backup/repo restore latest --target /mnt/target/out --include /home/user/Documents
restic -r /mnt/backup/repo check                         # is the repository healthy?
restic -r sftp:user@host:/backups/repo snapshots         # a repository over SSH
```

To browse a backup as a folder: `mkdir -p ~/snap && restic -r /mnt/backup/repo mount ~/snap`
(Ctrl+C to stop).

To make a new backup: `restic -r /mnt/target/repo init` once, then
`restic -r /mnt/target/repo backup /mnt/source`.
