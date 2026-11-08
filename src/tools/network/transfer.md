# curl, wget, lftp: downloading and uploading

**Packages:** `curl`, `wget`, `lftp`

```sh
curl -LO https://example.org/file.iso         # download, keep the name, follow redirects
curl -I https://example.org                   # headers only
wget -c https://example.org/file.iso          # download, resuming if interrupted
wget -r -np https://example.org/dir/          # a folder, recursively
lftp sftp://user@host                         # interactive FTP/SFTP client (mirror, get, put)
lftp -e 'mirror /remote/dir /local/dir; quit' ftp://user@host
```
