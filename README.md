# Lenovo ThinkPad X380 Yoga - OpenCore Configuration

<img align="right" src="https://p1-ofp.static.pub/medias/bWFzdGVyfHJvb3R8MzY5NzQ4fGltYWdlL3BuZ3xoMTEvaGMwLzE0NDQ4MTg0NTI0ODMwLnBuZ3wyZjE4MmQ5YmEyN2U1M2VhOTJkZDM4NzFjMTUzNDk2M2NmOGQ5OTQ2MjYxNTVlNjY3YmYxMTU4ZDM2Y2RmNjlk/lenovo-laptop-thinkpad-x380-2-in-1-hero.png" alt="macOS running on the X380 Yoga" width="425">

[![macOS](https://img.shields.io/badge/macOS-Ventura-brightgreen.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sonoma-brightgreen.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Sequoia-brightgreen.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.6-blue.svg)](https://github.com/acidanthera/OpenCorePkg)
[![Model](https://img.shields.io/badge/Model-20LJ-9cf)](https://psref.lenovo.com/syspool/Sys/PDF/ThinkPad/ThinkPad_X380_Yoga/ThinkPad_X380_Yoga_Spec.PDF)
[![BIOS](https://img.shields.io/badge/BIOS-1.41-blue)](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x380-yoga/downloads/driver-list/component?name=BIOS%2FUEFI&id=5AC6A815-321D-440E-8833-B07A93E0428C)
[![issues](https://img.shields.io/github/issues/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh-OpenCore)](https://github.com/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh-OpenCore/issues)
[![last commit](https://img.shields.io/github/last-commit/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh-OpenCore)](https://github.com/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh-OpenCore)
[![License](https://img.shields.io/badge/license-MIT-purple.svg)](/LICENSE)

**DISCLAIMER:**  
This OpenCore EFI works fine on my Thinkpad X380 Yoga. 
As you embark on your Hackintosh journey you are encouraged to **READ** the entire README and [Dortania](https://dortania.github.io/getting-started/) guides before you start to get an understanding of the install process. It will save many a message instructing you to read the manual. 

With that said I'm happy to help when/where I can. When you encounter bug or want to improve this repo, consider opening an issue or pull request. You can also find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

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
| Touchoad  | ELAN v4 LEN2034 PS2 Interace                         | Trackpad not working? You can disable trackpoint in bios.    |
| Wifi & BT | Intel AC 8265 and Bluetooth                          | Use AirportItlwm for your macOS version and enjoy native Wi-Fi control. |
| Ethernet  | Intel I219-LM4 Gigabit Ethernet                      |                                                              | 
| Input     | PS2 Keyboard & I2CHID TrackPad (touchscreen and pen) | I'm using [YogaSMC](https://github.com/zhen-zen/YogaSMC) for media keys. The kext is in the folder but **you'll need to install the app.** |

</details>

<details>
<summary><strong>📦 Main software</strong></summary>

| Component     | Version |
| ------------- | ------- |
| macOS Sequoia | 15.7.2  |
| OpenCore      | v1.0.6  |

</details>

## 📖 Installation

<details>  
<summary><strong>How to install macOS</strong></summary>
</br>

1. [Create an installation media](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer)
1. Download the [latest EFI folder](https://github.com/kotakbiasa/ThinkPad-X380-Yoga-Hackintosh/archive/refs/heads/main.zip) and copy it into the ESP partiton
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
7. Replace `ROM` with your MAC Address (`System Preferences -> Network -> Ethernet -> Advanced -> Hardware -> MAC Address`, then remove all the colons `:`). Or you can also try using a real Apple MAC Address
8. Save and Reboot
9. Check the Serial Number validity. Repeat step 5 and choose different result (or generate new set of SMBIOS) until you find invalid Serial Number
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

Although the Intel AC-8265 Card is compatible with both kexts (use either one or the other), there are Pros and Cons to both of them (check the [**FAQs**](https://openintelwireless.github.io/itlwm/FAQ.html#features) for other differences):

> [!IMPORTANT]
> **WiFi Kext Compatibility**: The included `AirportItlwm.kext` is specifically for **macOS Sequoia**.  
> If you plan to install **macOS Sonoma**, you **MUST** replace this kext with the version compiled for Sonoma. Using the wrong version will result in boot failures or non-functional WiFi.

- **AirportItlwm**: (used in macOS Sonoma)
	- **Pro**: Can be used during macOS Setup/Recoveery which is not possible with `itlwm.kext`
	- **Pro**: Supports Location Services and "Find My Mac"
 	- **Pro**: Connects faster to Wi-Fi Hotspots than `itlwm.kext`
	- **Con**: Doesn't perform as well as `itlwm.kext`
	- **Con**: Can't connect to hidden WiFi Networks
	- **Con**: Requires the correct kext per macOS version, so running multiple version of macOS requires multiple versions of this kext controlled via `MinKernel` and `MaxKernel` settings

- **itlwm.kext** (used in Sequoia)
	- **Pro**: `itlwm.kext` works across _multiple_ versions of macOS
	- **Pro**: Loading webpages feels a lot quicker than with `AirportItlwm` 
	- **Pro**: Can connect to hidden WiFi Networks
 	- **Pro**: Does work with iMessage and FaceTime 	
	- **Con**: Requires [**HeliPort**](https://github.com/diepeterpan/HeliPort/releases) app to connect to Wi-Fi hotspots, so it can't be used during macOS Setup/Recovery
	- **Con**: Doesn't support Location Services

- Pre-compiled WiFi kexts for other versions of macOS can be found in the [Additional Files](hhttps://github.com/OpenIntelWireless/itlwm/releases) section! You will need them if you want to run other macOS versions than Sonoma or Sequioa!

> **🗒️Note:**
> 
> My config uses `AirportItlw.kext` by default since it allows accessing the internet during macOS installation (unlike `itlwm.kext` which requires an additional app to do so). Currently, AirportItlwm kexts for macOS Sequoia is included but you must patch using [OCLP-Mod](https://github.com/laobamac/OCLP-Mod/releases). If you want to use itlwm, disable AirportItlwm (all variants) and enable itlwm in the config.plist instead. Next, download the Helipad app, run it and add it to "Login Items" (in System Settings) so that it starts automatically with macOS.

</details>

<details>  
<summary><strong>CPUFriend power management</strong></summary>
<br>

Generate `CPUFriendDataProvider` or `ssdt_data.aml` (choose one) for your machine [here](https://github.com/acidanthera/CPUFriend) or use the ssd_data.aml file provided. My files are set for power conservation over performance. Highly recommended that you use power management.

</details>

<details> 
<summary><strong>USB Port Mapping</strong></summary>

While first port mapping I followed the [Dortania guide here](https://dortania.github.io/OpenCore-Post-Install/usb/#macos-and-the-15-port-limit) with USBInjectAll.kext install...  when doing so the internal USB ports did not show up and the cameras, touch screen, and bluetooth did not function. I noticed on the `USBmap tool` screen that RHUB was showing so I Googled it and it brought me back to the [Dortania guide here](https://dortania.github.io/OpenCore-Post-Install/usb/manual/manual.html#special-notes). I added the SSDT-RHUB.aml to the APCI folder rebooted and all the ports showed up. I then mapped the USB ports creating the included USBMap.kext file.

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
	- Drag the `YogaSMC` app into the "Programs" folder and run it
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
1. Press `PrtSc` on your keyboard (it should came out as `F13`)

</details>

<details>
<summary><strong>Use Thinkpad Assistant </strong></summary>
</br>

1. Get a pair of Patch & SSDT from [Samples](./Tools/Thinkpad%20Assistant/Samples/SSDT-X380-KBRD.dsl) folder
2. Compile SSDT (ex. `iasl -vo SSDT-X380-KBRD.dsl`)
3. Copy `SSDT.aml` to EFI/OC/ACPI
4. Apply patch on `config.plst` with [OCAT](https://github.com/ic005k/OCAuxiliaryTools)
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

- [x] Intel HD 620 Graphics `incuding graphics acceleration`
- [x] Battery management
- [x] USB ports
- [x] Internal camera `working fine on FaceTime, Skype, Zoom and others`
- [x] Sleep / Wake / Shutdown / Reboot
- [X] Intel WiFi & Bluetooth (thanks to [itlwn](https://github.com/OpenIntelWireless/itlwm) & [Heliport](https://github.com/OpenIntelWireless/HeliPort) )
- [x] iMessage, FaceTime, App Store, iTunes Store `Please generate your own SMBIOS`
- [x] Speakers and headphones combo jack
- [x] Microphone
- [x] Keyboard map and hotkeys with [YogaSMC](https://github.com/zhen-zen/YogaSMC)
- [x] Multi-Touch Screen `Touchscreen just feel more natural than using Touchpad (Touchpad gesture enabled). Pen also working`
- [x] SIP and FileVault 2 can be turned on
- [ ] Micro SD Card Reader `Kext removed in 1.0.6 update`

</details>

<details>  
<summary><strong>⚠️ What's not working</strong></summary>
</br>

- [ ] Safari DRM `Use Chromium engine to watch Apple TV+, Amazon Prime Video, Netflix and others`
- [ ] Fingerprint reader - `No. Don't expect macOS driver any time soon.`
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
- [r/hackintosh](https://www.reddit.com/r/hackintosh/) community for helping me find solution to various issue I came across
---
