# ThinkPad-T480-OpenCore0.6.6-Hackintosh
 ThinkPad T480 OC0.6.6 黑苹果引导EFI

**状态 | 稳定**

![](https://img.shields.io/badge/MacOS-11.2.1-brightgreen)

![OpenCore](https://img.shields.io/badge/OpenCore-0.6.6-blue.svg)

**免责声明:**

在开始配置您的EFI之前，请您务必仔细阅读 [OpenCore 0.6.6](https://dortania.github.io/OpenCore-Install-Guide/) 的官方安装指导文档，如使用本引导导致硬件出现各种故障或损坏，本人概不负责。如果您在使用本引导出现错误或者一些问题时，可以考虑在 `issues` 提问。

如果您发现本 `EFI` 引导程序对你很有帮助，请给本仓库点一个 `Star` 以便让更多的人们看到。

本仓库大量参考自[https://github.com/EETagent/T480-OpenCore-Hackintosh](https://github.com/EETagent/T480-OpenCore-Hackintosh) 仓库，在此对原仓库作者表示感谢。

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
| 声卡             | 瑞昱  @ 英特尔 High Definition Audio 控制器 |                                                              |
| 键鼠             | PS2 Keyboard & Synaptics TrackPad           | [YogaSMC](https://github.com/zhen-zen/YogaSMC) 用于媒体键（如麦克风开关等）PrtSc映射为F13 |

</details>  

<details>
<summary><strong>软件版本</strong></summary>
<br>

| Component     | Version        |
| ------------- | -------------- |
| macOS Big Sur | 11.2.1 (20C69) |
| OpenCore      | v0.6.6         |

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
|  AudioDxe.efi   | OpenCorePkg 0.6.5 |
|   HfsPlus.efi   | OcBinaryData      |
| OpenCanopy.efi  | OpenCorePkg 0.6.5 |
| OpenRuntime.efi | OpenCorePkg 0.6.5 |
</details>

<details>
    <summary><strong>Neofetch 截图</strong></summary>
    <br>
    <p float="left">
        <img src="https://i.loli.net/2021/02/28/YBIPstrCp7Fc23W.png" alt="Neofetch BigSur" width="350">
    </p>
</details> 
## Before installation

<details>  

<summary><strong>UEFI settings</strong></summary>
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

<summary><strong>Own prev-lang-kbd</strong></summary>
<br>

Either add as a string or as a data ( HEX data [(ProperTree)](https://github.com/corpnewt/ProperTree) )

Format is lang-COUNTRY:keyboard

- 🇺🇸 | [0] en_US - U.S --> en-US:0 --> 656e2d55 533a30

- 🇨🇿 | [30776] cs - Czech --> cs-CZ:30776 --> 63732d43 5a3a3330 373736

- 🇨🇿 | cs-CZ:0 --> 63732d43 5a3a30

etc.

[AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

</details>

<details>

<summary><strong>Secure Boot (Optional)</strong></summary>
<br>

1. Set Secure Boot to Setup Mode. Secure Boot should be reported as off by UEFI main tab
2. Create FAT32 formatted USB
3. Create EFI folder in the root of the newly formatted flash drive and move there content of SecureBoot/KeyTool
4. Boot flash drive via F12 boot menu
5. Choose **Edit keys**


<img src="./Other/README_Resources/SecureBoot/MainMenu.png" alt="Main menu">

6. Start by **replacing** Signature Database. Select .auth file


<img src="./Other/README_Resources/SecureBoot/ManipulateKey.png" alt="Select key to manipulate with">
<img src="./Other/README_Resources/SecureBoot/SelectAuth.png" alt="Select .auth file">


7. Do the same for Key Exchange Keys Database (KEK) and Platform Key (PK) **in this order**
8. Exit and shutdown your machine
9. Boot into the UEFI settings and check if Secure Boot is reported as `on`
10. Boot you favorite OS with Secure Boot enabled

[More detailed information here](https://habr.com/en/post/273497)

```diff
! Still quite experimental
```

</details>

## Post-Install

<details>  

<summary><strong>Colour banding</strong></summary>
<br>

If you encounter some serious colour banding issues ( Keep in mind that T480 1080p stock panel colour accuracy is not really good, cca 50-60% sRGB), your only solution is to replace GPU properties as bellow or replace the stock panel with one from T490 (400 nits, Low power).

```
<key>AAPL,ig-platform-id</key>
<data>AAAWGQ==</data>
<key>device-id</key>
<data>FhkAAA==</data>
</dict>
```

Do not use these any additional boot arguments! Get custom WhateverGreen version instead from Other folder

You can check your screen in gradient test [here](https://www.eizo.be/monitor-test/) or just by simple look at Launchpad background.

</details>  

<details>  

<summary><strong>Generate your own SMBIOS</strong></summary>
<br>

[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

- MacBookPro14,1

- MacBookPro15,2

</details>  

<details>  

<summary><strong>CPUFriend power management</strong></summary>
<br>

Generate CPUFriendDataProvider for your machine [here](https://github.com/fewtarius/CPUFriendFriend) or use at your own risk files provided in the Other folder.

</details>  

<details>  

<summary><strong>VoltageShift undervolt</strong></summary>
<br>

It is possible to use VoltageShift directly from the EFI folder instead of disabling SIP. You need to use specific version provided in the Other folder.

```diff
! If you want to use this feature, enable it in config.plist
```
</details>  

<details>  

<summary><strong>Android USB Tethering | HoRNDIS</strong></summary>
<br>

> **Important:** Mac computers can't tether with Android. 

I don't think so Google.

1. Using a USB cable, connect your phone to the other device. A "Connected as a…" notification shows at the top of the screen.
2. Open your phone's Settings app.
3. Tap Network & internet ![And then](https://lh3.googleusercontent.com/WD3LKKej34vq3cZXwilgeahIPOiokN2uarmkDxtMqKMFg4SSys8BkOBJbn4_4R930gE=h18 "And then") Hotspot & tethering.
4. Turn on USB tethering.

You should see new Ethernet connection in the network settings. Works with USB Type C and USB A.

```diff
! If you want to use this feature, enable it in config.plist
```
Problems with recreating new `en` device every time are now solved on latest macOS versions with patched version of this kext. If it does not work for you, revert to official version.

</details>  

## Status

<details>  

<summary><strong>What's working ✅</strong></summary>

- [x] Battery percentage

- [x] Bluetooth - Intel Wireless-AC 8265 (0x0A2B) 

- [x] Boot chime

- [x] Boot menu `OpenCanopy` 

- [x] CPU power management / performance `Now on par with Windows without XTU undervolt.`

- [x] FireVault 2 `No config.plist changes needed` 

- [x] GPU UHD 620 hardware acceleration / performance 

- [x] HDMI `Closed and opened lid. With audio.`

- [x] iMessage, FaceTime, App Store, iTunes Store. **Generate your own SMBIOS**

- [x] Intel I219V Ethernet port

- [x] Keyboard `Volume and brightness hotkeys. Another media keys with YogaSMC.`

- [x] Microphone `With keyboard switch using ThinkPad Assistant.`

- [x] Realtek® ALC3287 ("ALC257") Audio

- [x] SD card reader `Fortunately, USB connected.`

- [x] Sidecar wired `Works with 15,2 SMBIOS.`

- [x] Sleep/Wake 

- [x] TouchPad `1-5 fingers swipe works. Emulate force touch using longer and more voluminous touch.`

- [x] TrackPoint  `Works perfectly. Just like on Windows or Linux.`

- [x] USB Ports `USB Map is different for devices with Windows Hello camera.`

- [x] Web camera

- [x] Wifi - Intel Wireless-AC 8265 `Use HeliPort app for Wi-Fi control`

- [x] DRM `Widevine, validated on Firefox 82. WhateverGreen's DRM is broken on Big Sur`

</details>  

<details>  

<summary><strong>What's not working ⚠️</strong></summary>

- [ ] Fingerprint reader  `There is finally after many years working driver for Linux (python-validity), don't expect macOS driver any time soon.`

- [ ] PM 981 `Still unstable. Could work for some, not for others.`

- [ ] Sidecar wireless `If you want to use this feature, buy a compatible Broadcom card!`

- [ ] Windows/Linux from OC boot menu `It's best practice to not boot from OC when planning to perform firmware upgrade`


</details>  

<details>  

<summary><strong>Untested</strong></summary>

- [ ] Thunderbolt  `No device to test.`

</details>  

## UEFI modding

<details>  

<summary><strong>CFG Lock | Advanced menu</strong></summary>
<br>

<img align="left" src="./Other/README_Resources/SPI_Programmer_CH341a.jpg" alt="SPI_Programmer_CH341a.jpg" width="220">

It's possible to unlock Advanced menu thus disable CFG Lock natively in UEFI + Other Advanced menu benefits. SPI Programmer CH341a is required

<br>
https://www.reddit.com/r/thinkpad/comments/ffqqx5/currently_testing_skyra1n/

[T480 consuming 60w (~85w total) - unlimited TDP : thinkpad](https://www.reddit.com/r/thinkpad/comments/g8fk51/t480_consuming_60w_85w_total_unlimited_tdp/)

[ThinkPad discord](discord.gg/Ybdz7AS)

</details>  