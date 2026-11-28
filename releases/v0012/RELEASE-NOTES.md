# OycZERO 0012

Build `20261128T200841Z-g66f8745db3b3` from clean source commit
`66f8745db3b35a89e7081b3d682329a36e444a90`.

OycZERO 0012 adds local browser-based image customization while preserving the
immutable Buildroot host, DATA-resident applications and signed A/B updates.

## Highlights

- Adds [OycZERO Config](https://oycze.github.io/OyczERO/OycZERO-Config/), a
  static browser tool that customizes the reviewed installer locally. The
  selected image and entered credentials are not uploaded to a server.
- Supports owner password, one optional ordinary user, visible or hidden Wi-Fi,
  initial installer mute, offline package selection and Shell, MLauncher or
  WiFiT3 autostart in one generated image.
- Keeps both provisioning records bounded and checksummed, verifies their
  read-back, imports secrets transactionally and erases them after successful
  application.
- Creates volatile host identities before udev coldplug. This fixes MLauncher
  framebuffer and keyboard permissions after a real boot while later applying
  the DATA-resident owner credentials.
- Retains Debian runtime `1.1.9`, APPLaunch/Store `0.6.111` and WiFiT3 `0.7.2`.

## Artifacts

- `oyczero-v0012-install.img.xz`: complete universal fresh-install/recovery
  image for Raspberry Pi Imager and the input for OycZERO Config. It replaces
  the card layout and DATA.
- `oyczero-20261128T200841Z-g66f8745db3b3-update.oyu`: signed A/B update for an
  existing OycZERO installation. It preserves DATA.
- `debian-runtime-1.1.9-arm64.oyp`: signed offline Debian application runtime.
- `applaunch_0.6.111-oyczero.2_arm64.deb` and
  `oyczero-m5market_0.6.111-oyczero.2_arm64.deb`: locked native launcher suite.
- `wifit3-0.7.2-arm64.oyp`: signed optional terminal package.

## Standard installation

Write `oyczero-v0012-install.img.xz` with Raspberry Pi Imager through
**Use custom** and allow all ten graphical stages to finish. Do not remove
power during card preparation or package installation.

## Customized installation

1. Open [OycZERO Config](https://oycze.github.io/OyczERO/OycZERO-Config/).
2. Download the reviewed v0012 image from the page and select that local file.
3. Verify the embedded release identity, choose the required settings and save
   the generated `.img`.
4. Write the generated image with Raspberry Pi Imager.

All processing stays in the browser. A customized image intentionally contains
the entered password and Wi-Fi credentials until its first successful boot.
Keep it private and delete it when no longer needed. The page does not write an
SD card directly and cannot infer its capacity; Raspberry Pi Imager remains the
write and verification step.

## Update an installed system

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

The updater verifies the signature and every payload hash, writes only the
inactive slot and commits it after a successful trial boot. DATA is preserved.

## Validation

- Full Stage 3 on the exact clean image: 1,670 passed, 15 later-stage
  requirements deselected.
- The disposable ten-step installation integration passed.
- XZ integrity passed and streaming decompression reproduced the archived raw
  image byte-for-byte by size and SHA-256.
- The production update parser verified Ed25519, sequence 12, layout `ab-v3`
  and all 368 payload hashes.
- The Web Image Builder unit suite, production build, Chromium smoke and exact
  clean-image streaming test passed.
- The launcher-permission fix was installed through signed A/B update on the
  hardware candidate. The trial committed on slot B; after a real reboot,
  MLauncher was visible and keyboard-responsive with correct framebuffer and
  input permissions and no unknown udev groups.

## Hardware evidence boundary

The accepted dirty v0012 candidate exercised custom owner, Wi-Fi, audio,
package and autostart provisioning. The final launcher fix was then accepted
through a signed dirty A/B update from the exact release source. The final
clean image and update differ in build identity and were verified on the host;
they were not written to a second card. Release metadata records that boundary
instead of claiming an exact clean-image hardware flash.

## Known limitations

- Full installation replaces DATA. Use the signed `.oyu` update to preserve an
  existing DATA partition.
- OycZERO Config requires a modern Chromium-family browser and local storage
  space for both the downloaded compressed image and generated raw image.
- The generated customized image contains the entered secrets until first boot.
- WiFiT3 requires a supported external USB wireless adapter. Internal `wlan0`
  is deliberately protected from takeover.
- HDMI hot-plug discovery is unavailable with the legacy framebuffer backend;
  connect and power the display before boot.
