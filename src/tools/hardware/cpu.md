# cpuid and cpupower: CPU details

**Packages:** `cpuid`, `cpupower` · **Writes to disks:** no

```sh
lscpu                         # model, cores, threads, caches, flags (util-linux)
cpuid -1                      # everything the CPU reports, for one core
cpupower frequency-info       # frequency limits and the current governor
sudo cpupower frequency-set -g performance   # run at full speed (until reboot)
```
