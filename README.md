# Deskmini-H470-OpenCore-EFI
This is an efi boot sample file for deskmini h470 on OpenCore 0.7.5.  
Hackintosh is highly hardware dependent so you might need to change your config.plist.  
Big Sur now archived with OC 0.7.4 stable, focus on Monterey from now on  
[繁體中文](README_ZH-TW.md)  
[简体中文](README_zh-CN.md)

| Harware  |   My Setup |  comment |
|----------|-------------|------|
| MotherBoard |  Asrock H470-stx | All in one mini PC. |
| CPU |    intel i3-10100   |   Comet lake processor. |
| CPU cooler| ID-cooling IS-40x | Need to lift the case when installing, fan works without hitting the case. |
| GPU | Intergrated UHD630 | Supports up to 3 displays. |
| RAM |  Crucial DDR4 3200 8GB SODIMM x2 | Overspect as i3-10100 only supports up to 2666mz on this board. |
| Storsage |    Cruicial P5 Nvme 1tb | Picker to login in 13ish seconds. |
| Sound card | Realtek ALC235 | Somehow the website listed as ALC233 but both macOS and windows recognized as ALC235. | 
| Wifi/Bluetooth | BCM94352Z/DW1560 | Airdrop works, sidecar currently broken on macOS 12 |
| Operating system | Win 10, Big Sur | Dual boot on one nvme drive. |

# Hackintosh
1. HDMI and DP boots, type c not rested.
2. Sound through HDMI or DP works.
3. Sleep/wake works.
4. Powermanagement options restored via [Dortania's OpenCore OpenCore Post-Install-Fixing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html).
5. ~Update tested(Fine from Big Sur 11.5.2-> 11.6 ->11.6.1, OpenCore 7.2-> 7.3 -> 7.4)~.
6. Airdrop and ~~sidecar~~ works.
7. Iservices such as facetime and imessages works as long as you generate your own SerialNumber, UUID, MLB, ROM and had a valid Apple ID in good standing(Prefered logged into a valid Apple's device before). Follows [Dortania's OpenCore Post-Install-iservices](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html).

# Kexts
To my understanding, kexts are like plugins to pass on hardware information so macOS knows what to do with them. Although SSDTS could serve the same purpose, kexts are more modular and more resilent thus less prone to fail when Apple updates. Number of kexts do affect boot time to some degree so you could customize to your own need.

| Kexts |      comment |
|----------|-------------|
| [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup) | Fix wifi for Broadcom wifi/BT cards. | 
| [AppleALC](https://github.com/acidanthera/AppleALC) | Apple sound codecs. |   
| ~~[BrcmBluetoothInjector](https://github.com/acidanthera/BrcmPatchRAM)~~ | ~~Fix Bluetooth for Broadcom wifi/BT cards. Dropped support on macOS 12.0 Monterey~~ | 
| [BlueToolFixup](https://github.com/acidanthera/BrcmPatchRAM) | Temporary soulution for Bluetooth, not stable and sidecar broken. Required for macOS 12 or newer |
| [BrcmFirmwareData](https://github.com/acidanthera/BrcmPatchRAM) | Fix Bluetooth for Broadcom wifi/BT cards. |
| [BrcmPatchRAM3](https://github.com/acidanthera/BrcmPatchRAM) |  Fix Bluetooth for Broadcom wifi/BT cards. | 
| [CPUFriendDataProvider](https://github.com/stevezhengshiqi/one-key-cpufriend) | Power/Energy saving management options. |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock) | Allows AirPlay to Mac, Sidecar and Universal Control Unlock, NightShift Unlock on older models. | 
| [IntelMausi](https://github.com/acidanthera/IntelMausi) | Intel Ethernet LAN driver for macOS. |
| [Lilu](https://github.com/acidanthera/Lilu) | Arbitrary kext and process patching on macOS. |
| [NVMeFix](https://github.com/acidanthera/NVMeFix) |  Patches for the Apple NVMe storage driver. | 
| [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) |  Monitor hardware informations. |
| [USBPorts](https://dortania.github.io/OpenCore-Post-Install/usb/) | Allows proper USB mappings for speed and bluetooth. | 
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC) | Apple SMC emulator. |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen) | GPU, display related. | 

# Known issues
1. When booting with dual screen on, horizontal stripes/artifacts appears on screen which can be solved by repluging the moniter or turn on screen after login
2. Popping/ hissing sound for speakers/headphone when booting, shutting down or sleeping, no issues when using macOS. Same issue is present in deskmini H310 and [viorel78] (https://github.com/viorel78/ASRock-DeskMini-310/issues/1) suggests that adding rear audio cable could resolve this issue.
3. DRM contents such as Netflix is not playable on Safari, use Firefox, Chrome or Edge instead. (As of Big Sur, DRM are baked in Apple's hardware)
4. Sidecar broken due to incomplete Bluetooth fix

# To be done in the future
1. Bulid my own custom SSDTs.
2. Follow up on display fixes and sound fixes.
3. Dual boots Monterey and Win11 with secure boot in the future.

# Debugging journey
1. Always try resetting NVRAM first.
2. Change OpenCore to debug version and try to follow [Dortania's OpenCore Install Guide-debugging](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html).
