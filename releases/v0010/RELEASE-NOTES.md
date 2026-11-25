# OycZERO 0010 dirty pre-release

Build `20261125T215516Z-g2963de15d72b-dirty` from commit
`2963de15d72bbdc390c6f50089def15b7f1f274c` plus reviewed local changes.

This is a public development pre-release for hardware acceptance. It does not
replace stable OycZERO 0009 and is not marked latest.

## Highlights

- Adds the signed optional wifit3 `0.7.2` package for external USB wireless
  adapters. The host broker validates interface ownership, moves an eligible
  adapter into monitor mode, restores managed mode on exit and keeps runtime
  state on DATA.
- Adds HDMI auto-fit behavior, explicit LCD/HDMI terminal focus controls and
  public recovery instructions for blank or hot-plugged legacy-fbdev displays.
- Makes the two-second Fn+Esc launcher exit use the host-owned cleanup path so
  APPLaunch returns to a clean local Shell.
- Keeps the OycZERO core immutable while the Debian runtime, MLauncher, Store
  and optional applications remain on DATA.

## Artifacts

- `oyczero-v0010-pre-install.img.xz`: complete development fresh-install image
  for Raspberry Pi Imager. It replaces the card layout and DATA.
- `oyczero-20261125T215516Z-g2963de15d72b-dirty-update.oyu`: signed A/B update
  for an existing OycZERO installation. It preserves DATA.
- `wifit3-0.7.2-arm64.oyp`: signed optional CardputerZero application package.

## Install the development update

Enable the development channel and install the newest published candidate:

```sh
oyczero update channel dev
oyczero update install latest
```

The direct local-file form is:

```sh
oyczero update install /data/oyczero-20261125T215516Z-g2963de15d72b-dirty-update.oyu
```

## Install wifit3

Download the signed package on another computer, copy it to DATA and install it
through the OycZERO package manager. For example, from PowerShell:

```powershell
scp -O .\wifit3-0.7.2-arm64.oyp root@DEVICE_IP:/data/
ssh root@DEVICE_IP
```

Then run on OycZERO:

```sh
oyczero app install /data/wifit3-0.7.2-arm64.oyp
```

Run it from the local Shell with an external USB wireless adapter:

```sh
oyczero wifit3
```

Only audit networks and equipment that you own or are explicitly authorized to
test.

## Current validation

- Full host Stage 3: 1,553 passed, 15 later-stage requirements deselected.
- The exact compressed installer passed XZ CRC and extracted-SHA-256 checks.
- The device parsers accepted the update signature, all 368 update payload
  hashes, the wifit3 signature and all application payload hashes.
- The exact public `.oyu` downloaded through the development channel, committed
  from slot A to B and preserved the sampled DATA configuration.
- The exact public wifit3 asset installed through `oyczero app install`,
  registered version `0.7.2`, passed its signed ARM64 smoke mode and rejected
  handing the internal `wlan0` radio to the application.

The exact compressed installer has not been written to a physical card.

## Known limitations

- This candidate intentionally reports `dirty: true` and is not eligible to
  become a stable release.
- wifit3 requires a supported external USB wireless adapter. The internal
  managed interface is protected from automatic takeover.
- HDMI hot-plug detection is unavailable with the legacy framebuffer backend;
  connect and power the display before boot.
