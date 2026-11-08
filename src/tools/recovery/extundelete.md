# extundelete: undelete on ext3/ext4

**Package:** `extundelete` · **Writes to disks:** no (to the scanned file system); recovered files go to the current folder

Recovers deleted files from an ext3 or ext4 file system using its journal.
The file system must be **unmounted**.

```sh
cd /mnt/target                                         # somewhere on another disk
sudo extundelete /dev/sdX1 --restore-all               # everything it can find
sudo extundelete /dev/sdX1 --restore-file home/user/report.odt   # one file
sudo extundelete /dev/sdX1 --restore-directory home/user/Photos  # one folder
sudo extundelete /dev/sdX1 --restore-all -o /mnt/target/undeleted   # choose the output folder
```

Recovered files go to `RECOVERED_FILES/` in the current folder, or to the
folder given with `-o`. Paths are relative to the root of the file system,
without a leading `/`.

The sooner it runs after the deletion, the better: anything written to that
file system since may have reused the blocks.
