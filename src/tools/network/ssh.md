# ssh, scp, rsync, sshfs: working over SSH

**Packages:** `openssh`, `rsync`, `fuse-sshfs`

```sh
ssh user@host                                  # remote shell
scp file.img user@host:/backup/                # copy a file to another machine
rsync -aP /mnt/source/ user@host:/backup/      # copy a folder, with progress, resumable
rsync -aP --dry-run /mnt/source/ /mnt/target/  # show what would be copied, copy nothing
mkdir -p ~/remote && sshfs user@host:/data ~/remote   # mount a remote folder
fusermount3 -u ~/remote                        # unmount it
```

Copying a recovered disk image to another machine is often easier than
finding a local disk big enough.

The **SSH server** is off. To let others in, see [Network](../../network/index.md#ssh-server).
