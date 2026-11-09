# Recovery

Tools to copy data off failing disks, find lost partitions and files, and
back up or restore file systems.

On a failing disk, **copy first, repair later**: every read of a dying disk
may be one of the last. Image it with [ddrescue](ddrescue.md) onto a healthy
disk, then run the other tools on the image (see [losetup](../disks/losetup.md)).

| Tool | For |
|---|---|
| [ddrescue](ddrescue.md) | copying a failing disk, skipping and retrying bad areas |
| [testdisk](testdisk.md) | finding lost partitions, repairing boot sectors, undeleting |
| [photorec](photorec.md) | recovering files by their content, whatever the file system |
| [extundelete](extundelete.md) | undeleting files on ext3/ext4 |
| [partclone](partclone.md) | imaging only the used blocks of a file system |
| [fsarchiver](fsarchiver.md) | backing up and restoring file systems as archives |
| [gpart](gpart.md) | guessing a lost MBR partition table |
| [restic](restic.md), [borg](borg.md) | getting files back from backups |
