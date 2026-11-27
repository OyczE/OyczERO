# OycZERO 0011

Build `20261127T201522Z-gd79a6e2fd903` from clean source commit
`d79a6e2fd903708c5b85873c39c92258b2ae2e9c`.

OycZERO 0011 keeps the Buildroot host immutable and moves applications,
package state and the Debian runtime to the persistent DATA partition.

## Highlights

- Updates the offline Debian runtime to `1.1.9`. The runtime includes
  Picamera2, the pinned Raspberry Pi OS Lite `rpicam` command stack and an
  `rpicam-apps` compatibility dependency for compatible Store packages.
- Adds F4 Debian quick help and safe F5, F6 and F7 command-line shortcuts for
  the normal Debian Shell, administrative Shell and application profile.
- Restores the main LCD terminal cleanly after leaving a nested Debian Shell
  through `exit` or Ctrl+D.
- Starts the accepted boot intro earlier, overlaps independent startup work and
  removes redundant launcher and inactive-service checks. The accepted hardware
  candidate reached responsive MLauncher in about 25 seconds.
- Reduces the Esc autostart cancellation window to one second while keeping the
  MLauncher-only two-second Fn+Esc managed exit.
- Retains native APPLaunch/Store `0.6.111-oyczero.2`, HDMI modes, signed A/B
  updates and the guarded WiFiT3 `0.7.2` package flow.

## Artifacts

- `oyczero-v0011-install.img.xz`: complete universal fresh-install/recovery
  image for Raspberry Pi Imager. It replaces the card layout and DATA.
- `oyczero-20261127T201522Z-gd79a6e2fd903-update.oyu`: signed A/B update for an
  existing OycZERO installation. It preserves DATA.
- `debian-runtime-1.1.9-arm64.oyp`: signed offline Debian application runtime.
- `applaunch_0.6.111-oyczero.2_arm64.deb` and
  `oyczero-m5market_0.6.111-oyczero.2_arm64.deb`: locked native launcher suite.
- `wifit3-0.7.2-arm64.oyp`: signed optional terminal package.

## Initial installation

Write the `.img.xz` asset with Raspberry Pi Imager through **Use custom** and
allow the graphical ten-step installation to finish. The measured complete path
to MLauncher took 11 minutes 25 seconds on the original M5Stack 32 GB card; a
slower card can take longer. Step 7 decompresses and configures the offline
runtime and is normally the longest stage. Do not remove power.

From step 7 onward, a failure screen shows temporary recovery SSH details and
the current IP address. Copy `/data/oyczero/install/` before retrying. See
[Installing and updating OycZERO](../INSTALL.md) for the complete recovery
procedure, password setup and music controls.

## Debian shortcuts

At the main OycZERO Shell prompt, F4 prints Debian help. F5, F6 and F7 fill the
corresponding command line but never execute it automatically. Review the
command and press Enter. Leave an interactive Debian Shell with `exit` or
Ctrl+D.

## Update an installed system

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

The updater verifies the signature and every payload hash, writes only the
inactive slot and commits it after a successful trial boot. A failed trial
returns to the previous slot automatically. DATA is preserved.

## Validation

- Full Stage 3 on the exact clean build: 1,595 passed, 15 later-stage
  requirements deselected.
- The complete disposable ten-step installer integration test passed.
- The exact ARM64 Debian runtime, native APPLaunch and Store artifacts passed
  runtime smoke, package transaction, interrupted-state recovery, persistence,
  upgrade and removal checks.
- XZ integrity passed and the decompressed installer SHA-256 exactly matched
  the archived raw image.
- The accepted dirty 0011 hardware candidate completed the full ten-step
  offline installation on the original M5Stack 32 GB card in 11 minutes 25
  seconds. MLauncher, Store applications, Debian package installation, htop,
  Ctrl+D restoration, F3 launcher return and reboot were exercised. The final
  clean installer differs in build identity and was verified on the host rather
  than written to a second card.
- The signed update parser verified the exact clean update signature, manifest,
  368 payload hashes and A/B layout before the hardware trial.

## Known limitations

- Full installation replaces DATA. Use the signed `.oyu` update to preserve an
  existing DATA partition.
- Step 7 is CPU- and storage-intensive. Music can briefly stutter without
  affecting installer progress.
- WiFiT3 requires a supported external USB wireless adapter. Internal `wlan0`
  is deliberately protected from takeover.
- HDMI hot-plug discovery is unavailable with the legacy framebuffer backend;
  connect and power the display before boot.
- The host BusyBox `wget` supports HTTP/FTP only. Use `curl -fL` for HTTPS.
