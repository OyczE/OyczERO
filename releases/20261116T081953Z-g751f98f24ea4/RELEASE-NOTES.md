# OyczERO first binary release candidate

Build: `20261116T081953Z-g751f98f24ea4`. Source commit: `751f98f24ea4` (clean).
Status: locally staged; not published and not yet cleared for redistribution.
Target: CardputerZero v0.5 / ARM64. Installer layout: ab-v3.

## Changes

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

- `oyczero-20261116T081953Z-g751f98f24ea4-install-host.img.xz`: USB Host/Ethernet profile.
- `oyczero-20261116T081953Z-g751f98f24ea4-install-adb.img.xz`: USB peripheral/ADB profile.
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

- 684 stage-3 source/image checks passed; 27 future-stage checks deselected.
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


### Host first-boot sanity update

The owner flashed this Host candidate. SSH inspection confirmed the exact clean
build, successful first-install stages with LCD detected, read-only root A,
writable expanded DATA, LCD service readiness, working Ethernet/SSH, installer
ready state and matching A/B payload hashes. B trial boot and ADB-profile cold
boot remain untested. A later installer-logo enhancement is not in these assets.
