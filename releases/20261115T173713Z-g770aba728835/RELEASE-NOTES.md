# OyczERO — First development release

Build **`20261115T173713Z-g770aba728835`** is staged locally for the project
owner's CardputerZero test. It has not been published to GitHub, and physical
boot of this exact image is pending.

Copyright (c) 2026 Mateusz Ziółek - LAB5 (lab5.eu.com).
Original materials: [OyczERO Proprietary License](../../LICENSE.md).
Bundled components: [Third-party notices](../../THIRD-PARTY-NOTICES.md).

## Files

Both images target **CardputerZero v0.5 / ARM64** and are 208,666,624 bytes
(199 MiB). Use the Host profile for the normal LAN setup.

| File | Purpose |
| --- | --- |
| `oyczero-20261115T173713Z-g770aba728835-host.img` | Normal USB Host profile with onboard Ethernet |
| `oyczero-20261115T173713Z-g770aba728835-adb.img` | USB-C2 peripheral diagnostics; Slave switch, onboard USB LAN unavailable |
| [SHA256SUMS](SHA256SUMS) | SHA-256 hashes for both images and the kernel configuration |
| [manifest.json](manifest.json) | File names, sizes, profiles and hashes |
| [build.json](build.json) | Build timestamp, full source commit and clean/dirty state |
| [kernel.config](kernel.config) | Actual kernel build configuration |
| [validation.json](validation.json) | Image inspection and recorded test results |

The `.img` files are ignored by Git and belong in Release attachments. Public
image downloads are not available yet. Authorized maintainers can use a draft
under [GitHub Releases](https://github.com/OyczE/OyczERO/releases) once its assets
are uploaded; a draft is not a published release.

## Included functionality

- LCD/HDMI console, built-in keyboard, root autologin with Bash, splash and sound.
- Battery/RTC information and a fixed LCD status bar with M/W/L/B indicators.
- Wi-Fi with saved-profile reconnection, preferred Ethernet routing and fallback.
- On-demand SSH and USB ADB diagnostics, framebuffer screenshots and unified
  `oyczero COMMAND` controls.
- Grove/EXT power selection, shared-UART protection and native JanOS-app support
  with the console-title fix. Grove Monster ping/app operation has prior hardware
  acceptance; this exact build still needs its own device check.
- Persistent ext4 `/data` and experimental A/B tooling in the development project.
  These supplied images use the legacy three-partition layout.

This rebuild uses source commit `770aba728835077729b0ddb427280d6e4761c598`, with
unchanged tracked file contents and no personal SSH seed. Linux executable modes
were restored for shebang scripts in the disposable build workspace. Full build
configuration synchronization enabled legacy Netfilter options/modules compared
with the earlier 15:50 build; `kernel.config` records the resulting configuration.

## Installation and access

**These are fresh-install images. Writing one replaces `/data`, including saved
Wi-Fi settings and SSH authorization. Back up first.** There is no data-preserving
updater or production A/B rollback in this release.

Follow the [installation guide](../INSTALL.md). Local login is `root` with an
empty password and automatic Bash login. SSH requires your own authorized public
key; no computer is pre-authorized. SSH and ADB remain off after every boot.

## Validation and limits

- **454 source/image tests passed; 27 later-stage tests deselected.**
- QEMU ARM64 tests passed for networking on a read-only root, SSH key acceptance,
  rejected foreign keys/passwords, SCP, reconnect and persistent host identity.
- Image inspection checked all three filesystems, matching embedded build IDs,
  an empty data seed and the absence of pre-authorized/private access key files.
- Staged bytes match the build archive and SHA-256 manifest.
- This is host/image/QEMU evidence, not physical boot or electrical validation.
  Record a device test against this build ID after flashing.
- Signed updates, the desktop/web flasher, JanOS autostart and further power
  management remain pending. Physical EXT-only peripheral, Bluetooth pairing,
  JanOS SD/reconnect and complete keyboard acceptance also remain.
- External distribution is not yet cleared: the component notices identify
  corresponding-source/license work and pending JanOS-app redistribution permission.

[Changelog](../../CHANGELOG.md) · [Build index](../README.md)
