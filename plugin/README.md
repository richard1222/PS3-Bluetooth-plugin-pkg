# PS3 Bluetooth Headphone Audio — the real solution

## TL;DR
A hand-written "Cobra plugin" is **not** the right way to get third‑party
Bluetooth headphones (Bose QC35 etc.) playing game audio on the PS3, and it
is not needed — a working solution already exists.

The PS3 firmware has **no A2DP** (stereo / high-quality Bluetooth audio). That is the
real limitation; no `.sprx` can add it. The PS3 can only use a BT headset's
**HSP/HFP voice** channel (mono). The community fix is to **re-route game
audio into that voice stream** by swapping one module:

    /dev_flash/sys/external/libaudio.sprx   (stock: ~15 KB)

with a **patched libaudio.sprx**. That patched module *is* the "plugin".

Credit: libaudio patch reverse‑engineered by **Zer0xFF** for CFW
(PS3Xploit team did the HEN version); installer PKGs by **Coro**
(PSX‑Place) and **aldostools** (webMAN MOD).

## Why the stub in `plugin/` can't become the real thing
* Requires the Sony PS3 SDK (`ppu-gcc`/`cell`) to build a PRX — not available here.
* Even with the SDK, an external plugin cannot add A2DP (no codec/stack in firmware).
* The correct intervention is the `libaudio.sprx` swap, which is a *module patch*,
  not a standalone plugin. Writing our own would just be a worse copy of Zer0xFF's work.

## How to apply (CFW, e.g. Rebug 4.84.2)
Get the files from the releases folder on the Desktop (`PS3 BT Audio/`):
* `install_libaudio_patched.pkg` — enable
* `install_libaudio_original.pkg` — revert

**webMAN MOD method:** install the patched PKG → reboot → pair headset →
Audio Device Settings → pick the headset → OK → start a game.

**dev_blind method:** overwrite `/dev_blind/sys/external/libaudio.sprx`
(back up the original first) → reboot.

webMAN MOD auto-maps `/dev_hdd0/tmp/libaudio.sprx` at boot.

## Result / limits
* Works, but **mono / low quality** (rides the compressed voice channel).
* Headset must still **pair** normally, else the patch does nothing.
* **Deal-breaker on many modern headsets:** the moment the PS3 is told to use the
  headset as the *audio output device* it opens the HSP/SCO **voice link**, and
  some headsets (e.g. Bose QC35) **drop that link after a few seconds**. The
  patch cannot fix a link that will not stay up.

## When the software patch cannot help (headset keeps dropping)
The PS3's Bluetooth only carries the **chat / HSP** channel. It was never built
for A2DP, so it is picky about non‑Sony headsets. If the headset disconnects a
few seconds after you assign it as output, stop fighting the radio and move the
audio off Bluetooth — the PS3 then treats it as a normal audio device and the
link is rock solid.

Two reliable hardware routes (no libaudio patch needed):

1. **USB Bluetooth transmitter (recommended).**
   A USB dongle that presents itself as a **USB sound card**. The PS3 sends full
   **stereo game audio** to it and the dongle does A2DP to the headset.
   PS3 sees native USB audio; the headset is paired to the *dongle*, not the PS3.

2. **Optical (TOSLINK) Bluetooth transmitter.**
   PS3 → `Settings > Sound Settings > Audio Output Settings > Optical Digital`
   → transmitter → A2DP → headset. Works with any PS3 revision and gives stereo.

Either way: **pair the QC35 to the transmitter, unpair it from the PS3**, and you
get stereo game audio with a stable link.

### Codec caveat (Bose QC35)
The QC35 (I/II) supports only **SBC + AAC** — no aptX / aptX LL / LDAC. So every
transmitter falls back to SBC for it (**~150–250 ms lag**). A transmitter fixes
the *connection* and gives **stereo**, but never the latency. For lag-free play,
a wire is the only option.

### Recommended transmitters (US prices, ~2026 — fluctuate)
Optical route (safest on PS3):
* **Avantree Audikast 3** — ~$50 (Audikast 4 ~$60)
* **Avantree Oasis Plus 2** — ~$60–80 (optical pass-through)
* **1Mii B03 / B03Pro** — ~$50 / ~$66 ; **1Mii ML300** ~$30 ; **1Mii B06TX** ~$22

USB route (convenient, but PS3 USB-audio is picky; marketed for PS5/PS4/PC, not PS3):
* **Avantree DG80P / DG60P** — ~$30–40

Optical setup: transmitter optical-in → PS3 `DIGITAL OUT (OPTICAL)`; PS3
`Audio Output Settings > Optical Digital` set to **Linear PCM 2 Ch.** (no
Dolby/DTS); pair QC35 to the **transmitter**.

## Sources
* https://github.com/aldostools/webMAN-MOD/issues/493
* https://github.com/aldostools/Resources/releases (Addons)
* https://www.psx-place.com/threads/get-game-audio-sound-from-headset-bluetooth-usb-not-only-in-chat.26999/
* https://manuals.playstation.net/document/en/ps3/current/settings/audiodevice.html

## Sources
* https://github.com/aldostools/webMAN-MOD/issues/493
* https://github.com/aldostools/Resources/releases (Addons)
* https://www.psx-place.com/threads/get-game-audio-sound-from-headset-bluetooth-usb-not-only-in-chat.26999/
