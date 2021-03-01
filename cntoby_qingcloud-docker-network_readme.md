# 青云Docker网络插件
[![Build Status](https://travis-ci.org/nicescale/qingcloud-docker-network.svg?branch=master)](https://travis-ci.org/nicescale/qingcloud-docker-network)

通过本插件在青云平台使用Docker时，可以为每个容器创建一块独立的网卡，
让Docker直接对接青云的SDN网络，无需端口映射。
用户可以直接为容器分配一个EIP，也可以把容器添加到负载均衡后面。
如果用户与青云建立了VPN连接，可以直接通过桌面浏览器访问容器里的服务。

用户可通过青云的防火墙按需配置每个容器的安全策略。

本网络插件由[希云cSphere](https://csphere.cn)团队开发和维护，欢迎试用和提出宝贵的改进意见。

![csphere](misc/csphere.jpg)

## 注意事项
1. 由于IPAM插件需要通过`--ipam-opt`参数指定vxnet，而这个参数是在Docker 1.10版本才引入的，所以1.10以下的版本目前无法使用本插件。

# 使用方法
1. 登录青云控制台，创建一个VPC网络，然后创建两个私有网络(分别命名为mgmt和user)，并将之加入VPC网络。
2. 基于CentOS 7 64位镜像创建虚拟机，网络选择mgmt。
3. 登录虚拟机，执行 yum remove -y NetworkManager 删除NetworkManger，否则机器上绑定多个网卡时会污染默认路由导致虚拟机无法登录。
4. 向`/etc/sysconfig/network-scripts/ifcfg-eth0`文件里写入以下内容来配置虚拟机主网卡:
  
  ```bash
  TYPE=Ethernet
  DEVICE=eth0
  NAME=eth0
  ONBOOT=yes
  NM_CONTROLLED=no
  BOOTPROTO=dhcp
  ```
5. 执行 `curl https://get.docker.com|bash` 安装Docker
6. 安装并启动青云Docker插件:

  从源码编译安装（依赖于Docker 1.9以上环境）：
  
  ```bash
  git clone https://github.com/nicescale/qingcloud-docker-network.git /tmp/qingcloud-docker-network
  # 国内用户可 git clone https://git.oschina.net/csphere/qingcloud-docker-network.git /tmp/qingcloud-docker-network
  cd /tmp/qingcloud-docker-network
  make
  cp bin/qingcloud-docker-network /bin/
  ```
  
  启动：
  
  ```bash
  ACCESS_KEY_ID=xxxxxxxx SECRET_KEY=xxxxxxxxxx ZONE=sh1a /usr/bin/qingcloud-docker-network
  ```

  或者基于Docker镜像运行插件：
  
  ```bash
	docker run -d --restart=always --name=netplugin --net=host \
    --cap-add NET_ADMIN \
    -v /var/lib/docker/qingcloud-network:/var/lib/docker/qingcloud-network \
    -v /var/run/docker/plugins:/var/run/docker/plugins \
    -e ACCESS_KEY_ID=xxxxxxxx \
    -e SECRET_KEY=xxxxxxxxxx \
    -e ZONE=sh1a \
    csphere/qingcloud-docker-network
  
  ```
7. 创建网络:

  ```bash
  docker network create \
    -d qingcloud \
    --subnet=172.25.1.0/24 \
    --gateway=172.25.1.1 \
    -o vxnet=vxnet-qpxj8ci \
    --ipam-driver=qingcloud  \
    --ipam-opt vxnet=vxnet-qpxj8ci \
    vxnet-qpxj8ci

  ```
  
  其中vxnet 填写给容器使用的那个私有网络的ID，可在青云控制台查看。
  gateway和subnet需要在青云把私有网络加入路由器时指定的网络参数一致。
8. 创建容器测试: docker run -it --rm --net=vxnet-qpxj8ci alpine sh

# Copyright and License
Code developed by cSphere (https://csphere.cn) and released under the Apache 2.0 License.



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)