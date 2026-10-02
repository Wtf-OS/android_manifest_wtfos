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
