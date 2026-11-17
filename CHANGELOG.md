# OyczERO changelog

## 2026-11-17 - OyczERO 0004 (stable release)

- Release [`v0004`](https://github.com/OyczE/OyczERO/releases/tag/v0004), build
  `20261117T203636Z-gba2622bd85bd`. Install on a running OyczERO system with
  `oyczero update install latest`; settings and files are kept.
- Wi-Fi monitor mode for USB adapters: `oyczero monitor list|on|channel|off|status`.
  `off` returns the adapter to normal Wi-Fi and saved networks reconnect.
- Capture tools: `tcpdump`, `airodump-ng`, `aireplay-ng`, `aircrack-ng`.
- Verified with the ALFA AWUS036AC (RTL8812AU) on 2.4 and 5 GHz; the built-in
  Wi-Fi has no monitor mode. Other adapters and frame injection are not
  verified yet. Use only on networks you own or are authorised to test.

## 2026-11-17 - OyczERO 0003 (stable release)

- Release [`v0003`](https://github.com/OyczE/OyczERO/releases/tag/v0003), build
  `20261117T201626Z-gb9874b812b35`. Install on a running OyczERO system with
  `oyczero update install latest`; settings and files are kept.
- Fixes the 0001 known issue: the occasional hang during start-up and during
  the restart into an update was caused by an SD card driver error; the system
  now recovers from it.
- USB Wi-Fi adapters: firmware for 22 chipsets; verified on hardware: ALFA
  AWUS036AXML (MT7921AU) and AWUS036AC (RTL8812AU).
- Stable Wi-Fi names (`wlan0` for the built-in radio, `wlx<MAC>` for USB
  adapters), power saving off for USB adapters, automatic reconnect of saved
  networks, and reuse of a network saved for another adapter in Setup.
- 0002 was an internal test version and was not released.

## 2026-11-16 - OyczERO 0001 (first stable release)

- Release [`v0001`](https://github.com/OyczE/OyczERO/releases/tag/v0001), build
  `20261116T222503Z-gcccb27546516`. Install on a running OyczERO system with
  `oyczero update install latest`; settings and files are kept.
- Releases are now numbered. `oyczero version` shows the number and the build.
- Update channels: `stable` (default) installs numbered releases only;
  `oyczero update channel dev` also installs development pre-releases.
- Safer updates: if the new system hangs or does not confirm a healthy start
  within 3 minutes, the device restarts into the previous system by itself;
  a failed health check restarts it at once; an update interrupted right after
  it was committed is recognised and finished on the next start.
- Known issue: in one of seven test updates the device stopped during the
  restart into the new system and needed a power cycle; it then started the
  previous system and the retry succeeded. A fix is planned for 0002.


## 2026-11-16 - Over-the-air A/B updates (development channel)

- New `oyczero update check|install latest|status`: downloads a signed update
  package from GitHub, writes the inactive system slot, restarts once to try it
  and keeps it only after a successful start. Settings and files are kept.
- Verified on hardware: local and GitHub updates in both directions, rejection
  of modified and foreign packages, automatic return after a failed trial.
- First updater build: `20261116T184024Z-gfce776c6ce74` (needs one fresh
  installation). First published package: `update-20261116T192908Z-g0eec177f2b79`
  (pre-release). Not yet covered: power loss during an update, hung-kernel
  recovery. See [Update packages](releases/README.md#update-packages-development-channel).


## 2026-11-16 - Reliable Wi-Fi and hidden networks (GREEN)

Build `20261116T173028Z-g2c142df3759d`; clean source commit `2c142df3759d`. Exact Host image
accepted on hardware (GREEN). [Release notes](releases/20261116T173028Z-g2c142df3759d/RELEASE-NOTES.md).

- Fixed Wi-Fi sometimes staying down after boot or when the cable was unplugged:
  the saved country is applied before the network manager starts, the radio is
  no longer blocked again during start-up, and start-up verifies that `wlan0`
  is up (one retry). Automatic Wi-Fi takeover passed 6/6 A-B-A cycles; the
  previous candidate failed 3/6.
- Added hidden Wi-Fi networks to Setup (`h: add a hidden network`): name plus
  hidden password, saved on `/data`, automatic reconnect; failed attempts leave
  no saved profile. Enterprise networks still need connmanctl.
- First-install restart (introduced in the previous candidate) is now part of
  committed source; no `-dirty` suffix.
- Verified: fresh install with one automatic restart, A/B layout, persistent
  install logs, automatic `wlan0`, DATA preserved across six slot switches.
- Pending: ADB image hardware test, third-party notices/corresponding sources,
  JanOS-app redistribution approval. No OTA updater or automatic rollback yet.


## Hardware follow-up: 20261116T100207Z-g5cdfe51b8172-dirty

## Additional physical acceptance: A-B-A and Wi-Fi

One-shot boot of B and normal return to A passed; DATA sentinel and network-policy
hashes were preserved. Wi-Fi association, DHCP, gateway ping and SSH over wlan0
passed. After returning to A, disabling Ethernet automatically connected saved
Wi-Fi; re-enabling Ethernet restored route preference.

**Known intermittent issue:** the first automatic Wi-Fi attempt during the B
trial failed with `connect-failed`; explicit reconnect using the saved profile
succeeded. Repeated reconnect reliability is not yet accepted. These tests do
not qualify automatic rollback, power-loss recovery or an update installer.
Both slots ran the same build. Exact ADB profile testing remains pending.

## 2026-11-16 - Clean first-install reboot accepted

Build `20261116T100207Z-g5cdfe51b8172-dirty`. Exact Host image accepted by the owner (GREEN).

- Restart after verified provisioning and preserve logs on DATA.
- Normal boot initializes Wi-Fi correctly; automatic wlan0 confirmed on hardware.
- 690 automated checks and two installer integrations passed.
- ADB profile, Wi-Fi association and slot-B boot remain separate pending tests.
- Development build provenance retained; publication/license gates still apply.


## Hardware follow-up: 20261116T084926Z-g5cdfe51b8172

### Hardware follow-up

The exact Host image booted on the device; the user accepted its appearance.
SSH inspection confirmed the logo and all installer stages in retained logs,
valid ready records, matching A/B payload hashes, writable DATA, LCD, HDMI
mirroring, Ethernet and SSH. This does not establish a boot of slot B or the
ADB profile, nor a second-boot persistence test.

**Known release blocker:** Wi-Fi has no interface on this first boot. Kernel
logs report `brcmf_fwvid_request_module: mod=cyw: failed -2` and attach failure.
Diagnosis and a verified fix are required before publication.

Changes are listed newest first. This history describes local development;
none of the entries below is a published GitHub release. Commit IDs refer to
the private development history and do not require publishing its source.
Earlier milestones are summarized from their local commit records.

## 2026-11-16 - First-install logo candidate

Build `20261116T084926Z-g5cdfe51b8172`; clean source commit `5cdfe51b8172`.

- Added the accepted OyczERO bitmap logo to the first-install display path.
- Reveal letters for 1.75 seconds, then hold the complete word for one second.
- Keep LCD/HDMI progress, terminal appearance controls and automatic rollback.
- Preserve the normal completed-card boot path and skip logo delay if headless.
- Added logo bounds/timing tests; consolidated the private implementation TODO.
- Recorded successful sanity of the preceding clean Host image separately from
  pending cold-boot acceptance of this new pair. Not a published release.

## 2026-11-16 - Compact installer and configurable HDMI candidate

Build `20261116T081953Z-g751f98f24ea4`; clean local source commit `751f98f24ea4`.
HDMI implementation commit: `258859c4853d`.

- Added compact first-install A/B provisioning and bootstrap LCD firmware access.
- Added independent HDMI terminal, selectable resolution and 16/24/32 px fonts.
- Replaced setup keyboard-routing rows with the requested appearance controls.
- Added 15-second display preview confirmation and rollback on timeout/disconnect.
- Fixed terminal cleanup after shell hangup and kept keyboard routing in CLI.
- Removed implicit inclusion of local SSH authorization seeds from standard builds.
- Prepared Host/ADB installer payloads and checksums. Nothing published.
- Remaining gates: exact-image acceptance and third-party redistribution material.

## Unreleased

### Added

- GitHub Pages content under `docs/`, configured for branch `main` / `/docs`.
  This replaces the original `webpages/` staging directory.
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

## 2026-11-15 - Clean setup release candidate

Build: `20261115T215239Z-gbbdc8f6a0c1e`. Source commit: `bbdc8f6a0c1eea52fd13d2da7d7a0111c29b2d88`.
Local clean rebuild; not published. [Release notes](releases/20261115T215239Z-gbbdc8f6a0c1e/RELEASE-NOTES.md).

Includes personal SSH setup, SSH/ADB boot profiles, keyboard settings, F1/F2/F3,
welcome IP/access status, persistent EXT/Grove power and Wi-Fi setup/boot policy.
The update architecture remains documented; these images retain the legacy
three-partition layout and are fresh installations, not OTA updates.

## 2026-11-15 - Shell shortcuts and persistent setup

Build: `20261115T205648Z-g770aba728835-dirty`. Staged locally, not published.
See [release notes](releases/20261115T205648Z-g770aba728835-dirty/RELEASE-NOTES.md).

- F1 info, F2 setup, F3 JanOS at the Bash prompt; built-in Fn+1/2/3.
- Colored welcome command hints, connected IPv4 addresses and truthful access startup.
- Saved EXT/Grove 5V preferences restored after reboot, with verified controls and rollback.
- Wi-Fi country/SSID/hidden-password workflow plus an independent Wi-Fi-at-boot toggle.
- Correct text/password terminal mode when F2 launches setup from readline.
- 637 source/image tests passed; ARM64 read-only network/SSH/setup and Bash welcome
  passed. Physical 20:11 base plus RAM modules passed menu/LCD/power/Wi-Fi and
  software Ethernet fallback checks; new-image cold boot and physical keys pending.

## 2026-11-15 — Access setup and expansion power

Build: `20261115T201146Z-g770aba728835-dirty`.
Source base: `770aba728835`, plus uncommitted development changes recorded by
the original `-dirty` build identity. Status: staged locally; not published.
See the [release notes](releases/20261115T201146Z-g770aba728835-dirty/RELEASE-NOTES.md).

### Added

- Personal SSH password setup with `oyczero ssh setup`, persistent authentication
  state on `/data`, and optional public-key authorization. Passwords accept
  1–100 UTF-8 bytes; empty passwords are rejected. No shared remote password.
- Automatic SSH in the Host image after credentials exist, automatic USB ADB in
  the ADB image, and independent persistent autostart switches. `start/stop` and
  `on/off` aliases work; stopping also cancels a pending boot start for this session.
- Keyboard `oyczero setup` with arrows or F/Z/X/C, Enter to apply, preview before
  applying, password entry and normal console restoration on exit.
- Welcome-screen `oyczero setup` hint and current SSH/ADB service states.
- Independent EXT 5V and Grove 5V setup switches with verified enable readback,
  unavailable-state reporting and shared JanOS ownership protection. Power
  applies immediately, leaves routing unchanged and defaults off at the next boot.

### Validation

- 540 source/image tests passed; 27 later-stage tests were deselected.
- Actual ARM64 read-only-root network, SSH authentication and keyboard setup
  checks passed. Both generic image payloads match their archived hashes and
  contain the tested setup/port modules without personal access credentials.
- Physical build `20261115T190142Z-g770aba728835-dirty` plus RAM modules passed
  menu/LCD checks, independent EXT/Grove enable changes and Grove Monster `pong`.
  Both outputs and the console were restored; saved settings stayed unchanged.
  The owner also confirmed the updated menu works. These are not cold-boot
  acceptance results for the newly staged image, which the owner is flashing.

### Retained limits

- Full-image flashing replaces `/data`. This package is a fresh install, not
  a data-preserving updater; the desktop/web flasher and signed OTA remain planned.
- Complete physical-key coverage, current-image access autostart and EXT-only
  electrical/peripheral acceptance remain to test. Existing third-party
  distribution checks still apply.

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
