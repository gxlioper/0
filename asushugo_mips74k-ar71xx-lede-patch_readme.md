Custom LEDE Patch For TL-WDR3500/3600/4300/4310/MW4350R
======================================================

Dependencies
------------

* LEDE BuildRoot
* LEDE BuildRoot Dependencies
* Java Runtime

How to use
----------

* Install all the development packages required for LEDE BuildRoot
* Install Java Runtime
* Clone the LEDE Repository

    git clone https://github.com/lede-project/source.git lede

Clone this Repository and copy into the LEDE repository

    git clone https://github.com/gwlim/mips74k-lede-patch.git temp ; mv temp/* lede/; rm -rf temp

Change directory into the LEDE Repository

    cd lede

Run the script

./patch_LEDE.sh

Make Menuconfig Default Target Profile is TL-WDR4300 (all the packages and config is inside)

    make menuconfig

Save and make

    make V=s


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)