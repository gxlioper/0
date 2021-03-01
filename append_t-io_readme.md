
## **t-io: 百万级TCP长连接即时通讯框架，让天下没有难开发的即时通讯**

t-io是基于jdk aio实现的易学易用、稳定耐操、性能强悍、内置功能丰富、核心代码只有3000多行的即时通讯框架，字母 t 寓意talent。

####  **常见应用场景**
    
- IM（官方提供了im例子，含web端）
- 实时监控
- 推送服务（已内置API）
- RPC
- 游戏
- 物联网（已有很多案例）
- 其它实时通讯类型的场景，不一一列举

## maven坐标
```
 
     org.t-io 
     tio-core 
     1.7.0.v20170501-RELEASE 
 
```
## **各种传送门**

 - [官 网][1]
 - [代码托管平台码云](https://git.oschina.net/tywo45/t-io)
 - [开源中国收录地址](https://www.oschina.net/p/t-io)
 - [极速入门][2]
 - [图解bytebuffer](https://my.oschina.net/talenttan/blog/889887)
 - [t-io源码阅读小记](https://my.oschina.net/talenttan/blog/884466)
 - [给jfinal写的t-io插件](https://my.oschina.net/u/1168934/blog/864239)----小徐同学花10分钟完成的作品
 - [用t-io实现的简单rpc](https://my.oschina.net/longtutengfei/blog/892053)----仅作思路参考，部分实现待完善
 - [jfinal + t-io完成的im项目](https://git.oschina.net/kobe577590/im)----作者天蓬小猪正在完善
 - [API][3](只需要看[Aio.java][4])
 - [资料及问题汇总][5]



## **t-io特点**
###  极简洁、清晰、易懂的API
- 没有生涩难懂的新概念，原生态bytebuffer既减少学习成本，又减少各种中间对象的创建
- 只需花上30分钟学习helloworld，就能较好地掌握并实现一个性能极好的即时通讯应用

###  极震撼的性能
- 单机轻松支持**百万级tcp长连接**，彻底甩开业界C1000K烦恼；
- 最高时，每秒可以收发500万条消息，约165M

###  对开发人员极体贴的内置功能
- 心跳检测
- 心跳发送
- 自动重连
    
```
//只需要设置ReconnConf对象即可
ReconnConf  reconnConf = new ReconnConf (5000L);
ClientGroupContext  clientGroupContext = new ClientGroupContext<>(aioClientHandler, aioListener, reconnConf);
```
    
- 绑定用户
    
```
Aio.bindUser(channelContext, userid);
```
    
- 解绑用户

```
Aio.unbindUser(channelContext);
```

- 绑定群组

```
Aio.bindGroup(channelContext, groupid);
```

- 解绑所有群组

```
Aio.unbindGroup(channelContext);
```

- 解绑指定群组

```
Aio.unbindGroup(group, channelContext);
```

- 发消息到群组

```
//方法1
Aio.sendToGroup(groupContext, groupid, packet);
//方法2
Aio.sendToGroup(groupContext, groupid, packet, channelContextFilter);
```

- 发消息给所有连接

```
Aio.sendToAll(groupContext, packet, channelContextFilter);
```

- 发消息给用户

```
Aio.sendToUser(groupContext, userid, packet);
```

- 各项消息统计等功能，全部一键内置搞定，省却各种烦恼

```
//某条链路的统计数据
public class ChannelStat {
/**
 * 最近一次收到业务消息包的时间(一个完整的业务消息包，一部分消息不算)
 */
private long latestTimeOfReceivedPacket = SystemTimer.currentTimeMillis();

/**
 * 最近一次发送业务消息包的时间(一个完整的业务消息包，一部分消息不算)
 */
private long latestTimeOfSentPacket = SystemTimer.currentTimeMillis();

/**
 * ChannelContext对象创建的时间
 */
private long timeCreated = SystemTimer.currentTimeMillis();

/**
 * 第一次连接成功的时间
 */
private Long timeFirstConnected = null;

/**
 * 连接关闭的时间
 */
private long timeClosed = SystemTimer.currentTimeMillis();

/**
 * 进入重连队列时间
 */
private long timeInReconnQueue = SystemTimer.currentTimeMillis();

/**
 * 本连接已发送的字节数
 */
private AtomicLong sentBytes = new AtomicLong();

/**
 * 本连接已发送的packet数
 */
private AtomicLong sentPackets = new AtomicLong();

/**
 * 本连接已处理的字节数
 */
private AtomicLong handledBytes = new AtomicLong();

/**
 * 本连接已处理的packet数
 */
private AtomicLong handledPackets = new AtomicLong();

/**
 * 本连接已接收的字节数
 */
private AtomicLong receivedBytes = new AtomicLong();

/**
 * 本连接已接收的packet数
 */
private AtomicLong receivedPackets = new AtomicLong();

// getter and setter
}


//某一组条链路的统计数据(一般情况下这一组就是代表所有链路)
public class GroupStat {
/**
 * 关闭了多少连接
 */
private AtomicLong closed = new AtomicLong();
/**
 * 接收到的消息包
 */
private AtomicLong receivedPacket = new AtomicLong();
/**
 * 接收到的消息字节数
 */
private AtomicLong receivedBytes = new AtomicLong();
/**
 * 处理了的消息包数
 */
private AtomicLong handledPacket = new AtomicLong();
/**
 * 发送了的消息包数
 */
private AtomicLong sentPacket = new AtomicLong();

/**
 * 发送了的字节数
 */
private AtomicLong sentBytes = new AtomicLong();
// getter and setter
}
```

## **性能数据**
 - IM实例收发速度500万条/秒----此数据系网友提供（i7 6700 + 固态硬盘 + win10），作者本地只跑到了333万/秒
 - IM实例17.82万TCP长连接且正常收发消息只消耗800M内存，CPU使用率极低，目测t-io可以支撑200万长连接
 - 17.82万长连接 + 各种破坏性测试，服务器内存保持稳定（600多M到900M间）

## **性能测试步骤**

### 测试单机吞吐量
1. 机器准备
    - CPU: i7 6700 / i7 4790
    - 内存：8G/4G
    - 操作系统：windows7/windows10
    - 说明：客户机和服务器位于同一台机器
2. 测试步骤
    - 双击 "bin/start-im-server.bat" 启动im server
    - 双击 "bin/start-im-client.bat" 启动im client
    - 保持下图参数进行测试
    ![image](http://git.oschina.net/tywo45/t-io/raw/master/docs/performance/500%E4%B8%87.png)
3. 测试结果
    - 500万条/秒约165M----此数据系网友提供（i7 6700 + 固态硬盘 + win10）
    - 333万条/秒约97M----此数据系本人亲测数据（i7 4790 + 固态硬盘 + win7），测试参数与上图略有差别，不一一说明

### 测试centos下可以支持多少长连接数
1. 机器准备
    - 服务器一台：centos6.x,  虚拟机，一个4核E5 CPU，内存16G
    - 客户机11台：windows，硬件没什么特别要求
2. 测试步骤
    - 修改centos操作系统参数，使之支持更大的长连接数，细节略（可百度之）
    - 在centos上运行 "bin/start-im-server.sh" 启动im server
    - 修改dist\examples\im\client\config\app.conf，参考下面的值，注意把server指向centos的ip
    ```
        #服务器
        server=127.0.0.1
        
        #服务器port
        port=9321
        
        #连接多少个连接到服务器
        client.count=16200
        
        #进入到哪个组
        group=g
        
        #聊天消息发的内容
        chat.content=he
        
        #一次发多少条(这个数字不要太大)
        send.count=1
    ```
    - 把dist\examples\im\client拷到各客户机并运行"bin/start-im-client.bat"
3. 测试结果
    - 11个客户机 ，每个客户机连16200个TCP连接，服务器一共承受17.82万TCP长连接，服务器内存只消耗800M，CPU使用率极低（其中有一台客户担任破坏性测试机）
    - 根据测试结果初步推测：t-io支持200万长连接没什么问题，各位有条件的可以测测。

## t-io学习步骤（供参考，具体步骤根据各人而异）
学习t-io的最好方式，是从helloworld的例子入手，顺瓜摸藤阅读t-io的源代码，已经有很多人阅读过t-io的源代码，譬如j-net的作者、[hutool](https://git.oschina.net/loolly/hutool/)的作者、[天蓬小猪](https://my.oschina.net/u/257950/)、[守护天使](https://git.oschina.net/yyljlyy)，并且反馈良好，源代码毕竟只有3000多行，读读无妨！如果懒于阅读代码，就按照下面的步骤来学习吧！

### 初步认识t-io
- 安装1.7以上版本的jdk及maven（已安装的略过此步骤）
- 从[https://git.oschina.net/tywo45/t-io](https://git.oschina.net/tywo45/t-io)处下载源代码（已下载的略过此步骤）
- 双击 "bin/start-im-server.bat" 启动im server
- 双击 "bin/start-im-client.bat" 启动im client
- 对着界面把玩几下，测试一把性能数据，对t-io形成感性认识（注意：好的性能数据需要预热几把，让线程池活起来）
- 熟悉客户端界面（版本不一样，此界面会不一样，以实物为准）
![image](http://git.oschina.net/tywo45/t-io/raw/master/docs/performance/500%E4%B8%87.png)
- 服务器端界面（版本不一样，此界面会不一样，以实物为准）
![image](http://git.oschina.net/tywo45/t-io/raw/master/docs/im/server.png)

### 了解代码目录结构
所有工程都是maven工程，后续目录有可能稍有变动，不定期更新

```
├─bin----------------脚本目录（方便快速操作）
│      clean.bat----------------清空所有工程的target目录
│      clean.sh
│      deploy.bat----------------作者用来发布到maven中心仓库的脚本，放出来主要是供大家参考
│      deploy.sh
│      dist-examples.bat----------------把所有的例子打包到dist目录，方便用户直接执行
│      dist-examples.sh
│      install.bat----------------安装工程到本地仓库
│      install.sh
│      start-helloworld-client.bat----------------启动helloworld的客户端
│      start-helloworld-client.sh
│      start-helloworld-server.bat----------------启动helloworld的服务端
│      start-helloworld-server.sh
│      start-im-client.bat----------------启动im的客户端
│      start-im-client.sh
│      start-im-server.bat----------------启动im的服务端
│      start-im-server.sh
│      start-im-simple-client.bat----------------启动简化版协议的im的客户端
│      start-im-simple-client.sh
│      start-im-simple-server.bat----------------启动简化版协议的im的服务端
│      start-im-simple-server.sh
│      start-showcase-client.bat----------------启动showcase的客户端
│      start-showcase-client.sh
│      start-showcase-server.bat----------------启动showcase的服务端
│      start-showcase-server.sh
├─docs
│  │  
│  ├─blog----------------本人博客草稿（大部分博客是在线编辑，所以此处就没有了）
│  │      
│  ├─performance----------------一些性能测试截图（随着版本的增多，有些截图已经过时，但仍保留）
│  │
│  ├─release----------------新版本发布时的log
│  
├─dist----------------成品
│  └─examples----------------用t-io写的例子成品
│      ├─helloworld
│      │  ├─client----------------helloworld的客户端
│      │  └─server----------------helloworld的服务端
│      ├─im
│      │  ├─client----------------im的客户端
│      │  └─server----------------im的服务端
│      │─im-simple
│      │  ├─client----------------简化版协议的im的客户端
│      │  └─server----------------简化版协议的im的服务端
│      └─showcase
│          ├─client----------------showcase的客户端
│          └─server----------------showcase的服务端
└─src
    ├─core----------------t-io的核心代码
    ├─example----------------用t-io写的例子的源代码
    │  ├─parent----------------例子的maven parent
    │  ├─helloworld----------------helloworld的源代码
    │  │  ├─client
    │  │  ├─common
    │  │  └─server
    │  ├─im----------------im的源代码
    │  │  ├─client
    │  │  ├─common
    │  │  └─server
    │  ├─im-simple----------------简化版协议的im的源代码
    │  │  ├─client
    │  │  ├─common
    │  │  └─server
    │  └─showcase----------------showcase的源代码，这个例子是为了帮助用户学习t-io专门写的
    │      ├─client
    │      ├─common
    │      └─server
    └─parent----------------maven工程的parent
```

### 导入t-io官方提供的例子
去[t-io码云托管地址](https://git.oschina.net/tywo45/t-io)下载源代码及例子，里面的showcase例子是专门为学习t-io而写的，其设计也是准生产级别的，**可以直接拿来做您项目的手脚架**。下载完成后，请按下面步骤导入到eclipse中
[![image](https://git.oschina.net/tywo45/t-io/raw/master/docs/blog/t-io%E7%B3%BB%E5%88%97%E6%96%87%E6%A1%A3%E4%B9%8Bhelloworld%EF%BC%881%EF%BC%89/import-1.png)](https://git.oschina.net/tywo45/t-io/raw/master/docs/blog/t-io%E7%B3%BB%E5%88%97%E6%96%87%E6%A1%A3%E4%B9%8Bhelloworld%EF%BC%881%EF%BC%89/import-1.png)
---
[![image](https://git.oschina.net/tywo45/t-io/raw/master/docs/blog/t-io%E7%B3%BB%E5%88%97%E6%96%87%E6%A1%A3%E4%B9%8Bhelloworld%EF%BC%881%EF%BC%89/import-2.png)](https://git.oschina.net/tywo45/t-io/raw/master/docs/blog/t-io%E7%B3%BB%E5%88%97%E6%96%87%E6%A1%A3%E4%B9%8Bhelloworld%EF%BC%881%EF%BC%89/import-2.png)
---
[![image](https://git.oschina.net/tywo45/t-io/raw/master/docs/blog/t-io%E7%B3%BB%E5%88%97%E6%96%87%E6%A1%A3%E4%B9%8Bhelloworld%EF%BC%881%EF%BC%89/import-3.png)](https://git.oschina.net/tywo45/t-io/raw/master/docs/blog/t-io%E7%B3%BB%E5%88%97%E6%96%87%E6%A1%A3%E4%B9%8Bhelloworld%EF%BC%881%EF%BC%89/import-3.png)

### 学习万能的helloworld例子
花30分钟看一下t-io官方提供的helloworld，了解一下TCP编程的大概流程，文档传送门: [t-io的hello world](https://my.oschina.net/talenttan/blog/884806)

### 学习用于进阶的showcase例子
showcase一词是从springside借来的，放这很应景，[天蓬元帅](https://git.oschina.net/kobe577590/im)就是这样学习的，可以和他交流，他后面会出详细的教程。

## 案 例
案例太多，此处仅列举t-io开源第一个月内的案例，你也可以来[t-io开源中国收录地址](https://www.oschina.net/p/t-io)看看其它网友们反馈的案例
- 某网管系统(管理数百台刀片服务器的系统)
- 某直播平台(视频直播+聊天)
- 某智能设备检测系统(数据采集)
- 某物联网系统(服务端)
- 深圳市某在线技术发展有限公司(中银联投资)：某网络安全运营支撑平台
- [redisx](https://git.oschina.net/websterlu/redisx)
- [talent_dubbo](https://git.oschina.net/kangjie1209/talent_dubbo)
- 某移动省公司CRM业务受理消息采集平台(数据采集)

## 列一下作者本人用过的国产开源软件
网上很多人对国产开源的印象还停留在n年前，此处列一下作者本人一直在用的部分国产开源软件，其中有的是有争议的，也有暴过漏洞的，但是我们想一下struts、netty、mongodb这些国外知名软件不也暴过严重漏洞吗？
1. [https://www.oschina.net/p/weixin-java-tools-new](https://www.oschina.net/p/weixin-java-tools-new) （使用一年）
2. [https://www.oschina.net/p/ztree](https://www.oschina.net/p/ztree) （使用五年以上吧）
3. [https://www.oschina.net/p/echarts](https://www.oschina.net/p/echarts) （使用两年以上吧）
4. [http://git.oschina.net/tywo45/talent-validate](http://git.oschina.net/tywo45/talent-validate) （使用十年了，开源出来有五年以上吧，原来是博客开源，现在移到开源中国了）
5. [https://www.oschina.net/p/hutool](https://www.oschina.net/p/hutool)（使用两个月）
6. [https://www.oschina.net/p/t-io](https://www.oschina.net/p/t-io)（使用五年了，开源出来半年）
7. [https://www.oschina.net/p/druid](https://www.oschina.net/p/druid)（使用三年以上吧）
8. [https://www.oschina.net/p/dubbo](https://www.oschina.net/p/dubbo)（使用两年）
9. [https://git.oschina.net/jfinal/jfinal-weixin](https://git.oschina.net/jfinal/jfinal-weixin/)（使用一年左右）
10. [https://www.oschina.net/p/fastjson](https://www.oschina.net/p/fastjson)（使用三年以上）

## 参与t-io
- t-io是将多线程技巧运用到极致的框架，所以一旦您参与到本项目，将会从本项目中学到很多关于多线程的技巧。
- 提交Issue 给项目提出有意义的新需求，或是帮项目发现BUG，或是上传你本地测试的一些数据让作者参考以便进一步优化。
- **点击右上方的 Star 以便随时掌握本项目的动态（据说star过t-io的用户会受到作者特别对待^_^）**


## [大家一起助力t-io生态发展](http://www.t-io.org:9292/donate.html?v=3)
- 由于各种原因，t-io曾经有三天是要打算闭源的----并且在此期间关闭了所有捐赠渠道，包括码云官方的捐赠渠道。
- 2017年5月4号 t-io 1.7.0发布后，重新开放了助力渠道
- t-io本身不需要助力也能活得很好，**t-io生态系统发展，还希望大家助一臂之力**。


[助力后请私我一下](http://wpa.qq.com/msgrd?v=3&uin=33745965&site=qq&menu=yes) | [助力后请私我一下](http://wpa.qq.com/msgrd?v=3&uin=33745965&site=qq&menu=yes) | [请先看t-io入群规范](https://my.oschina.net/talenttan/blog/888808)
---|---|---
![微信赞助](https://git.oschina.net/tywo45/t-io/raw/master/docs/pay/wechat_300px.png?9) | ![马云赞助](https://git.oschina.net/tywo45/t-io/raw/master/docs/pay/ali_300px.png?9)| ![t-io官方QQ群](https://git.oschina.net/tywo45/t-io/raw/master/docs/qq/qq_300px.png)










  [1]: http://www.t-io.org:9292/
  [2]: https://my.oschina.net/talenttan/blog/884806
  [3]: http://www.t-io.org:9292/apidocs/org/tio/core/Aio.html
  [4]: http://www.t-io.org:9292/apidocs/org/tio/core/Aio.html
  [5]: https://my.oschina.net/talenttan/blog/863545
  [6]: https://my.oschina.net/talenttan/blog


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)