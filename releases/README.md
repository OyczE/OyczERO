# OyczERO releases

Latest candidate: [20261116T173028Z-g2c142df3759d](20261116T173028Z-g2c142df3759d/RELEASE-NOTES.md) (GREEN Host acceptance).
Compact Host and ADB `.img.xz` files are staged in that directory as ignored
Release attachments. They are not Git-tracked binaries or published downloads.
See the candidate's checklist before external publication.

---

# OS releases

## Build notes

These are local development records, not published GitHub releases. The latest
generic Host/ADB image pair is staged for the owner's device test. The previous
17:37 package remains historical; its existing remote draft is unchanged.

| Build | Status | Notes |
| --- | --- | --- |
| `20261116T173028Z-g2c142df3759d` | Latest; clean; GREEN Host acceptance; 6/6 A-B-A Wi-Fi takeover; hidden networks in Setup | [Changes and validation](20261116T173028Z-g2c142df3759d/RELEASE-NOTES.md) |
| `20261116T100207Z-g5cdfe51b8172-dirty` | Previous; GREEN for install/boot; intermittent Wi-Fi takeover (fixed in 20261116T173028Z-g2c142df3759d) | [Changes and validation](20261116T100207Z-g5cdfe51b8172-dirty/RELEASE-NOTES.md) |
| `20261115T215239Z-gbbdc8f6a0c1e` | Latest clean build from bbdc8f6; cold boot pending | [Changes and validation](20261115T215239Z-gbbdc8f6a0c1e/RELEASE-NOTES.md) |
| `20261115T205648Z-g770aba728835-dirty` | Previous candidate; shortcuts, Wi-Fi setup, saved power and welcome corrections; cold boot pending | [Files, validation and installation](20261115T205648Z-g770aba728835-dirty/RELEASE-NOTES.md) |
| `20261115T201146Z-g770aba728835-dirty` | Previous candidate; owner confirmed boot and password SSH after reboot | [Files, validation and installation](20261115T201146Z-g770aba728835-dirty/RELEASE-NOTES.md) |
| `20261115T173713Z-g770aba728835` | First development release; Host/ADB images staged, hardware boot pending | [Files, validation and installation](20261115T173713Z-g770aba728835/RELEASE-NOTES.md) |
| `20261115T155005Z-g770aba728835` | Clean local build; Host boot confirmed on Zero | [Changes, validation and limits](20261115T155005Z-g770aba728835/RELEASE-NOTES.md) |

See the [changelog](../CHANGELOG.md) for earlier source milestones and unreleased
work, the [installation guide](INSTALL.md) for flashing/access, and the
[project README](../README.md) for the current system overview.

## Preparing a release

Stage reviewed output under a versioned directory named with its build ID.
Expected payloads are fresh-install images and, once implemented, signed
data-preserving update bundles. Attach large files to GitHub Releases.

Keep public release notes, manifests, checksums and signed catalog metadata
with the corresponding version. Do not reuse an existing version for changed
bytes. A full image is a fresh installation, not a data-preserving update.

Normal development output remains in `output/releases/` outside this workspace.
Only selected distributable builds are copied here after verification. A build
with a personal SSH authorization seed is not a generic public release.

Add `RELEASE-NOTES.md` for each selected build. Record its build ID, source
commit, compatible board/layout, changes, validation and known limitations.
Keep pending plans separate from shipped behavior, and link the entry from
this index and `CHANGELOG.md`. Record publication status explicitly.

The current package contains two compact installer `.img.xz` files (about
80 MiB each), their installer manifests, `kernel.config`,
`build.json`, `manifest.json`, `SHA256SUMS`, `validation.json` and release notes.
The images are local staging files ignored by Git. Upload them as Release
attachments when publication is authorized; commit only the reviewed metadata
and documentation. Preserve the original build ID, including `-dirty`.

## Update packages (development channel)

Systems from build `20261116T184024Z-gfce776c6ce74` onwards can update
themselves without erasing settings or files:

```
oyczero update check            # look for a newer package on GitHub
oyczero update install latest   # download, verify, install, restart once
oyczero update status           # running build, other slot, last result
```

Packages (`oyczero-BUILD-update.oyu`, about 80 MB) are published as GitHub
pre-releases named `update-BUILD`. Each package is signed; the device rejects
modified or foreign packages. The update is written to the inactive system
slot and tried once; it becomes the default only after a successful start,
otherwise the previous system keeps running. Older images without the updater
need one fresh installation first. These are development builds; version
numbering (0001) starts with the first stable update channel.
