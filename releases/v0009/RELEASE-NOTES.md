# OycZERO 0009

Build `20261125T140614Z-g2963de15d72b` from clean source commit
`2963de15d72bbdc390c6f50089def15b7f1f274c`.

## Highlights

- Adds a coherent graphical ten-step offline installer with progress, recovery
  SSH, looping installation audio, mute and volume controls.
- Installs the default application suite entirely on DATA: signed Debian 13
  runtime `1.1.8`, official APPLaunch `0.6.111`, matching Store and the OycZERO
  launcher adapter. MLauncher starts automatically and runs as unprivileged
  user `pi`; Esc keeps Shell during startup and Fn+Esc returns to Shell.
- Keeps Buildroot as the immutable system core while Debian applications,
  package state, home data and cache remain writable and persistent on DATA.
- Adds camera support for IMX219, BMI270/BMM150 sensor access, IR access and a
  constrained CardputerZero Cap-Bus/GPIO application profile.
- Adds `ip`, `iw` and `rfkill` to the application runtime, stable internal
  `wlan0` and external `wlan1` names, plus MediaTek `mt7921u` firmware for ALFA
  AWUS036AXML-class adapters.
- Improves boot graphics, prompt timing, launcher recovery and clean
  reboot/poweroff handoff without exposing application diagnostics on the
  console.

## Artifacts

- `oyczero-v0009-install.img.xz`: complete universal fresh-install/recovery
  image for Raspberry Pi Imager. It replaces the SD-card layout and DATA.
- `oyczero-20261125T140614Z-g2963de15d72b-update.oyu`: signed A/B update for an
  existing OycZERO installation. It preserves DATA.
- `debian-runtime-1.1.8-arm64.oyp`: signed DATA-resident Debian application
  runtime.
- `applaunch_0.6.111-oyczero.2_arm64.deb`: native official APPLaunch payload
  and OycZERO integration metadata for the runtime.
- `oyczero-m5market_0.6.111-oyczero.2_arm64.deb`: matching native Store package.

## Install or update

Write the `.img.xz` file with Raspberry Pi Imager through **Use custom**. A
fresh image replaces DATA, so back up settings and user files first.

For an existing A/B installation, copy the `.oyu` file to DATA and run:

```sh
oyczero update install /data/oyczero-20261125T140614Z-g2963de15d72b-update.oyu
```

F3 installs or repairs the exact default suite when it is absent and opens
MLauncher when it is ready. The equivalent command is:

```sh
oyczero app install m5launcher
```

## Validation

- 1,546 tests passed from the exact clean release commit. The read-only-system
  harness also passed immutable-root, DATA, network, SSH, password and recovery
  checks.
- The exact installer passed XZ and extracted-hash verification and completed
  its full offline ten-step disposable-loop timeline in 343.32 seconds.
- The update signature and all 368 payload hashes were verified. The exact
  `.oyu` committed from slot A to B on physical hardware and preserved every
  sampled DATA hash, including network, SSH, runtime and launcher state.
- After a controlled normal reboot, Debian runtime `1.1.8`, APPLaunch/Store
  `0.6.111` and MLauncher autostart were active as user `pi`.
- Internal Wi-Fi remained `wlan0`, an ALFA adapter remained `wlan1`, both were
  unblocked, and `oyczero monitor` captured 802.11 frames before restoring the
  external adapter to managed mode.

The exact final `.img.xz` was not written to a physical card. Its exact root
was accepted through the signed physical update, while the complete image and
installer ran through the offline host harness. QEMU user mode and loop devices
use the host kernel and do not emulate the complete CM0 board or peripherals.

## Known limitations

- Bluetooth remains disabled in this release.
- Bruce currently selects `wlan0` in its upstream interface. External `wlan1`
  monitor mode is available through `oyczero monitor` and ordinary Linux tools.
- One warm trial boot showed a transient Broadcom SDIO firmware-download error.
  Reloading the driver recovered it, and the following controlled normal reboot
  initialized both wireless adapters without the error.
