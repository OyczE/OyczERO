# OyczERO changelog

Changes are listed newest first. This history describes local development;
none of the entries below is a published GitHub release. Commit IDs refer to
the private development history and do not require publishing its source.
Earlier milestones are summarized from their local commit records.

## Unreleased

### Added

- A distribution workspace for release material, installer packages, built
  web pages and flasher deliverables, separate from the full development source.
- A project README, this changelog and notes for the latest clean local build.
- A developer-first updater design: Tauri desktop clients for Windows, Linux
  and macOS, plus a GitHub Pages browser client sharing one device update engine.
- The OyczERO Proprietary License for original materials, credited to
  Mateusz Ziółek - LAB5 (lab5.eu.com), with third-party license exceptions and
  attribution requirements for permitted copies and forks.

### Planned, not implemented

- Signed update packages, inactive-slot installation, boot confirmation and
  qualified rollback that preserve `/data` during routine updates.
- Desktop SD installation, device updates through SSH/ADB, and backup/restore.
- Browser USB updates of a running Zero. Raw SD installation belongs to the
  native desktop client; it is not a browser SD-reader feature.

The updater design and directory structure do not provide a working installer,
website or OTA service. JanOS autostart is also deferred.

## 2026-11-15 — First development release

Build: `20261115T173713Z-g770aba728835`.
Source commit: `770aba728835` (clean source contents).
Status: staged locally for the project owner's test; not published.
See the [release notes](releases/20261115T173713Z-g770aba728835/RELEASE-NOTES.md).

### Packaged

- Host and ADB fresh-install images, 199 MiB each, with checksums, build metadata,
  the actual kernel configuration, validation results and installation guidance.
- No personal SSH authorization seed, private access keys or saved user settings.
  Owners provision their own SSH public keys after installation.
- Existing committed features from `770aba7`; no new updater or A/B migration.
  A full configuration synchronization also enabled the legacy Netfilter modules
  selected by the build, recorded in the archived kernel configuration.

### Validation

- 454 source/image tests passed; 27 later-stage tests were deselected.
- QEMU ARM64 checks passed for immutable-root networking and SSH authentication,
  SCP, reconnect, persistent host identity and occupied-port handling.
- Both staged images match their SHA-256 manifest and embedded build identity.
- Physical boot of this exact build is pending. External distribution also
  requires the checks in [Third-party notices](THIRD-PARTY-NOTICES.md).

## 2026-11-15 — Monster ports, JanOS fixes and A/B groundwork

Source commit: `770aba728835`.
Clean local build: `20261115T155005Z-g770aba728835`.
See the [build notes](releases/20261115T155005Z-g770aba728835/RELEASE-NOTES.md).

### Added

- A common `oyczero COMMAND` interface, retaining legacy helper compatibility.
- Explicit Grove/EXT power selection, bounded Monster probes, shared-UART
  ownership checks and an M status indicator based on verified communication.
- Experimental A/B image tooling with two system slots and separate data,
  plus data-layout validation that retains legacy `/data` growth support.

### Fixed

- Stale command titles after leaving the JanOS raw console.
- Conflicting port operations while another client owns the shared UART.

### Validation and limits

- The clean build passed 454 source/image tests; 27 later-stage tests were
  deselected. Archived image checksums matched, and the Host image booted on Zero.
- Earlier live acceptance covered Grove power/ping, JanOS 1.7.7 version/help,
  menu navigation, raw ping/pong and console restoration. Those checks used
  an earlier base image with temporary overrides before the clean build.
- Physical A/B boot, rollback and EXT-only peripheral communication remain
  unqualified. Full-image flashing still replaces `/data`.

## 2026-11-15 — Saved Wi-Fi selection and Ethernet fallback

Source commit: `a54a8cf`.

### Fixed

- ConnMan no longer treats every discovered Wi-Fi network as a default favorite,
  allowing saved profiles to reconnect when Ethernet disappears.
- Ethernet keeps route preference while associated Wi-Fi remains available.

### Validation

- Physical cable removal/reinsertion verified Wi-Fi fallback, Ethernet DHCP
  recovery and return of the preferred Ethernet route.
- Subsequent user acceptance confirmed automatic Wi-Fi association after reboot
  with a saved profile. This does not preserve profiles through full-image flashing.

## 2026-11-15 — CM0 WPA3 Wi-Fi, LAN diagnostics and boot audio

Source commit: `08e5b81`.

### Added and fixed

- Correct CM0 Wi-Fi NVRAM, EAP/SAE support for WPA3 and writable resolver state.
- LAN diagnostics for USB Host/peripheral conflicts and disappearing interfaces.
- ES8389 codec/amplifier integration, playback tools and bounded asynchronous
  boot sound with a persistent on/off setting.

### Validation

- 414 source/image tests passed. Staged device fixes passed WPA3, DHCP, DNS,
  HTTPS, SSH and service reconnection checks; speaker playback was user-confirmed.

## 2026-11-15 — Traceable build names and archives

Source commit: `75481f5`.

### Added

- Shared UTC timestamp/commit build IDs for Host and ADB images, including
  clean/dirty source state and `oyczero version` output.
- Named archives, file sizes and SHA-256 checksums, with protection against
  overwriting an existing build or publishing an incomplete local archive.

### Validation

- 404 host/image tests passed, including archive failure cases and ARM64 version
  reporting. Build identity does not claim byte-for-byte reproducibility.

## 2026-11-15 — USB diagnostics and persistent LCD status bar

Source commit: `dadc916`.

### Added and fixed

- Locally enabled USB-only ADB and a separate peripheral diagnostic image.
- A fixed status row for RTC, battery/charging and M/W/L/B indicators, with a
  persistent setup toggle, JanOS viewport integration and framebuffer screenshots.
- Console scrolling/color fixes and reduced terminal-to-framebuffer latency.

### Validation

- 395 host/image tests and recorded physical shell, file-transfer, scrolling,
  status-bar, JanOS and crash-recovery checks passed.
- Measured framebuffer latency improved from about 205 ms to 13 ms. This is a
  software measurement, not an optical refresh-rate or power measurement.

## 2026-11-15 — Networking, JanOS integration and on-demand SSH

Source commit: `84fea68`.

### Added and fixed

- Battery/storage/RTC welcome information, explicit Wi-Fi setup, ConnMan,
  Grove controls and the pinned native JanOS frontend.
- Persistent-state links compatible with the read-only system root.
- On-demand, key-only Dropbear SSH with persistent host identity.

### Validation

- 345 tests passed; 27 future-stage tests were deselected. ARM64 read-only
  ConnMan/SSH checks passed. Physical networking acceptance followed later.

## 2026-11-14 — OyczERO base system

Source commit: `d4ed899`.

### Added

- Buildroot ARM64 images, CardputerZero v0.5 drivers, LCD/HDMI console,
  keyboard mapping, root autologin and Bash.
- Animated OyczERO boot splash and a growing persistent `/data` partition.
- An optional Debian ARM64 development environment with `apt` and compilers.
- Read-only BQ27220 battery monitoring and RX8130 RTC clock restoration.
- Build, image, host and QEMU checks with a physical hardware acceptance checklist.

### Validation

- 240 tests passed; 42 future-stage requirements were deselected. Driver-function
  checks and ARM64 RTC boundary tests passed; this did not qualify physical battery
  measurements or RTC retention.
