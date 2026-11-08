# Forensics

Tools to image disks with hashes, open forensic image formats and examine
file systems without mounting them.

A careful workflow, in short:

1. Make the source read-only ([blockdev](../disks/blockdev.md)).
2. Image it with hashes ([dcfldd](dcfldd.md) or [ewfacquire](ewf.md)) onto
   another disk.
3. Verify the image (`ewfverify`, or compare the hashes).
4. Work only on the image: list and extract files with the
   [Sleuth Kit](sleuthkit.md), carve deleted data with [foremost](foremost.md),
   or mount it read-only ([xmount](xmount.md), [losetup](../disks/losetup.md)).

d77orphaned gives you tools that do not write unless told to. Chain of
custody, notes and procedure are yours.

| Tool | For |
|---|---|
| [sha256sum and friends](hashes.md) | hashing disks, images and files |
| [dcfldd](dcfldd.md) | raw images with hashes computed while copying |
| [ewfacquire, ewfverify, ewfinfo, ewfmount](ewf.md) | EWF (E01) images |
| [affinfo](afflib.md) | AFF images |
| [xmount](xmount.md) | presenting E01/AFF images as raw disks |
| [Sleuth Kit](sleuthkit.md) | partitions, files and deleted files inside an image |
| [foremost](foremost.md) | carving files out of raw data |
| [binwalk](binwalk.md) | finding embedded files and firmware |
| [xxd and hexedit](hex.md) | looking at raw bytes |
