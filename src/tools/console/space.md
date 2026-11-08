# ncdu and tree: disk space

**Packages:** `ncdu`, `tree`

```sh
sudo ncdu -x /mnt      # what takes space under /mnt, without crossing into other file systems
tree -L 2 /mnt         # folder structure, two levels deep
tree -h --du /mnt      # with sizes
```
