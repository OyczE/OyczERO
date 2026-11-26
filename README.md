# OycZERO

OycZERO is a custom ARM64 Linux system for CardputerZero v0.5. The system
partition is read-only, while settings, credentials and user files persist on
`/data`.

## Downloads

Use the assets attached to the numbered
[GitHub Releases](https://github.com/OyczE/OyczERO/releases). Verify the
published SHA-256 checksum before installation.

The current stable release is [OycZERO 0010](https://github.com/OyczE/OyczERO/releases/tag/v0010).
It provides one universal Host/LAN and USB-peripheral/ADB SD-card image plus a
separate signed update for an already installed OycZERO A/B system. Its
offline default suite installs the Debian application runtime, official
APPLaunch `0.6.111` and Store on DATA while the Buildroot core remains
read-only. WiFiT3 `0.7.2` is available as a separate signed optional package
for supported external USB wireless adapters.

Artifact types are intentionally separate:

- `.img.xz`: complete initial installation or recovery through Raspberry Pi
  Imager; replaces the card layout and DATA.
- `.oyu`: signed A/B operating-system update for a running OycZERO system;
  preserves DATA.
- `.oyp`: signed OycZERO package stored on DATA.
- `.deb`: native Debian application component installed inside the DATA runtime;
  it is not installed directly by the Buildroot host.

See [installation instructions](releases/INSTALL.md), the
[release layout](releases/README.md), the [changelog](CHANGELOG.md) and
[third-party notices](THIRD-PARTY-NOTICES.md).

## HDMI display and terminal (0010 and later)

Connect and power the HDMI monitor before starting or rebooting CardputerZero.
The legacy framebuffer backend selects its output geometry during boot and
cannot reliably detect a monitor connected later. If the display stays blank
after a hot-plug, leave it connected and reboot OycZERO.

Run `oyczero setup` from the local Shell and select one of these HDMI modes:

- **Off** disables the HDMI service.
- **Mirror LCD** scales the CardputerZero LCD framebuffer to HDMI.
- **Terminal** renders an independent Shell on `tty2`; the LCD Shell remains on
  `tty1`.

The equivalent command-line controls are:

```sh
oyczero hdmi mirror
oyczero hdmi terminal
oyczero hdmi off
oyczero hdmi status
oyczero hdmi resolution auto
oyczero hdmi resolution 1920x1080
oyczero hdmi font 24
```

Resolution and font changes show a timed preview and are saved only after
confirmation. Supported resolutions are `auto`, `1280x720` and `1920x1080`;
supported terminal font preferences are `16`, `24` and `32` px. If the active
framebuffer is too small for the saved preference, Terminal uses the largest
smaller supported font without overwriting the preference. `oyczero hdmi
status` reports both the saved and active font sizes.

Terminal keyboard focus is explicit:

```sh
oyczero hdmi focus  # move the Cardputer keyboard to the HDMI tty2
oyczero hdmi lcd    # return the keyboard to the LCD tty1
```

Typing `exit` inside the HDMI Shell also closes that Shell and returns focus to
the LCD. Return to the LCD before changing HDMI mode from the local Terminal.
SSH remains available as the recovery path; use `oyczero hdmi status`,
`oyczero hdmi lcd` and `/run/oyczero-hdmi.log` to diagnose a blank or failed
session.

## Repository contents

This repository contains public distribution material only: release metadata,
package metadata, built web content and exported flasher deliverables. OycZERO
source code, tests, build tools, TODO files and implementation plans are not
published here.

Large images and packages are GitHub Release assets and are not stored in Git
history.
