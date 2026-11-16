# OyczERO Wi-Fi reliability and hidden networks

Build: `20261116T173028Z-g2c142df3759d` (clean source commit `2c142df3759d`;
after a later private history cleanup the identical source tree is commit
`81b2b2bbe452`).

**Host hardware acceptance: GREEN.** This status covers the tested installation,
Wi-Fi and A/B checks below, not all planned features or redistribution clearance.

## Changes since 20261116T100207Z-g5cdfe51b8172-dirty

- **Reliable Wi-Fi after boot and on cable loss.** The saved country is applied
  while the radio is still blocked, before the network manager starts. Wi-Fi is
  then switched on once instead of being blocked and unblocked again, which
  previously left `wlan0` down. Wi-Fi start-up also confirms that the interface
  is actually up and retries once when it is not.
- **Hidden Wi-Fi networks in Setup.** Setup > Wi-Fi setup now offers
  `h: add a hidden network`: enter the network name and the password (hidden
  input; press Enter for an open network). The network is saved on `/data` and
  reconnects automatically. A failed or unreachable network leaves no saved
  profile. WPA-Enterprise networks are not supported in Setup.
- **Clean build provenance.** The first-install restart from the previous
  candidate is now committed; this build carries no `-dirty` suffix.

## Verified on hardware (exact Host image)

- Fresh SD installation: logo, five stages, one automatic restart, normal login.
- Layout: BOOT 256 MiB, system A 1 GiB, system B 1 GiB, DATA uses the rest.
  Installation logs are kept on DATA; system root is read-only.
- `wlan0` appears automatically; no manual driver reload.
- Hidden home network joined from Setup and reconnected after every reboot.
- **6/6 A-B-A cycles** (B, A, B, A, B, A): correct slot each time, DATA preserved,
  automatic Wi-Fi takeover with Ethernet disabled (gateway reachable over Wi-Fi),
  Ethernet restored as the preferred route. The previous candidate failed the
  Wi-Fi takeover in 3 of 6 cycles.

## Automated checks

- Stage-3 source and image suite passed, including new Wi-Fi start-up and
  hidden-network regression tests.
- System root hashes match both installer manifests; packaged root contains both
  changes; no private keys or authorization seeds in the image.
- Compressed package checksums and `xz -t` integrity verified.

## Remaining limits

- Exact ADB image hardware test is pending; Host is the accepted profile.
- Hidden network wrong-password cleanup is covered by tests, not yet on hardware.
- Booting slot B used a one-shot test helper; there is no updater, automatic
  rollback or power-loss recovery yet. Both slots contain the same build.
- HDMI-attached installation, power/battery behaviour and Bluetooth are not part
  of this acceptance.
- Third-party notices/corresponding sources and JanOS-app redistribution
  approval remain publication gates.

## Install

Choose `install-host.img.xz` for Ethernet/SSH or `install-adb.img.xz` for USB
ADB. Write it with Raspberry Pi Imager ("Use custom"). **Fresh flashing erases
all data on the card.** Allow the automatic restart after the five stages, then
run `oyczero setup` for country, Wi-Fi and SSH. No shared password is included.
A new SSH host key is generated on every fresh installation.

These are fresh-install images, not data-preserving update packages.
