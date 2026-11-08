# Secure erasure and sanitization

> **Everything in this chapter destroys data, and it cannot be undone.** Check
> each device by model and serial first (`lsblk -d -o NAME,SIZE,MODEL,SERIAL,TRAN`).
> Only erase disks you own or are authorized to erase. Nothing here runs by
> itself: d77orphaned erases only what you tell it to.

## Which method for which disk

| Disk | Use | Why |
|---|---|---|
| Hard disk (HDD) | [nwipe](nwipe.md) | overwriting reaches every sector the disk shows |
| SATA SSD | [ATA Secure Erase](hdparm.md) | the drive erases itself, including areas software cannot reach |
| NVMe SSD | [NVMe sanitize or format](nvme.md) | same, through the NVMe commands |
| SAS or SCSI disk | [sg_sanitize](sg_sanitize.md) | the SCSI equivalent |
| USB stick, SD card | [nwipe](nwipe.md), then treat as *not guaranteed* | adapters usually block firmware commands |
| Any disk already encrypted | [destroy the keys](cryptsetup.md), then one of the above | fast, and the data is unreadable without keys |

## Why overwriting is not enough on SSDs

An SSD maps what you write to whichever flash cells it chooses, and keeps spare
cells you cannot address. Overwriting the whole drive can leave old data in
those cells. The drive's own erase commands reach them, so use those on SSDs.

On a hard disk, one pass is enough: [NIST SP 800-88](https://csrc.nist.gov/pubs/sp/800/88/r1/final)
treats a single overwrite as sufficient for modern drives. Multi-pass methods
such as Gutmann or DoD take far longer, and exist for older drives or for
policies that require them.

## Check it worked

- After [nwipe](nwipe.md): its verification pass, and its log or PDF report.
- After a firmware erase: the drive only reports what it did, and you are
  trusting its firmware. You can check that it reads as empty, for example
  `sudo cmp /dev/sdX /dev/zero` (zeros are common, but not every drive returns them).
- For data that must never be recovered, physically destroy the drive as well.

## Several disks at once

nwipe wipes several disks at the same time by itself. For the other tools, see
[parallel](parallel.md).

> What has been tested: `nwipe` and `parallel`, in a virtual machine. The
> firmware commands (`hdparm`, `nvme`, `sg_sanitize`) have **not** been run on
> real drives by this project; their pages come from the tools' own
> documentation. Try them on a drive you can lose first.
