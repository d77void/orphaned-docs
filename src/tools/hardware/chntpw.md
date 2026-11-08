# chntpw: Windows local accounts

**Package:** `chntpw` · **Writes to disks:** yes, when you save a change

Lists the local accounts of a Windows installation and can clear a
password or unlock an account. It works on the `SAM` file of the Windows
partition, mounted **read-write**. Only on machines you are authorized to
administer.

```sh
sudo ntfs-3g /dev/sdX3 /mnt                           # the Windows partition, read-write
cd /mnt/Windows/System32/config
sudo chntpw -l SAM                                    # list the accounts
sudo chntpw -u Administrator SAM                      # interactive menu for one account
sudo umount /mnt
```

In the menu, "Clear (blank) user password" and "Unlock and enable user
account" are the usual choices; then `q` and `y` to save.

Windows must have been **shut down fully** (not hibernated or Fast
Startup), or NTFS will not mount read-write safely. Accounts linked to a
Microsoft account and BitLocker-encrypted drives are not handled this way.
