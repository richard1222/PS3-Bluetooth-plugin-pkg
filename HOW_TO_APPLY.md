HOW TO APPLY A COBRA .sprx PLUGIN ON REBUG 4.84.2

1. Get the plugin file (.sprx)
   - Place it on USB/FTP: e.g. /dev_hdd0/plugins/btfix.sprx or /dev_usb000/plugins/btfix.sprx

2. Edit boot_plugins.txt
   - On Rebug with Cobra, boot_plugins.txt tells Cobra which .sprx to load at boot
   - Can be in /dev_hdd0/boot_plugins.txt or /dev_flash/vsh/etc/boot_plugins.txt (changes persist)
   
   Example:
   /dev_hdd0/plugins/btfix.sprx

   Or if on USB:
   /dev_usb000/plugins/btfix.sprx

3. Install & reboot
   - Save boot_plugins.txt, reboot PS3
   - Plugin loads on boot

4. Test Bluetooth
   - Try pairing Bose QC35 etc
   - Check audio output in Settings > Sound Settings > Audio Output Settings

NOTES
- Wrong plugin can cause freeze at boot - keep recovery in mind (safe mode)
- Plugin must be built for PS3 Cell (SPRX) and be Cobra-compatible
- Rebug 4.84.2 uses Cobra 8.1 - compatibility matters
- Best is a tested plugin for Rebug 4.84.x

KNOWN PLUGINS TO LOOK FOR
- Check PSX-Place resources: search "Bluetooth A2DP plugin Rebug"
- webMAN MOD has some BT related stuff but not main focus
- Some forks of Cobra plugins for BT exist

