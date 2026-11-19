# Installing and updating OyczERO

Always download artifacts from the matching numbered GitHub Release and verify
their SHA-256 checksums before use.

## Initial installation or recovery

A file named `oyczero-vNNNN-install.img.xz` is a complete SD-card image for
Raspberry Pi Imager. Select it through **Use custom**, choose the correct SD
card and complete write verification.

This operation replaces the partition table and erases existing DATA, including
settings, credentials and user files. Back up required files first.

Starting with 0006, one universal image follows the physical switch. Host
exposes the internal hub and Ethernet. Slave exposes owned USB ADB through
USB-C2. Switching roles does not require a reboot.

## Updating an installed system

A file named `oyczero-BUILD-ID-update.oyu` is not a disk image and must not be
opened with Raspberry Pi Imager. Install the latest stable update on OyczERO:

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

For a package copied to DATA, use its actual path:

```sh
oyczero update install /data/oyczero-BUILD-ID-update.oyu
```

The updater verifies the signed package, writes the inactive system slot and
tries it once. A successful trial becomes the default; a failed trial returns
to the previous slot. DATA is preserved.

## Optional tool packages

Optional DATA-resident tools use `.oyp` packages and their own version numbers.
They are separate from both the initial-install image and the `.oyu` operating-
system update. Follow the package's release notes for compatibility and install
commands.

OyczERO 0007 or newer can install the pinned M5Launcher package directly:

```sh
oyczero app install m5launcher
```

F3 installs M5Launcher when absent and opens it when installed. Package payloads
and mutable state remain on DATA. Hold Fn+Esc for about two seconds to exit the
running launcher and return to Shell.
