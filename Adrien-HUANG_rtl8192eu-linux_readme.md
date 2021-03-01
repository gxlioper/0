## rtl8192eu-linux
Realtek rtl8192eu official Linux driver v5.2.19.1

This driver is based on the (latest) official Realtek v5.2.19.1 driver with fixes and improvements to support the latest kernels (up to 5.1).

### Automated install 

Run from driver directory:

./install_wifi.sh

### Manual install

Remove available drivers with (skip if `sudo lshw -C network` and `dkms status` do not show any wifi drivers):

```
sudo rmmod 8192eu
sudo rmmod rtl8xxxu
sudo dkms remove rtl8192eu/1.0 --all
```

Blacklist default driver (rtl8xxxu on Ubuntu):

```
echo "blacklist rtl8xxxu" >> ./blacklist-rtl8xxxu.conf
sudo mv ./blacklist-rtl8xxxu.conf /etc/modprobe.d/
```

Run add and install commands from driver directory:

```
sudo dkms add .
sudo dkms install rtl8192eu/1.0
```

Load driver (or reboot):

`sudo modprobe 8192eu`






 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)