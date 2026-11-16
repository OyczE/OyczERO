# OyczERO clean first-install reboot

Build: `20261116T100207Z-g5cdfe51b8172-dirty`.

**Host hardware acceptance: GREEN, accepted by the owner.** This status covers
the tested installation/normal boot and hardware sanity below, not all planned
features or redistribution clearance. No public release has been published.

## Changes

- After successful A/B provisioning, display `Installation complete - restarting`.
- Preserve installation logs on DATA, sync, unmount the runtime and reboot.
- On the next boot, skip installation and start system A with a fresh kernel.
- Fix first-install Wi-Fi initialization: early installer driver state no longer
  carries into the normal OS. BCM43439 firmware and vendor module load normally.
- Keep the accepted logo, progress display and HDMI setup controls unchanged.

## Verified

- 690 automated stage-3 checks passed; 27 later-stage checks deselected.
- Two disposable-loop/ARM64 installer integrations passed.
- Both packaged profiles contain the expected bootstrap, installer and applets.
- Exact Host image: owner accepted boot appearance; normal completed-card boot,
  retained installation logs, ready records and both A/B payload hashes verified.
- Root A read-only, DATA writable, LCD, Ethernet and SSH confirmed.
- wlan0 appeared automatically without manual module reload; ConnMan detects it.
- Compressed package hashes and decompression readback verified.

## Remaining limits

- Initial inspection had Wi-Fi powered off; subsequent Wi-Fi results and the
  intermittent reconnect finding are recorded below.
- Exact ADB image hardware test and automatic rollback remain pending.
- The splash may appear later with underlying console content briefly visible;
  the owner accepted this appearance and requested no further change.
- Source was uncommitted at build time (`dirty`). Preserve this exact build ID;
  a later source commit does not turn these tested bytes into a clean build.
- Third-party notices/corresponding sources and JanOS-app redistribution approval
  remain publication gates. Native/web updaters and signed OTA are not implemented.

## Install

Select Host for Ethernet/SSH or ADB for USB access. Write the `.img.xz` using
Raspberry Pi Imager. The 257 MiB raw installer provisions BOOT, 1 GiB system A,
1 GiB system B and DATA using the remaining space. **Fresh flashing erases DATA.**
Allow the automatic restart after the five installation stages. Configure access
with `oyczero setup` / `oyczero ssh setup`; no shared password is included.

These are fresh-install images, not DATA-preserving update packages.

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
