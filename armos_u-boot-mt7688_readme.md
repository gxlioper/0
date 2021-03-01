#u-boot-mt7688
##dhcpd uboot for Widora V1.0.7
***
#How to use
* 1.make menuconfig
* 2.select MT7628 board
* 3.make clean;make

#Note
* note:compile need java such as 1.7.0_79

#update list
* change bps to 115200,fix gpio39,40,41,42 low when startup
* add all gpio test,just press 'WPS' button with more than 7 seconds at power on
* web failsafe update mode,just press 'WPS' button with 2 to 7 seconds at power on
* web failsafe IP is 192.168.1.111
* DDR2 can be 64MB or 128MB,just select 512Mbit or 1024Mbit in menuconfig
* add dhcp server,address pool(192.168.1.100 - 192.168.1.200)
* QQ:771992497
* mail:[QQMAIL](771992497@qq.com)
* weibo:[@芒果Geek](http://weibo.com/linuxgeek) [@mleaf](http://weibo.com/techlele)
* mleaf: 350983773@qq.com
*##Thanks to Manfeel、cleanwrt、Piotr Dymac、Adam Dunkels。


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)