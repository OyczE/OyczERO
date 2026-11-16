# OyczERO

A custom ARM64 Linux system for **CardputerZero v0.5**, with a read-only
SquashFS system and persistent settings and files on `/data`.

## Current binary candidate

**20261116T173028Z-g2c142df3759d** is the current GREEN Host build from clean source commit `2c142df3759d`. Host and ADB compact installers,
checksums and release documentation are prepared. It adds reliable Wi-Fi start-up and takeover
(6/6 A-B-A cycles on hardware) and hidden Wi-Fi networks in Setup. The ADB
profile and third-party distribution checks remain pending; see release notes.

- [Release notes](releases/20261116T173028Z-g2c142df3759d/RELEASE-NOTES.md)
- [Publication checklist](releases/20261116T173028Z-g2c142df3759d/PUBLICATION-CHECKLIST.md)
- [Installation and access](releases/INSTALL.md)
- [Changelog](CHANGELOG.md)
- [Release directory](releases/README.md)
- [Third-party notices](THIRD-PARTY-NOTICES.md)

The installer writes 257 MiB and provisions two 1 GiB system slots plus DATA
on first boot. **Fresh flashing erases existing settings and files.** A/B
layout is present; signed OTA and automatic rollback are not implemented.

Features include Bash root console, LCD/status bar, Wi-Fi/LAN controls,
SSH setup, USB ADB, persistent port power and JanOS/Monster Grove integration.
HDMI supports Off, Mirror LCD and Terminal. Setup includes resolution and
font size controls with a timed confirmation preview. First installation now
shows the original OyczERO letter-reveal logo before the progress stages, then
restarts automatically into the installed system.

Run `oyczero setup`; navigate with arrows or F/Z/X/C and confirm with Enter.
The local console logs in as root. Choose your own SSH password using
`oyczero ssh setup`; images contain no shared SSH credentials.

This repository holds distribution material only. Native desktop installers
and a browser updater are planned, not available packages. Large binaries
belong in [GitHub Releases](https://github.com/OyczE/OyczERO/releases), not Git.
See [LICENSE.md](LICENSE.md) for original-material terms and third-party exceptions.
