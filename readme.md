# ThinkPad X230 Clover Config for macOS 10.12.6

Saved for future use.
Maybe I want to play someday :)

留存供日后使用。
万一我哪天想拿出来玩了呢~
中文版向后翻。

## Summary

**Hardware**

 - CPU : Intel Core i5 - 3320M
 - RAM : 4GB DDR3 1600MHz x2
 - Storage : 120G LITEONIT M3S
 - WLAN Card : Atheros AR9285
 - Screen : 1080p IPS (Using special kit - NOT RECOMMEND - making a lot of problems on hacktonish)
 
-----

**Not working**
 - VGA Port (not exist on a real macbook)
 - SDCard Reader
 - Sleep (fail to awake)
 - Brightness control (issue after macOS 10.12.4)
 
-----

**BIOS Configuration**

| Item                                                    	| Setting   	| Remarks                                                                                                       	|
|---------------------------------------------------------	|-----------	|---------------------------------------------------------------------------------------------------------------	|
| Config/Network/Wake On Lan                              	| Disabled  	| Not Supported.                                                                                                	|
| Config/USB UEFI BIOS Support                            	| Enabled   	| Important for booting into USB Installer for OS X/ macOS.                                                     	|
| Config/USB 3.0 Mode                                     	| Enabled   	| Enables USB 3.0                                                                                               	|
| Config/Power/Intel SpeedStep Technology                 	| Enabled   	| Enables Intel SpeedStep.                                                                                      	|
| Config/Power/Intel Rapid Start Technology               	| Disabled  	| This feature requires a hibernation partition (0xA0). Not supported on OS X / macOS.                          	|
| Config/Power/CPU Power Management                       	| Enabled   	| Enables CPU Power Management.                                                                                 	|
| Config/Serial ATA (SATA)/SATA Controller Mode Option    	| AHCI      	| Enables AHCI which is better for SSDs and HDDs.                                                               	|
| Security/Predesktop Authentication                      	| Optional  	| Fingerprint is not supported on macOS / OS X but you can still use it for waking your ThinkPad.               	|
| Security/Security Chip                                  	| Disabled  	| Disable it if you have a modified UEFI Firmware.                                                              	|
| Security/Memory Protection/Execution Prevention         	| Enabled   	| This enables NX which is required for macOS / OS X installations.                                             	|
| Security/Virtualization/Intel Virtualization Technology 	| Enabled   	| Delete boot argument named "dart=0" in config.plist if you set this as Disabled.                              	|
| Security/Virtualization/Intel VT-d Feature              	| Enabled   	| Delete boot argument named "dart=0" in config.plist if you set this as Disabled.                              	|
| Security/Secure Boot/Secure Boot                        	| Disabled  	| Not supported by Clover.                                                                                      	|
| Startup/Boot Mode                                       	| Quick     	| This is optional.                                                                                             	|
| Startup/UEFI / Legacy Boot                              	| UEFI Only 	| Reduces Confusion.                                                                                            	|
| Startup/UEFI / Legacy Boot/CSM Support                  	| No        	| Setting this key as Yes requires a CSM Video Driver in Clover to provide proper video output on macOS / OS X. Only change this to Yes if you are dual booting with Windows 7 and installed CSMVideoDxe Driver in /EFI/CLOVER/drivers64UEFI/. 	

-----

**For Users who have i3 / i7 ThinkPad X230, Please replace your SSDT to enable Native CPU Power Management**
(Credit goes to Piker-Alpha)

1.  Download ssdtPRGen.sh (using Google)
2.  Run this command  `sudo sh ssdtPRGen.sh`
3.  Obtain SSDT.aml from ~/Library/ssdtPRGen/
4.  Copy (Or Replace) it to /EFI/CLOVER/ACPI in your EFI System Partition of the SATA HDD/SSD in your ThinkPad.

--------------------
## Issues about High-resolution kit(1080p or 2K Display)

1.	**HiDpi only supports 1280*800**
	Because Intel HD4000 can only support 3840*2160(single screen) or 2560*1600(dual screen)
	Hi-res kit uses "Duplicate Mode", which means it actually output on two screen(one is lvds onboard, another one is using the DisplayPort from dock).
	HiDpi actually renders a larger(2x) size(example:1280*800 -> 2560*1600).
	2560*1600 is the limit of HD4000.
	So HiDpi only supports 1280*800.
	If you kit doesn't use Duplicate Mode, everything should be ok.
	
2.	**Screen may not "light" after wake**
	Because the screen was treated as an external screen, and stay unpowered.
	I am wondering if non-duplicate mode kit can solve this problem.

3.	**Battery Drain**
	As render 2 screens always consume more power than one...

-------------------

## 概述
**硬件**

 - CPU : Intel Core i5 - 3320M
 - 内存 : 4GB DDR3 1600MHz x2
 - 硬盘 : 120G 建兴 M3S
 - 无线网卡 : Atheros AR9285
 - 屏幕 : 1080p IPS (使用X教授套件 - 不建议改过屏的机器黑苹果，可能会有很多意料之外的问题)
 
-----

**已知问题**
 - VGA接口 (因为Macbook确实没这玩意)
 - SD卡读卡器
 - 待机休眠 (唤醒之后点不亮)
 - 亮度调节 (macOS 10.12.4之后出现的问题)
 
-----

**BIOS设置**

| 选项                                                    	| 设置      	|
|---------------------------------------------------------	|-----------	|
| Config/Network/Wake On Lan                              	| Disabled  	|
| Config/USB UEFI BIOS Support                            	| Enabled   	|
| Config/USB 3.0 Mode                                     	| Enabled   	|
| Config/Power/Intel SpeedStep Technology                 	| Enabled   	|
| Config/Power/Intel Rapid Start Technology               	| Disabled  	|
| Config/Serial ATA (SATA)/SATA Controller Mode Option    	| AHCI      	|
| Security/Predesktop Authentication                      	| 随意		  	|
| Security/Security Chip                                  	| Disabled  	|
| Security/Memory Protection/Execution Prevention         	| Enabled   	|
| Security/Virtualization/Intel Virtualization Technology 	| Disabled   	|
| Security/Virtualization/Intel VT-d Feature              	| Disabled   	|
| Security/Secure Boot/Secure Boot                        	| Disabled  	|
| Startup/Boot Mode                                       	| Quick     	|
| Startup/UEFI / Legacy Boot                              	| UEFI Only 	| 
| Startup/UEFI / Legacy Boot/CSM Support                  	| No        	|

-----

**使用 i3 / i7 处理器的 ThinkPad X230用户, 请自行生成SSDT.aml文件来启用电源管理**
(感谢Piker-Alpha)

1.  下载ssdtPRGen.sh (上网找一下)
2.  在中断运行 `sudo sh ssdtPRGen.sh`
3.  去 ~/Library/ssdtPRGen/ 找到生成的SSDT.aml
4.  把SSDT.aml复制到/EFI/CLOVER/ACPI （如果存在了就替换掉）

--------------------
## 高分屏套件可能存在的问题(1080p 或 2K 屏幕)

1.	**HiDpi 仅支持 1280*800**
	因为 Intel HD4000 机能所限，只能输出3840*2160(单屏幕)或2560*1600(双屏)
	而高分屏套件大多使用复制模式，意味着实际上是在输出两块屏幕(一个是板载的lvds，另一块是实际显示的屏幕，从底座的DP接口转接而来).
	而HiDpi实际上是渲染画面的两倍大小，再压进物理分辨率(例子：1280*800 -> 2560*1600).
	2560*1600 又恰好是 HD4000 双屏时的极限.
	于是 HiDpi 只能支持 1280*800.
	不是通过复制模式来实现的套件应该没有这个问题
	
2.	**唤醒之后屏幕无法点亮**
	因为屏幕被当作外屏处理，唤醒后没有送电。
	好奇非复制模式的套件是否有这个问题。

3.	**耗电**
	渲染两个屏幕的画面总比一个耗电……

-------------------
## Reference 参考资料

1.	关于屏幕亮度的修正（不知道为啥我这一直不太成功）
	Fix about screen brightness control(not success on my machine, but worth trying)
	https://www.tonymacx86.com/threads/guide-laptop-backlight-control-using-applebacklightinjector-kext.218222/
2.	https://github.com/chuckhacker/ThinkPad-X230-macOS-10.12.2
3.	https://github.com/Bizzaro/x230-osx