# Deskmini-H470-Opencore-EFI
此为deskmini h470专用之opencore 7.3导引文件范例。  
黑苹果之完成度与硬件有关，任何硬件上个改变皆可能需要重新设定config.plist文件。  
[English](README.md)        
[繁體中文](README_ZH-TW.md)

| 硬体设备  |  我的硬件 |  评语 |
|----------|-------------|------|
| 主机板 |  Asrock H470-stx | 华擎迷你主机。 |
| CPU |    intel i3-10100   |   Comet lake处理器。 |
| CPU 散热器| ID-cooling IS-40x | 安装时风扇会刮到机壳，稍微抬起机壳即可塞入，风扇可运转不会打机壳。|
| 显卡 | 内显UHD630 | 最多支持三个萤幕。 |
| 记忆体 |  Crucial DDR4 3200 8GB SODIMM x2 | 效能过剩，i3-10100在此主机板只能跑到2666MHz频率。 |
| 硬碟 |    Cruicial P5 Nvme 1tb | Opencore选择画面到登入画面约13秒。 |
| 音效卡 | 内建Realtek ALC235 | 官方规格列为ALC233但苹果和微软都判定为ALC235编码。 | 
| Wifi/Bluetooth | BCM94352Z/DW1560 | Sidecar及airdrop都可用。 |
| Operating system | Win 10, Big Sur | 同一固态硬碟上双开苹果和微软系统。 |

# Hackintosh
1. HDMI和DP揭开机有画面type c输出没有测。
2. HDMI及DP的音效皆可。
3. 睡眠/唤醒可。
4. 依[Dortania's OpenCore OpenCore Post-Install-Fixing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html)启用能源节省项目。  
5. Opencore和系统更新测试可(从Big Sur 11.5.2-> 11.6, Opencore 7.2-> 7.3)。
6. Airdrop和sidecar可用。
7. Facetime和imessages等需要更改SerialNumber, UUID, MLB, ROM且最好有一个用过一阵子的Apple ID(比较不起疑，有正版苹果装置登录过最好)，参阅[Dortania's OpenCore Post-Install-iservices](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html)。

# Kexts
就我的理解，kexts就像插件一样用来沟通硬件和macOS之间的讯息。而SSDT虽然有一样的功能，但kexts外挂和模组化的特性能让升级macOS时减少损坏的机会。Kexts的数量会稍微影响开机的速度，可因自己的需求和硬体斟酌哪些kext是自己需要的。  

| Kexts |     简单介绍 |
|----------|-------------|
| [AirportBrcmFixup](https://github.com/acidanthera/AirportBrcmFixup) | 让Broadcom的wifi/BT网卡能辨识，才能有Wifi。 | 
| [AppleALC](https://github.com/acidanthera/AppleALC) | 辨识音讯硬体而有声音。 |   
| [BrcmBluetoothInjector](https://github.com/acidanthera/BrcmPatchRAM)| 辨识Broadcom的蓝芽功能，三件套1/3一组。 | 
| [BrcmFirmwareData](https://github.com/acidanthera/BrcmPatchRAM) | 辨识Broadcom的蓝芽功能，三件套2/3一组。 |
| [BrcmPatchRAM3](https://github.com/acidanthera/BrcmPatchRAM) |  辨识Broadcom的蓝芽功能，三件套3/3一组。 | 
| [CPUFriendDataProvider](https://github.com/stevezhengshiqi/one-key-cpufriend) | 启用电脑的节能选项。 |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock) | 让较旧的Mac和Ipad启用AirPlay, Sidecar, Universal Control Unlock, NightShift等功能。 | 
| [IntelMausi](https://github.com/acidanthera/IntelMausi)| 辨识Intel的乙太网路。 |
| [Lilu](https://github.com/acidanthera/Lilu) | macOS的核心相关，基本上必备。 |
| [NVMeFix](https://github.com/acidanthera/NVMeFix) | 修补Apple对于NVMe磁碟的相容性和功能。 | 
| [SMCSuperIO](https://github.com/acidanthera/VirtualSMC) | 修补监测硬件资讯的功能。 |
| [USBPorts](https://dortania.github.io/OpenCore-Post-Install/usb/) | 定义USB孔的硬件资讯。 | 
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC) | 模拟Apple的System Management Controller系统。 |
| [WhateverGreen](https://github.com/acidanthera/WhateverGreen) | 显示功能相关，基本必备。 | 

# Known issues
1. 双萤幕皆开启的情况下开机，进入macOS会有水平状的黑条，可热插拔萤幕或进入macOS后再开启第二萤幕解决。
2. 进入opencore选择器，苹果商标跑进度条时和睡眠/唤醒时会爆音，Deskmini H310也有相同问题而[viorel78](https://github.com/viorel78/ASRock-DeskMini-310/issues/1) 提出购买官方的后置音源线可解决此问题的办法。
3. DRM内容由于苹果是用绑定硬件的方式，因此只有内显无法用Safari拨放Netflix等网站。可以用Firefox、Chrome、Edge等浏览器取代。

# To be done in the future
1. 客製自己的SSDTs。
2. 持续关注显示问题和声音问题的解决方法。
3. 双启动macOS Monterey和Win11且研究bios启用secure boot的方法。

# Debugging journey
1. 有问题先重设NVRAM
2. 利用opencore的除错版本取得资讯，参阅[Dortania's OpenCore Install Guide-debugging](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/debug.html)
