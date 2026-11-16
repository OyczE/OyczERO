# OyczERO - Setup shortcuts, Wi-Fi and persistent power

Build **`20261115T205648Z-g770aba728835-dirty`** is staged locally for CardputerZero v0.5. It has not
been uploaded or published. New-image cold-boot acceptance is pending.

Copyright (c) 2026 Mateusz Ziółek - LAB5 (lab5.eu.com).
[License](../../LICENSE.md) and [Third-party notices](../../THIRD-PARTY-NOTICES.md).

## Files

Both fresh-install images use Linux 6.18.39-v8, ARM64 and the existing
BOOT/SquashFS/ext4-data layout. Each is 208,666,624 bytes (199 MiB).

| File | Purpose |
| --- | --- |
| `oyczero-20261115T205648Z-g770aba728835-dirty-host.img` | Host/LAN; SSH starts after personal credentials exist |
| `oyczero-20261115T205648Z-g770aba728835-dirty-adb.img` | Automatic USB-C2 ADB with the Slave switch; onboard USB LAN unavailable |
| [SHA256SUMS](SHA256SUMS) | Image and kernel-configuration hashes |
| [manifest.json](manifest.json) | Artifact names, sizes and SHA-256 |
| [build.json](build.json) | Immutable build identity |
| [kernel.config](kernel.config) | Actual kernel configuration |
| [validation.json](validation.json) | Validation scope and remaining tests |

Large images are staged beside these notes but ignored by Git. They belong in
Release attachments when publication is authorized. The source base is
`770aba728835077729b0ddb427280d6e4761c598` plus local changes; keep the `-dirty` suffix.
The earlier 17:37 remote draft is unchanged.

## Changes since 20:11

- **Shell shortcuts:** F1 information, F2 setup, F3 JanOS. Use Fn+1/2/3 on the
  built-in keyboard. They act at the Bash prompt and preserve an unfinished
  command. JanOS requires the local tty1 console.
- **Welcome:** connected LAN/Wi-Fi IPv4 addresses and one colored command line.
  Access startup reports starting while an owned worker is active and briefly
  waits for completion, avoiding an early false Off. F1 refreshes the snapshot.
- **Persistent power:** setup applies EXT/Grove 5V now and restores saved choices
  after reboot. Fresh installs default both off. Enable readback, independent
  routing and shared JanOS ownership are preserved. Direct port commands remain
  runtime-only. Failed saves attempt rollback and show any uncertain state first.
- **Wi-Fi setup:** select country/network and enter a hidden password directly
  from setup. The connected profile and AutoConnect state are verified. The
  Wi-Fi-at-boot toggle affects the next boot without disconnecting the current
  session. Initial transient scan errors are retried within a fixed limit.
- **Prompt input:** text and password editing work when F2 launches the menu
  from Bash/readline, and the original terminal state returns on exit.

The existing password/access profiles, display/status bar, audio, networking and
JanOS frontend remain included. The optional Debian environment is separate.

## Use

Follow [installation and first access](../INSTALL.md). Local root Bash login is
automatic; SSH requires your own password or authorized key. No shared remote
password, personal SSH authorization seed or private access key is included.

**Full SD flashing replaces `/data`, including Wi-Fi profiles, SSH credentials
and settings. Back up needed data first.** These are not update packages.

Run F2 or `oyczero setup`. Choose Wi-Fi setup, then enable Wi-Fi at boot for
restoration of the configured radio/saved networks. Ethernet remains preferred;
with LAN already connected, Wi-Fi may stay idle until needed for fallback.
For the 4-pin Monster enable Grove 5V, then run F3 or `janos-app` locally.

## Validation and limits

- **637 source/image tests passed; 27 later-stage tests excluded.** Actual ARM64
  read-only-root networking, SSH authentication/autostart and menu checks passed.
  The shipped ARM64 Bash welcome passed. This is user-mode QEMU, not board emulation.
- Both images match tested source modules, profiles and archived hashes, with
  clean data seeds and no personal access material.
- Physical base 20:11 plus new RAM modules passed menu/LCD, function-key dispatch,
  same-boot saved-power restore, Grove pong, hidden-input Wi-Fi setup and automatic
  fallback during a software Ethernet transition. LAN returned and became preferred.
- Physical Fn key presses, this image's cold boot, saved power/Wi-Fi choices after
  reboot, first-login access state and ADB enumeration still need acceptance.
  Software Ethernet control is not a physical cable test; GPIO readback is not
  connector voltage. RTC display remains UTC.
- Hidden/enterprise Wi-Fi uses advanced connmanctl configuration. Signed OTA,
  data-preserving updates, desktop/web flashing and JanOS autostart remain planned.
- Third-party license/source review and JanOS-app redistribution permission remain
  outstanding before sharing with other recipients.

[Changelog](../../CHANGELOG.md) | [Build index](../README.md)
