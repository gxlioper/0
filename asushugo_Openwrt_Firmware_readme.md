Custom OpenWRT Firmware
=======================

OpenWRT for WR1043NDv1 and MR3420v2
----------------------------------------

Source
------

https://github.com/gwlim/mips74k-barrier-breaker-patch
https://github.com/gwlim/mips24k-barrier-breaker-patch


Features
--------

* Customised CFLAGS for mips24kc (For WR1043NDv1) and mips74kc (For MR3420v2 and WDR4300v1)
* Do not use the image for MR3420v2 unless you upgrade the flash chip to at least 8MB
* Updated toolchain to latest Linaro GCC 4.8 and Linaro Binutils
* LuCI Interface Tweaks
* 6.5MB Base Image with Installable Modular Packages

Recovery
--------

* Firmware to restore to default TP-Link Software in [Backup Folder](https://github.com/gwlim/Openwrt_Firmware/tree/master/TP-Link_TL-WR1043ND/BackUp_Image)
* Uboot backup partition available
* Art backup partition available

Overclock
---------

* Overclock firmware for WR1043NDv1 is available in [Backup Folder](https://github.com/gwlim/Openwrt_Firmware/tree/master/TP-Link_TL-WR1043ND/BackUp_Image)
* 2 Preset Overclock: 
* 430MHZ CPU Clock, 430MHZ RAM, and 215MHZ AHB
* 420MHZ CPU Clock, 420MHZ RAM, and 210MHZ AHB
* Tested Stable and Working on my WR1043ND
* To use simply sysupgrade to default TP-Link Factory Firmware using the sysupgrade to factory image then upgrade again using the Overclocked Firmware



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)