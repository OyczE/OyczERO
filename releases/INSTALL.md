# Installing and updating OyczERO

Always download artifacts from the matching numbered GitHub Release and verify
their SHA-256 checksums before use.

## Initial installation or recovery

A file named `oyczero-vNNNN-install-host.img.xz` or
`oyczero-vNNNN-install-adb.img.xz` is a complete SD-card image for Raspberry Pi
Imager. Select it through **Use custom**, choose the correct SD card and complete
write verification.

This operation replaces the partition table and erases existing DATA, including
settings, credentials and user files. Back up required files first.

Choose the Host image for the normal USB-host/Ethernet profile. Choose the ADB
image only when USB device diagnostics are required and follow the release
notes for the physical USB-role switch position.

## Updating an installed system

A file named `oyczero-vNNNN-update.oyu` is not a disk image and must not be
opened with Raspberry Pi Imager. Install the latest stable update on OyczERO:

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

For a package copied to DATA, use its actual path:

```sh
oyczero update install /data/oyczero-vNNNN-update.oyu
```

The updater verifies the signed package, writes the inactive system slot and
tries it once. A successful trial becomes the default; a failed trial returns
to the previous slot. DATA is preserved.

## Optional tool packages

Optional DATA-resident tools use `.oyp` packages and their own version numbers.
They are separate from both the initial-install image and the `.oyu` operating-
system update. Follow the package's release notes for compatibility and install
commands.
