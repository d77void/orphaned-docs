# I am giving this computer away

**Writes to the disk:** yes, **everything, permanently**.

## 1. Before erasing

- **Copy what you want to keep,** and check that the copy opens on another computer.
- Sign out of what is tied to the machine: licences, cloud accounts, password
  managers. On Windows, save the BitLocker recovery key if you might need the old data.
- Note down the disk's model and serial for your records, if it matters.
- Are you sure this is the disk? **Check by model and serial,** and disconnect any
  disk or USB stick you do not mean to erase.

  ```sh
  lsblk -d -o NAME,SIZE,MODEL,SERIAL,TRAN
  ```

## 2. Pick the method by disk type

The `TRAN` column above says how it is connected; `sudo smartctl -i /dev/sdX` says
if it is solid state.

| Disk | Do this |
|---|---|
| Hard disk | [nwipe](../tools/erase/nwipe.md): one pass is enough |
| SATA SSD | [ATA Secure Erase](../tools/erase/hdparm.md) |
| NVMe SSD | [NVMe sanitize or format](../tools/erase/nvme.md) |
| Encrypted | [destroy the keys](../tools/erase/cryptsetup.md), then one of the above |
| USB-connected | [nwipe](../tools/erase/nwipe.md), and treat it as not guaranteed |

**Why not just nwipe on an SSD?** An SSD keeps spare cells that overwriting cannot
reach. Its own erase command can. The details are in
[Secure erasure and sanitization](../tools/erase/index.md).

A laptop's firmware often blocks the SATA command ("frozen"): the
[page](../tools/erase/hdparm.md) tells you what to do.

## 3. Check it

- After `nwipe`: its verification pass, and its log.
- After a firmware erase: `sudo cmp /dev/sdX /dev/zero` usually reports it reads as
  zeros. Not every drive returns zeros. You are trusting the drive's firmware.

## 4. If the disk leaves your hands and the data was sensitive

If a drive fails to erase, or the stakes are high, **take it out and destroy it**.
A new disk costs less than the consequences.

## 5. What remains in the computer

Firmware may hold the owner's name, passwords or boot entries: clear them in its
setup. On a TPM machine, clear the TPM there too. Remove any stick you left in.

> Tested: `nwipe` in a virtual machine and on real hardware. The firmware commands
> have **not** been run on real drives by this project.
