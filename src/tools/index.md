# Tools in the image

Each area has its own chapter, with a page per tool and its basic commands:
[Disks](disks/index.md). More chapters are being added.

All tools are official Void Linux packages, except `nmap` (from Void's
*nonfree* repository) and the graphical sessions (from the d77void
repository). A virtual-machine test checked that every program in the image
finds all its libraries, and that each command listed below exists.

| Area | Packages | Main commands |
|---|---|---|
| Disks and storage hardware | `util-linux` `parted` `gptfdisk` `smartmontools` `nvme-cli` `hdparm` `sdparm` `sg3_utils` `lsscsi` | `lsblk` `parted` `gdisk` `smartctl` `nvme` `hdparm` `sdparm` `sg_inq` `lsscsi` |
| Recovery and cloning | `ddrescue` `testdisk` `partclone` `fsarchiver` | `ddrescue` `testdisk` `photorec` `partclone.ext4` (and the other `partclone.*`) `fsarchiver` |
| File systems | `e2fsprogs` `xfsprogs` `btrfs-progs` `dosfstools` `exfatprogs` `ntfs-3g` `f2fs-tools` `mtools` | `mkfs.*` `fsck.*` `xfs_repair` `btrfs` `ntfs-3g` `mcopy` |
| Volumes and encryption | `cryptsetup` `lvm2` `mdadm` | `cryptsetup` `lvm` (`vgchange`, `lvs`, …) `mdadm` |
| Boot and EFI | `efibootmgr` `efivar` `os-prober` | `efibootmgr` `efivar` `os-prober` |
| Network | `iproute2` `iputils` `dhcpcd` `wpa_supplicant` `openssh` `curl` `rsync` | `ip` `ping` `dhcpcd` `wpa_supplicant` `ssh` `curl` `rsync` |
| Network diagnostics | `tcpdump` `nmap` `traceroute` `mtr` `ldns` `openbsd-netcat` `socat` `arp-scan` | `tcpdump` `nmap` `traceroute` `mtr` `drill` `nc` `socat` `arp-scan` |
| Forensics | `dcfldd` `libewf` `sleuthkit` `foremost` | `dcfldd` `ewfacquire` `mmls` `fls` (and the rest of the Sleuth Kit) `foremost` |
| Hardware and system | `dmidecode` `pciutils` `usbutils` `hwinfo` `chntpw` `f3` `lynis` `acpid` | `dmidecode` `lspci` `lsusb` `hwinfo` `chntpw` `f3probe` `lynis` |
| Everyday | `tmux` `vim` `less` `man-db` `lsof` `strace` `pv` `zstd` `p7zip` `squashfs-tools` `dialog` `chrony` `xtools-minimal` | `tmux` `vim` `man` `lsof` `strace` `pv` `zstd` `7z` `mksquashfs` |

Memtest86+ is in the [boot menu](../getting-started/boot-menu.md), not in
the running system.

## Some tools write to disks

Several of these tools exist to change disks: `parted`, `gdisk`, `mkfs.*`,
`fsck.*`, `testdisk` (when you tell it to write), `partclone` and
`fsarchiver` when restoring, `chntpw`, `efibootmgr`. They do what you ask,
on the device you name. Check the device twice, and see
[Working safely with disks](../disks/index.md).

## Security tools

The network tools are here for diagnostics and for testing networks you are
**authorized** to test. Nothing in d77orphaned scans, captures or connects
anywhere on its own.

## Not included

Left out on purpose: automounting (`udisks2`, `udiskie`, `gvfs`) because it
mounts disks by itself; `nwipe` because it is destructive by nature;
NetworkManager (`dhcpcd` and `wpa_supplicant` are enough); ZFS (needs a
compiler and a lot of space); Wireshark's graphical interface (very large).

Candidates for a later version: `exiftool`, `tshark`, `yara`, `binwalk`,
`john`, `wireguard-tools`, `iperf3`, `sshfs`, `nfs-utils`, `cifs-utils`,
`lshw` and console accessibility tools.
