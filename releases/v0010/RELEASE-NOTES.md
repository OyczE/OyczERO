# OycZERO 0010

Build `20261126T192918Z-gaa154dd9fbab` from clean source commit
`aa154dd9fbab603bdf1900f3891e2ccc637ddaf3`.

OycZERO 0010 keeps the Buildroot core immutable while the Debian runtime,
MLauncher, Store and optional applications remain on DATA.

## Highlights

- Adds the signed optional WiFiT3 `0.7.2` package for supported external USB
  wireless adapters. The host broker validates ownership, protects internal
  `wlan0`, hands one eligible adapter to the application and restores managed
  mode and runtime state on exit.
- Adds HDMI Terminal font auto-fit, explicit LCD/HDMI keyboard focus controls
  and recovery instructions for blank or hot-plugged legacy-fbdev displays.
- Restores the two-second Fn+Esc emergency exit for native MLauncher through
  the host-owned cleanup path.
- Retains the offline Debian runtime `1.1.8`, native APPLaunch/Store
  `0.6.111-oyczero.2`, conventional `wlan0`/`wlan1` names, PIO SD-card path,
  camera, sensor, IR and Cap-Bus application access from OycZERO 0009.

## Artifacts

- `oyczero-v0010-install.img.xz`: complete universal fresh-install/recovery
  image for Raspberry Pi Imager. It replaces the card layout and DATA.
- `oyczero-20261126T192918Z-gaa154dd9fbab-update.oyu`: signed A/B update for an
  existing OycZERO installation. It preserves DATA.
- `debian-runtime-1.1.8-arm64.oyp`: signed Debian application runtime.
- `applaunch_0.6.111-oyczero.2_arm64.deb` and
  `oyczero-m5market_0.6.111-oyczero.2_arm64.deb`: locked native launcher suite.
- `wifit3-0.7.2-arm64.oyp`: signed optional terminal package.

## Update an installed system

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

The updater verifies the signature and every payload hash, writes only the
inactive slot and commits it after a successful trial boot. A failed trial
returns to the previous slot automatically.

## Install WiFiT3

Download `wifit3-0.7.2-arm64.oyp` on another computer, copy it to DATA and
install it through the OycZERO package manager:

```powershell
scp -O .\wifit3-0.7.2-arm64.oyp root@DEVICE_IP:/data/
```

```sh
oyczero app install /data/wifit3-0.7.2-arm64.oyp
oyczero wifit3
```

WiFiT3 requires a supported external USB wireless adapter. The internal
managed `wlan0` interface is deliberately protected from takeover. Only audit
networks and equipment that you own or are explicitly authorized to test.

## Validation

- Full Stage 3 on the exact clean build: 1,553 passed, 15 later-stage
  requirements deselected.
- XZ integrity passed and the decompressed installer SHA-256 exactly matched
  the archived raw image.
- The exact clean signed update verified all 368 payloads, committed from slot
  A to B on CardputerZero and preserved SSH, MLauncher/Store, WiFiT3 and the
  Store-installed `2048` application.
- The immediately preceding public 0010 prerelease completed the full offline
  ten-step fresh installation on a physical 32 GB card in about ten minutes.
  Both slots contained the selected build, DATA was clean, MLauncher/Store ran
  as `pi`, and no MMC, ext4 or SquashFS error was observed. The final clean
  installer differs in build identity and was verified on the host rather than
  written to a second card.
- On the fresh installation, Store downloaded, installed and launched `2048`.
  The exact signed WiFiT3 package installed, passed its ARM64 smoke mode,
  rejected internal `wlan0` and survived the clean A/B update.
- After the clean update, MLauncher autostarted as `pi`, SSH returned, HDMI
  Terminal was ready, internal `wlan0` was managed and unblocked, and the SD
  driver reported `DMA disabled`.

## Known limitations

- WiFiT3 requires a supported external USB wireless adapter. The final signed
  package was accepted without an attached adapter; earlier controlled hardware
  testing qualified MT7921AU handoff and recovery.
- Simultaneous large LAN transfers while MT7921AU shares the internal USB hub
  remain under investigation. Release the external adapter during large
  downloads.
- The host BusyBox `wget` supports HTTP/FTP only. Use `curl -fL` for HTTPS.
- HDMI hot-plug detection is unavailable with the legacy framebuffer backend;
  connect and power the display before boot.
