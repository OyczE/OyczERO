# OyczERO 0006

Build `20261118T203814Z-g69ff5e74d90f` from clean source commit
`69ff5e74d90ffeef4dcb4a316e6b1292af34f19b`.

## Highlights

- Replaces separate Host and ADB images with one universal system. The physical
  Host position exposes the internal hub and LAN; Slave automatically exposes
  owned USB ADB through USB-C2. No reboot is required when switching roles.
- Keeps SSH independent of the USB role, so LAN or saved Wi-Fi remains a rescue
  path when enabled.
- Preserves update-v1 compatibility. The 0005 updater can install this release;
  the universal BOOT profile is committed only after the new slot passes its
  signed trial health check.
- Fixes A/B slot detection when the running SquashFS appears as `/dev/root`.
- Keeps the base OS clean. JanOS-app, wifit3, airgeddon, AppLauncher, the
  M5Stack market client and a Debian runtime remain future optional DATA
  packages and are not bundled in 0006.

## Artifacts

- `oyczero-v0006-install.img.xz`: complete universal fresh-install/recovery
  image for Raspberry Pi Imager. It replaces the SD-card layout and DATA.
- `oyczero-20261118T203814Z-g69ff5e74d90f-update.oyu`: signed A/B update for an
  existing OyczERO installation. It preserves DATA and is not a disk image.

## Install or update

Write the `.img.xz` file with Raspberry Pi Imager through **Use custom**. A
fresh image replaces DATA, so back up settings and user files first.

For an existing A/B installation, copy the `.oyu` file to DATA and run:

```sh
oyczero update install /data/oyczero-20261118T203814Z-g69ff5e74d90f-update.oyu
```

## Validation

- 941 stage 0-3 tests passed; 23 later-stage requirements were deselected.
- Disposable-loop first/second installation and shipped ARM64 runtime tests
  passed for the final image payload.
- The exact final build passed ARM64/QEMU-user immutable-root, D-Bus/ConnMan,
  SSH, SCP, password/key persistence and Setup tests.
- XZ integrity, extracted installer SHA-256, Ed25519 update signature and all
  367 update payload hashes were verified.
- The exact final `.oyu` committed A-to-B on physical hardware, preserved DATA,
  the network backup and ConnMan profiles, and returned on LAN/SSH.
- On the exact final build, Host-to-Slave exposed Windows ADB with a root shell
  and `DEVICE_ACTIVE`; Slave-to-Host removed ADB and restored the internal hub,
  Ethernet carrier, `192.168.0.94` and SSH without rebooting.
- A metadata-dirty candidate from the same source passed an additional
  byte-identical physical ADB push/pull round trip before the clean rebuild.

The exact final `.img.xz` was not re-flashed after the clean metadata rebuild.
Its installer and ARM64 runtime passed the disposable-loop test harness, while
its exact final root and role lifecycle passed through the signed update on the
physical CardputerZero. QEMU user mode and loop devices use the host kernel and
do not emulate the complete CM0 board or its peripherals.
