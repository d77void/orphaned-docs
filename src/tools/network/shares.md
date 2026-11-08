# NFS and SMB shares

**Packages:** `nfs-utils`, `cifs-utils`

```sh
sudo mount -t nfs server:/export /mnt/share              # NFS
sudo mount -t nfs -o ro server:/export /mnt/share        # read-only
sudo mount -t cifs //server/share /mnt/share -o username=user          # Windows/Samba (asks for the password)
sudo mount -t cifs //server/share /mnt/share -o username=user,vers=3.0 # force SMB 3
sudo umount /mnt/share
```

Useful to save images and recovered files directly to a NAS or a Windows
share.
