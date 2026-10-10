# WtfOS osprey manifest

WtfOS ROM variants for the Motorola Moto G3 2015 (`osprey`, MSM8916).
Both variants are experimental device ports.

## ROM variants

| Variant | Android / LineageOS | Kernel | Android userspace | Source branch |
| --- | --- | --- | --- | --- |
| A15 legacy | Android 15 / LineageOS 22.1 | Motorola downstream Linux 3.10 | ARM 32-bit | `lineage-22.1-wtfos` |
| A16 mainline | Android 16 / LineageOS 23.2 | Linux 7 mainline | ARM 32-bit on an ARM64 kernel | `lineage-23.2-mainline` |

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
