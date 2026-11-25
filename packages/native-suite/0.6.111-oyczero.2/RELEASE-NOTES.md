# APPLaunch and Store native suite 0.6.111-oyczero.2

This locked pair installs official APPLaunch `0.6.111` content and the matching
Store revision inside OycZERO's DATA-resident Debian runtime. The OycZERO
packaging revision adds deterministic ownership, paths and runtime integration;
it does not make these `.deb` files Buildroot packages.

Use F3 or `oyczero app install m5launcher`. OycZERO downloads, verifies and
installs both files as one suite. Do not pass the `.deb` files directly to
`oyczero app install`.
