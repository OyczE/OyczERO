# Third-party notices and distribution status

OyczERO includes software and firmware from other authors. The
[OyczERO Proprietary License](LICENSE.md) covers only the applicable original
materials of Mateusz Ziółek - LAB5 (lab5.eu.com); it does not replace licenses
of bundled components or their derivatives.

## Current distribution status

OyczERO 0005 is a clean base OS and does not contain JanOS-app or other optional
application packages. JanOS-app redistribution therefore is not part of this
release; any future optional package requires its own license and redistribution
review.

The public v0005 assets contain only the two binary installation images, the
signed binary update, its manifest and checksums. The private development source,
build workspace and local compliance archives are not published in this
distribution repository or attached to the release.

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

Buildroot's `legal-info` target is an aid to collecting material. Its output
requires review and is not an automatic certification of redistribution rights.
The binary-only release does not change or replace the original component
licenses.
