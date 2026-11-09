# Emergency procedures

For when something has gone wrong, and you need the steps rather than the tools.

| What happened | Go to | Writes to the disk? |
|---|---|---|
| The computer no longer starts | [The computer does not boot](no-boot.md) | yes, the boot loader |
| Strange noises, read errors, files vanishing | [The disk is dying](dying-disk.md) | no, only to the copy |
| A partition disappeared | [I deleted a partition](deleted-partition.md) | yes, the partition table |
| A locked Windows disk | [I need the files from a BitLocker disk](bitlocker.md) | no |
| Bigger disk, or a new computer | [I want to move to another disk](migrate.md) | yes, the new disk |
| The computer changes hands | [I am giving this computer away](give-away.md) | yes, everything |

## Before anything else

1. **Stop using the disk.** Every write can destroy what you hope to recover.
   Do not run `fsck`, and do not reinstall, before you have read the procedure.
2. **Do you have a copy of what matters?** If not, and the data is worth more
   than the machine, [copy the disk first](dying-disk.md).
3. **Identify the disk by model and serial,** not by letter: `sdX` can change
   between boots.

   ```sh
   lsblk -d -o NAME,SIZE,MODEL,SERIAL,TRAN
   ```

4. **Save your work outside the live system.** Files in the running system, such
   as images, are in memory and vanish at reboot.

d77orphaned does not touch a disk until you tell it to. These procedures do tell
it to, and each one says where.

## When to stop

Stop and get professional help if the data is irreplaceable and the disk clicks,
grinds, or is not detected. Each attempt can make a physical failure worse, and a
data recovery lab has better chances with a disk nobody has kept running.

## How far these were tested

Each page says what was tested. "In a virtual machine" means on disposable disks,
with simulated faults: real failures are messier.
