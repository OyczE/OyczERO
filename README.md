# OyczERO

OyczERO is a custom ARM64 Linux system for **CardputerZero v0.5**, built with
Buildroot. It combines a read-only SquashFS system with persistent settings
and files on the ext4 `/data` partition.

## Status and history

The **first development build** is **`20261115T173713Z-g770aba728835`**, with Host
and ADB SD images prepared for testing. Public image downloads are pending
hardware acceptance and the remaining third-party distribution checks.
Native installer packages and the webflasher remain planned.

Repository: [OyczE/OyczERO](https://github.com/OyczE/OyczERO).
Published downloads, when available, will appear under
[Releases](https://github.com/OyczE/OyczERO/releases). Draft releases are visible
only to authorized maintainers and are not public downloads.

- [Changelog](CHANGELOG.md): dated development milestones and pending changes.
- [First development release](releases/20261115T173713Z-g770aba728835/RELEASE-NOTES.md):
  images, checksums, validation and known limitations.
- [Installation and access](releases/INSTALL.md): SD flashing, first boot,
  Wi-Fi setup and provisioning your own SSH key.
- [Release directory](releases/README.md): artifact naming and release policy.

The current system includes the LCD/HDMI console, built-in keyboard, root
autologin with Bash, boot splash and sound, battery/RTC information, a persistent
status bar, Wi-Fi and Ethernet, on-demand SSH/USB ADB, and the native JanOS app
with Monster communication over Grove. An optional Debian environment provides
`apt` and development tools; it is separate from the Buildroot base system.
Feature-specific validation and remaining hardware checks are recorded in the
build notes.

**A full SD image is a fresh installation: writing it replaces `/data`, including
saved Wi-Fi settings.** Data-preserving updates and qualified A/B rollback remain
planned or experimental. The Tauri desktop flasher and browser client are design
work only; no working updater or flasher is available yet. Back up device data
before a fresh installation.

## Build identity

Run `oyczero version` on the device to identify the installed system. Build IDs
use a UTC timestamp and the first 12 characters of the source commit, for example
`20261115T173713Z-g770aba728835`. A `-dirty` suffix records local source changes.
These IDs identify builds; they do not imply a published release or semantic
version. The changelog keeps unreleased work separate from built milestones.

## Ownership and licensing

Copyright (c) 2026 **Mateusz Ziółek - LAB5 (lab5.eu.com)**.
Project website: [lab5.eu.com](https://lab5.eu.com).

Original OyczERO materials are covered by the
[OyczERO Proprietary License](LICENSE.md), with the stated use permissions and
required attribution in permitted copies and forks. Third-party components
retain their own licenses. See [Third-party notices](THIRD-PARTY-NOTICES.md)
for the outstanding checks before sharing images with other recipients.

## Distribution layout

This distribution repository holds release material, installable packages,
public web assets and exported flasher deliverables. The full OS and application
development sources and their Git history remain in a separate local repository.

| Directory | Content |
| --- | --- |
| [releases/](releases/README.md) | Release notes and, when ready, selected OS images, update bundles, manifests and checksums |
| [packages/](packages/README.md) | Future Windows, Linux and macOS installer packages |
| [docs/](docs/README.md) | GitHub Pages content and future browser flasher assets; publish from `main` / `/docs` |
| [flasher/](flasher/README.md) | Future portable flasher deliverables and public usage documentation |

Large binary payloads are ignored by Git here and belong in GitHub Releases,
not Git history. Small public metadata and static HTML/CSS/JavaScript may be
tracked in the distribution repository. Browser-delivered code is necessarily
public; this does not authorize exporting the development source tree.

Only reviewed distribution exports belong here. Do not copy the development
repository's `.git` directory, source tree or history into this repository.

Never include private keys, credentials, user-data backups, logs, build caches
or private diagnostic images. Ignore rules are safeguards, not a substitute
for inspecting an export. Check dependencies and release licensing before
distributing binaries.
