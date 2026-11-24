# OrangeFox Recovery patches for LG G7 (judyln)

Unofficial source patches for the LG G7 OrangeFox R11.1-20261121.1 work. This repository is a patch set, not a complete Android build tree or a flashable download.

## Sources

| File | Upstream base |
| --- | --- |
| `patches/recovery.patch` | [OrangeFox Recovery](https://gitlab.com/OrangeFox/bootable/Recovery), `e93fe10c0f58a5f86eff2d986a330bb94f3e880f` |
| `patches/theme.patch` | [OrangeFox theme](https://gitlab.com/OrangeFox/misc/theme), `1ca4c084ad71123763173108b22db7324a35befc` |
| `config/twrp.fstab` | G7 **recovery-only** fstab, used at `/system/etc/twrp.fstab` in the Fox ramdisk; not Android's first-stage fstab |

From each corresponding checkout at the specified revision, run `git apply --check <path-to-patch>` followed by `git apply <path-to-patch>`. Apply the theme patch separately in the `gui/theme` checkout. Both patches passed apply checks against clean archives of those bases. The fstab is provided separately as a device integration input.

## Included changes

- G7 A/B target handling and boot-control compatibility, USB/MTP changes, rear torch support, and release display.
- System, Vendor and OP: ext4 read/write mounting in Fox, offline repair and bounded grow through the native UI. EROFS stays read-only. Maintenance refreshes statistics only for the selected partition and slot. Neither the Android first-stage fstab nor GPT is changed by these patches.
- Source-level regression tests for ext4 maintenance and the torch backend.

## Build and distribution scope

These are selected cumulative source changes. A complete build additionally requires the Android Q build tree, G7 device integration, and device-specific dependencies. A clean, bit-identical reproduction of the previously tested combined boot image has not been established. The image, proprietary LG/Qualcomm binaries, device dumps, build outputs, and logs are not distributed here. The EROFS kernel work is developed separately in [the G7 kernel repository](https://github.com/Fer1d/android_kernel_lge_sdm845); the tested image used the kernel from the build associated with `1c78b1d82df5`, not the later zram changes.

See `NOTICE` and the original source headers for license and attribution. This project is not an official OrangeFox release.
