<p align="center">
    <img width="25%" height="25%" alt="logo2" src="https://github.com/user-attachments/assets/5596a357-61c3-471c-9a1e-b8c3d6de33c8" />
</p>

<h1 align="center"> Vue-After-Free — 5.05 to 13.04 </h1>
<p  align="center">
    PlayStation Vue userland code execution exploit for PS4, with the 663 (Relapse) entry.
</p>

> [!NOTE]
> 1. This is a port of [Vuemony/vue-after-free](https://github.com/Vuemony/vue-after-free). and fork of [Francis-play/vue-663](https://github.com/Francis-play/vue-663) solely for the purpose of keeping it simple.
> 2. **The goal of this repository is to enable *jailbreaking* on firmware versions 13.02 and 13.04 by using the VUE method—whether because you prefer to avoid using WebKit, because you need a local method, or because WebKit causes stability issues for you.**
> 3. It is not possible to use Vue on version 13.52; Sony has disabled the Vue application for those versions.

# Compatibility (choose by firmware)

| vue-after-free (Userland) | Lapse (KEX) | Netctrl (KEX) | Relapse / 663 (KEX) |
| :------------------------ | :---------- | :------------ | :------------------ |
| 5.05–13.04                | 1.01–12.02  | 1.01–13.00    | 13.02–13.04 (stable) · 12.50–13.00 (experimental) |

* 663 (Relapse) is **this repo's** entry. Relapse itself supports up to **13.52**, but this repo only ships **13.02–13.04** as tested; **12.50 / 12.52 / 13.00** are new and **experimental** (kernel table cross-validated, **not yet hardware-tested** — on failure they fall back to Netctrl automatically).
* Any other firmware keeps using Lapse / Netctrl.
* The userland exploit works 5.05–13.04 as is.

## Requirements
* Jailbreak using WebKit (for example: https://webkitty.arabpixel.net/) _Don't worry, this will be the last time, and it's only for configuring VUE._
* Any kind of network connection to launch the app.
* Fake or legit activated PS4 user account.
* FTP access to the console
* PlayStation Vue 1.01 base + 1.24 patch, if installing fresh. [Download](https://www.mediafire.com/file/45owcabezln2ykm/CUSA00960.zip/file)

# Changing NP Environment (Highly recommended)
Relying solely on DNS or payloads to block update downloads leaves the door open for Sony to push updates to PS Vue that could end up breaking the method.

By modifying the environment name, the console attempts to communicate with a server path different from the one used in the retail version. Since Sony’s public servers do not recognize this new identifier, communication with the official PlayStation Network (PSN) is severed, which prevents the use of online features. Furthermore, the console loses the ability to verify, search for, or download firmware, application, or game updates over the network—even when attempting to perform these actions manually.
  1. First, enable debug settings by going to Goldhen>Debug Settings> Enable Debug Settings and choose Full Menu.
  2. Navigate to Settings → Scroll to the bottom and find Debug settings → PlayStation Network → NP Environment, and simply change it from np to anything else (do not set it to sp-int), for example: noupdt123 and PS4 it will restart.
  3. This setting persists after a restart, entering sleep mode, or switching to a different internet network.

# Setup Instructions
  1. Jailbreak your console. _Don't worry, this will be the last time, and it's only for configuring VUE._
  2. Enable FTP.
  3. Install Apollo Save Tool. [Download](https://github.com/bucanero/apollo-ps4/releases/latest)
  4. Download PS Vue 1.01 pkg and 1.24 patch and place them on the USB. [Download](https://www.mediafire.com/file/45owcabezln2ykm/CUSA00960.zip/file)
  5. Open Apollo Save Tool and fake activate your account by going to `User Tools`>`Activate PS4 Accounts` then press R2 then X and then keep pressing `O` till you are asked if you want to exit to the XMB accept with `X` then restart the console and jailbreak again.
  6. Connect to the console with FTP.
  7. Download the `VueManualSetup_13.04.zip` or `VueLiteManualSetup_13.04.zip` from releases. If you choose Lite mode, the exploit will launch automatically as soon as you open the application—following the initial prompt—and will select the appropriate exploit; 12.02 and lower → Lapse; 12.50–13.00 → Relapse (reverts to "NETCTRL-FALLBACK" in the log if the experimental tables are missing); 13.02–13.04 → Relapse.
  8. Go to the following path with FTP `/user/download/CUSA00960/` (create path if needed) and place `download0.dat` there.
  9. On your USB unpack the save.zip ( or FTP to `/data/fakeusb/` ). The files will show up in USB Saves as if it is a real USB. It can be toggled in Apollo Settings>USB Saves Sources to be the only thing displayed even while a real USB is plugged in.
  11. Plug the USB into the console.
  12. In Apollo Save Tool go to USB Saves and select the PS Vue save(CUSA00960) and choose the option "Copy save game to HDD".
  13. Install PS Vue from your package installer, make sure `Background Installation` is off press on yes when it asks if you want to install it again (only for 1.01) then install the 1.24 patch. 
  14. Reboot your console
  15. Next **without performing a jailbreak** open PS Vue; a message will appear stating: "This service requires you to sign in to PlayStation Network." Select "Accept" to continue. Execute the exploit by pressing the "jailbreak" button, or configure the "autoloader" and "auto close" options. Please note that if you are using HEN, you must edit the `config.json` file before configuring the "auto close" feature; add 20 seconds to the closing timeout by entering the value `20000`.

# Config -Not for VUE Lite-
For some config changes to apply, the application must be closed and opened again.
**These do not apply to the VUE Lite package; it automatically selects the most suitable options for the console.**
Vue comes with a few custom options. The **Jailbreak button** auto-detects firmware and picks the matching exploit. In the config menu, under **JB Behavior**, you can choose:
  * **Auto Detect** — default. Below 12.50 → Lapse. 12.50–13.00 → Relapse (experimental, auto Netctrl fallback). 13.02/13.04 → Relapse.
  * **Lapse** — forced, 7.00–12.02.
  * **NetControl** — forced, 12.50–13.00 (runs on 9.00+).
  * **Relapse (663)** — forced. Stable on 13.02–13.04; experimental on 12.50/12.52/13.00 (fails safe back to Netctrl).

Other options: **Auto Lapse** / **Auto Relapse** (launch a kernel exploit on opening the app), **Auto Close** (close the app after a successful jailbreak), **Auto GoldHEN** (see below), **Music** (on/off — background music loads only after the jailbreak finishes, never during the exploit), **Theme**.

### Auto GoldHEN
Default **ON**. Controls which HEN-family payload is applied:
* **ON** — the auto payload is GoldHEN, shipped as `payload.bin` (app root) and loaded first by binloader.
* **OFF** — GoldHEN is not downloaded/applied; `hen.bin` (in `payloads/`) is loaded instead. The app warns "GoldHEN auto OFF".

The updater honors this: if GoldHEN is already present it is not re-downloaded; if missing and the switch is ON it is downloaded and applied; if OFF, HEN is applied instead.

# Payloads
Vue After Free comes preloaded with some payloads.

> [!IMPORTANT]
> The np-fake-signin should not be run on a real PSN account.

## FTP
The `ftp-server.ts` payload gives you sandbox FTP to quickly swap exploit or cosmetic files without running a kernel exploit.

## ELFLDR
`elfldr.elf` is used to load elf and bin payloads post-exploit when HEN or GoldHEN have not been loaded.

## WebUI
Example code for running userland code with the browser as the UI (possible alternative to jsmaf).

# Themes
Themes can be added by copying the folder to `/download0/themes/`. The default theme is a good example.

# FAQ & Troubleshooting

**Q: Will this work on 13.02 or above?**
Only the userland and the 663 (Relapse) entry. This repo ships **13.02–13.04** stable; **12.50/12.52/13.00** are experimental with automatic Netctrl fallback. Relapse supports up to 13.52, but files above 13.04 are not provided here yet.

**Q: Do I need an internet connection?**
You need any form of a network connection, not specifically internet. Vue will not launch the exploit without one and will show "There was a problem connecting to the internet". See [Connecting to the internet](#connecting-to-the-internet).

**Q: I am getting "There is a network communication issue".**
Your Vue app most likely updated. Changing NP Environment and reinstall VUE.

**Q: I am getting "This service requires you to sign in to PlayStation Network" even after replacing the save file.**
Your Vue app most likely updated. Changing NP Environment and reinstall VUE.

**Q: I ran Vue and the app crashed / the console shut down.**
The exploit failed. If it crashed, shut down and retry. On a kernel panic, press the power button twice, then retry.

**Q: How can I run a payload?**
Closing and reopening Vue is required between running JS payloads, but `.bin` / `.elf` payloads can be run one after the other from the Payload Menu.

**Q: My payload is not recognized.**
Format your USB drive as MBR partition and exFAT.

**Q: The updater says a bin is "FTP needed".**
The downloaded size did not match, so it was discarded on purpose. Send that bin to `payloads` over FTP once.

**Q: Which exploit ran on my firmware?**
The on-screen log says it: 12.02 and below → Lapse; 12.50–13.00 → Relapse (falls back to "NETCTRL-FALLBACK" in the log if the experimental tables miss); 13.02–13.04 → Relapse.

# Credits
Port / 663 (Relapse) entry: francis-play.

Based on [Vuemony/vue-after-free](https://github.com/Vuemony/vue-after-free) and [Francis-play/vue-663](https://github.com/Francis-play/vue-663):
- [c0w-ar](https://github.com/c0w-ar/) — Lapse and NetCtrl porting, Reverse Engineering
- [earthonion](https://github.com/earthonion) — UI, initial JS injection, Payload host, Netctrl porting, binloader, Reverse engineering and remote installer
- [ufm42](https://github.com/ufm42) — Userland Exploit and reverse engineering
- [D-Link Turtle](https://github.com/iMrDJAi) — General support for userland exploitation
- [Gezine](https://github.com/gezine) — Local JS method and PSN bypass research
- [Helloyunho](https://github.com/Helloyunho) — TypeScript port, Reverse Engineering
- [Dr.Yenyen](https://github.com/DrYenyen) — Extensive testing, quality control, end-user support/ideas, system backup and extended storage method
- [AlAzif](https://github.com/Al-Azif) — Reference for exploit table, retail application advice, Lapse AIO Fix kpatches and 12.50-13.00 kpatches
- abc — Lapse
- [TheFlow](https://github.com/TheOfficialFloW) — NetCtrl
- [Lua Loader project](https://github.com/shahrilnet/remote_lua_loader) — Remote Lua loader foundation
- [Cryptogenic](https://github.com/Cryptogenic/PS4-6.20-WebKit-Code-Execution-Exploit) — Reference for CVE-2018-4441
- [rebelle3](https://github.com/rebelle3/cve-2017-7117) — Reference for CVE-2017-7117

Relapse AIO multi-cancel KEX based on [jb-polpno](https://github.com/mansoor0x0/jb-polpno) by mansoor0x0.

## payload sources:
- [elfldr.elf](https://github.com/ps4-payload-dev/elfldr) by John Törnblom
- [AIOfix_network.elf](https://github.com/Gezine/BD-JB-1250/blob/main/payloads/lapse/src/org/bdj/external/aiofix_network.c) by Gezine
- [np-fake-signin](https://github.com/earthonion/np-fake-signin) by earthonion
