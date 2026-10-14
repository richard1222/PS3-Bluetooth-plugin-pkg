# PS3 Bluetooth Plugin for 3rd Party Headphones (Rebug 4.84.2)
Repo reference: https://github.com/richard1222/PS3-Bluetooth-plugin-pkg

## Goal
This project replicates Evilnat 4.93's expanded Bluetooth support on Rebug CFW 4.84.2 to allow 3rd party Bluetooth headphones (Bose QC35/QC45, Sony WH-1000XM3/4, JBL, etc.) to pair and get proper A2DP stereo audio.

## Problem
The PS3's stock/Sony Bluetooth stack restricts device compatibility via whitelist/compatibility checks (device class, profiles, SDP negotiation). Modern Bluetooth headsets often fail these checks - either won't pair, or connect as HSP only (mono/low quality) instead of A2DP stereo.

## What Evilnat 4.93 Changed
Evilnat 4.93 reportedly expanded Bluetooth device compatibility. Based on research, likely changes are in:
- /dev_flash/sys/internal/bluetooth.sprx - main BT stack, device validation/whitelist
- /dev_flash/sys/external/libbt.sprx - BT library functions, profile handling

## Research Done

### CFW Files Analyzed
- REBUG_4.84.2.PUP (target base) - work/ps3_fw/REBUG_4.84.2.PUP
- EVILNAT_4.93_FROM_RAR.PUP (reference with fix) - work/ps3_fw/EVILNAT_4.93_FROM_RAR.PUP

### Files Created
- work/PS3_BT_HEADPHONES_README.md - Detailed research
- work/ps3_bluetooth_research.txt - Full research/plan
- work/ps3_bt_links.md - Useful links (PSX-Place, PS3DevWiki, Rebug, Evilnat)
- work/BT_FINAL_SUMMARY.txt - Complete status
- work/HOW_TO_APPLY_BT_PLUGIN.txt - Installation instructions for plugin
- work/BT_PLUGIN_TEMPLATE.txt - Technical details
- work/ps3_bt_status.txt - Current state

## Technical Approach
Create a Cobra .sprx (PRX) plugin that hooks the BT stack at runtime to bypass restrictive checks. This is safer than replacing firmware modules (reversible, less risk of bricking).

Plugin approach:
1. Extract bluetooth.sprx and libbt.sprx from both PUPs
2. Binary diff to identify Evilnat's patches
3. Hook equivalent functions in Rebug 4.84.2 (Cobra 8.1) to apply same behavior
4. Load via boot_plugins.txt

## Current Status - BLOCKED
We need a PS3-specific PUP unpacker to extract firmware modules from the PUP files. PS4 unpackers don't work for PS3 PUP format. Once extracted, diffing and plugin creation is feasible with ps3dev toolchain.

## How To Apply (When Plugin Available)
1. Copy btfix.sprx to /dev_hdd0/plugins/
2. Add to /dev_hdd0/boot_plugins.txt:
   /dev_hdd0/plugins/btfix.sprx
3. Reboot on Rebug 4.84.2 (Cobra 8.1)
4. Pair 3rd party BT headphones, test A2DP

## Contributing
To help complete this:
1. Provide a PS3 PUP unpacker (puad_gui, ps3pupunpack, etc.)
2. Or extract bluetooth.sprx and libbt.sprx from both PUPs and share them
3. Test and report results

## Safety
Use at your own risk. Plugin loading via Cobra is reversible - remove from boot_plugins.txt to disable. Keep safe mode recovery option available.

## Links
- PSX-Place: https://www.psx-place.com/
- PS3DevWiki: https://wiki.psdevwiki.com/ps3/Bluetooth
- Rebug: https://rebug.me/
- Evilnat: https://github.com/Evilnat
