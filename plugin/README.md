# PS3 Bluetooth Fix Plugin (btfix.sprx)

## Status: STUB
This is a placeholder plugin. The actual implementation requires extracting and diffing firmware modules.

## Why stub?
To build the real fix, we need to:
1. Extract bluetooth.sprx and libbt.sprx from both PUPs (REBUG_4.84.2.PUP and EVILNAT_4.93_FROM_RAR.PUP)
2. Find what Evilnat patched to allow 3rd party BT headsets
3. Write hooks to replicate those patches for Rebug 4.84.2 (Cobra 8.1)

## Build Requirements
- PS3 SDK / ps3dev toolchain (ppu-gcc, make)
- Cobra SDK headers (for PRX/plugin development)
- Properly set CELL_SDK environment variable

## Installation
1. Build btfix.sprx (when implemented)
2. Copy to /dev_hdd0/plugins/
3. Add to /dev_hdd0/boot_plugins.txt: /dev_hdd0/plugins/btfix.sprx
4. Reboot