# Local manifest for the Redmi Pad (yunluo), LineageOS 24.0

This local manifest adds the device-specific repositories needed to build
LineageOS 24.0 (Android 17) for the Xiaomi Redmi Pad, codename `yunluo`
(MediaTek MT6789).

## Repositories

| Path | Repository | Revision |
| --- | --- | --- |
| `device/xiaomi/yunluo` | [damnms/android_device_xiaomi_yunluo](https://github.com/damnms/android_device_xiaomi_yunluo) | tag `yunluo-24.0-20261111` |
| `device/xiaomi/yunluo-kernel` | [damnms/android_device_xiaomi_yunluo-kernel](https://github.com/damnms/android_device_xiaomi_yunluo-kernel) | tag `yunluo-24.0-20261111` |
| `vendor/xiaomi/yunluo` | [damnms/android_vendor_xiaomi_yunluo](https://github.com/damnms/android_vendor_xiaomi_yunluo) | tag `yunluo-24.0-20261111` |
| `hardware/mediatek` | [damnms/android_hardware_mediatek](https://github.com/damnms/android_hardware_mediatek) | tag `yunluo-24.0-20261111` |
| `device/mediatek/sepolicy_vndr` | LineageOS, unchanged | pinned commit |
| `hardware/xiaomi` | LineageOS, unchanged | pinned commit |

Every revision is fixed, so a sync always gives the exact sources of
build `20261111`. The rest of the tree comes from the LineageOS manifest,
branch `lineage-24.0`.

## Usage

```bash
mkdir -p ~/android/lineage && cd ~/android/lineage
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs --no-clone-bundle
git clone https://github.com/damnms/android_local_manifests_yunluo.git .repo/local_manifests
repo sync -c -j16 --no-tags
```

Build:

```bash
source build/envsetup.sh
breakfast yunluo userdebug
m bacon -j16
```

The result is
`out/target/product/yunluo/lineage-24.0-<date>-UNOFFICIAL-yunluo.zip`.

## Notes

- Release builds are signed with private keys that are not part of any
  repository. Without your own keys in `vendor/lineage-priv/keys`, the
  build is signed with the public test keys.
- The Soong analysis needs more than 42 GB of memory (RAM plus swap).
  With 32 GB RAM, add zram and a swap file before building.
- The device uses Virtual A/B. When installing from recovery, format
  data first, then sideload, then reboot. Formatting data after the
  sideload discards the pending update.
