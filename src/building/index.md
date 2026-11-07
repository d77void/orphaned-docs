# Building the ISO

The ISO is built from the
[d77void/d77orphaned](https://github.com/d77void/d77orphaned) repository
with `mkorphaned.sh`, a wrapper around `mklive.sh` from
[void-mklive](https://github.com/void-linux/void-mklive).

## Requirements

- A Void Linux x86_64 (glibc) computer, and root.
- A few GB free in the repository directory.
- `mtools`, if the computer's kernel cannot mount vfat images.

## Build

From the repository root:

```sh
sudo ./mkorphaned.sh
```

The result is `d77orphaned-live-x86_64-<date>.iso` in the same directory, as
with void-mklive. Options after `--` go to `mklive.sh`, for example a
different keyboard layout and language:

```sh
sudo ./mkorphaned.sh -- -k pt-latin1 -l pt_PT.UTF-8
```

## Repositories

Besides the official Void repositories, the build uses:

- the **d77void** repository on SourceForge, for pwm, wasp, Utumno, the
  greeter and Kantele;
- Void's **nonfree** repository, for `nmap`.

`-n` leaves both out, and `-r <repository>` adds one. Repositories given
first take precedence. For example, to use packages you built yourself with
`xbps-src`:

```sh
sudo ./mkorphaned.sh -n \
  -r /path/to/void-packages/hostdir/binpkgs/d77 \
  -r https://repo-default.voidlinux.org/current/nonfree
```

Packages already downloaded are cached in `xbps-cachedir-x86_64/`.

## The build does not touch your /boot

`mklive.sh` installs Memtest86+ into a helper directory that has no shell.
When that happens, XBPS runs the package's post-install script on the
computer doing the build, and that script regenerates the computer's own
`/boot/grub/grub.cfg` (running `os-prober` on its disks as well). This comes
from void-mklive.

The regenerated file is normally the same as an `update-grub` would make, but
a build should not change the computer that runs it. `mkorphaned.sh`
therefore runs the whole build in a private mount namespace, with an empty
`/boot`. The script then has nothing to regenerate, and the build fails if
the computer's `grub.cfg` changes anyway.

## Testing

`tests/qemu-harness.py` boots the ISO in QEMU (with KVM when available) and
runs the test scenarios: boot menus, sessions, tools and disk integrity. See
the repository's `README.md` and `docs/TEST_REPORT.md`.
