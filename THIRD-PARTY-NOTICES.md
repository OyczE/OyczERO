# Third-party notices and distribution status

OyczERO includes software and firmware from other authors. The
[OyczERO Proprietary License](LICENSE.md) covers only the applicable original
materials of Mateusz Ziółek - LAB5 (lab5.eu.com); it does not replace licenses
of bundled components or their derivatives.

## Current distribution status

OyczERO 0007 keeps its base OS free of optional application payloads. The
separately downloadable M5Launcher package repackages the official ARM64
APPLaunch `0.6.110` artifact and pinned Debian runtime components. Its archive
contains the applicable upstream notices and license files. JanOS-app is not
included; any future package requires its own license and redistribution review.

The public v0007 assets contain one binary installer, one signed binary update,
one signed optional application package, the release manifest and checksums.
The private development source, build workspace and local compliance archives
are not published in this distribution repository or attached to the release.

Third-party components remain governed by their respective licenses. This file
does not replace those terms or constitute automatic legal certification.

## Component references

This list is a starting point, not a complete software bill of materials.

| Component | Reference | Treatment |
| --- | --- | --- |
| Buildroot and selected packages | [Buildroot licensing guidance](https://buildroot.org/downloads/manual/manual.html#legal-info) | Package-specific licenses and source obligations apply |
| Linux, BusyBox, Bash and other runtime dependencies | License files of the exact built versions | Preserve applicable upstream notices and license terms |
| Bootlin external AArch64 toolchain | [Bootlin toolchains](https://toolchains.bootlin.com/) | Toolchain and component-specific terms apply |
| CardputerZero vendor code and firmware | [CardputerZero](https://github.com/CardputerZero) | Preserve each pinned component's upstream license and notices |
| M5Stack APPLauncher 0.6.110 | [CardputerZero/launcher](https://github.com/CardputerZero/launcher/tree/launcher-v0.6.110) | Distributed only as the optional signed package; bundled notices are retained |
| Debian runtime libraries in the M5Launcher package | [Debian copyright information](https://www.debian.org/doc/debian-policy/ch-docs.html#copyright-information) | Exact package versions, hashes, copyright files and licenses are retained inside the package |

Buildroot's `legal-info` target is an aid to collecting material. Its output
requires review and is not an automatic certification of redistribution rights.
The binary-only release does not change or replace the original component
licenses.
