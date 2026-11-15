# OS releases

## Build notes

These are local development records, not published GitHub releases. The first
generic Host/ADB image package is now staged for the owner's device test.

| Build | Status | Notes |
| --- | --- | --- |
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
