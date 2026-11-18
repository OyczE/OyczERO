# OyczERO release layout

Each numbered operating-system release uses one canonical directory:

```text
releases/
  v0005/
    RELEASE-NOTES.md
    manifest.json
    SHA256SUMS
```

Do not create release directories named after development timestamps, commits,
dirty worktrees or local candidates. The exact build identity belongs in the
release manifest.

The corresponding large artifacts are staged locally with the same release
version and uploaded as GitHub Release assets:

```text
oyczero-v0005-install-host.img.xz
oyczero-v0005-install-adb.img.xz
oyczero-20261118T140549Z-g71a33183923e-update.oyu
oyczero-v0005-third-party-sources.tar.xz
oyczero-v0005-bootlin-toolchain-sources.tar.xz
```

Images and package payloads are ignored by Git. Release directories contain
only reviewed public metadata, checksums and release notes. They must not
contain build logs, test output, publication checklists, TODO files, internal
plans, credentials, keys, backups or source-workspace paths.

See [INSTALL.md](INSTALL.md) for the distinction between initial installation,
operating-system updates and optional tool packages.
