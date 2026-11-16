# Installing the compact OyczERO candidate

Current staged build: `20261116T173028Z-g2c142df3759d`. Select Host for USB Host/Ethernet or ADB for
USB-C2 peripheral diagnostics, with the physical USB role switch set accordingly.
Verify `SHA256SUMS`, select the `.img.xz` file in Raspberry Pi Imager, and write
it to an SD card of at least nominal 4 GB. **This erases existing DATA.**

The image writes 257 MiB. First boot provisions BOOT, two 1 GiB system slots,
and DATA using the remaining card capacity. Keep power connected until login.
An OyczERO logo is shown before the first-install progress stages.
Use `oyczero setup` for network, ports and HDMI settings. HDMI resolution and
font size changes require Y + Enter within 15 seconds or are reverted.
Fonts apply to Terminal mode. Use `oyczero hdmi focus` / `oyczero hdmi lcd` for
advanced keyboard routing; `exit` closes the HDMI shell and returns to LCD.

Local console user: root (automatic login). Set your own SSH password with
`oyczero ssh setup`; no developer key or shared SSH password is included.
ADB images enable local USB diagnostics. Back up your DATA before future
fresh installs. OTA/update packages are not available yet.

Exact-image acceptance and third-party distribution clearance remain pending.

---

## Historical image instructions

# Installing an OyczERO development image

These instructions cover the current CardputerZero v0.5 images with BOOT,
SquashFS root and ext4 data partitions. The current package is
`20261115T215239Z-gbbdc8f6a0c1e`. Check the chosen build's notes first.
For the older `20261115T173713Z-g770aba728835` package, see the legacy access
note below: it has no password-setup flow or automatic access startup.

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

The local console logs in automatically as `root` with Bash. A fresh image
has no configured personal SSH password and no pre-authorized computer.
Remote login requires your own password or public key; there is no shared
default remote password. Local autologin remains available after SSH setup.

```sh
oyczero version
oyczero data status
oyczero net status
oyczero setup
```

Configure Wi-Fi explicitly with `oyczero wifi setup`; setup is not forced during
boot. With the Host image and an attached LAN cable, use `oyczero lan on` if
Ethernet is not enabled, then inspect addresses with `ip -4 addr`.

Wi-Fi setup offers numbered SSID selection and hidden password entry. For a
hidden network press `h`, then enter its name and password (Enter for an open
network); it is saved and reconnects automatically. Enterprise networks still
need manual connmanctl configuration. Wi-Fi at boot
defaults On and restores a configured/enabled radio after reboot. Its toggle does
not disconnect a current session. LAN remains preferred, so saved Wi-Fi can remain
idle while Ethernet is connected and reconnect automatically when LAN is lost.

The setup menu uses arrows or **F=Up, Z=Left, X=Down, C=Right**. Enter applies a
change; Escape/Q exits. Left/right previews a value and moving to another row
cancels the preview. It includes the status bar, SSH password, SSH/ADB autostart,
EXT 5V, Grove 5V, Wi-Fi setup and Wi-Fi at boot. Password entry uses normal
characters, including F/Z/X/C.
The welcome shows current SSH/ADB states and connected IPv4 addresses. F1 refreshes
it, F2 opens setup and F3 launches JanOS locally. Use Fn+1/2/3 on the built-in keyboard.

EXT/Grove switches control separate supplies, take effect immediately and
save the choice for reboot. Fresh installs default both off. They leave routing
unchanged and cannot change power
while JanOS owns the shared port. An unavailable control shows N/A.

## 4. Enable diagnostics

Generic distribution images contain no pre-authorized personal SSH key.
Access defaults depend on the image profile:

| Profile | Default boot behavior |
| --- | --- |
| Host | Start SSH after a personal password or authorized key exists |
| ADB | Start USB-C2 ADB automatically, with the physical switch in Slave |

Each profile has its own persistent autostart preference in `oyczero setup`.
Use `oyczero ssh autostart on|off|status` or `oyczero adb autostart on|off|status`
from the shell. Changing autostart does not stop the current session; use
`oyczero ssh stop` or `oyczero adb stop` for that. `on/off` are also accepted.

### Host profile: set your personal SSH password

On Zero, run:

```sh
oyczero ssh setup
oyczero ssh status
ip -4 addr
```

Enter and confirm your password. Input is hidden. The accepted length is
1–100 UTF-8 bytes; an empty password is rejected. Setup saves authentication
state on `/data` and starts SSH. Connect from the computer, substituting the
address displayed by Zero:

```sh
ssh root@DEVICE_IP
```

The password and device SSH identity survive an ordinary reboot on the same
card. Host-profile SSH starts on later boots when autostart is enabled.
A full SD reflash removes that saved state. Verify the device host-key
fingerprint when connecting for the first time.

### USB ADB profile

Connect USB-C2 to the computer in Slave mode. ADB starts automatically in this
image. If it was stopped or autostart was disabled, run locally on Zero:

```sh
oyczero adb start
```

With Android platform tools installed on the computer:

```sh
adb devices -l
adb shell
```

This is root USB access without host authentication. Turn it
off with `oyczero adb stop` when finished. To authorize your own SSH public key,
copy only the public `.pub` file and import it:

```sh
adb push YOUR_PUBLIC_KEY.pub /run/owner.pub
adb shell oyczero ssh authorize /run/owner.pub
adb shell oyczero ssh on
```

SSH then needs a network connection; the ADB profile can use configured Wi-Fi.
Never copy the private key onto Zero or into release assets.

### Optional: import an SSH key from the SD boot partition

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

### Legacy first package

Build `20261115T173713Z-g770aba728835` accepts public-key SSH only and leaves
SSH/ADB off after boot. Use the public-key import steps above and run
`oyczero ssh on` manually, or `oyczero adb start` on its ADB image. Its menu
does not include the new access or port controls. The personal-password and
autostart instructions apply to the new package.

## 5. Record the device test

Record `oyczero version` with the test result. Check LCD/keyboard, the status
bar, boot sound, LAN/Wi-Fi and the attached Monster independently. In the
current Grove setup, use `oyczero monster on --port grove` before `janos-app`.
Exit JanOS from its home screen before using standalone Monster/port commands.

[Build index](README.md) · [Project overview](../README.md)
