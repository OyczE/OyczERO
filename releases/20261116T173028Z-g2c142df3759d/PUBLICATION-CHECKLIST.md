# Publication checklist

- [x] Clean source commit; build ID without `-dirty`.
- [x] Owner acceptance of the exact Host image: GREEN for the tested scope.
- [x] Automated suite passed; root hashes match installer manifests.
- [x] No private keys, authorization seeds, credentials or backups in images.
- [x] Exported artifact checksums verified.
- [x] Wi-Fi association, automatic takeover and Ethernet preference: 6/6 A-B-A.
- [x] Hidden-network join and reboot reconnect on hardware.
- [ ] Exact ADB hardware acceptance (or limit the release to Host).
- [ ] Required third-party notices and corresponding sources reviewed.
- [ ] JanOS-app redistribution permission resolved.
- [ ] Explicit owner instruction to make the Release public.

Slot-B boot passed with a one-shot helper; automatic rollback and OTA updates
are not implemented. Do not advertise working OTA.
