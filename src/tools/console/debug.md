# lsof, strace, ltrace: what programs are doing

**Packages:** `lsof`, `strace`, `ltrace`

```sh
lsof /mnt                   # which processes keep files open there ("target is busy")
lsof -i                     # network connections and listening ports
strace -f -e trace=file program   # files a program tries to open
sudo strace -p 1234         # attach to a running process
ltrace program              # library calls
```

`umount: target is busy` → `lsof /mnt` shows what to close.
