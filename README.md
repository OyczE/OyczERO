# OycZERO

OycZERO is a custom ARM64 Linux system for CardputerZero v0.5. It combines an
immutable Buildroot core with a writable Debian application runtime stored on
the DATA partition. System updates use signed A/B slots, while settings,
credentials, applications and user files persist under `/data`.

## Downloads

Download numbered releases from
[GitHub Releases](https://github.com/OyczE/OyczERO/releases) and verify the
published SHA-256 checksum before installation.

The current stable release is
[OycZERO 0012](https://github.com/OyczE/OyczERO/releases/tag/v0012).

OycZERO 0012 provides:

- one universal Host/LAN and USB-peripheral/ADB SD-card image;
- a separate signed A/B update for existing installations;
- the offline Debian runtime `1.1.9`, official APPLaunch `0.6.111` and its
  matching Application Store on DATA;
- deterministic Raspberry Pi camera command dependencies for compatible Store
  applications;
- signed optional packages such as WiFiT3 `0.7.2`;
- graphical first installation, early animated boot intro, default MLauncher
  autostart and a one-second Esc cancellation window;
- native Debian Shell and application shortcuts on F4 through F7.
- [OycZERO Config](https://oycze.github.io/OyczERO/OycZERO-Config/) for
  assembling a customized installer locally in a modern browser;
- first-boot owner, optional user, Wi-Fi, audio, package and autostart
  provisioning without sending the selected image or entered credentials to a
  server;
- early volatile identity creation so udev assigns the correct MLauncher
  framebuffer and keyboard permissions on every cold boot.

Artifact types are intentionally separate:

- `.img.xz`: complete initial installation or recovery through Raspberry Pi
  Imager; replaces the card layout and DATA.
- `.oyu`: signed A/B operating-system update for a running OycZERO system;
  preserves DATA.
- `.oyp`: signed OycZERO package stored on DATA.
- `.deb`: native Debian component installed inside the DATA runtime; it is not
  installed directly by the Buildroot host.

See the [complete user guide](USAGE.md),
[installation instructions](releases/INSTALL.md),
[release history](CHANGELOG.md), [package catalog](packages/README.md) and
[third-party notices](THIRD-PARTY-NOTICES.md).

## Quick start

1. Write `oyczero-v0012-install.img.xz` with Raspberry Pi Imager using
   **Use custom**. A full image erases the existing card and DATA.
2. Let the graphical ten-step installer finish. Card preparation normally takes
   about ten minutes and can take longer on a slower SD card. A long step 7 is
   expected; do not remove power.
3. Set the owner password when prompted. This password enables root SSH and is
   also assigned to the Debian `pi` user for `sudo`.
4. MLauncher starts automatically. Press Esc during the one-second countdown
   to stay in OycZERO Shell for that boot.

To preconfigure a private image, open
[OycZERO Config](https://oycze.github.io/OyczERO/OycZERO-Config/), download and
select the reviewed v0012 `.img.xz`, choose the required settings and save the
generated `.img`. All assembly happens locally. Write that generated file with
Raspberry Pi Imager. It contains the entered password and Wi-Fi credentials
until the first successful boot, so keep it private and delete it after use.

From step 7 onward, the temporary installer recovery login is available; a
failure screen shows its current IP address. It uses `pi` / `pi` only for the
active continuation and is removed when installation completes.

The installer first verifies its embedded system, creates the A/B layout,
writes and reads back both immutable system slots, creates DATA and restarts.
It then decompresses the offline Debian runtime on DATA, configures its native
dependencies, installs MLauncher and Store, verifies the result and starts the
launcher. Relaxing 8-bit music plays while this work continues. Press F or Up
to raise the volume, X or Down to lower it, and M to mute or unmute playback.

## Keyboard shortcuts

Shortcuts work at the main interactive OycZERO Shell prompt. Applications keep
their own keyboard handling.

| Key | Action |
| --- | --- |
| F1 | Refresh OycZERO system information. |
| F2 | Open Setup. |
| F3 | Start, install or repair MLauncher and Store. |
| F4 | Show Debian quick help. |
| F5 | Fill the Debian `pi` Shell command. |
| F6 | Fill the Debian root Shell command. |
| F7 | Fill the root application-profile command prefix. |

F5 through F7 fill the command line but do not execute it. Review or complete
the command and press Enter. During MLauncher startup, Esc cancels autostart for
the current boot. While MLauncher is running, hold Fn+Esc for about two seconds
to return through the managed cleanup path. For any foreground application,
SSH recovery can use `oyczero app shutdown`.

## Common commands

```sh
oyczero info
oyczero setup
oyczero version
oyczero app list
oyczero app install m5launcher
oyczero dev --user pi enter
oyczero update check
oyczero update install latest
oyczero update status
```

The Buildroot host intentionally has no `apt` or `sudo`. Debian commands must
run through `oyczero dev`; see the [user guide](USAGE.md#native-debian-runtime).

## HDMI display and terminal

Connect and power the HDMI monitor before starting or rebooting CardputerZero.
The legacy framebuffer backend selects output geometry during boot and cannot
reliably discover a monitor connected later.

```sh
oyczero hdmi mirror
oyczero hdmi terminal
oyczero hdmi off
oyczero hdmi status
oyczero hdmi resolution auto
oyczero hdmi resolution 1920x1080
oyczero hdmi font 24
oyczero hdmi focus
oyczero hdmi lcd
```

Resolution and font changes use a timed confirmation. Terminal focus is
explicit: `focus` moves the Cardputer keyboard to HDMI `tty2`, while `lcd`
returns it to LCD `tty1`. Typing `exit` in the HDMI Shell also returns focus to
the LCD.

## Repository contents

This repository contains public distribution material only: release metadata,
package metadata, documentation and exported flasher deliverables. OycZERO
source code, tests, build tools, TODO files and implementation plans are not
published here.

Large images and packages are GitHub Release assets and are not stored in Git
history.
