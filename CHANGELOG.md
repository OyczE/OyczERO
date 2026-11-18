# OyczERO changelog

This changelog lists published stable releases only.

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
