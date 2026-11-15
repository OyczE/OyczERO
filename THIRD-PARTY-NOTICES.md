# Third-party notices and distribution status

OyczERO includes software and firmware from other authors. The
[OyczERO Proprietary License](LICENSE.md) covers only the applicable original
materials of Mateusz Ziółek - LAB5 (lab5.eu.com); it does not replace licenses
of bundled components or their derivatives.

## Current distribution status

The first image package is staged for local development and testing by
the project owner. It has not been published or cleared for distribution to
other recipients. Hosting a package in a private repository does not itself
settle the licensing obligations of sharing it with other people.

The following items must be resolved before external distribution:

- Collect and review the package license texts, copyright notices and the
  corresponding sources, patches and build material required by each license.
- Confirm permission to redistribute the pinned JanOS-app version. The current
  build recipe records it as `Proprietary` with redistribution disabled because
  its upstream revision contains no redistribution license. This is a pending
  permission check, not a claim that LAB5 owns that upstream application.
- Review firmware, vendor code, bundled assets and any other separately licensed
  material. Preserve their original notices.

## Component references

This list is a starting point, not a complete software bill of materials.

| Component | Reference | Treatment |
| --- | --- | --- |
| Buildroot and selected packages | [Buildroot licensing guidance](https://buildroot.org/downloads/manual/manual.html#legal-info) | Package-specific licenses and source obligations apply; collect and review `legal-info` output |
| Linux, BusyBox, Bash and other runtime dependencies | License files of the exact built versions | Retain their licenses and provide required corresponding sources when distributing |
| CardputerZero vendor code and firmware | [CardputerZero](https://github.com/CardputerZero) | Review each pinned component separately; preserve upstream notices |
| JanOS-app | [Pinned upstream revision](https://github.com/D3h420/JanOS-app/tree/dac0fc038390e996668a6ad621e5f16de98350bd) | Redistribution permission remains to be confirmed |

Buildroot's `legal-info` target is an aid to collecting material. Its output
requires review and is not an automatic certification of redistribution rights.
The full private OyczERO development history is not a substitute for a reviewed
corresponding-source package for components that require one.
