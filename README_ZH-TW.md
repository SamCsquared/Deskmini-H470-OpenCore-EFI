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
就我的理解，kexts就像插件一樣用來溝通硬體和macOS之間的訊息。而SSDT雖然有一樣的功能，但kexts外掛和模組化的特性能讓升級macOS時減少損壞的機會。Kexts的數量會稍微影響開機的速度，可因自己的需求和硬體斟酌哪些kext是自己需要的。

| Kexts |     簡單介紹 |
|----------|-------------|
| AirportBrcmFixup | 讓Broadcom的wifi/BT網卡能辨識，才能有Wifi | 
| AppleALC | 辨識音訊硬體而有聲音 |   
| BrcmBluetoothInjector| 辨識Broadcom的藍芽功能 | 
| BrcmFirmwareData | 辨識Broadcom的藍芽功能 |
| BrcmPatchRAM3 |  辨識Broadcom的藍芽功能 | 
| CPUFriendDataProvider | 啟用電腦的節能選項 |
| FeatureUnlock | 讓較舊的Mac和Ipad啟用AirPlay, Sidecar, Universal Control Unlock, NightShift等功能 | 
| IntelMausi| 辨識Intel的乙太網路 |
| Lilu | macOS的核心相關，基本上必備 |
| NVMeFix | 修補Apple對於NVMe磁碟的相容性和功能 | 
| SMCSuperIO | 修補監測硬體資訊的功能 |
| USBPorts | 定義USB孔的硬體資訊 | 
| VirtualSMC | 模擬Apple的System Management Controller |
| WhateverGreen | 顯示功能相關，基本必備 | 

# Known issues
1. 雙螢幕接開啟的情況下開機，進入macOS會有水平狀的黑條，可熱插拔螢幕或進入macOS後再開啟第二螢幕解決。
2. 進入opencore選擇器，蘋果商標跑進度條時和睡眠/喚醒時會爆音，Deskmini H310有相同問題而[viorel78](https://github.com/viorel78/ASRock-DeskMini-310/issues/1) 提出購買官方的後置音源線可解決此問題。
3. DRM contents such as Netflix is not playable on Safari, use Firefox, Chrome or Edge instead.(As of Big Sur, DRM are baked in Apple's hardware)

# To be done in the future
1. Bulid my own custom SSDTs
2. Follow up on display fixes and sound fixes
3. Dual boots Monterey and Win11 with secure boot in the future

# Debugging journey
1. Always try resetting NVRAM first
2. Change opencore to debug version and try to follow [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
