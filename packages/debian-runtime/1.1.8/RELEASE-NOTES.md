# OycZERO Debian runtime 1.1.8

This signed DATA package initializes the pinned Debian 13 application runtime
used by OycZERO 0009. It adds the official Raspberry Pi camera stack,
`python3-picamera2`, `iproute2`, `iw`, `rfkill`, graphics and media dependencies
needed by compatible Store applications.

Install it through the OycZERO default-suite flow. Direct installation is also
available for recovery:

```sh
oyczero app install /data/debian-runtime-1.1.8-arm64.oyp
```

Removing the package normally preserves runtime state. Explicit purge remains a
separate guarded operation.
