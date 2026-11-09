# testssl.sh: audit a server's TLS

**Package:** `testssl.sh` · For servers you are authorized to test

Checks a server's TLS versions, ciphers, certificate and known weaknesses.

```sh
testssl.sh https://example.org          # the full check (takes minutes)
testssl.sh --quiet --vulnerable example.org:443   # only known vulnerabilities
testssl.sh --protocols example.org      # only which TLS versions it offers
```
