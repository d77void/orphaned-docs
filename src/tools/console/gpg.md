# gpg: signatures and encryption

**Package:** `gnupg`

```sh
gpg --verify file.sig file          # check a detached signature (needs the signer's key)
gpg --import key.asc                # import a public key
gpg -c file                         # encrypt with a passphrase → file.gpg
gpg -d file.gpg > file              # decrypt
```

Encrypt recovered data with `gpg -c` before carrying it on a USB stick.
