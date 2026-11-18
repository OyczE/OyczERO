# OyczERO 0005

Build `20261118T140549Z-g71a33183923e` from clean source commit
`71a33183923ea1df6a31c26eda5d29a02bb62990`.

## Highlights

- Restores complete Raspberry Pi Imager fresh-install images for both the
  Host/SSH and USB-peripheral/ADB boot profiles.
- Keeps routine upgrades separate as a signed, DATA-preserving A/B `.oyu`
  package with a one-shot trial boot, health confirmation and rollback state.
- Ships a clean base OS without JanOS-app or optional applications. Application
  packaging starts in 0006; wifit3, airgeddon, JanOS-app, AppLauncher and the
  M5Stack market remain future optional DATA packages.
- Adds guarded ADB cable-reconnect recovery while preserving explicit manual
  stop and persistent autostart policy.
- Fixes ADB-launched updates by moving service shutdown and the trial restart to
  a detached worker, so stopping `adbd` cannot kill the updater before tryboot.
- Corrects saved ConnMan credential reuse for escaped SSIDs and passphrases,
  including spaces and shell-significant characters.
- Includes the reviewed Buildroot legal-info/source bundle and the separate
  Bootlin external-toolchain source/license supplement.

## Artifacts

- `oyczero-v0005-install-host.img.xz`: destructive fresh installation with the
  USB Host/SSH access profile.
- `oyczero-v0005-install-adb.img.xz`: destructive fresh installation with the
  USB-peripheral/ADB access profile.
- `oyczero-20261118T140549Z-g71a33183923e-update.oyu`: signed A/B update for an
  existing installation; preserves DATA and is not a disk image.
- `oyczero-v0005-third-party-sources.tar.xz`: Buildroot legal-info, exact
  Buildroot source, component sources, patches and licenses.
- `oyczero-v0005-bootlin-toolchain-sources.tar.xz`: external toolchain sources,
  patches, licenses and build metadata.

## Install or update

Write either `.img.xz` file with Raspberry Pi Imager through **Use custom**. A
fresh image replaces DATA, so back up settings and user files first.

For an existing A/B installation, copy the canonical `.oyu` file to DATA and
run:

```sh
oyczero update install /data/oyczero-20261118T140549Z-g71a33183923e-update.oyu
```

## Validation

- 919 stage 0-3 tests passed; 23 later-stage requirements were deselected.
- Disposable-loop first/second install and shipped ARM64 runtime tests passed.
- ARM64 read-only root, SSH and Setup tests passed.
- Windows ADB command, interactive shell, binary push/pull and emulated
  reconnect tests passed.
- The exact signed `.oyu` committed on physical hardware, preserved DATA and
  restored ADB after the trial boot.
- Two physical cable reconnects created working replacement daemon generations;
  explicit `ADB off` survived another reconnect and explicit start restored it.
- All release hashes, compressed/extracted installer hashes, 367 update payload
  hashes and 122 Bootlin manifest hashes were verified.

The preceding clean v0005 Host and ADB candidates passed physical fresh-install
acceptance. The final installer bootstrap is unchanged and its exact artifacts
passed disposable-loop and ARM64 runtime tests; the final root was physically
accepted through the exact signed update. The final `.img.xz` files were not
re-flashed after the updater-only source correction. QEMU user mode and loop
devices do not emulate the complete CM0 board or its peripherals. The project
owner accepted this split as the final release gate: full installers in the
disposable-loop/ARM64 harness and the exact final update plus ADB lifecycle on
the physical CardputerZero.
