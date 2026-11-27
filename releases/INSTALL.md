# Installing and updating OycZERO

Always download artifacts from the matching numbered GitHub Release and verify
their SHA-256 checksums before use.

## Initial installation or recovery

A file named `oyczero-vNNNN-install.img.xz` is a complete SD-card image for
Raspberry Pi Imager. Select it through **Use custom**, choose the correct SD
card and complete write verification.

This operation replaces the partition table and erases existing DATA, including
settings, credentials and user files. Back up required files first.

The OycZERO 0011 installer presents ten graphical stages covering card
preparation, both system slots, DATA, verification and the offline application
suite. Allow about ten minutes for provisioning and longer on a slow card. The
accepted 0011 path to a responsive MLauncher took 11 minutes 25 seconds on the
original M5Stack 32 GB card. Steps 7 through 9 can take several minutes while
the offline Debian runtime is decompressed on DATA, native dependencies are
configured and MLauncher plus Store are installed. Do not remove power.

The earlier stages verify the embedded payload, create BOOT, both immutable
system slots and DATA, write and read back both slots, then restart into the
installed system. Relaxing 8-bit music plays independently of this work: F or
Up raises volume, X or Down lowers volume, and M mutes or unmutes playback. The
installer does not wait for a track to finish. From step 7 onward, temporary
recovery SSH is available for the active continuation. A failure screen shows
`pi@DEVICE_IP:22` when an address is available; the temporary password is `pi`.
This recovery account is removed when installation completes.

If step 7 or a later step fails, keep power connected and record the displayed
error. Connect with `ssh pi@DEVICE_IP`, then copy the persistent evidence to a
Windows computer before retrying:

```powershell
scp -O -r pi@DEVICE_IP:/data/oyczero/install .\oyczero-install-recovery
```

Inspect `oyczero-install.log` and `oyczero-default-suite.log` in that directory.
For a one-time transient failure, run `su -`, then `sync` and `reboot`; the
validated continuation retries automatically. Do not delete continuation or
package state by hand. If the failure repeats, keep the logs and rewrite the
card with a newly verified full image. Recovery SSH is unavailable before step
7, so record an earlier console error and reflash instead of repeatedly
interrupting slot or DATA writes.

Starting with 0006, one universal image follows the physical switch. Host
exposes the internal hub and Ethernet. Slave exposes owned USB ADB through
USB-C2. Switching roles does not require a reboot.

On the first normal boot, set an owner password at the local prompt. OycZERO
uses it for root SSH and for the Debian `pi` user, including `sudo`. There is no
permanent default password and no minimum complexity rule beyond one to 100
bytes without line breaks.

## Updating an installed system

A file named `oyczero-BUILD-ID-update.oyu` is not a disk image and must not be
opened with Raspberry Pi Imager. Install the latest stable update on OycZERO:

```sh
oyczero update check
oyczero update install latest
oyczero update status
```

For a package copied to DATA, use its actual path:

```sh
oyczero update install /data/oyczero-BUILD-ID-update.oyu
```

The updater verifies the signed package, writes the inactive system slot and
tries it once. A successful trial becomes the default; a failed trial returns
to the previous slot. DATA is preserved.

## Application packages

Optional DATA-resident tools use `.oyp` packages and their own version numbers.
They are separate from both the initial-install image and the `.oyu` operating-
system update. Follow the package's release notes for compatibility and install
commands.

OycZERO 0011 fresh installations include an offline DATA-resident default
suite: Debian runtime `1.1.9`, official APPLaunch `0.6.111` and its matching
Store. The same immutable release assets can repair or complete an updated
system without replacing DATA.

Install or repair the suite through F3, or run:

```sh
oyczero app install m5launcher
```

The signed `.oyp` initializes the Debian runtime. The two published `.deb`
assets are verified against the release lock and installed inside that runtime;
they are not passed directly to `oyczero app install`. MLauncher is the default
startup target. Esc during its startup countdown keeps Shell for the current
boot. OycZERO 0011 uses a one-second startup countdown. Holding Fn+Esc for
about two seconds exits the running launcher through the host-owned cleanup
path.

The immutable Buildroot host does not provide `apt` or `sudo`. To install a
reviewed local Debian package manually, first copy it into the DATA-resident
Debian root and run `apt` there as root:

```sh
cp /data/PACKAGE_arm64.deb \
  /data/oyczero/apps/debian-runtime/state/rootfs/tmp/
oyczero dev --user root run apt install -y /tmp/PACKAGE_arm64.deb
```

Use `oyczero dev --user root enter` for an interactive Debian shell. The host
BusyBox `wget` supports HTTP/FTP only; use the host `curl -fL` for HTTPS
downloads and save them under `/data`.

At the main OycZERO Shell prompt, F4 prints Debian help, F5 fills the Debian
`pi` Shell command, F6 fills the Debian root Shell command and F7 fills the
root application-profile prefix. These shortcuts never execute a command
automatically. See the [complete user guide](../USAGE.md).
