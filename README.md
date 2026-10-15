# PS3 Bluetooth Plugin for 3rd Party Headphones (Rebug 4.84.2)

This project aims to enable 3rd party Bluetooth headphones (Bose QC35/QC45, Sony WH-1000XM3/4, etc.) to work properly with A2DP audio on **Rebug CFW 4.84.2** by replicating the expanded Bluetooth support found in Evilnat 4.93.

## Background

The PS3's Bluetooth stack has strict device compatibility checks. Many modern Bluetooth headsets fail to pair or connect without stereo A2DP audio. Evilnat 4.93 expanded this support, and this project aims to bring similar functionality to Rebug 4.84.2 (Cobra 8.1).

## Research Summary

- **Base firmware:** Rebug 4.84.2 (target)
- **Reference firmware:** Evilnat 4.93 (expanded BT support)
- **Target modules:** luetooth.sprx (internal) and libbt.sprx (external) in firmware
- **Approach:** Create a Cobra .sprx plugin that hooks the relevant BT functions at runtime (safer than replacing firmware modules)

## Work Done

CFW PUPs collected and ready for analysis:
- REBUG_4.84.2.PUP (212.25 MB)
- EVILNAT_4.93_FROM_RAR.PUP (222.56 MB)

All research documentation is available in the repo/workspace files.

## How to Use (When Plugin is Released)

1. Place tfix.sprx in /dev_hdd0/plugins/ on your PS3
2. Create or edit /dev_hdd0/boot_plugins.txt and add:
   `
   /dev_hdd0/plugins/btfix.sprx
   `
3. Reboot with Rebug 4.84.2 + Cobra 8.1
4. Pair your 3rd party Bluetooth headphones and test A2DP audio

## Status

**Currently blocked:** Need PS3 PUP unpacker to extract firmware modules from both PUPs and perform binary diff against Evilnat to identify exact patches. Once extracted, the Cobra plugin can be built.

## Safety Notes

- Using custom plugins carries risk - wrong plugin can cause boot freeze. Keep PS3 recovery/safe mode in mind.
- Plugin must be Cobra-compatible (Cobra 8.1 on Rebug 4.84.2).
- This is reversible - just remove the line from boot_plugins.txt and delete the sprx.

## Plugin Status
The plugin in plugin/ is currently a **stub**. It compiles but does not yet contain the actual BT patches. The real patches require extracting and diffing luetooth.sprx/libbt.sprx from the CFW PUPs.


## Blocker Update
PUPExtractor GUI provided but requires manual interaction. Need CLI PS3 PUP unpacker or manual extraction. CFW PUPs available: REBUG_4.84.2.PUP and EVILNAT_4.93_FROM_RAR.PUP in work/ps3_fw/.

---

## Community

- **Discord:** unosdopplegange
- **Discord server:** https://discord.gg/MDcaC5nPuA
