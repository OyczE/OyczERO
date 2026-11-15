# Desktop installer packages

Stage native OyczERO Flasher installers by platform:

- `windows/`: Windows setup executables; MSI if later supported.
- `linux/`: AppImage and Debian packages for tested architectures.
- `macos/`: DMG packages for tested Apple Silicon/Intel targets.

Record installer version, architecture, required OS version, checksum and
signing status. These are build outputs; source remains in `apps/updater/`
outside the distribution workspace. Binary packages are uploaded as GitHub
Release assets and excluded from Git history by this workspace's ignore rules.

No installer binaries have been built or copied into these directories yet.
