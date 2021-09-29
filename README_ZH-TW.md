# Deskmini-H470-Opencore-EFI
此為deskmini h470專用之opencore 7.3導引文件範例
黑蘋果之完成度與硬體有關，任何硬體上個改變皆可能需要重新設定config.plist

| 硬體設備  |  我的硬體 |  評語 |
|----------|-------------|------|
| 主機板 |  Asrock H470-stx | All in one mini PC |
| CPU |    intel i3-10100   |   Comet lake processor |
| CPU 散熱器| ID-cooling IS-40x | 安裝時風扇會刮到機殼，稍微抬起機殼即可塞入，風扇可運轉不會打機殼|
| 顯卡 | 內顯UHD630 | 最多支持三個螢幕 |
| 記憶體 |  Crucial DDR4 3200 8GB SODIMM x2 | 效能過剩，i3-10100在此主機板只能跑到2666MHz |
| 硬碟 |    Cruicial P5 Nvme 1tb | Opencore選擇畫面到登入畫面約13秒 |
| 音效卡 | 內建Realtek ALC235 | 官方規格列為ALC233但蘋果和微軟都判定為ALC235 | 
| Wifi/Bluetooth | BCM94352Z/DW1560 | Sidecar及airdrop都可用 |
| Operating system | Win 10, Big Sur | 同一固態硬碟上雙開蘋果和微軟系統 |

# Hackintosh
1. HDMI和DP揭開機有畫面type c輸出沒有測
2. HDMI及DP的音效皆可
3. 睡眠喚醒可
4. 依[Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)啟用能源節省項目  
5. Opencore和系統更新測試可(從Big Sur 11.5.2-> 11.6, Opencore 7.2-> 7.3)
6. Airdrop and sidecar可用
7. Facetime和imessages等需要更改SerialNumber, UUID, MLB, ROM且最好有一個用過一陣子的Apple ID(比較不起疑)

# Kexts
To my understanding, kexts are like plugins to pass on hardware information so macOS knows what to do with them. Although SSDTS could serve the same purpose, kexts of more modular and more resilent thus less prone to fail when Apple updates. Number of kexts do affect boot time to some degree so you could customize to your own need.

| Kexts |      comment |
|----------|-------------|
| AirportBrcmFixup | Fix wifi for Broadcom wifi/BT cards | 
| AppleALC | Apple sound codecs |   
| BrcmBluetoothInjector| Fix Bluetooth for Broadcom wifi/BT cards | 
| BrcmFirmwareData | Fix Bluetooth for Broadcom wifi/BT cards |
| BrcmPatchRAM3 |  Fix Bluetooth for Broadcom wifi/BT cards | 
| CPUFriendDataProvider | Power/Energy saving management options |
| FeatureUnlock | Allows AirPlay to Mac, Sidecar and Universal Control Unlock, NightShift Unlock on older models | 
| IntelMausi| Intel Ethernet LAN driver for macOS |
| Lilu | Arbitrary kext and process patching on macOS |
| NVMeFix |  Patches for the Apple NVMe storage driver | 
| SMCSuperIO |  Monitor hardware informations |
| USBPorts | Allows proper USB mappings for speed and bluetooth | 
| VirtualSMC | Apple SMC emulator |
| WhateverGreen | GPU, display related | 

# Known issues
1. When booting with dual screen on, horizontal stripes/artifacts appears on screen which can be solved by repluging the moniter or turn on screen after login
2. Popping/ hissing sound for speakers/headphone when booting, shutting down or sleeping, no issues when using macOS. Same issue is present in deskmini H310 and [viorel78](https://github.com/viorel78/ASRock-DeskMini-310/issues/1) suggests that adding rear audio cable could resolve this issue.
3. DRM contents such as Netflix is not playable on Safari, use Firefox, Chrome or Edge instead.(As of Big Sur, DRM are baked in Apple's hardware)

# To be done in the future
1. Bulid my own custom SSDTs
2. Follow up on display fixes and sound fixes
3. Dual boots Monterey and Win11 with secure boot in the future

# Debugging journey
1. Always try resetting NVRAM first
2. Change opencore to debug version and try to follow [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
