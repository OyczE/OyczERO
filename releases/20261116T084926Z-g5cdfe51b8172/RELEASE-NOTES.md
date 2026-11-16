# OyczERO first binary release candidate

Build: `20261116T084926Z-g5cdfe51b8172`. Source commit: `5cdfe51b8172` (clean).
Status: locally staged; not published and not yet cleared for redistribution.
Target: CardputerZero v0.5 / ARM64. Installer layout: ab-v3.

## Changes

- Animated OyczERO logo before installation stage 1: 1.75-second letter reveal
  and a one-second full-word hold. Uses initialized LCD/HDMI outputs and skips
  the delay when headless. The user accepted the live visual preview.
- Compact 257 MiB fresh installer with one system payload. First boot creates
  BOOT (256 MiB), system A/B (1 GiB each), and DATA using the remaining card.
- LCD/HDMI first-install progress and persistent installation diagnostics.
  Kernel firmware is accessible during the initial bootstrap.
- HDMI Off, Mirror LCD and independent Terminal modes.
- Setup now provides HDMI resolution (Auto, 1280x720, 1920x1080) and terminal
  font size (16, 24, 32 px). Keyboard-routing entries were removed from setup.
- Display previews require confirmation within 15 seconds; timeout or client
  disconnect restores the saved configuration.
- Adaptive terminal dimensions; Full HD/32 px uses the accepted 93x21 layout.
  CLI keyboard routing remains available with `oyczero hdmi focus` and `lcd`.
- Shell cleanup restores LCD keyboard focus after exit, including tty hangup.
- Default builds no longer embed local developer SSH authorization keys.

Earlier features include Bash root console, setup and F1/F2/F3 shortcuts,
Wi-Fi/LAN controls, persistent port power, status bar, boot splash/sound,
SSH password setup, ADB diagnostics and JanOS/Monster Grove integration.

## Files and installation

- `oyczero-20261116T084926Z-g5cdfe51b8172-install-host.img.xz`: USB Host/Ethernet profile.
- `oyczero-20261116T084926Z-g5cdfe51b8172-install-adb.img.xz`: USB peripheral/ADB profile.
- `SHA256SUMS`, `manifest.json`, `build.json`, per-image installer metadata,
  `kernel.config`, `validation.json` and this document.

Verify SHA-256 and write the selected `.img.xz` using Raspberry Pi Imager.
Each uncompressed image is 257 MiB. The first boot creates the final layout;
keep power connected. Use a card of at least nominal 4 GB.
**Fresh installation erases existing DATA, settings and files. These are not
DATA-preserving update packages.** See [installation](../INSTALL.md).

The local console autologs in as root. No shared SSH password, personal public
key or private host key is provided. On the Host profile, run `oyczero ssh setup`
to choose your own password before remote access. The ADB profile is intended
for physical USB diagnostics. Never use a previous developer password.

## Validation and remaining acceptance

- 686 stage-3 source/image checks passed; 27 future-stage checks deselected.
- Two disposable-loop installer integrations passed, including real ARM64
  userspace under QEMU. This is not full CardputerZero hardware emulation.
- Packaged HDMI/setup sources match the committed implementation.
- Both profile boot commands and common root payload were checked.
- Root payload checked for personal SSID, developer authorization and private
  SSH key payloads; none present. Decompression hashes checked before export.
- On-device source preview passed timeout rollback, confirmed appearance changes,
  720p/24 px terminal geometry, focus switching, restart and exit cleanup.
- This exact installer pair still requires cold-boot/reboot hardware acceptance.
  Slot-B trial boot, automatic rollback, power interruption, hotplug and actual
  energy savings remain unqualified. Signed OTA is not implemented.

## Publication gate

The existing [third-party notices](../../THIRD-PARTY-NOTICES.md) remain applicable.
Before external distribution, finish the required license/corresponding-source
material and resolve JanOS-app redistribution permission. These candidates
are staged for the owner, not represented as a public or stable release.
Large binaries are Release attachments, never Git-tracked blobs. No source
repository history, credentials or private diagnostic files belong in this export.

### Acceptance provenance

The preceding clean Host build (20261116T081953Z-g751f98f24ea4) passed physical
first boot and SSH sanity: LCD ready, read-only root A, writable DATA, completed
installation and matching A/B payload hashes. The added logo passed live visual
preview. This is not full cold-boot acceptance of the new installer pair.

### Hardware follow-up

The exact Host image booted on the device; the user accepted its appearance.
SSH inspection confirmed the logo and all installer stages in retained logs,
valid ready records, matching A/B payload hashes, writable DATA, LCD, HDMI
mirroring, Ethernet and SSH. This does not establish a boot of slot B or the
ADB profile, nor a second-boot persistence test.

**Known release blocker:** Wi-Fi has no interface on this first boot. Kernel
logs report `brcmf_fwvid_request_module: mod=cyw: failed -2` and attach failure.
Diagnosis and a verified fix are required before publication.
