# OyczERO changelog

This changelog lists published stable releases only.

## 0007 — 2026-11-19

[Release v0007](https://github.com/OyczE/OyczERO/releases/tag/v0007)

- Added signed optional `.oyp` packages stored entirely on DATA while keeping
  the immutable base OS application-free.
- Added `oyczero app` management, F3 install/open integration and Setup startup
  selection; Shell remains the default.
- Published the official ARM64 M5Stack APPLauncher `0.6.110` as the first
  optional package.
- Added a two-second startup cancellation window and a physical Fn+Esc hold to
  terminate the launcher and return to a clean Shell.
- Prevented shell input and application diagnostics from leaking onto the GUI
  or the restored console.

## 0006 — 2026-11-18

[Release v0006](https://github.com/OyczE/OyczERO/releases/tag/v0006)

- Replaced separate Host and ADB images with one universal image that follows
  the physical Host/Slave switch without rebooting.
- Added automatic Host/LAN to owned ADB transitions while keeping SSH
  independently available over LAN or Wi-Fi.
- Kept update-v1 compatibility: a signed update from 0005 migrates the shared
  BOOT selectors only after the new slot passes its trial health check.
- Fixed active A/B slot detection when the running SquashFS is mounted as
  `/dev/root`.
- Kept the base OS application-free; optional DATA packages remain the next
  development priority.

## 0005 — 2026-11-18

[Release v0005](https://github.com/OyczE/OyczERO/releases/tag/v0005)

- Restored complete Raspberry Pi Imager fresh-install images for Host/SSH and
  USB-peripheral/ADB profiles.
- Kept the signed DATA-preserving A/B update as a separate artifact.
- Removed JanOS-app and optional applications from the base OS; optional DATA
  packages begin in 0006.
- Added guarded ADB cable-reconnect recovery with explicit-stop suppression.
- Fixed ADB-launched updates so access shutdown cannot kill the updater before
  the trial restart.
- Corrected ConnMan credential reuse for escaped SSIDs and passphrases.

## 0004 — 2026-11-17

[Release v0004](https://github.com/OyczE/OyczERO/releases/tag/v0004)

- Added USB Wi-Fi monitor mode through `oyczero monitor`.
- Added `tcpdump`, `airodump-ng`, `aireplay-ng` and `aircrack-ng`.
- Verified capture and channel hopping with ALFA AWUS036AC on 2.4 and 5 GHz.
- Distributed as a DATA-preserving `.oyu` update for an installed OyczERO
  system. No full initial-install image is attached to this release.

## 0003 — 2026-11-17

[Release v0003](https://github.com/OyczE/OyczERO/releases/tag/v0003)

- Fixed an SD-card driver failure that could stop startup or an update restart.
- Added firmware for additional USB Wi-Fi chipsets.
- Added stable Wi-Fi interface names and automatic saved-network reconnect.
- Verified ALFA AWUS036AXML and AWUS036AC adapters.

## 0001 — 2026-11-16

[Release v0001](https://github.com/OyczE/OyczERO/releases/tag/v0001)

- Introduced numbered stable releases and stable/development update channels.
- Added signed A/B updates with trial boot, health confirmation and automatic
  return to the previous slot after a failed trial.
- Preserved settings and files on DATA during operating-system updates.
