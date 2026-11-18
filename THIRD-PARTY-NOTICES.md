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

The v0005 release provides two source-and-license assets alongside the binary
images and signed update:

- `oyczero-v0005-third-party-sources.tar.xz`: Buildroot `legal-info`, upstream
  source archives, applied patches, exact Buildroot 2026.08.1 source and build
  identity.
- `oyczero-v0005-bootlin-toolchain-sources.tar.xz`: the external Bootlin
  AArch64 toolchain source, patches, license texts and reproducible-build
  metadata, with a SHA-256 manifest.

These collections preserve the reviewed material for the exact release. They do
not replace the terms of each component's license or constitute automatic legal
certification.

## Component references

This list is a starting point, not a complete software bill of materials.

| Component | Reference | Treatment |
| --- | --- | --- |
| Buildroot and selected packages | [Buildroot licensing guidance](https://buildroot.org/downloads/manual/manual.html#legal-info) | Exact v0005 collection included in the third-party source asset |
| Linux, BusyBox, Bash and other runtime dependencies | License files and sources of the exact built versions | Included in the reviewed Buildroot collection where applicable |
| Bootlin external AArch64 toolchain | [Bootlin toolchains](https://toolchains.bootlin.com/) | Separate source, patches, licenses and build metadata asset included |
| CardputerZero vendor code and firmware | [CardputerZero](https://github.com/CardputerZero) | Preserve each pinned component's upstream license and notices |

Buildroot's `legal-info` target is an aid to collecting material. Its output
requires review and is not an automatic certification of redistribution rights.
The full private OyczERO development history is not a substitute for the
published source-and-license assets or the original component licenses.
