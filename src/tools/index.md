# Tools in the image

Each area has its own chapter, with a page per tool and its basic commands:
[Disks](disks/index.md), [Recovery](recovery/index.md), [File systems and volumes](filesystems/index.md), [Forensics](forensics/index.md), [Network](network/index.md), [Hardware and boot](hardware/index.md), [Console](console/index.md).

All tools are official Void Linux packages, except `nmap` (from Void's
*nonfree* repository) and, from the d77void repository, the graphical
sessions, Kantele, Mullvad Browser and `d77-slock`. A virtual-machine test
checked that every program in the image (2006 of them) finds all its
libraries.

| Area | Packages |
|---|---|
| Disks and storage hardware | `util-linux` `parted` `gptfdisk` `smartmontools` `nvme-cli` `hdparm` `sdparm` `sg3_utils` `lsscsi` `f3` |
| Recovery and cloning | `ddrescue` `testdisk` `partclone` `fsarchiver` `extundelete` `gpart` |
| File systems | `e2fsprogs` `xfsprogs` `xfsdump` `btrfs-progs` `dosfstools` `exfatprogs` `fuse-exfat` `ntfs-3g` `f2fs-tools` `jfsutils` `mtools` |
| Volumes and encryption | `cryptsetup` `lvm2` `mdadm` `dislocker` |
| Forensics | `dcfldd` `libewf` `afflib` `sleuthkit` `foremost` `xmount` `binwalk` `hexedit` `xxd` |
| Boot and EFI | `efibootmgr` `efivar` `os-prober` `kexec-tools` |
| Network | `NetworkManager` `iproute2` `iputils` `dhcpcd` `wpa_supplicant` `iw` `ethtool` `openssh` `curl` `wget` `lftp` `links` `rsync` `fuse-sshfs` `nfs-utils` `cifs-utils` `wireguard-tools` `openvpn` |
| Network diagnostics | `tcpdump` `nmap` `traceroute` `mtr` `bind-utils` `whois` `ldns` `openbsd-netcat` `socat` `arp-scan` `iperf3` `iftop` `nethogs` `net-tools` `ipcalc` |
| Hardware and system | `dmidecode` `pciutils` `usbutils` `hwinfo` `lshw` `inxi` `lm_sensors` `acpi` `memtester` `stress` `fio` `cpuid` `cpupower` `chntpw` `lynis` |
| Console | `tmux` `screen` `mc` `ranger` `vim` `nano` `less` `htop` `iotop` `sysstat` `ncdu` `tree` `lsof` `strace` `ltrace` `pv` `mbuffer` `psmisc` `moreutils` `bash-completion` |
| Archives | `zstd` `p7zip` `zip` `unzip` `lz4` `lzop` `cabextract` `unp` `squashfs-tools` |
| Other | `gnupg` `minicom` `tio` `chrony` `xtools-minimal` `man-db` |
| Desktop | pwm, wasp + Utumno, Kantele, `mullvad-browser`, `feh`, `conky`, `zathura`, PipeWire (sound), `upower` (battery), `d77-slock` |

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
`dmraid` and `bcache-tools` because they activate volumes on their own at
boot; ZFS (needs a compiler and a lot of space); Wireshark's graphical
interface (very large).

Candidates for a later version: `exiftool`, `tshark`, `yara`, `john`,
`git`, `gparted`, `samba`, backup tools (`restic`, `borg`) and console
accessibility tools.
