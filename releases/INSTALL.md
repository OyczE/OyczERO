# Installing and updating OycZERO

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
opened with Raspberry Pi Imager. Install the latest stable update on OycZERO:

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

## Application packages

Optional DATA-resident tools use `.oyp` packages and their own version numbers.
They are separate from both the initial-install image and the `.oyu` operating-
system update. Follow the package's release notes for compatibility and install
commands.

OycZERO 0009 fresh installations include an offline DATA-resident default
suite: Debian runtime `1.1.8`, official APPLaunch `0.6.111` and its matching
Store. The same immutable release assets can repair or complete an updated
system without replacing DATA.

Install or repair the suite through F3, or run:

```sh
oyczero app install m5launcher
```

The signed `.oyp` initializes the Debian runtime. The two published `.deb`
assets are verified against the release lock and installed inside that runtime;
they are not passed directly to `oyczero app install`. MLauncher is the default
startup target. Esc during its startup countdown keeps Shell for the current
boot. Starting with OycZERO 0010, holding Fn+Esc for two seconds exits the
running launcher through the host-owned cleanup path. On 0009, use
`oyczero app shutdown` over SSH when launcher recovery is required.
