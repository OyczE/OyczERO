# Third-party notices and distribution status

OycZERO includes software and firmware from other authors. The
[OycZERO Proprietary License](LICENSE.md) covers only the applicable original
materials of Mateusz Ziółek - LAB5 (lab5.eu.com); it does not replace licenses
of bundled components or their derivatives.

## Current distribution status

OycZERO 0010 keeps the immutable Buildroot core separate from application
payloads. The fresh installer carries an offline default suite that is installed
on DATA: the signed Debian runtime `1.1.8`, official ARM64 APPLaunch `0.6.111`
content and its matching Store revision. The same immutable components are
published as separate release assets for update and repair. Their archives and
runtime retain applicable upstream notices and Debian copyright files. JanOS-app
is not included; any future package requires its own license and redistribution
review.

The public v0010 assets contain one binary installer, one signed binary update,
one signed runtime package, two native Debian packages, the signed optional
WiFiT3 package, the release manifest and checksums. WiFiT3 retains its GPL-2.0
notice, exact upstream provenance and corresponding source archive inside the
signed package. The private OycZERO development source, build workspace and
local compliance archives are not published in this distribution repository or
attached to the release.

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
| M5Stack APPLaunch 0.6.111 | [CardputerZero/launcher](https://github.com/CardputerZero/launcher/tree/launcher-v0.6.111) | Official ARM64 content is installed inside the DATA runtime; bundled notices are retained |
| CardputerZero Store revision `1ceeaed7` | [CardputerZero/Store](https://github.com/CardputerZero/Store) | Built as a native Debian package locked to APPLaunch 0.6.111 |
| wifit3 0.7.2 | [derv82/wifit3](https://github.com/derv82/wifit3) | GPL-2.0-only terminal package; signed payload includes exact provenance and corresponding source |
| Debian 13 application runtime | [Debian copyright information](https://www.debian.org/doc/debian-policy/ch-docs.html#copyright-information) | Exact package versions, hashes, copyright files and licenses are retained inside the signed runtime package |
| Raspberry Pi and Broadcom boot firmware | License files shipped with the exact firmware release | Applicable firmware notices, including `LICENCE.broadcom`, are retained in the image |

Buildroot's `legal-info` target is an aid to collecting material. Its output
requires review and is not an automatic certification of redistribution rights.
The binary-only release does not change or replace the original component
licenses.
