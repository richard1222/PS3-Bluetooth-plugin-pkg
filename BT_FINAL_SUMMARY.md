=== PS3 Bluetooth 3rd Party Headphones Research (Rebug 4.84.2) ===
Date: Wed Oct 14 2026

GOAL
Enable 3rd party BT headphones (e.g. Bose QC35) on Rebug 4.84.2. Evilnat 4.93 reportedly has this feature.

FILES COLLECTED
- CFW PUPs in work\ps3_fw\:
  1. REBUG_4.84.2.PUP (212.25 MB) - target base
  2. EVILNAT_4.93_FROM_RAR.PUP (222.56 MB) - compare against
- Extraction dirs: work\ps3_fw_extracted\{rebug,evilnat}

RESEARCH
- Saved: work\ps3_bluetooth_research.txt (detailed plan, module targets, approach)
- Links: work\ps3_bt_links.md (PSX-Place, PS3DevWiki, Rebug, Evilnat)
- Quick guide: work\BT_QUICK_GUIDE.txt

APPROACH
1. Extract PUPs (need PS3 PUP unpacker) to get firmware modules
2. Locate BT modules: likely bluetooth.sprx, libbt.sprx (and related audio routing)
3. Binary diff vs Evilnat 4.93 - find compatibility/whitelist changes
4. Create Cobra .sprx plugin (boot_plugins.txt) or patch modules for Rebug 4.84.2
5. Test on Rebug 4.84.2 with Bose QC35/other headsets

BLOCKER
Need PS3 PUP unpacker tool (PS3-specific; PS4 tool won't work). Once provided, I can extract and analyze.

