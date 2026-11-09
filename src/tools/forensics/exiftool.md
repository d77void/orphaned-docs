# exiftool: file metadata

**Package:** `exiftool` · **Writes to disks:** only with the options that change metadata

Reads metadata from photos, documents, videos and many more: dates, camera,
GPS position, author, software used.

```sh
exiftool photo.jpg                         # everything it finds
exiftool -a -G1 document.pdf               # with duplicates, grouped by origin
exiftool -gps:all photo.jpg                # only the GPS position
exiftool -r -csv /mnt/evidence/Photos > photos.csv   # a whole folder, as a table
```

> **Writes:** options that set a value (such as `-all=`) change the file, and
> keep a copy named `file_original`. Never on evidence: work on a copy.
