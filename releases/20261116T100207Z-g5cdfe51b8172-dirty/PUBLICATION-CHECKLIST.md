# Publication checklist

- [x] Owner accepted the exact Host image: GREEN for tested hardware scope.
- [x] Automated checks and installer integrations passed.
- [x] Exported artifact checksums verified.
- [x] Public export excludes private source snapshots and diagnostic access data.
- [ ] Commit reviewed source/export work locally; preserve dirty build provenance.
- [ ] Exact ADB hardware acceptance (or explicitly limit release to Host).
- [x] Wi-Fi association/DHCP, traffic and SSH verified.
- [ ] Resolve/retest intermittent automatic Wi-Fi reconnect failure.
- [ ] Required third-party notices and corresponding sources reviewed.
- [ ] JanOS-app redistribution permission resolved.
- [ ] Explicit owner instruction to upload/publish the selected artifacts.

Slot-B boot passed; automatic rollback remains development work. Do not advertise working OTA.

## Additional physical acceptance: A-B-A and Wi-Fi

One-shot boot of B and normal return to A passed; DATA sentinel and network-policy
hashes were preserved. Wi-Fi association, DHCP, gateway ping and SSH over wlan0
passed. After returning to A, disabling Ethernet automatically connected saved
Wi-Fi; re-enabling Ethernet restored route preference.

**Known intermittent issue:** the first automatic Wi-Fi attempt during the B
trial failed with `connect-failed`; explicit reconnect using the saved profile
succeeded. Repeated reconnect reliability is not yet accepted. These tests do
not qualify automatic rollback, power-loss recovery or an update installer.
Both slots ran the same build. Exact ADB profile testing remains pending.
