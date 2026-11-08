# nwipe: overwrite whole disks

**Package:** `nwipe` · **Writes to disks:** yes, it erases them

The tool behind [ShredOS](https://github.com/PartialVolume/shredos.x86_64). It
overwrites whole disks, several at a time, verifies the result and writes a
report.

```sh
sudo nwipe                                  # interactive: pick disks and method, keys are shown on screen
sudo nwipe --method=zero /dev/sdX           # interactive, offering only this disk, with one zero pass
sudo nwipe --method=dodshort --verify=all /dev/sdX /dev/sdY
sudo nwipe --method=verify_zero /dev/sdX    # write nothing: check the disk is all zeros
```

In the interactive screen, nothing is erased until you select disks and press
the key to start.

## Methods

| `--method=` | What it does |
|---|---|
| `zero` (or `quick`) | one pass of zeros; enough for a hard disk |
| `one` | one pass of 0xFF |
| `random` (or `prng`, `stream`) | random data; the default |
| `dodshort` (or `dod3pass`) | 3 passes (DoD) |
| `dod522022m` (or `dod`) | 7 passes (DoD 5220.22-M) |
| `gutmann` | 35 passes; very slow, for old drives |
| `ops2`, `is5enh`, `bruce7`, `bmb` | other standards |
| `verify_zero`, `verify_one` | only check the disk's content |

## Useful options

- `--verify=off|last|all`: verify nothing, the last pass (default) or every pass.
- `--rounds=N`: repeat the method N times.
- `--logfile=FILE`: keep the log in a file.
- `-P PATH`: where the PDF report goes (`-P noPDF` for none). Save it somewhere
  that survives a reboot, such as `/mnt/d77-data`.
- `--exclude=/dev/sdA,/dev/sdB`: never touch these devices.
- `--nousb`: ignore USB devices.

## What protects you, and what does not

nwipe refuses devices that are in use. Verified in a virtual machine: the
d77orphaned boot stick (also with the RAM boot entry) and a mounted disk were
left untouched, and a disk given to `--exclude` too. `--force` removes this
protection; do not use it.

> **Danger:** `--autonuke` **without a device starts at once and erases every
> disk not in use**, with no questions. `--nogui` needs it. Always name the
> devices: `sudo nwipe --autonuke --nogui --method=zero /dev/sdX`.

Verified in a virtual machine: a disk wiped with `--method=zero --verify=last`
read back as all zeros.
