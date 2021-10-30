# Deskmini-H470-OpenCore-EFI
此為deskmini h470專用之OpenCore 7.4導引文件範例。  
黑蘋果之完成度與硬體有關，任何硬體上個改變皆可能需要重新設定config.plist文件。  
[English](README.md)    
[简体中文](README_zh-CN.md)

| 硬體設備  |  我的硬體 |  評語 |
|----------|-------------|------|
| 主機板 |  Asrock H470-stx | 華擎迷你主機。 |
| CPU |    intel i3-10100   |   Comet lake處理器。 |
| CPU 散熱器| ID-cooling IS-40x | 安裝時風扇會刮到機殼，稍微抬起機殼即可塞入，風扇可運轉不會打機殼。|
| 顯卡 | 內顯UHD630 | 最多支持三個螢幕。 |
| 記憶體 |  Crucial DDR4 3200 8GB SODIMM x2 | 效能過剩，i3-10100在此主機板只能跑到2666MHz頻率。 |
| 硬碟 |    Cruicial P5 Nvme 1tb | OpenCore選擇畫面到登入畫面約13秒。 |
| 音效卡 | 內建Realtek ALC235 | 官方規格列為ALC233但蘋果和微軟都判定為ALC235碼。 | 
| Wifi/Bluetooth | BCM94352Z/DW1560 | Sidecar及airdrop都可用。 |
| Operating system | Win 10, Big Sur | 同一固態硬碟上雙開蘋果和微軟系統。 |

# Hackintosh
1. HDMI和DP揭開機有畫面type c輸出沒有測。
2. HDMI及DP的音效皆可。
3. 睡眠/喚醒可。
4. 依[Dortania's OpenCore OpenCore Post-Install-Fixing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html)啟用能源節省項目。  
5. Opencore和系統更新測試可(從Big Sur 11.5.2-> 11.6-> 11.6.1, OpenCore 7.2-> 7.3 -> 7.4)。
6. Airdrop和sidecar可用。
7. Facetime和imessages等需要更改SerialNumber, UUID, MLB, ROM且最好有一個用過一陣子的Apple ID(比較不起疑，有正版蘋果裝置登錄過最好)，參閱[Dortania's OpenCore Post-Install-iservices](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html)。

# Kexts
就我的理解，kexts就像插件一樣用來溝通硬體和macOS之間的訊息。而SSDT雖然有一樣的功能，但kexts外掛和模組化的特性能讓升級macOS時減少損壞的機會。Kexts的數量會稍微影響開機的速度，可因自己的需求和硬體斟酌哪些kext是自己需要的。

| Kexts |     簡單介紹 |
|----------|-------------|
| [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup) | 讓Broadcom的wifi/BT網卡能辨識，才能有Wifi。 | 
| [AppleALC](https://github.com/acidanthera/AppleALC) | 辨識音訊硬體而有聲音。 |   
| [BrcmBluetoothInjector](https://github.com/acidanthera/BrcmPatchRAM)| 辨識Broadcom的藍芽功能，三件套1/3一組。 | 
| [BrcmFirmwareData](https://github.com/acidanthera/BrcmPatchRAM) | 辨識Broadcom的藍芽功能，三件套2/3一組。 |
| [BrcmPatchRAM3](https://github.com/acidanthera/BrcmPatchRAM) |  辨識Broadcom的藍芽功能，三件套3/3一組。 | 
| [CPUFriendDataProvider](https://github.com/stevezhengshiqi/one-key-cpufriend) | 啟用電腦的節能選項。 |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock) | 讓較舊的Mac和Ipad啟用AirPlay, Sidecar, Universal Control Unlock, NightShift等功能。 | 
| [IntelMausi](https://github.com/acidanthera/IntelMausi)| 辨識Intel的乙太網路。 |
| [Lilu](https://github.com/acidanthera/Lilu) | macOS的核心相關，基本上必備。 |
| [NVMeFix](https://github.com/acidanthera/NVMeFix) | 修補Apple對於NVMe磁碟的相容性和功能。 | 
| [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) | 修補監測硬體資訊的功能。 |
| [USBPorts](https://dortania.github.io/OpenCore-Post-Install/usb/) | 定義USB孔的硬體資訊。 | 
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC) | 模擬Apple的System Management Controller系統。 |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen) | 顯示功能相關，基本必備。 | 

# Known issues
1. 雙螢幕皆開啟的情況下開機，進入macOS會有水平狀的黑條，可熱插拔螢幕或進入macOS後再開啟第二螢幕解決。
2. 進入opencore選擇器，蘋果商標跑進度條時和睡眠/喚醒時會爆音，Deskmini H310也有相同問題而[viorel78](https://github.com/viorel78/ASRock-DeskMini-310/issues/1) 提出購買官方的後置音源線可解決此問題的辦法。
3. DRM內容由於蘋果是用綁定硬體的方式，因此只有內顯無法用Safari撥放Netflix等網站。可以用Firefox、Chrome、Edge等瀏覽器取代。

# To be done in the future
1. 客製自己的SSDTs。
2. 持續關注顯示問題和聲音問題的解決方法。
3. 雙啟動macOS Monterey和Win11且研究bios啟用secure boot的方法。

# Debugging journey
1. 有問題先重設NVRAM
2. 利用OpenCore的除錯版本取得資訊，參閱[Dortania's OpenCore Install Guide-debugging](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html)
