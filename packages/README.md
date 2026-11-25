# OycZERO packages

Optional tool packages use one directory per package and package version. The
version combines the upstream version with an OycZERO packaging revision:

```text
packages/
  catalog.json
  debian-runtime/
    1.1.8/
  native-suite/
    0.6.111-oyczero.2/
  m5launcher/
    0.6.110-r1/
      manifest.json
      SHA256SUMS
      RELEASE-NOTES.md
```

Package payloads use the `.oyp` extension, include their architecture in the
filename and are uploaded as immutable GitHub Release assets:

```text
m5launcher-0.6.110-arm64.oyp
```

M5Launcher `0.6.110-r1` is attached to system release `v0007` because the first
catalog implementation pins that exact stable asset. Future independently
versioned packages can use their own `pkg-ID-VERSION` release tags. Published
assets are never replaced in place; a changed payload creates a new packaging
revision or upstream version.

Only reviewed public metadata, checksums, release notes, license notices and
required corresponding-source references belong in these directories. Build
trees, caches, tests, logs, TODO files, internal plans, credentials and private
source material remain outside this distribution repository.

Native desktop flasher installers may use versioned platform directories under
`packages/desktop/` after those artifacts exist and pass platform-specific
testing.

The public catalog contains only packages accepted directly by `oyczero app`,
including the signed Debian runtime `.oyp`. APPLaunch and Store `.deb` files are
documented under `native-suite/`; OycZERO verifies and installs them inside the
runtime as one locked suite. They are not direct Buildroot packages and are not
catalog entries.
