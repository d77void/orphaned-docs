# htop, iotop, iostat: processes and disk activity

**Packages:** `htop`, `iotop`, `sysstat`

```sh
htop                   # processes, CPU and memory (F6 sort, F9 kill, q quit)
sudo iotop -o -P       # only processes doing disk I/O right now
iostat -dx 2           # per-disk utilisation every 2 seconds (%util near 100 = disk saturated)
```
