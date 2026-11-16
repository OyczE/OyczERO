# Publication checklist

- [x] Clean source commit and versioned build.
- [x] Automated source/image tests and disposable installer tests.
- [x] Personal authorization/credential scan of packaged root.
- [x] User accepted the live installer-logo preview.
- [ ] Exact Host and ADB installer hardware cold-boot/reboot acceptance.
- [ ] Required third-party licenses and corresponding-source bundle reviewed.
- [ ] JanOS-app redistribution permission resolved.
- [ ] Owner instruction to upload/publish this selected release.

Do not present staging or a checksum as a signed OTA release.

### Hardware follow-up

The exact Host image booted on the device; the user accepted its appearance.
SSH inspection confirmed the logo and all installer stages in retained logs,
valid ready records, matching A/B payload hashes, writable DATA, LCD, HDMI
mirroring, Ethernet and SSH. This does not establish a boot of slot B or the
ADB profile, nor a second-boot persistence test.

**Known release blocker:** Wi-Fi has no interface on this first boot. Kernel
logs report `brcmf_fwvid_request_module: mod=cyw: failed -2` and attach failure.
Diagnosis and a verified fix are required before publication.
