# OycZERO release layout

Each numbered operating-system release uses one canonical directory:

```text
releases/
  v0011/
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
oyczero-v0011-install.img.xz
oyczero-20261127T201522Z-gd79a6e2fd903-update.oyu
debian-runtime-1.1.9-arm64.oyp
applaunch_0.6.111-oyczero.2_arm64.deb
oyczero-m5market_0.6.111-oyczero.2_arm64.deb
wifit3-0.7.2-arm64.oyp
```

Images and package payloads are ignored by Git. Release directories contain
only reviewed public metadata, checksums and release notes. They must not
contain build logs, test output, publication checklists, TODO files, internal
plans, credentials, keys, backups or source-workspace paths.

See [INSTALL.md](INSTALL.md) for the distinction between initial installation,
operating-system updates and optional tool packages.
