# Installing an OyczERO development image

These instructions cover the current CardputerZero v0.5 images with BOOT,
SquashFS root and ext4 data partitions. Check the chosen build's notes first.

## 1. Choose the profile and verify the file

- Choose the **Host** image for normal use with onboard Ethernet and USB host
  peripherals. Set the device's USB role switch to Host.
- Choose the **ADB** image for USB-C2 diagnostics. Set the USB role switch to
  Slave. This profile cannot use the shared onboard USB Ethernet path.

Compare the image's SHA-256 hash with the matching line in the build's
`SHA256SUMS`. On Windows, run `Get-FileHash IMAGE_FILE -Algorithm SHA256` with
the actual image path. On Linux, run `sha256sum -c SHA256SUMS`; on macOS use
`shasum -a 256 -c SHA256SUMS` from a complete extracted build directory.

## 2. Write the SD card

**A full-image write replaces the partition table and `/data`, including saved
Wi-Fi profiles, SSH authorization and user files. Back up the data first.**
This is a fresh installation, not an update that preserves settings.

1. Power off Zero and connect its microSD card to the computer through a reader.
2. Select the chosen `.img` as a custom image in the SD imaging application.
3. Select the correct SD card, write the image and complete verification.
4. Safely eject the card, insert it into Zero and boot.

If verification fails, retain the exact error and check the card/reader and
image hash. A successful boot alone does not verify all written bytes.

## 3. First boot

The local console logs in automatically as `root` with Bash. The local root
password is empty. SSH does not accept passwords and starts disabled.

```sh
oyczero version
oyczero data status
oyczero net status
```

Configure Wi-Fi explicitly with `oyczero wifi setup`; setup is not forced during
boot. With the Host image and an attached LAN cable, use `oyczero lan on` if
Ethernet is not enabled, then inspect addresses with `ip -4 addr`.

## 4. Enable diagnostics

Generic distribution images contain no pre-authorized personal SSH key.
SSH and ADB are off after each boot.

### USB ADB profile

Connect USB-C2 to the computer in Slave mode and run locally on Zero:

```sh
oyczero adb start
```

With Android platform tools installed on the computer:

```sh
adb devices -l
adb shell
```

This is locally enabled root USB access without host authentication. Turn it
off with `oyczero adb stop` when finished. To authorize your own SSH public key,
copy only the public `.pub` file and import it:

```sh
adb push YOUR_PUBLIC_KEY.pub /run/owner.pub
adb shell oyczero ssh authorize /run/owner.pub
adb shell oyczero ssh on
```

SSH then needs a network connection; the ADB profile can use configured Wi-Fi.
Never copy the private key onto Zero or into release assets.

### Host profile: import a key from the SD boot partition

After writing the image, copy your SSH public key to the FAT boot partition as
`authorized_keys`. After boot, import it locally using a read-only mount:

```sh
mkdir -p /run/oyczero-key-import
mount -t vfat -o ro,nodev,nosuid,noexec /dev/mmcblk0p1 /run/oyczero-key-import
oyczero ssh authorize /run/oyczero-key-import/authorized_keys
umount /run/oyczero-key-import
oyczero ssh on
```

`oyczero ssh authorize` replaces the authorized-key list. Use a file containing
one public key per line to authorize multiple computers. Connect as `root`
using the matching private key on your computer; SCP requires legacy mode `-O`.
Verify the device host-key fingerprint on the first connection.

## 5. Record the device test

Record `oyczero version` with the test result. Check LCD/keyboard, the status
bar, boot sound, LAN/Wi-Fi and the attached Monster independently. In the
current Grove setup, use `oyczero monster on --port grove` before `janos-app`.
Exit JanOS from its home screen before using standalone Monster/port commands.

[Build index](README.md) · [Project overview](../README.md)
