# OycZERO

OycZERO is a custom ARM64 Linux system for CardputerZero v0.5. The system
partition is read-only, while settings, credentials and user files persist on
`/data`.

## Downloads

Use the assets attached to the numbered
[GitHub Releases](https://github.com/OyczE/OyczERO/releases). Verify the
published SHA-256 checksum before installation.

The current stable release is [OycZERO 0009](https://github.com/OyczE/OyczERO/releases/tag/v0009).
It provides one universal Host/LAN and USB-peripheral/ADB SD-card image plus a
separate signed update for an already installed OycZERO A/B system. Its
offline default suite installs the Debian application runtime, official
APPLaunch `0.6.111` and Store on DATA while the Buildroot core remains
read-only.

Artifact types are intentionally separate:

- `.img.xz`: complete initial installation or recovery through Raspberry Pi
  Imager; replaces the card layout and DATA.
- `.oyu`: signed A/B operating-system update for a running OycZERO system;
  preserves DATA.
- `.oyp`: signed OycZERO package stored on DATA.
- `.deb`: native Debian application component installed inside the DATA runtime;
  it is not installed directly by the Buildroot host.

See [installation instructions](releases/INSTALL.md), the
[release layout](releases/README.md), the [changelog](CHANGELOG.md) and
[third-party notices](THIRD-PARTY-NOTICES.md).

## Repository contents

This repository contains public distribution material only: release metadata,
package metadata, built web content and exported flasher deliverables. OycZERO
source code, tests, build tools, TODO files and implementation plans are not
published here.

Large images and packages are GitHub Release assets and are not stored in Git
history.
