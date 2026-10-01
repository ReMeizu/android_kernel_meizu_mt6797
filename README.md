# Meizu MX6 kernel

Linux 3.18.22 for the Meizu MX6 (MT6797 / M95).

| Component | Source | Status |
| --- | --- | --- |
| Display | MediaTek DDP, Sharp FT8716 panel | Present in the previously linked device kernel |
| Touch | FocalTech FT8716 | Present in the previously linked device kernel |
| Accelerometer / gyroscope | IIO ST LSM6DS3 | Bounded awake and USB power-transition tests passed on the previous build; deep sleep remains open |
| Wi-Fi | MediaTek gen3 | Driver source included; complete current acceptance remains open |
| GPU / display synchronization | Mali Midgard r12p1 and Android sync fences | Pending-fence close predicate corrected; successor target build and runtime tests pending |

The pending-fence change preserves reference ownership, callback removal and normal signaling. It does not force completion or establish a graphics performance improvement.

`arch/arm64/configs/mx6_verified.config` keeps the previously compiled device configuration, changing only the appended DTB filename. `meizu6797_6c_m_flat.dts` contains the complete previously compiled board tree, including its generated board data; the original DTS and DWS sources are retained. This target does not need the proprietary DCT host executable. Firmware binaries, signing keys, build outputs and private coordination data are excluded.

Use AOSP GCC 4.9 at commit `7a28c220c2e9001825328dca6188ef0077a80a88`, its `real-aarch64-linux-android-gcc` ELF as `CC`, and its original `aarch64-linux-android-ld`. Seed the output `.config` from `mx6_verified.config`, run `olddefconfig`, then build `Image.gz-dtb` with `ARCH=arm64`, `TARGET_BUILD_VARIANT=userdebug` and `HOSTCFLAGS=-fcommon`. The selected DTB must match SHA-256 `fdb55490fdba9d78f4a2d1eedf04091f8b67d0d6253e3852d117402f94303b52`.

This source export has not yet produced a new boot image or passed device acceptance.

GPL licensing information is in [COPYING](COPYING); upstream notes remain in [README](README).
