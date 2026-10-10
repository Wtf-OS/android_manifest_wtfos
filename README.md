# WtfOS osprey manifest

Local manifest overrides for WtfOS (Lineage 22.1, Moto G3 osprey).

## Sync

```
repo init -u https://github.com/LineageOS/android -b lineage-22.1 --git-lfs
cp wtfos.xml .repo/local_manifests/
repo sync
```

All WtfOS changes live on branch `lineage-22.1-wtfos` in the
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

The sync instructions and `wtfos.xml` above describe the Android 15 / kernel
3.10 port; they do not select the Android 16 mainline ROM.
