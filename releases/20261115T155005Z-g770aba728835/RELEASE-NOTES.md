# OyczERO 20261115T155005Z-g770aba728835

**Local development build; not a published release.** These notes document an
existing build. Its binaries have not been copied into this distribution
workspace, and this page is not a download offer.

| Field | Value |
| --- | --- |
| Built at | 2026-11-15 15:50:05 UTC |
| Source commit | `770aba728835077729b0ddb427280d6e4761c598` |
| Source state at build time | Clean |
| Board | CardputerZero v0.5, ARM64 |
| Image profiles | Host and ADB; each 208,666,624 bytes (199 MiB) |
| Image layout | Legacy BOOT + read-only SquashFS root + persistent ext4 data |

## Changes since a54a8cf

- Unified public commands under `oyczero`, with legacy helpers retained.
- Added explicit Monster Grove/EXT power selection, bounded ping probes and
  shared-UART ownership checks; the M indicator follows verified communication.
- Fixed stale JanOS raw-console command titles and added regression coverage.
- Added experimental A/B image tooling and dual-layout data validation. The
  ordinary Host/ADB images listed above retain the legacy layout.

The build also includes earlier Wi-Fi/Ethernet fixes, SSH/ADB diagnostics,
boot audio, the LCD status bar, keyboard/Bash console and battery/RTC support.
See the [changelog](../../CHANGELOG.md) for their development history.

## Choosing an image

- **Host:** normal USB Host profile for the onboard Ethernet path and attached
  USB peripherals. This is the profile booted in the latest recorded device test.
- **ADB:** USB peripheral diagnostic profile. Start USB access locally with
  `oyczero adb start`; this profile does not provide the shared onboard USB LAN
  path. ADB is development root access without host authentication.

SSH is enabled on demand with `oyczero ssh on` and requires an authorized key.
SSH and ADB remain off after reboot. A public distribution image must exclude
personal development SSH authorization seeds.

## Validation

- The build completed and passed **454 source/image tests**, with **27 later-stage
  tests deselected**. Archived image checksums were verified.
- The clean Host image booted on Zero and its build ID was confirmed over SSH.
  After restoring the saved network configuration, Wi-Fi associated and passed
  a gateway ping while Ethernet retained route preference.
- Earlier device acceptance covered Grove power, Monster `pong`, JanOS 1.7.7
  version/help, menu navigation, raw-console ping and return to the shell.
  Those checks used temporary overrides on an earlier base image; they were not
  a complete acceptance rerun on this clean build. Menu automation used synthetic
  keyboard events.
- Experimental data-layout helpers passed 13 native/ARM64 integration checks.
  This does not validate physical A/B boot or rollback.

## Known limitations

- **Writing either full image replaces `/data`**, including Wi-Fi profiles and
  other saved state. Back up first. Profile restoration is not update persistence.
- Signed OTA, the production updater, physical A/B rollback and the desktop/web
  flasher are not implemented. No migration of the live card is included.
- EXT-only Monster communication, complete physical key coverage, JanOS SD
  transfers/reconnect, Bluetooth pairing and power-management acceptance remain.
- JanOS autostart is deferred. Timezone setup and battery-saving policies are
  also pending.

[All build notes](../README.md) · [Project overview](../../README.md)
