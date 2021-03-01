[![license][1]][2]
[![PRs Welcome][3]][4]
[![Issue Welcome][5]][6]
[![Release Version][7]][8]
[![OpenWRT][11]][12]


[1]: https://img.shields.io/badge/license-GPLV3-brightgreen.svg?style=plastic
[2]: https://github.com/wificoin-project/wwas/edit/master/LICENSE
[3]: https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=plastic
[4]: https://github.com/wificoin-project/wwas/pulls
[5]: https://img.shields.io/badge/Issues-welcome-brightgreen.svg?style=plastic
[6]: https://github.com/wificoin-project/wwas/issues/new
[7]: https://img.shields.io/badge/release-0.8.150-red.svg?style=plastic
[8]: https://github.com/wificoin-project/wwas/releases
[11]: https://img.shields.io/badge/Platform-%20OpenWRT%7C%20LEDE%20-brightgreen.svg?style=plastic
[12]: https://github.com/KunTengRom/kunteng-lede-17.01.4



# wificoin-wifidog-auth-server
wwas is an [apfree wifidog](https://github.com/liudf0716/apfree_wifidog) auther server (it also support original wifidog), which especially supporting wfc payment  and weixin lian.

## how to run server side

```
git clone https://github.com/wificoin-project/wificoin-wifidog-auth-server

cd wificoin-wifidog-auth-server

npm install 

npm start

```

## how to run apfree wifidog side

the config of apfree wifidog in openwrt is the following:

```
config wifidog
	option	gateway_interface	'br-lan'
	option	auth_server_hostname	'wifidog.kunteng.org.cn'
	option	auth_server_port	8001
	option	auth_server_path	'/wifidog/'	
	option	check_interval		60
	option	client_timeout		72000
	option	httpd_max_conn		200
	option	pool_mode			1
	option	thread_number		5
	option	queue_size			20
	option	wired_passed		0
	option	enable		1

config mqtt	'mqtt'
  	option	mqtt_hostname	'wifidog.kunteng.org.cn'
  	option	mqtt_port		'8883'
  	option	mqtt_topic		''

```

### ui config

![image](https://github.com/heartache1987/images/blob/master/wifidog%20%E7%95%8C%E9%9D%A2%E9%85%8D%E7%BD%AE.png)

u can change 'wifidog.kunteng.org.cn' to your own wifidog auth server domain

## How To Contribute

Feel free to create issues or pull-requests if you have any problems.

**Please read [CONTRIBUTING.md](https://github.com/wificoin-project/wificoin-wifidog-auth-server/blob/master/CONTRIBUTING.md) before pushing any changes.**


## contact us
qq group: 424031785


## donate
### wfc: [weiKbu9DYg26gH2zucSHJHgH5KsuuZd3wW](https://wfc.xyblock.net/#/wifiPortal/donate)


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)