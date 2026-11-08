# dcfldd: raw images with hashes

**Package:** `dcfldd` · **Writes to disks:** to the output

`dd` with hashing and progress built in.

```sh
sudo dcfldd if=/dev/sdX of=/mnt/target/disk.img hash=sha256 hashlog=/mnt/target/disk.sha256
sudo dcfldd if=/dev/sdX of=/mnt/target/disk.img hash=md5,sha256 hashwindow=1G hashlog=/mnt/target/disk.hashes
```

- `hash=`: md5, sha1, sha256, sha384 or sha512 (several, separated by commas).
- `hashlog=`: where the hashes go; `hashwindow=` also hashes each chunk of
  that size, to locate damage later.

dcfldd stops on read errors like `dd`. For a failing disk use
[ddrescue](../recovery/ddrescue.md), then hash the image.

> **Writes:** to `of=`. Check `if=` (source) and `of=` (target) twice.
