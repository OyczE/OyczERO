# OycZERO user guide

This guide describes OycZERO 0011 on CardputerZero v0.5.

## System model

OycZERO boots a read-only Buildroot system. Persistent configuration,
credentials, application packages, the Debian runtime, Store state and user
files live on the writable DATA partition at `/data`.

The Debian runtime is a namespaced ARM64 environment sharing the OycZERO kernel
and network. It is not a virtual machine. The Buildroot host remains in control
of boot, updates, display ownership, application cleanup and hardware policy.

## Initial installation

Write the numbered `.img.xz` release image with Raspberry Pi Imager through
**Use custom**. Full-image installation replaces the partition table and erases
the existing DATA partition.

The graphical installer uses ten stages:

1. Starting installer
2. Preparing SD card
3. Writing system A
4. Writing system B
5. Preparing user storage
6. Verifying system
7. Preparing Debian runtime
8. Installing M5Launcher
9. Installing Application Store
10. Finalizing OycZERO

Allow about ten minutes for the provisioning stages and longer for a slow SD
card. In 0011 acceptance testing, the complete path from first power-on to a
responsive MLauncher took 11 minutes 25 seconds on the original M5Stack 32 GB
card. Step 7 is normally the longest visible stage. Continued progress messages
and music mean the installer is still working; do not remove power.

Steps 1 through 6 verify the embedded SquashFS payload, create the four-partition
BOOT/A/B/DATA layout, write and read back both immutable system slots, create
and check DATA, then restart into the installed system. Steps 7 through 10
decompress the offline Debian runtime onto DATA, configure its native package
dependencies, install MLauncher and Store, verify their registration and select
MLauncher as the initial autostart target. This work is performed locally and
does not require Internet access.

Relaxing 8-bit music plays independently while installation work continues; the
installer never waits for a track to finish. The bottom line shows the controls:

- F or Up increases installation volume;
- X or Down decreases installation volume;
- M mutes or unmutes playback without restarting the track.

From step 7 onward, temporary recovery SSH uses user `pi`, password `pi`, TCP
port 22. If installation fails, the screen shows the current LAN or Wi-Fi
address when one is available. This temporary account is scoped to the active
step-7 continuation and is removed after successful installation.

For a step-7-or-later failure, keep power connected, record the displayed error
and connect with `ssh pi@DEVICE_IP`. Inspect `/data/oyczero/install/` and copy it
to Windows before retrying:

```powershell
scp -O -r pi@DEVICE_IP:/data/oyczero/install .\oyczero-install-recovery
```

A one-time transient failure can be retried with `su -`, followed by `sync` and
`reboot`; the validated continuation resumes automatically. Do not manually
delete the continuation, package registry or Debian runtime. If the same error
repeats, preserve the logs and write a newly verified full image. Recovery SSH
does not exist before step 7; record an earlier console error and reflash rather
than repeatedly interrupting card writes.

On the first normal boot, OycZERO requires an owner password before starting
MLauncher. The same password enables root SSH and the Debian `pi` account for
`sudo`. Passwords may contain one to 100 bytes except line breaks; OycZERO does
not require a complexity policy and stores only password hashes.

## Normal boot and application ownership

The early firmware stage keeps the LCD black until Linux can start the OycZERO
intro. Network and application checks continue while the accepted animation and
sound play. MLauncher is the default startup target.

OycZERO prints:

```text
Starting m5launcher in 1 second. Press Esc to stay in Shell.
```

Press Esc to keep Shell for that boot. The saved autostart target is unchanged.
F3 starts or repairs MLauncher later. While MLauncher is running, holding
Fn+Esc for about two seconds requests a clean exit. This chord is intentionally
limited to MLauncher. Use the following command over SSH to stop any managed
foreground application:

```sh
oyczero app shutdown
```

## Shell shortcuts

These shortcuts belong to interactive Bash on the main LCD Shell. They do not
override keys inside Setup, MLauncher, Store, Debian Shell or another
application.

| Key | Result |
| --- | --- |
| F1 | Run `oyczero info`. |
| F2 | Run `oyczero setup`. |
| F3 | Start, install or repair the native launcher suite. |
| F4 | Print Debian quick help. |
| F5 | Fill `oyczero dev --user pi enter`. |
| F6 | Fill `oyczero dev --user root enter`. |
| F7 | Fill `oyczero dev --profile application --user root run `. |

F5 through F7 refuse to overwrite a non-empty command line and never execute
automatically. Press Enter after reviewing or completing the command. Leave a
Debian Shell with `exit` or Ctrl+D on an empty prompt.

## Setup

Open Setup with F2 or:

```sh
oyczero setup
```

Use the arrow keys or F/Z/X/C for up/left/down/right. Enter applies the current
choice; Escape or Q exits. Setup controls the owner password, SSH and ADB
autostart, Wi-Fi, HDMI, MLauncher startup, status bar and persistent Grove/Cap
port power choices.

## Command reference

Run `oyczero` or `oyczero help` for built-in help.

| Purpose | Commands |
| --- | --- |
| System information | `oyczero info`, `oyczero version`, `oyczero version --json` |
| Settings | `oyczero setup` |
| Wi-Fi | `oyczero wifi on`, `off`, `setup`; `oyczero country` |
| Network diagnostics | `oyczero net status`, `oyczero net prepare` |
| Ethernet | `oyczero lan on`, `off`, `status` |
| Bluetooth radio | `oyczero bluetooth on`, `off` |
| USB Wi-Fi monitor mode | `oyczero monitor list`, `status`, `on [--channel N]`, `channel N`, `off` |
| WiFiT3 | `oyczero wifit3 [wlanN] [--force]` |
| SSH | `oyczero ssh setup`, `on`, `off`, `status`, `authorize KEY_FILE` |
| SSH at boot | `oyczero ssh autostart on`, `off`, `status` |
| USB ADB | `oyczero adb start`, `stop`, `status` |
| ADB at boot | `oyczero adb autostart on`, `off`, `status` |
| Physical USB role | `oyczero usb-role auto`, `host`, `adb`, `status` |
| USB serial/network gadget | `oyczero usb start`, `stop`, `status` |
| Battery and RTC | `oyczero battery`; `oyczero rtc read`, `restore`, `save` |
| DATA | `oyczero data status` |
| Applications | `oyczero app list`, `status ID`, `install SOURCE`, `run ID`, `remove ID`, `autostart [TARGET]`, `shutdown` |
| Debian runtime | `oyczero dev status`, `enter`, `run COMMAND...`, `help` with optional `--profile` and `--user` |
| Display status bar | `oyczero status-bar on`, `off`, `status` |
| HDMI | `oyczero hdmi off`, `mirror`, `terminal`, `status`, `focus`, `lcd` |
| HDMI geometry | `oyczero hdmi resolution auto\|1280x720\|1920x1080`; `oyczero hdmi font 16\|24\|32` |
| Sound | `oyczero sound on`, `off`, `play`, `status` |
| Screenshot | `oyczero screenshot /data/screen.png` |
| System update | `oyczero update status`, `check`, `install FILE.oyu\|latest`, `channel [stable\|dev]` |
| Port status | `oyczero ports status` |
| Grove | `oyczero ports grove uart`, `i2c`, `power on\|off` |
| Cap/EXT | `oyczero ports cap gpio`, `usb`, `power on\|off` |
| Monster | `oyczero monster on`, `off`, `ping`, `status [--port ext\|grove]` |

`oyczero update install` accepts `--allow-downgrade` for deliberate recovery
only. Do not use it for routine updates.

## Applications and Application Store

List and inspect signed OycZERO packages:

```sh
oyczero app list
oyczero app status m5launcher
```

Install a catalog package or a reviewed local `.oyp`:

```sh
oyczero app install m5launcher
oyczero app install /data/wifit3-0.7.2-arm64.oyp
```

Run a terminal package with arguments after `--`:

```sh
oyczero app run wifit3 -- wlan1
```

Set Shell or an installed application as the startup target:

```sh
oyczero app autostart shell
oyczero app autostart m5launcher
oyczero app autostart
```

Removing an application preserves its persistent state unless its package
supports and the user explicitly selects a guarded purge:

```sh
oyczero app remove PACKAGE_ID
oyczero app remove PACKAGE_ID --purge
```

MLauncher and Store run as unprivileged Debian user `pi`. Store applications
are ordinary Debian packages installed through the locked runtime repositories
and package policy. A package that omits required Debian dependencies can still
fail even when Store itself is healthy; inspect its package metadata before
changing the base runtime.

## Native Debian runtime

The Buildroot host has no `apt` or `sudo`. Open Debian as the normal user:

```sh
oyczero dev --user pi enter
```

Open an administrative Debian Shell:

```sh
oyczero dev --user root enter
```

Install a package from the pinned Debian repositories:

```sh
oyczero dev --user root run apt install -y htop
```

For a reviewed local `.deb`, download it to DATA with host `curl`, copy it into
the Debian root and install it there:

```sh
cd /data
curl -fL --retry 3 -O https://example.invalid/PACKAGE_arm64.deb
cp /data/PACKAGE_arm64.deb \
  /data/oyczero/apps/debian-runtime/state/rootfs/tmp/
oyczero dev --user root run apt install -y /tmp/PACKAGE_arm64.deb
```

Do not pass `.deb` files to `oyczero app install`; that command accepts signed
OycZERO `.oyp` packages.

Run a CLI program as `pi`:

```sh
oyczero dev --user pi run htop
```

Graphical and hardware applications require the application profile:

```sh
oyczero dev --profile application --user pi run PROGRAM
oyczero dev --profile application --user root run PROGRAM
```

Prefer MLauncher for installed GUI applications. Only one session of each
Debian profile can run at a time.

## Networking, USB and wireless tools

The built-in radio remains `wlan0`; the first external USB radio is `wlan1`.
ConnMan manages saved networks and prefers Ethernet when available.

Starting with 0006, one universal image follows the physical switch. Host
exposes the internal USB hub and Ethernet. Slave exposes owned USB ADB through
USB-C2. SSH remains independent and can work over LAN or saved Wi-Fi in either
position.

Monitor mode and WiFiT3 are intended for supported external USB adapters. The
internal managed `wlan0` is protected from WiFiT3 takeover. Only audit networks
and devices that you own or are explicitly authorized to test.

The Buildroot BusyBox `wget` supports HTTP and FTP only. Use `curl -fL` for
HTTPS downloads.

## HDMI

Connect and power HDMI before boot. Select **Off**, **Mirror LCD** or
**Terminal** in Setup, or use:

```sh
oyczero hdmi mirror
oyczero hdmi terminal
oyczero hdmi off
oyczero hdmi status
```

The legacy framebuffer does not support reliable hot-plug discovery. If HDMI
was connected after boot and remains blank, leave it connected and reboot.

Terminal mode uses LCD `tty1` and HDMI `tty2`. Move the Cardputer keyboard with:

```sh
oyczero hdmi focus
oyczero hdmi lcd
```

Typing `exit` in the HDMI Shell closes it and returns focus to the LCD. SSH is
the recovery path for an incorrect focus or blank display.

## Hardware exposed to applications

The application profile provides controlled access to the CardputerZero LCD,
keyboard, audio, IMX219 camera, BMI270/BMM150 sensors, IR devices and selected
Cap-Bus/GPIO interfaces. Applications still need correct device support and
Debian package dependencies; exposing a device does not guarantee that every
third-party application knows how to use it.

The runtime includes Picamera2 and the Lite `rpicam-hello`, `rpicam-still` and
`rpicam-vid` command stack. OycZERO also provides an unversioned `rpicam-apps`
compatibility dependency without pulling the Raspberry Pi desktop camera
metapackage.

## Updates and persistence

The SD card has four functional areas:

| Area | Role | Update behavior |
| --- | --- | --- |
| p1 BOOT | Shared Raspberry Pi firmware, boot selectors and per-slot boot files. | The updater stages only the target slot's boot files and changes the default selector only after a healthy trial. |
| p2 System A | Read-only OycZERO SquashFS slot. | Either the running default or the inactive update target. |
| p3 System B | Read-only OycZERO SquashFS slot. | Either the running default or the inactive update target. |
| p4 DATA | Writable settings, credentials, logs, packages, Debian runtime, Store state and user files. | Preserved by `.oyu` updates and ordinary slot changes. |

An A/B update never overwrites the running system slot. It verifies the signed
manifest and payload hashes, writes the other SquashFS slot, stages that slot's
boot files and records the pending trial under DATA. The next restart is a
one-shot boot into the new slot while the previous slot remains the default.

During the trial, OycZERO checks that the expected build is running and DATA is
writable. A successful check commits the new slot as the default and assigns the
other slot as the next inactive target. If the trial cannot start or confirm,
the Raspberry Pi tryboot mechanism returns to the previous default. A trial
watchdog also resets a hung, unconfirmed boot so recovery does not require a
manual power cycle.

Check and install the latest stable signed update:

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

Install a copied update package:

```sh
oyczero update install /data/oyczero-BUILD-ID-update.oyu
```

`oyczero update status` shows the running build and slot, the build found in the
other slot, the selected update channel, and any pending or completed trial.

Full-image installation is different: it replaces DATA, including network
profiles, owner credentials, SSH host identity, installed applications and user
files. Back up required DATA before writing an image.

## Recovery checklist

- Press Esc during the startup countdown to stay in Shell.
- Press F3 to repair the native launcher suite.
- Use `oyczero app shutdown` over SSH to stop a managed foreground app.
- Use `oyczero hdmi lcd` over SSH to return keyboard focus to the LCD.
- Inspect `oyczero update status` after an interrupted update.
- During an unfinished step-7 continuation, use the temporary `pi` / `pi`
  recovery account at the IP shown on the failure screen, copy
  `/data/oyczero/install/`, then retry once with a controlled reboot.
- If DATA must be replaced, write the full numbered image and restore only a
  reviewed private backup.
