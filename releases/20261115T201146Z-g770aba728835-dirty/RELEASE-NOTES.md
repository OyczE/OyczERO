# OyczERO — Access setup and expansion power

Build **`20261115T201146Z-g770aba728835-dirty`** is staged locally for the
owner's CardputerZero test. It has not been uploaded or published as a GitHub
release. The owner later confirmed boot, password setup and SSH after reboot.
Remote SSH verified this exact build; it became the base for the next RAM tests.

Copyright (c) 2026 Mateusz Ziółek - LAB5 (lab5.eu.com).
Original materials: [OyczERO Proprietary License](../../LICENSE.md).
Bundled components: [Third-party notices](../../THIRD-PARTY-NOTICES.md).

## Files and compatibility

Both images target **CardputerZero v0.5 / ARM64** with Linux `6.18.39-v8` and
the existing three-partition BOOT/SquashFS/ext4-data layout. Each is
208,666,624 bytes (199 MiB). They are fresh-install images, not OTA packages.

| File | Purpose |
| --- | --- |
| `oyczero-20261115T201146Z-g770aba728835-dirty-host.img` | Normal USB Host/LAN profile; SSH autostarts after personal credentials exist |
| `oyczero-20261115T201146Z-g770aba728835-dirty-adb.img` | Automatic USB-C2 ADB; Slave switch, onboard USB LAN unavailable |
| [SHA256SUMS](SHA256SUMS) | Hashes of both images and the kernel configuration |
| [manifest.json](manifest.json) | Artifact names, sizes, profiles and SHA-256 hashes |
| [build.json](build.json) | UTC build time, full source commit and dirty state |
| [kernel.config](kernel.config) | Actual kernel configuration |
| [validation.json](validation.json) | Public validation summary and remaining device checks |

The image files are staged beside these notes but ignored by Git. Large files
belong in GitHub Release attachments; no public download exists for this build.
The existing draft for the older 17:37 build is a different package.

The source base is `770aba728835077729b0ddb427280d6e4761c598` plus local changes.
Keep the original `-dirty` suffix: the commit alone does not identify those
changes. Artifact hashes identify the exact built bytes.

## Changes since the first development package

- **Personal SSH access:** run `oyczero ssh setup` to set a password and start
  SSH. Authentication state lives on `/data`. Passwords may contain 1–100
  UTF-8 bytes; empty passwords are rejected. Public keys remain supported.
- **Access profiles:** Host starts SSH after credentials exist; the ADB image
  starts USB diagnostics automatically. Saved autostart switches are independent
  and apply to their respective images. Both `start/stop` and `on/off` work.
- **Keyboard setup:** `oyczero setup` supports arrows and F=Up, Z=Left, X=Down,
  C=Right. Enter applies; Escape/Q exits. Moving cancels a pending preview.
  Password entry accepts ordinary letters without interpreting navigation keys.
- **Welcome information:** the local welcome includes `Setup: oyczero setup`
  and actual SSH/ADB service states. Refresh it with `oyczero info`.
- **Expansion power:** separate EXT 5V (14-pin) and Grove 5V (4-pin) switches
  apply immediately and verify enable readback. They leave routing unchanged,
  respect JanOS ownership and default off after reboot. Unavailable controls
  show N/A. All seven rows fit the LCD; smaller terminals scroll the menu.

The existing console, battery/RTC information, status bar, Wi-Fi/LAN policy,
audio, unified CLI and JanOS/Grove application remain included. The optional
Debian development environment is a separate package, not bundled here.

## Installation and first access

**Writing a full image replaces `/data`, including network settings, personal
SSH credentials and files. Back up needed data first.**

Follow the [installation guide](../INSTALL.md). The local Bash console logs in
automatically as `root`. There is no shared remote password or pre-authorized
personal computer. On Host, use `oyczero ssh setup` once, then connect as root
with your own password. On ADB, connect USB-C2 in Slave mode and use `adb shell`.
USB ADB provides root access without host authentication.

For the currently tested Grove Monster, enable **Grove 5V**; EXT is independent.
Use `oyczero monster on --port grove` to select UART, enable power and probe,
then `janos-app`. Setup's power switches do not launch or probe the application.

## Validation and remaining work

- **540 source/image tests passed; 27 later-stage tests deselected.**
- Actual ARM64 read-only-root networking, SSH password/key authentication,
  autostart settings, SCP, host identity and keyboard-menu checks passed.
  This is QEMU user-mode software testing, not complete board emulation.
- Image inspection verified the tested setup/system/Monster/access/welcome
  modules, build identities, boot profiles and absence of personal access seeds,
  private access keys and a preset remote password. Staged checksums match.
- Physical build `20261115T190142Z-g770aba728835-dirty` with RAM modules passed
  SSH PTY navigation, Enter-only independent power changes, Grove Monster
  `pong`, LCD captures and console restoration. Saved settings/credentials
  stayed unchanged and both outputs were restored off. The owner confirmed
  the updated menu works. This evidence predates flashing the present image.
- Exact-image cold boot/access autostart and full physical-key coverage remain
  pending. EXT readback verifies an enable signal, not output voltage or an
  EXT-connected peripheral. RTC display remains UTC.
- Signed OTA, data-preserving updates, qualified A/B rollback, desktop/web
  flashing, broader power management and JanOS autostart are not provided.
- The existing third-party license/source review and JanOS-app redistribution
  permission remain unresolved before distribution to other recipients.

[Changelog](../../CHANGELOG.md) · [Build index](../README.md)
