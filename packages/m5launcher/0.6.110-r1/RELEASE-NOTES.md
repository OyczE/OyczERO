# M5Stack APPLauncher 0.6.110-r1

This optional OyczERO package contains the official unmodified ARM64 APPLaunch
`0.6.110` release plus pinned private runtime libraries and data required by the
OyczERO Buildroot base. It installs entirely on DATA and requires OyczERO 0007
or newer on CardputerZero v0.5.

Install it with:

```sh
oyczero app install m5launcher
```

F3 installs or opens the package. Setup can select it for startup; Esc during
the two-second countdown keeps Shell for that boot. Hold Fn+Esc for about two
seconds to exit a running launcher.

The package was built three times with the same SHA-256, accepted by the
production signature/parser path and exercised on physical hardware. The
upstream AppStore's stock Debian application installation is not supported
until the optional Debian runtime and compatibility adapter are implemented.
