# OyczERO 0007

Build `20261119T094552Z-gaf19aa709bd6` from clean source commit
`af19aa709bd6b3409a784a1dc78cb2b4ad3c8de7`.

## Highlights

- Adds signed optional application packages while keeping the immutable base OS
  application-free. Package payloads, private libraries, configuration, home
  data and cache remain on DATA and survive A/B operating-system updates.
- Adds `oyczero app` install, list, status, run, remove and autostart commands.
  F3 installs or opens M5Launcher, and Setup selects the startup target. Shell
  remains the default.
- Publishes the first optional package: the official unmodified ARM64 M5Stack
  APPLaunch `0.6.110`, with pinned runtime libraries and license notices.
- Shows a two-second startup countdown. Esc keeps Shell for the current boot.
  While M5Launcher is running, holding Fn+Esc for about two seconds returns to
  a clean Shell.
- Gives foreground applications exclusive console ownership and stores their
  diagnostics in DATA instead of drawing logs or typed shell input over the GUI.

## Artifacts

- `oyczero-v0007-install.img.xz`: complete universal fresh-install/recovery
  image for Raspberry Pi Imager. It replaces the SD-card layout and DATA.
- `oyczero-20261119T094552Z-gaf19aa709bd6-update.oyu`: signed A/B update for an
  existing OyczERO installation. It preserves DATA.
- `m5launcher-0.6.110-arm64.oyp`: signed optional M5Launcher package for
  CardputerZero v0.5 running OyczERO 0007 or newer.

## Install or update

Write the `.img.xz` file with Raspberry Pi Imager through **Use custom**. A
fresh image replaces DATA, so back up settings and user files first.

For an existing A/B installation, copy the `.oyu` file to DATA and run:

```sh
oyczero update install /data/oyczero-20261119T094552Z-gaf19aa709bd6-update.oyu
```

Install M5Launcher from the pinned release asset:

```sh
oyczero app install m5launcher
```

F3 performs the same installation when the package is absent and opens it when
installed.

## Validation

- 978 stage 0-3 tests passed; 23 later-stage requirements were deselected.
- The exact installer passed XZ/extracted-hash checks and a disposable 4-GB
  first/second-install test. The delivered ARM64 BusyBox and Python bootstrap
  ran through QEMU user mode.
- The update signature and all 367 payload hashes were verified. The exact
  `.oyu` committed from slot A to B on physical hardware and preserved DATA and
  the installed M5Launcher package.
- Three package builds were byte-identical. The production parser verified the
  package signature and every payload member.
- On the final physical system, M5Launcher rendering and keyboard input passed;
  Fn+Esc returned status 0, removed the child and temporary mounts, restored
  the console and kept Shell as the default startup target.

The exact final `.img.xz` was not written to a physical card. Its installer and
ARM64 runtime passed the disposable-loop test harness, while its exact root was
accepted through the signed physical update. QEMU user mode and loop devices
use the host kernel and do not emulate the complete CM0 board or peripherals.

## Optional-package limitations

The upstream APPLaunch AppStore can display its catalog, but OyczERO 0007 does
not yet provide the planned Debian runtime, `apt`, `dpkg`, systemd or a market
compatibility adapter. Installing stock market `.deb` applications is therefore
not supported. Bluetooth-dependent launcher functions also remain unavailable
because BlueZ is not part of the base OS.
