# OyczERO packages

Optional tool packages use one directory per package and package version. The
version combines the upstream version with an OyczERO packaging revision:

```text
packages/
  catalog.json
  wifit3/
    0.7.1-r1/
      manifest.json
      SHA256SUMS
      RELEASE-NOTES.md
  airgeddon/
    12.10-r1/
      manifest.json
      SHA256SUMS
      RELEASE-NOTES.md
```

Package payloads use the `.oyp` extension, include their architecture in the
filename and are uploaded as immutable GitHub Release assets:

```text
wifit3-0.7.1-r1-aarch64.oyp
airgeddon-12.10-r1-aarch64.oyp
```

Each package revision has its own release tag, for example
`pkg-wifit3-0.7.1-r1`. Published assets are never replaced in place. A newer
package creates an `r2` revision or a new upstream-version directory, while the
catalog retains exact versioned download URLs for supported older revisions.
Assets remain available until their release is deliberately retired.

Only reviewed public metadata, checksums, release notes, license notices and
required corresponding-source references belong in these directories. Build
trees, caches, tests, logs, TODO files, internal plans, credentials and private
source material remain outside this distribution repository.

Native desktop flasher installers may use versioned platform directories under
`packages/desktop/` after those artifacts exist and pass platform-specific
testing.
