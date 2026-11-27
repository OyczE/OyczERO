# OycZERO changelog

This changelog lists numbered public releases. Prereleases are marked
explicitly; version 0002 was an internal test and was not published.

## 0011 — 2026-11-27

[Release v0011](https://github.com/OyczE/OyczERO/releases/tag/v0011)

- Updated the DATA-resident Debian runtime to `1.1.9` with the pinned Lite
  `rpicam` command stack and an `rpicam-apps` compatibility dependency for
  Store applications without pulling the full Raspberry Pi desktop stack.
- Added F4 Debian help plus F5, F6 and F7 command-line shortcuts for normal,
  administrative and application-profile Debian sessions.
- Fixed terminal restoration when leaving nested Debian Shells with `exit` or
  Ctrl+D.
- Started the accepted boot intro earlier, overlapped independent startup work,
  removed redundant launcher validation and skipped inactive optional-service
  probes. The accepted hardware candidate reached responsive MLauncher in
  approximately 25 seconds instead of 31 seconds.
- Reduced the Esc startup-cancellation window to one second while retaining
  the MLauncher-only two-second Fn+Esc managed exit.
- Preserved the immutable Buildroot core, signed A/B updates, DATA application
  model, native APPLaunch/Store `0.6.111`, HDMI modes and guarded WiFiT3 flow.

## 0010 — 2026-11-26

[Release v0010](https://github.com/OyczE/OyczERO/releases/tag/v0010)

- Added the signed optional WiFiT3 `0.7.2` package with guarded ownership and
  cleanup for supported external USB wireless adapters.
- Added HDMI Terminal font auto-fit, explicit LCD/HDMI keyboard focus controls
  and documented recovery for blank or hot-plugged legacy-fbdev displays.
- Restored the host-owned two-second Fn+Esc emergency exit for the native
  MLauncher while preserving clean console, mount and application state.
- Kept the internal `wlan0` radio protected from WiFiT3 takeover and retained
  conventional `wlan1` naming for the first external USB radio.
- Verified the complete offline installer, native APPLaunch/Store flow, a Store
  installation and launch of `2048`, signed WiFiT3 installation and a clean A/B
  update on CardputerZero hardware.

## 0009 — 2026-11-25

[Release v0009](https://github.com/OyczE/OyczERO/releases/tag/v0009)

- Added a graphical ten-step offline installer with progress, recovery SSH,
  installation audio, mute and volume controls.
- Added the DATA-resident Debian 13 application runtime `1.1.8`, official
  APPLaunch `0.6.111` and the matching Store as the default application suite.
- Runs APPLaunch as the unprivileged `pi` user and keeps applications, package
  state, home data and cache outside the immutable Buildroot core.
- Added CardputerZero camera, BMI270/BMM150 sensor, IR and Cap-Bus/GPIO access
  required by compatible Debian applications.
- Added stable `wlan0`/`wlan1` naming, `ip`, `iw`, `rfkill`, MediaTek
  `mt7921u` firmware and verified external monitor-mode capture.
- Improved boot graphics, clean reboot/poweroff handoff and DATA integrity
  checks for SD-card installation and A/B updates.

## 0008 — 2026-11-22 — prerelease

[Prerelease v0008](https://github.com/OyczE/OyczERO/releases/tag/v0008)

- Published a package-only hardware-validation build of the optional Debian
  application stack.
- Included Debian runtime `1.1.1`, upstream APPLaunch `0.6.110` and the matching
  OycZERO Store integration package.
- Deliberately omitted a full installer and signed OS update while application
  runtime validation remained in progress.

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
