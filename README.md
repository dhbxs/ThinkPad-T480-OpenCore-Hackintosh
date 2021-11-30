# ThinkPad-T480-OpenCore0.7.5-Hackintosh
 ThinkPad T480 OC0.7.5 黑苹果引导EFI

**状态 | 稳定**

![MacOS](https://img.shields.io/badge/MacOS-11.2.2-brightgreen) 
![OpenCore](https://img.shields.io/badge/OpenCore-0.6.7-blue.svg)



**免责声明:**

在开始配置您的EFI之前，请您务必仔细阅读 [OpenCore 0.7.5](https://dortania.github.io/OpenCore-Install-Guide/) 的官方安装指导文档，如使用本引导导致硬件出现各种故障或损坏，本人概不负责。如果您在使用本引导出现错误或者一些问题时，可以考虑在 `issues` 提问。

如果您发现本 `EFI` 引导程序对你很有帮助，请给本仓库点一个 `Star` 以便让更多的人们看到。

本仓库大量参考自 [https://github.com/EETagent/T480-OpenCore-Hackintosh](https://github.com/EETagent/T480-OpenCore-Hackintosh) 仓库，在此对原仓库作者表示感谢。

对于国内用户，下载较慢，请访问 `Gitee` 仓库 [https://gitee.com/dhbxs/think-pad-t480-open-core0.7.5-hackintosh](https://gitee.com/dhbxs/think-pad-t480-open-core0.6.7-hackintosh)

## 基本介绍

<details>
<summary><strong>硬件信息</strong></summary>
<br>

| 类别             | 型号                                        | 备注                                                         |
| ---------------- | ------------------------------------------- | ------------------------------------------------------------ |
| 主板             | 联想 20L系列                                | 7th/8th Generation Intel Processor Family I/O - 9D4E 笔记本芯片组 |
| BIOS             | 联想 N24ET60W (1.35)                        | BIOS程序发布日期: 2020/10/08                                 |
| CPU              | Intel Core i5-8250U                         | [英特尔 Core i5-8250U @ 1.60GHz 四核](https://ark.intel.com/content/www/us/en/ark/products/124967/intel-core-i5-8250u-processor-6m-cache-up-to-3-40-ghz.html) |
| GPU              | Intel UHD 620                               | 英特尔 UHD Graphics 620 ( 128 MB / 联想 )                    |
| SSD              | LITEON T11 Plus 256                         | 建兴256G nvme 固态硬盘                                       |
| 内存             | 16GB DDR4 2400Mhz                           | 海力士(Hynix) DDR4 2666MHz 8GB                                                   金士顿(Kingston) DDR4 2400MHz 8GB |
| 电池             | 单电池                                      | 单个外置电池，无内置电池                                     |
| 相机             | 720p 相机                                   |                                                              |
| WIFI & Bluetooth | Intel Wireless-AC 8265                      | 使用 [AirportItlwm v1.3.0-alpha](https://github.com/OpenIntelWireless/itlwm/releases) 驱动 |
| 有线网卡         | Ethernet Connection  I219-V                 | 英特尔 Ethernet Connection  I219-V / 联想                    |
| 声卡             | 瑞昱  @ 英特尔 High Definition Audio 控制器 | alc=11                                                       |
| 键鼠             | PS2 Keyboard & Synaptics TrackPad           | [YogaSMC](https://github.com/zhen-zen/YogaSMC) 用于媒体键（如麦克风开关等）PrtSc映射为F13 |

</details>  

<details>
<summary><strong>软件版本</strong></summary>
<br>

| Component     | Version |
| ------------- | ------- |
| macOS Big Sur | 11.2.1  |
| OpenCore      | v0.6.7  |

</details>

<details>
<summary><strong>Kernel 驱动版本</strong></summary>
<br>

| Kext                   | Version        |
| :--------------------- | -------------- |
| AirportItlwm           | v1.3.0-alpha   |
| AppleALC               | 1.5.7          |
| AppleBacklightSmoother | 1.0.2          |
| BrightnessKeys         | 1.0.1          |
| CPUFriend              | 1.2.3          |
| CPUFriendDataProvider  | i5-8250U       |
| HibernationFixup       | 1.3.9          |
| HoRNDIS                | Disabled, 9.2  |
| IntelBluetoothFirmware | 1.1.2          |
| IntelBluetoothInjector | 1.1.2          |
| IntelMausiEthernet     | 2.5.1.d1       |
| Lilu                   | 1.5.1          |
| NoTouchID              | 1.0.4          |
| NVMeFix                | 1.0.5          |
| RTCMemoryFixup         | 1.0.8          |
| VirtualSMC             | 1.2.0          |
| VoltageShift           | Disabled, 1.22 |
| VoodooPS2Controller    | 2.2.0          |
| VoodooRMI              | 1.3.0          |
| VoodooSMBus            | 3.0.0          |
| WhateverGreen          | 1.4.7          |
| YogaSMC                | 1.4.1          |

</details>

<details>
<summary><strong>UEFI drivers</strong></summary>
<br>

|     Driver      | Version           |
| :-------------: | ----------------- |
|  AudioDxe.efi   | OpenCorePkg 0.6.7 |
|   HfsPlus.efi   | OcBinaryData      |
| OpenCanopy.efi  | OpenCorePkg 0.6.7 |
| OpenRuntime.efi | OpenCorePkg 0.6.7 |

</details>

<details>
    <summary><strong>Neofetch 截图</strong></summary>
    <br>
    <p float="left">
        <img src="https://i.loli.net/2021/02/28/YBIPstrCp7Fc23W.png" alt="Neofetch BigSur" width="350"/>
    </p>
</details> 

## 安装前

<details>  
<summary><strong>UEFI 设置</strong></summary>
<br>
**Security**

- `Security Chip` **Disabled**
- `Memory Protection -> Execution Prevention` **Enabled**
- `Virtualization -> Intel Virtualization Technology` **Enabled**
- `Virtualization -> Intel VT-d Feature` **Enabled**
- `Anti-Theft -> Computrace -> Current Setting` **Disabled**
- `Secure Boot -> Secure Boot` **Disabled**
- `Intel SGX -> Intel SGX Control` **Disabled**
- `Device Guard` **Disabled**

**Startup**

- `UEFI/Legacy Boot` **UEFI Only**
- `CSM Support` **No**

**Thunderbolt**

- `Thunderbolt BIOS Assist Mode` **Disabled**
- `Wake by Thunderbolt(TM) 3` **Disabled**
- `Security Level` **User Authorization**
- `Support in Pre Boot Environment -> Thunderbolt(TM) device` **Enabled**

</details>  

<details>
<summary><strong>设置键盘规格</strong></summary>
<br>

根据你的键盘型号，填入以下值到`config.plist` -> `NVRAM` -> `7C436110-AB2A-4BBB-A880-FE41995C9F82` -> `prev-lang:kbd`

![截屏2021-03-06 下午8.09.10](https://cdn.jsdelivr.net/gh/zhao-v/blog-img@master/uPic/%E6%88%AA%E5%B1%8F2021-03-06%20%E4%B8%8B%E5%8D%888.09.10.png)

- 🇺🇸 | [0] en_US - U.S --> en-US:0 --> 656e2d55 533a30

- 🇨🇿 | [30776] cs - Czech --> cs-CZ:30776 --> 63732d43 5a3a3330 373736

- 🇨🇿 | cs-CZ:0 --> 63732d43 5a3a30

其他型号请查看以下文档：

[AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

</details>

## 安装后

<details>  

<summary><strong>生成你自己的 SMBIOS 信息</strong></summary>
<br>

[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

- MacBookPro15,2

</details>  

<details>  

<summary><strong>CPUFriend 电源管理</strong></summary>
<br>

如果想要配置自己的CPUFriend驱动，请查看 [here](https://github.com/fewtarius/CPUFriendFriend) 
也可以使用我提供的CPUFriend驱动。

</details>  

## 状态

<details>  

<summary><strong>正常工作的硬件 ✅</strong></summary>

- [x] 电池百分比

- [x] 蓝牙和Wi-Fi - Intel Wireless-AC 8265 (0x0A2B) 

- [x] Boot chime

- [x] Boot menu `OpenCanopy` 

- [x] CPU 电源管理/ 性能`Now on par with Windows without XTU undervolt.`

- [x] FireVault 2 `No config.plist changes needed` 

- [x] GPU UHD 620 显卡硬件加速/性能 

- [x] HDMI 接口`Closed and opened lid. With audio.`

- [x] iMessage, FaceTime, App Store, iTunes Store. **需要生成自己的SMBIOS信息**

- [x] Intel I219V 以太网卡/有线网卡

- [x] 键盘`Volume and brightness hotkeys. Another media keys with YogaSMC.`

- [x] 麦克风`With keyboard switch using ThinkPad Assistant.`

- [x] 声卡Realtek® ALC3287 ("ALC257") Audio

- [x] SD 读卡器/卡槽 `Fortunately, USB connected.`

- [x] 睡眠/唤醒

- [x] 触控板`1-5 fingers swipe works. Emulate force touch using longer and more voluminous touch.`

- [x] 指点杆/小红点`Works perfectly. Just like on Windows or Linux.`

- [x] USB 接口 `USB Map is different for devices with Windows Hello camera.`

- [x] Wifi - Intel Wireless-AC 8265 

- [x] DRM `Widevine, validated on Firefox 82. WhateverGreen's DRM is broken on Big Sur`

</details>  

<details>  

<summary><strong>未能正常工作的硬件⚠️</strong></summary>

- [ ] PM 981 `Still unstable. Could work for some, not for others.`

- [ ] 无线随航`需要更换 Broadcom 网卡`

- [ ] 从OC引导的Windows系统不能正常启动 


</details>  

<details>  

<summary><strong>未能测试</strong></summary>

- [ ] Thunderbolt雷电接口  `没有设备做测试`

</details>  