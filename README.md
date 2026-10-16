# Lenovo ThinkPad X380 Yoga - OpenCore Configuration

<img align="right" src="https://p1-ofp.static.pub/medias/bWFzdGVyfHJvb3R8MzY5NzQ4fGltYWdlL3BuZ3xoMTEvaGMwLzE0NDQ4MTg0NTI0ODMwLnBuZ3wyZjE4MmQ5YmEyN2U1M2VhOTJkZDM4NzFjMTUzNDk2M2NmOGQ5OTQ2MjYxNTVlNjY3YmYxMTU4ZDM2Y2RmNjlk/lenovo-laptop-thinkpad-x380-2-in-1-hero.png" alt="macOS running on the X380 Yoga" width="425">

[![macOS](https://img.shields.io/badge/macOS-Ventura-brightgreen.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sonoma-brightgreen.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sequoia-brightgreen.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.8-blue.svg)](https://github.com/acidanthera/OpenCorePkg)
[![Model](https://img.shields.io/badge/Model-20LJ-9cf)](https://psref.lenovo.com/syspool/Sys/PDF/ThinkPad/ThinkPad_X380_Yoga/ThinkPad_X380_Yoga_Spec.PDF)
[![BIOS](https://img.shields.io/badge/BIOS-1.41-blue)](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x380-yoga/downloads/driver-list/component?name=BIOS%2FUEFI&id=5AC6A815-321D-440E-8833-B07A93E0428C)
[![issues](https://img.shields.io/github/issues/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh)](https://github.com/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh/issues)
[![last commit](https://img.shields.io/github/last-commit/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh)](https://github.com/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh/commits/main)
[![License](https://img.shields.io/badge/license-MIT-purple.svg)](/LICENSE)

**DISCLAIMER:**  
This OpenCore EFI works fine on my Thinkpad X380 Yoga. 
As you embark on your Hackintosh journey you are encouraged to **READ** the entire README and [Dortania](https://dortania.github.io/getting-started/) guides before you start to get an understanding of the install process. It will save many a message instructing you to read the manual. 

With that said I'm happy to help when/where I can. When you encounter bug or want to improve this repo, consider opening an issue or pull request. You can also find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

## 📑 Contents

- [Introduction](#-introduction) — hardware specs & required tools
- [Installation](#-installation) — create installer, BIOS settings, Apple Services
- [Post-install](#-post-install-optional) — audio, Wi-Fi, fingerprint reader, power, USB mapping
- [Other tweaks](#️-other-tweaks) — HiDPI, YogaSMC, shortcuts, assistants, dock, dual-boot clock, hibernation
- [Status](#-status) — what works / doesn't
- [Performance](#-performance) — benchmarks
- [Credits](#credits)

## 👋 Introduction

<details>  
<summary><strong>📖 Getting started</strong></summary>
</br>

**Meet the Bootloader:**

- [Why OpenCore](https://dortania.github.io/OpenCore-Install-Guide/why-oc.html)
- Dortania's [website](https://dortania.github.io)

**Recommended tools:**

- Plist editor [ProperTree](https://github.com/corpnewt/ProperTree)
- Handy-dandy ESP mounting script [MountEFI](https://github.com/corpnewt/MountEFI)
- Cross-platform GUI management tools for OpenCore [OCAT](https://github.com/ic005k/OCAuxiliaryTools)
- Py script that uses acidanthera's macserial to generate SMBIOS [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- The Swiss army knife of vanilla Hackintoshing [Hackintool](https://github.com/benbaker76/Hackintool)

**Resources**

- [OpenCore](https://github.com/acidanthera/OpenCorePkg)

</details>

<details> 
<summary><strong>💻 My Hardware</strong></summary>
</br>

| Category  | Component                                            | Note                                                         |
| --------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| Type      | 20LJ                                                 |                                                              |
| CPU       | Intel(R) Core(TM) i5-8350U CPU @ 1.70GHz             |                                                              |
| GPU       | Intel UHD 620                                        |                                                              |
| SSD       | Lexar NM620 512GB M.2 NVMe SSD                       | Replaced cursed PM 981 which still doesn't work reliably. Read this [Anti-Hackintosh Buyers Guide - Storage](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/Storage.html)     |
| Screen    | 13.3" FHD 1920x1080                                  | Multi touch and pen* support working                         |
| Memory    | 16GB DDR4 2400Mhz                                    |                                                              |
| Camera    | 720p Camera + IR Camera                              |                                                              |
| Audio     | Conexant® CX8200                                     | I suggest trying several layout ID `3, 15, 21, 23, or 80`    |
| Touchpad  | ELAN v4 LEN2034 PS2 Interface                        | If the Trackpad is not working properly, try disabling the Trackpoint in the BIOS. |
| Wifi & BT | Intel AC 8265 and Bluetooth                          | Native Wi-Fi on Sequoia via [itlwm](https://github.com/laobamac/itlwm) (no HeliPort / OCLP patch needed). |
| Ethernet  | Intel I219-LM4 Gigabit Ethernet                      |                                                              | 
| Input     | PS2 Keyboard & I2CHID TrackPad (touchscreen and pen) | I'm using [YogaSMC](https://github.com/zhen-zen/YogaSMC) for media keys. The kext is in the folder but **you must install the YogaSMC app separately.** |

</details>

<details>
<summary><strong>📦 Main software</strong></summary>

| Component     | Version |
| ------------- | ------- |
| macOS Sequoia | 15.8.1  |
| OpenCore      | v1.0.8  |

</details>

<details>
<summary><strong>🔧 Drivers in this EFI</strong></summary>

| Driver | Version | Purpose |
| ---- | ------- | ------- |
| [Lilu](https://github.com/acidanthera/Lilu) | 1.7.2 | Patch engine — required by most of the below |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen) | 1.7.1 | Graphics, audio, Wi-Fi fixes |
| [AppleALC](https://github.com/acidanthera/AppleALC) | 1.9.8 | Audio (Conexant CX8200, `alcid=23`) |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC) | 1.3.8 | Sensors + battery/fan |
| [SMCBatteryManager](https://github.com/acidanthera/VirtualSMC) | 1.3.8 | Battery status |
| [SMCLightSensor](https://github.com/acidanthera/VirtualSMC) | 1.3.8 | Ambient light sensor |
| [SMCProcessor](https://github.com/acidanthera/VirtualSMC) | 1.3.8 | CPU temperature |
| [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) | 1.3.8 | Super I/O (fans, keys) |
| [YogaSMC](https://github.com/zhen-zen/YogaSMC) | 1.5.3 | Fn keys, fan control, battery limit |
| [IntelMausi](https://github.com/acidanthera/IntelMausi) | 1.0.9 | Ethernet I219-LM |
| [itlwm](https://github.com/laobamac/itlwm) — AirportItlwm | 2.4.0 | Native Wi-Fi, AC 8265 (Sequoia) |
| [IntelBTPatcher](https://github.com/acidanthera/IntelBluetoothFirmware) | 2.5.0 | Bluetooth firmware patcher |
| [IntelBluetoothFirmware](https://github.com/acidanthera/IntelBluetoothFirmware) | 2.5.0 | Bluetooth firmware |
| [HoRNDIS](https://github.com/abdullahselek/OpenIntelWireless) | 9.3 | USB Wi-Fi driver (unused by default) |
| [VoodooPS2Controller](https://github.com/acidanthera/VoodooPS2) | 2.3.7 | Trackpoint + keyboard |
| [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) | 2.9.1 | I²C (ELAN touchpad, touchscreen) |
| [VoodooI2CHID](https://github.com/VoodooI2C/VoodooI2C) | 1.0 | HID support for I²C devices |
| [USBToolBox](https://github.com/USBToolBox/tool) | 1.2.0 | USB injection engine |
| [UTBDefault](https://github.com/USBToolBox/tool) | 1.0 | USB port map (this machine) |
| [RealtekCardReader](https://github.com/0xFireWolf/RealtekCardReader) | 0.9.7 | SD card reader (RTS522A) |
| [RealtekCardReaderFriend](https://github.com/0xFireWolf/RealtekCardReaderFriend) | 1.0.4 | Companion to the above |
| [NVMeFix](https://github.com/acidanthera/NVMeFix) | 1.1.4 | NVMe compatibility |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock) | 1.1.9 | Unlocks Sidecar/Continuity features |
| [RestrictEvents](https://github.com/acidanthera/RestrictEvents) | 1.1.7 | Blocks unwanted firmware updates |
| [BlueToolFixup](https://github.com/acidanthera/BlueToolFixup) | 2.6.9 | Required by AirportItlwm |
| [AMFIPass](https://github.com/dortania/OpenCore-Legacy-Patcher) | 1.4.1 | Chainloads AMFIPatcher (see note below) |
| [NoTouchID](https://github.com/acidanthera/NoTouchID) | 1.0.4 | Disables Touch ID stack |
| [ECEnabler](https://github.com/1Revenger1/ECEnabler) | 1.0.6 | Embedded controller enable |
| [RTCMemoryFixup](https://github.com/1Revenger1/RTCMemoryFixup) | 1.0.8 | Fixes RTC RAM reset |
| [BrightnessKeys](https://github.com/1Revenger1/BrightnessKeys) | 1.0.4 | Brightness key support |

> **🗒️Note:**
> Load order in `config.plist` matters — Lilu and WhateverGreen must come before the kexts that depend on them.
>
> **VoodooInput:** VoodooPS2Controller and VoodooI2C each bundle their own `VoodooInput.kext`. Keep both at the **same version** (currently 1.1.6) — a mismatch makes the trackpoint and touchpad fight over the multitouch pipeline, which shows up as freezes or jumping cursor when both are used together. If you update either kext, copy the newer VoodooInput over the other.

</details>

## 📖 Installation

<details>  
<summary><strong>How to install macOS</strong></summary>
</br>

1. [Create an installation media](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer)
1. Download the [latest EFI folder](https://github.com/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh/archive/refs/heads/main.zip) and copy it into the ESP partition
1. Change your BIOS settings according to the table below
1. Boot from the USB installer (press `F12` to choose boot volume) and [start the installation process](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb)

### BIOS Config

| Menu     |                   |                                 | Setting     |
| -------- | ----------------- | ------------------------------- | ----------- |
| Config   | USB               | UEFI BIOS Support               | `Enable`    |
|          | Power             | Intel SpeedStep Technology      | `Enable`    |
|          |                   | CPU Power Management            | `Enable`    |
|          | CPU               | Hyper-Threading Technology      | `Enable`    |
| Security | Security Chip     |                                 | `Disable`   |
|          | Memory Protection | Execution Prevention            | `Enable`    |
|          | Virtualization    | Intel Virtualization Technology | `Enable`    |
|          |                   | Intel VT-d Feature              | `Enable`    |
|          | Anti-Theft        | Computrace                      | `Disable`   |
|          | Secure Boot       |                                 | `Disable`   |
|          | Intel SGX         |                                 | `Disable`   |
|          | Device Guard      |                                 | `Disable`   |
| Startup  | UEFI/Legacy Boot  |                                 | `UEFI Only` |
|          | CSM Support       |                                 | `No`        |
|          | Boot Mode         |                                 | `Quick`     |

</details>

<details>  
<summary><strong>Enable Apple Services</strong></summary>
</br>

Config to allow you to use Apple Services (such as iMessage)

> **🗒️Note:**
>
> If you (still) can't login to iMessage you may need to contact Apple Support to unblacklist your AppleID (You can try opening the Message app from terminal to check the log to see if you're getting a Customer Code error, which is an indication that your AppleID got blacklisted. [See more info here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#customer-code-error))

1. Download (or clone) [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and run it in terminal
2. Type `3` to generate SMBIOS, then press <kbd>Enter</kbd>
3. Type `MacBookPro15,2 5`, then press <kbd>Enter</kbd>
4. Open `EFI/Config.plist` (I highly recommend using [ProperTree](https://github.com/corpnewt/ProperTree)) and navigate to `PlatformInfo -> Generic`
5. Add one of the script's result to `MLB`, `SystemSerialNumber`, and `SystemUUID`
6. Replace `ROM` with your MAC Address (`System Preferences -> Network -> Ethernet -> Advanced -> Hardware -> MAC Address`, then remove all the colons `:`). Or you can also try using a real Apple MAC Address
7. Save and Reboot
8. Check the Serial Number validity. Repeat step 5 and choose different result (or generate new set of SMBIOS) until you find invalid Serial Number
</details>

## 🧰 Post-install (optional)

<details>  
<summary><strong>Audio Setup</strong></summary>

The X380 Yoga has CX8200 for audio which requires the boot-arg **or** device property below. You can use the boot-args to initially setup your config.plist file as suggested in the guide or simply add the device property. Everything should work, built-in microphone, speakers, headphone jack and microphone. 

NVRAM:

| Key       | Value    |
| --------- | -------- |
| boot-args | alcid=23 |

DeviceProperties

| Key                        | Type       | Value        |
| -------------------------- | ---------- | ------------ |
| PciRoot(0x0)/Pci(0x1F,0x3) | Dictionary |              |
| layout-id                  | Data       | **0f000000** |

</details>

<details>  
<summary><strong>Enable Intel WLAN cards</strong></summary>
</br>

This EFI uses **`AirportItlwm-Sequoia`** (native Wi-Fi interface, no extra app) for the Intel AC-8265. The alternative `itlwm.kext` + [HeliPort](https://github.com/OpenIntelWireless/HeliPort) works across multiple macOS versions and connects faster, but needs the HeliPort app and can't be used during Setup/Recovery.

> [!IMPORTANT]
> **WiFi Kext Compatibility**: the included `AirportItlwm.kext` is built specifically for **macOS Sequoia**.
> For **macOS Sonoma** you **MUST** swap in the Sonoma build (grab it from [releases](https://github.com/laobamac/itlwm/releases)). A mismatched kext means boot failure or dead Wi-Fi.

Quick comparison (see the [FAQ](https://openintelwireless.github.io/itlwm/FAQ.html#features) for the full list):

- **AirportItlwm**: native control in System Settings, works in Setup/Recovery, supports Location Services — but one build per macOS version (use `MinKernel`/`MaxKernel` if you multi-boot), and can't join hidden networks.
- **itlwm.kext**: one kext for many macOS versions, faster page loads, hidden networks OK, iMessage/FaceTime friendly — but requires the HeliPort app (add it to Login Items) and no Location Services.

> **🗒️Note:**
>
> On **macOS Sequoia** the included kext is **AirportItlwm-Sequoia v2.4.0-alpha from the [laobamac/itlwm](https://github.com/laobamac/itlwm) fork**, which drives the Intel AC-8265 through the **native Wi-Fi interface** (System Settings, no HeliPort) — tested working on Sequoia 15.8.1, **no [OCLP-Mod](https://github.com/laobamac/OCLP-Mod/releases) patch required**. To switch to itlwm instead, disable AirportItlwm (all variants) and enable itlwm in `config.plist`.

</details>

<details>  
<summary><strong>Enable Fingerprint Reader (experimental ✅)</strong></summary>
</br>

The X380 Yoga's Validity `138a:009d` reader **works for lock-screen unlock** (tested on Sequoia 15.8.1) via [VFS5011-hackintosh](https://github.com/hackintosh-user/VFS5011-hackintosh) (`active-development` branch). It is a user-space daemon (libusb + Accessibility password typing), not a kernel driver — no OpenCore changes needed.

> [!NOTE]
> `009d` reports sensor type `0xdb`, which needs the type-`0xdb` capture path. If calibration fails with `status=0x0534`, your client build predates that support — update to the latest `active-development`.

**Setup:**
```bash
# 1. Requirements: Xcode Command Line Tools, Homebrew, OpenCore ≥ 1.0.6
git clone --branch active-development https://github.com/hackintosh-user/VFS5011-hackintosh.git
cd VFS5011-hackintosh
./prep_and_build.sh --sensor metallica   # installs libusb/openssl/innoextract, builds client + agent
sudo ./hack-touchid
```
1. `[1] Enroll` — swipe one finger ~10x. If the sensor was ever paired on Windows/Linux, you'll be asked once for the laptop's real DMI product name + serial (e.g. from Windows `Get-CimInstance Win32_ComputerSystemProduct`), then it's remembered.
2. `[2] Verify` — one touch to confirm matching.
3. `[3] Deploy` — installs the daemon (approve the Accessibility prompt in System Settings).
4. Lock the screen (`Ctrl+Cmd+Q`) and swipe.

**Limitations:** no login right after reboot/shutdown, no `sudo` in Terminal. macOS updates wipe the daemon → re-run `[3] Deploy`. What it covers: lock screen, System Settings padlock, Finder password prompts, Passwords.app, Keychain Access.

</details>

<details>  
<summary><strong>CPUFriend power management</strong></summary>
<br>

Not used anymore — power management runs on native XCPM and the CPUFriend kexts were removed from this EFI. If you want custom frequency vectors, generate a `CPUFriendDataProvider` for your machine with [CPUFriend](https://github.com/acidanthera/CPUFriend) and add it back.

</details>

<details> 
<summary><strong>USB Port Mapping</strong></summary>

Ports are mapped with [USBToolBox](https://github.com/USBToolBox/tool) + the included `UTBDefault.kext`. One gotcha from the original mapping session: the internal ports (cameras, touchscreen, Bluetooth) only showed up after handling RHUB per the [manual mapping notes](https://dortania.github.io/OpenCore-Post-Install/usb/manual/manual.html#special-notes) — keep that in mind if you ever redo the map.

</details> 

## 🛠️ Other tweaks

<details>  
<summary><strong>Enable HiDPI</strong></summary>
</br>

1. [Disable SIP](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/troubleshooting.html#disabling-sip)
1. Run the following script in Terminal
   ```bash
   bash -c "$(curl -fsSL https://raw.githubusercontent.com/xzhih/one-key-hidpi/master/hidpi.sh)"
   ```
1. Follow the instructions, then reboot
1. Re-enable SIP (if desired)

Or try an [alternative method](https://github.com/bbhardin/A-Guide-to-MacOS-Scaled-Resolutions)

</details>

<details>  
<summary><strong>Enable multimedia keys, fan & LEDs control </strong></summary>
</br>

- Download [**YogaSMC-App**](https://github.com/zhen-zen/YogaSMC/files/14324664/Builds.zip) and mount it. This is a custom build which fixes the "Failed to open Preferences" [issue](https://github.com/zhen-zen/YogaSMC/issues/189) in Ventura and newer  
	- Double-click the YogaSMC **prefPane** to install it
	- Drag the `YogaSMC` app into the Applications folder and run it
	- Click on the icon (`⌥`) in the menu bar and select "Start at Login"
	- Now you can control performance profiles, fan speed and other settings
</details>

<details>  
<summary><strong>Use PrtSc key as Screenshot shortcut</strong></summary>
</br>

Super useful shortcut that I wish I had it on my previous MBP. Default is `⌘⇧5`.

1. Open SystemPreferences.app
1. Go under `Keyboard > Shortcuts > Screenshots`
1. Click on `Screenshot and recording options` field
1. Press `PrtSc` on your keyboard (it should come out as `F13`)

</details>

<details>
<summary><strong>Use Thinkpad Assistant </strong></summary>
</br>

1. Get a pair of Patch & SSDT from [Samples](./Tools/Thinkpad%20Assistant/Samples/SSDT-X380-KBRD.dsl) folder
2. Compile SSDT (e.g. `iasl -vo SSDT-X380-KBRD.dsl`)
3. Copy `SSDT.aml` to EFI/OC/ACPI
4. Apply patch on `config.plist` with [OCAT](https://github.com/ic005k/OCAuxiliaryTools)
5. Download [Thinkpad Assistant](./Tools/Thinkpad%20Assistant/ThinkpadAssistant.dmg)
6. Extract & Copy to Applications folder
7. Start Thinkpad Assistant & Tick 'Launch on Login' in Menubar
8. Reboot

</details>

<details>  
<summary><strong>Faster macOS dock animation</strong></summary>
</br>

This enables auto-hide and speeds up the animation

1. Run the following script in Terminal
   ```bash
   defaults write com.apple.dock autohide-delay -float 0; defaults write com.apple.dock autohide-time-modifier -float 0.5; killall Dock
   ```
   </details>

<details>  
<summary><strong>Fix Windows Time Sync</strong></summary>
</br>

`RealTimeIsUniversal` registry key still works in Windows 8, 10, and 11! Just tested it by myself. The instructions to use this method are explained lot of times everywhere, for example in this answer.

I will replicate the answer here:

`Win+S`, `regedit`, `Enter`.

Navigate to the key:

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation`.
Create new `DWORD (32-bit) Value`, name it `RealTimeIsUniversal`. Set its value to `1`.

After this is done, just reboot your machine. After it is up and running again, let Windows set time automatically (click on the current time in tray, `Date and Time` `Settings` > `Set Time Automatically`), this time it will not mess with it.
</details>

<details>  
<summary><strong>Boot process tweaks</strong></summary>
</br>

| Menu |       |            | Setting    | What does it do?     |
| :--- | :---- | :--------- | :--------- | :------------------- |
| Misc | Boot  | ShowPicker | `False`    | Skip bootloader page |
| UEFI | Audio | PlayChime  | `Disabled` | Always silent boot   |

</details>

<details>  
<summary><strong>Setup hibernation and sleep</strong></summary>
</br>

[Script](https://www.tonymacx86.com/threads/release-sleeponlowbattery-solb.264785) that performs auto sleep/hibernate at low battery.

1. Open terminal
1. Enter commands below one by one

   Settings for AC:

   ```
   sudo pmset -c standby 1
   sudo pmset -c hibernatemode 0
   ```

   Setting for battery:

   ```
   sudo pmset -b standby 1
   sudo pmset -b standbydelayhigh 900
   sudo pmset -b standbydelaylow 60
   sudo pmset -b hibernatemode 25
   sudo pmset -b highstandbythreshold 70
   ```

   Settings for all:

   ```
   sudo pmset -a acwake 0
   sudo pmset -a lidwake 1
   sudo pmset -a powernap 0
   ```

To restore default system settings run

```
sudo pmset restoredefaults
```
</details> 

<details> 
<summary><strong>Grant/remove accessibility permissions to any app</strong></summary>

tccutil with extended capabilities allowing you to grant/remove accessibility permissions to any app.

I never recommend manually modifying any system database because if a mistake is made you risk boot-looping your computer. This is why this tool is using the undocumented TCC.framework to make changes just like macOS does internally. 

Requires SIP and AMFI to be disabled.

Currently can only add one or all (not recommended) services at a time. Using `reset All` is fine.

```
tccplus [add/reset] SERVICE [BUNDLE_ID]
Services: 
 - All 
 - Accessibility 
 - AddressBook 
 - AppleEvents 
 - Calendar 
 - Camera 
 - ContactsFull 
 - ContactsLimited 
 - DeveloperTool 
 - Facebook 
 - LinkedIn 
 - ListenEvent 
 - Liverpool 
 - Location 
 - MediaLibrary 
 - Microphone 
 - Motion 
 - Photos 
 - PhotosAdd 
 - PostEvent 
 - Reminders 
 - ScreenCapture 
 - ShareKit 
 - SinaWeibo 
 - Siri 
 - SpeechRecognition 
 - SystemPolicyAllFiles 
 - SystemPolicyDesktopFolder 
 - SystemPolicyDeveloperFiles 
 - SystemPolicyDocumentsFolder 
 - SystemPolicyDownloadsFolder 
 - SystemPolicyNetworkVolumes 
 - SystemPolicyRemovableVolumes 
 - SystemPolicySysAdminFiles 
 - TencentWeibo 
 - Twitter 
 - Ubiquity 
 - Willow
 ```
Usage Example:
Get application bundle ID:

`grep 'BundleIdent' -A 1 /Applications/<APPLICATION NAME>/Contents/Info.plist`

Pass result to `tccplus`
```bash
user@iMac ~ % grep 'BundleIdent' -A 1 /Applications/Discord.app/Contents/Info.plist
    <key>CFBundleIdentifier</key>
    <string>com.hnc.Discord</string>
user@iMacc ~ % grep 'BundleIdent' -A 1 /Applications/zoom.us.app/Contents/Info.plist
    <key>CFBundleIdentifier</key>
    <string>us.zoom.xos</string>
user@iMac ~ % ./tccplus add Microphone com.hnc.Discord
Successfully added Microphone approval status for com.hnc.Discord
```

</details> 

<details>  
<summary><strong>Advanced energy management</strong></summary>

`acwake`: wake the machine when power source (AC/battery) is changed (value = 0/1)

`lidwake`: wake the machine when the laptop lid (or clamshell) is opened (value = 0/1)

`powernap`: enable/disable Power Nap on supported machines (value = 0/1)

`standbydelayhigh` and `standbydelaylow` specify the delay, in seconds,
before writing the hibernation image to disk and powering off memory for Standby.
standbydelayhigh is used when the remaining battery capacity is above `highstandbythreshold`(has a default value of 50 percent),
and standbydelaylow is used when the remaining battery capacity is below highstandbythreshold.

`hibernatemode` supports values of 0, 3, or 25. To disable hibernation, set hibernatemode to 0.  
`hibernatemode` = 0 by default on desktops. The system will not back memory up to persistent storage. The system must wake from the contents of memory; the system will lose context on power loss.  
`hibernatemode` = 3 by default on portables. The system will store a copy of memory to persistent storage (the disk), and will power memory during sleep. The system will wake from memory, unless a power loss forces it to restore from hibernate image.  
`hibernatemode` = 25 is only settable via pmset. The system will store a copy of memory to persistent storage (the disk), and will remove power to memory. The system will restore from disk image. If you want "hibernation" - slower sleeps, slower wakes, and better battery life, you should use this setting.

[Source](https://www.dssw.co.uk/reference/pmset.html)

</details>

## 📊 Status

<details>  
<summary><strong>✅ What's working</strong></summary>
</br>

- [x] Intel HD 620 Graphics `including graphics acceleration`
- [x] Battery management
- [x] USB ports
- [x] Internal camera `working fine on FaceTime, Skype, Zoom and others`
- [x] Sleep / Wake / Shutdown / Reboot
- [X] Intel WiFi & Bluetooth (native Wi-Fi via [itlwm](https://github.com/laobamac/itlwm), no HeliPort needed)
- [x] iMessage, FaceTime, App Store, iTunes Store `(Requires valid SMBIOS)`
- [x] Speakers and headphones combo jack
- [x] Microphone
- [x] Keyboard map and hotkeys with [YogaSMC](https://github.com/zhen-zen/YogaSMC)
- [x] Multi-Touch Screen `Touchscreen feels more natural than using Touchpad (Touchpad gesture enabled). Pen also working`
- [x] SIP and FileVault 2 can be turned on
- [x] Fingerprint reader (Validity `138a:009d`) — lock-screen unlock via VFS5011-hackintosh, see setup above `(experimental)`
- [x] Micro SD Card Reader (Realtek RTS522A via [RealtekCardReader](https://github.com/0xFireWolf/RealtekCardReader) 0.9.7 + Friend)

</details>

<details>  
<summary><strong>⚠️ What's not working</strong></summary>
</br>

- [ ] Safari DRM `Use Chromium engine to watch Apple TV+, Amazon Prime Video, Netflix and others`
- [ ] Samsung PM 981 NVME drive - `Still unstable. Could work for some, not for others. See `[Anti-Hackintosh Buyers Guide - Storage](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/Storage.html)
- [ ] Sidecar Wireless `doesn't work without apple native WIFI card`

</details>

<details>  
<summary><strong>🔄 Not tested</strong></summary>
</br>

- [ ] Apple Watch Unlock
- [ ] WWAN
- [ ] AirDrop
- [ ] HDMI
- [ ] Thunderbolt

</details>

## ⚡ Performance

<details>  
<summary><strong>🔥 Power consumption and thermals</strong></summary>
</br>

Sequoia
| Idle State                     | Max Frequency                  | 2 Thread Frequency             | All Thread Frequency           | GPU Max Frequency              |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| ![](/Images/ipg-idle-freq.png) | ![](./Images/ipg-max-freq.png) | ![](./Images/ipg-two-freq.png) | ![](./Images/ipg-all-freq.png) | ![](./Images/ipg-gpu-freq.png) |

Sonoma
| Idle State                     | Max Frequency                  | 2 Thread Frequency             | All Thread Frequency           | GPU Max Frequency              |
| ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ | ------------------------------ |
| ![](/Images/ipg-idle-freq-sonoma.png) | ![](./Images/ipg-max-freq-sonoma.png) | ![](./Images/ipg-two-freq-sonoma.png) | ![](./Images/ipg-all-freq-sonoma.png) | ![](./Images/ipg-gpu-freq-sonoma.png) |
</details>

<details>  
<summary><strong>⏱️ Benchmarks</strong></summary>
</br>

| CPU         | Single-Core | Multi-Core |
| :---------- | ----------: | ---------: |
| Geekbench 5 |         689 |       2670 |
| **GPU**     |  **OpenCL** |  **Metal** |
| Geekbench 5 |        4191 |       3683 |
<small>macOS Sequoia 15.2, EFI release 1.0.3, CPU: i5-8350U</small>

| CPU         | Single-Core | Multi-Core |
| :---------- | ----------: | ---------: |
| Geekbench 5 |         755 |       2479 |
| **GPU**     |  **OpenCL** |  **Metal** |
| Geekbench 5 |        2819 |       2471 |
<small>macOS Sonoma14.7.2, EFI release 1.0.3, CPU: i5-8350U</small>
</details>

## Credits

- [Apple](https://apple.com) for macOS.
- [Acidanthera](https://github.com/acidanthera) for OpenCore and all the lovely hackintosh work.
.
- [CorpNewt](https://github.com/corpnewt) for ProperTree, CPUFriendFriend and SSDTTime
- [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) Made the OpenCore Install Guide which was used to make this EFI.
- [ic005k](https://github.com/ic005k/OCAuxiliaryTools) for OpenCore Auxiliary Tools
- [benbaker76](https://github.com/benbaker76/Hackintool) for Hackintool
- [zhen-zen](https://github.com/zhen-zen/YogaSMC) for YogaSMC
- [laobamac](https://github.com/laobamac/itlwm) for the itlwm fork with native AirportItlwm on Sequoia & Tahoe — thank you for keeping Intel Wi-Fi alive on macOS! 🙏
- [r/hackintosh](https://www.reddit.com/r/hackintosh/) community for helping me find solution to various issue I came across
---
