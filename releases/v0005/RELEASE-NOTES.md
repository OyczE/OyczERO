# OyczERO 0005

Build `20261117T232634Z-gb229c39f22a1` from clean source commit `b229c39`.

## Changes

- Correct saved ConnMan passphrase reuse by decoding both ConnMan's
  `g_strescape` layer and the GLib key-file layer. Regression coverage uses an
  SSID containing a space and a synthetic passphrase containing spaces, quotes
  and a backslash; no real credential is included.
- Add complete Host and ADB fresh-install images for Raspberry Pi Imager.
- Keep the signed `.oyu` as a separate DATA-preserving A/B update for existing
  installations.

## Artifacts

- `oyczero-v0005-install-host.img.xz`: destructive fresh installation, USB Host
  profile with SSH access policy.
- `oyczero-v0005-install-adb.img.xz`: destructive fresh installation, USB
  peripheral profile with ADB access policy.
- `oyczero-v0005-update.oyu`: signed A/B update for an existing installation.
  It preserves DATA and must not be written as a disk image.

## Validation and draft boundary

The exact clean `.oyu` completed a physical trial update, committed its new
slot, preserved DATA and survived an additional normal reboot with Ethernet,
SSH and ConnMan ready. Host and QEMU-user image tests also passed.

This release remains a draft because the two `.img.xz` artifacts have not yet
completed Raspberry Pi Imager write/readback and fresh-install hardware
acceptance. QEMU user-mode does not emulate the complete CM0 board or its
devices. Do not publish this draft as a stable image release until those checks
are recorded in the manifest.
