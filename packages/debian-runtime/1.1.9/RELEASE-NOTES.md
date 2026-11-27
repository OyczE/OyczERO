# OycZERO Debian runtime 1.1.9

This signed DATA package is the pinned Debian 13 application runtime for
OycZERO 0011. It retains the 1.1.8 application stack and adds the official
Raspberry Pi OS Lite camera command packages:

- `librpicam-app1` `1.15.0-1`;
- `rpicam-apps-core` `1.15.0-1`;
- `rpicam-apps-lite` `1.15.0-1`;
- `oyczero-rpicam-apps-compat` `1.15.0-1+oyczero1`.

The compatibility package satisfies the unversioned `rpicam-apps` dependency
used by compatible Store applications without installing the full Raspberry Pi
desktop camera metapackage. The runtime provides `rpicam-hello`,
`rpicam-still`, `rpicam-vid` and Picamera2.

The signed package contains the locked migration dependencies required to move
an existing 1.1.8 runtime to 1.1.9 transactionally. Install or repair it through
the OycZERO default-suite flow. Direct recovery installation is also available:

```sh
oyczero app install /data/debian-runtime-1.1.9-arm64.oyp
```

Removing the package normally preserves runtime state. Explicit purge remains a
separate guarded operation.
