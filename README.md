# WtfOS osprey manifest

WtfOS ROM variants for the Motorola Moto G3 2015 (`osprey`, MSM8916).
All variants are experimental device ports.

## ROM variants

| Variant | Android / LineageOS | Kernel | Android userspace | Source branch |
| --- | --- | --- | --- | --- |
| A15 legacy | Android 15 / LineageOS 22.1 | Motorola downstream Linux 3.10 | ARM 32-bit | `lineage-22.1-wtfos` |
| A16 mainline | Android 16 / LineageOS 23.2 | Linux 7 mainline | ARM 32-bit on an ARM64 kernel | `lineage-23.2-mainline` |
| A17 mainline | Android 17 / LineageOS 24.0 | Linux 7 mainline | ARM 32-bit on an ARM64 kernel | `lineage-24.0-mainline` |

Machine-readable declarations are in [variants.json](variants.json).
The branches contain different device configurations, kernels and hardware
integration; select the sources belonging to the intended variant.

## Android 15 legacy ROM

This variant uses the Motorola downstream kernel and legacy Qualcomm/Motorola
hardware integration, adapted from the older osprey port. Its WtfOS overrides
are declared in [wtfos.xml](wtfos.xml). These overrides complement a LineageOS
22.1 checkout and its device/kernel/vendor dependencies; they are not a full
standalone manifest.

### Sync overrides

```
repo init -u https://github.com/LineageOS/android -b lineage-22.1 --git-lfs
cp wtfos.xml .repo/local_manifests/
repo sync
```

The Android 15 legacy overrides select `lineage-22.1-wtfos` in the
[Wtf-OS](https://github.com/Wtf-OS) forks.

## Android 16 mainline ROM

An experimental Moto G3 (`osprey`) ROM also exists based on **LineageOS 23.2
(Android 16)** and **Linux 7 mainline**, with an ARM64 kernel and 32-bit Android
userspace. It boots to the Android UI and has working GPU acceleration, Wi-Fi,
Bluetooth, audio and camera support; camera quality, performance and stability
remain experimental.

Its sources use the separate `lineage-23.2-mainline` branch in the Wtf-OS forks.
See [osprey-mainline](https://github.com/Wtf-OS/osprey-mainline/tree/lineage-23.2-mainline)
for pinned source revisions and the
[Android 16 port notes](https://github.com/Wtf-OS/osprey-mainline/blob/lineage-23.2-mainline/android16/README.md)
for packaging, installation history and known limitations.

The A16 source checkpoint includes device integration, libcamera, graphics,
Wi-Fi and runtime fixes. The kernel and libcamera revisions are recorded in
[`kernel-source-revision.json`](https://github.com/Wtf-OS/osprey-mainline/blob/lineage-23.2-mainline/android16/kernel-source-revision.json)
and [`libcamera-source-revision.json`](https://github.com/Wtf-OS/osprey-mainline/blob/lineage-23.2-mainline/android16/libcamera-source-revision.json);
Android component revisions are in
[`component-revisions.json`](https://github.com/Wtf-OS/osprey-mainline/blob/lineage-23.2-mainline/component-revisions.json).

A16 uses separate boot-package inputs and mainline hardware drivers, with
libcamera software image processing. Kernel/module builds, firmware and
packaging inputs still need separate preparation. The checkpoint is not a
complete standalone build manifest, and this repository does not yet provide
an A16 `repo sync` manifest. The A15 commands above select only the legacy ROM.

## Android 17 mainline ROM

The A17 port boots on osprey. Source commits are published separately on
`lineage-24.0-mainline`. [a17.xml](a17.xml) pins the Android checkout;
[osprey-mainline/android17](https://github.com/Wtf-OS/osprey-mainline/tree/lineage-24.0-mainline/android17)
records the separate kernel/libcamera inputs and seven patch-only dependencies.

```sh
repo init -u https://github.com/Wtf-OS/android_manifest_wtfos -b lineage-24.0-mainline -m a17.xml --git-lfs
repo sync
```

Apply the seven dependency patch queues from the source checkpoint after sync,
including Camera2 and TimeKeep. Their upstream base commits remain pinned here.
This manifest does not supply generated kernel modules, lk2nd or boot-package
assets. Follow the checkpoint notes before building or packaging; this is not
a complete one-command build. Radio without SIM is available for bring-up,
but cellular calls/data are untested. Suspend is s2idle; display PLL retuning
is fixed in the latest brightness/wake check. SELinux is Enforcing and KeyMint
is software-only. External backlight shutdown, persistent time restoration and
USB reconnection with the screen asleep have passed hardware checks. Camera
quality, long-term stability and standby drain remain experimental.
