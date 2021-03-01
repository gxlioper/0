![J2Cache](docs/J2Cache.png)

# J2Cache —— 基于内存和 Redis 实现的两级 Java 缓存框架

专用QQ群: `379110351`

J2Cache 是 OSChina 目前正在使用的两级缓存框架。第一级缓存使用内存(同时支持 Ehcache 2.x、Ehcache 3.x 和 Caffeine)，第二级缓存使用 Redis 。
由于大量的缓存读取会导致 L2 的网络成为整个系统的瓶颈，因此 L1 的目标是降低对 L2 的读取次数。
该缓存框架主要用于集群环境中。单机也可使用，用于避免应用重启导致的缓存冷启动后对后端业务的冲击。

J2Cache 已经有 Python 语言版本了，详情请看 [https://gitee.com/ld/Py3Cache](https://gitee.com/ld/Py3Cache)

J2Cache 从 1.3.0 版本开始支持 JGroups 和 Redis Subscribe 两种方式进行缓存事件的通知。在某些云平台上可能无法使用 JGroups 组播方式，可以采用 Redis 发布订阅的方式。详情请看 j2cache.properties 配置文件的说明。

视频介绍：http://v.youku.com/v_show/id_XNzAzMTY5MjUy.html  
该项目提供付费咨询服务，详情请看：https://zb.oschina.net/market/opus/12_277

J2Cache 的两级缓存结构

L1： 进程内缓存(ehcache)   
L2： Redis 集中式缓存

由于大量的缓存读取会导致 L2 的网络带宽成为整个系统的瓶颈，因此 L1 的目标是降低对 L2 的读取次数

		 
## 数据读取

1. 读取顺序  -> L1 -> L2 -> DB

2. 数据更新

    1 从数据库中读取最新数据，依次更新 L1 -> L2 ，发送广播清除某个缓存信息  
    2 接收到广播（手工清除缓存 & 一级缓存自动失效），从 L1 中清除指定的缓存信息

## J2Cache 配置

配置文件位于 core/resources 目录下，包含三个文件：

* ehcache.xml Ehcache 的配置文件，配置说明请参考 Ehcache 文档
* j2cache.properties J2Cache 核心配置文件，可配置 Redis 服务器、连接池以及缓存广播的方式
* network.xml JGroups 网络配置，如果使用 JGroups 组播的话需要这个文件，一般无需修改

实际使用过程需要将这三个文件复制到应用类路径中，如 WEB-INF/classes 目录。

J2Cache 运行时所需 jar 包请查看 core/pom.xml

## 测试方法

1. 安装 Redis  
2. `git clone https://gitee.com/ld/J2Cache`
3. 修改 `core/resource/j2cache.properties` 配置使用已安装的 Redis 服务器
4. 在命令行中执行 `mvn package -DskipTest=true` 进行项目编译  
5. 打开多个命令行窗口，同时运行 `runtest.sh` 
6. 在 > 提示符后输入 help 查看命令，并进行测试

## 示例代码

详细的使用方法请看 [J2CacheCmd.java](https://gitee.com/ld/J2Cache/blob/master/core/src/net/oschina/j2cache/J2CacheCmd.java)

## 使用方法

J2Cache 默认使用 Caffeine 作为一级缓存，使用 Redis 作为二级缓存。你还可以选择 Ehcache2 和 Ehcache3 作为一级缓存。

**准备工作**

1. 安装 Redis
2. 新建一个基于 Maven 的 Java 项目

**一. 引用 Maven**

```
 
   net.oschina.j2cache   
   j2cache-core   
   xxxxx   
 
```

**二. 准备配置**
 
拷贝 `j2cache.properties` 和 `caffeine.properties` 到你项目的源码目录，并确保这些文件会被编译到项目的 classpath 中。如果你选择了 ehcache 作为一级缓存，需要拷贝 `ehcache.xml` 或者 `ehcache3.xml` 到源码目录（后者对应的是 Ehcache 3.x 版本），这些配置文件的模板可以从 [https://gitee.com/ld/J2Cache/tree/master/core/resources](https://gitee.com/ld/J2Cache/tree/master/core/resources) 这里获取。

使用你喜欢的文本编辑器打开 `j2cache.properties` 并找到 `redis.hosts` 项，将其信息改成你的 Redis 服务器所在的地址和端口。

我们建议缓存在使用之前都需要预先设定好缓存大小以及有效时间，使用文本编辑器打开 caffeine.properties 进行缓存配置，配置方法请参考文件中的注释内容。

例如：default = 1000,30m #定义缓存名 default ，对象大小 1000，缓存数据有效时间 30 分钟。 你可以定义多个不同名称的缓存。

**三. 编写代码**

Test.java  

```
public static void main(String[] args) {
    CacheChannel cache = J2Cache.getChannel();
    
    //缓存操作
    cache.set("default", "1", "Hello J2Cache");
    System.out.println(cache.get("default", "1"));
    cache.evict("default", "1");
    System.out.println(cache.get("default", "1"));
    
    cache.close();
}
```
编译并运行查看结果，更多的用法请参考 [CacheChannel.java](https://gitee.com/ld/J2Cache/blob/master/core/src/net/oschina/j2cache/CacheChannel.java) 接口的方法。

*请注意 cache.close() 方法只需在程序退出时调用。*

**四. 集群测试**

为了方便测试集群模式下 J2Cache 的运行，我们提供了一个命令行小程序，请参考此页面前面的 [“测试方法”](#%E6%B5%8B%E8%AF%95%E6%96%B9%E6%B3%95)。

## 常见问题

1. **J2Cache 的使用场景是什么？**  
首先你的应用是允许在集群环境，使用 J2Cache 可以有效降低节点间的数据传输量；其次单节点使用 J2Cache 可以避免应用重启后对后端业务系统的冲击
2. **为什么不能在程序中设置缓存的有效期**  
在程序中定义缓存数据的有效期会导致缓存不可控，一旦数据出问题无从查起，因此 J2Cache 的所有缓存的有效期都必须在 `一级缓存` 的配置中预设好再使用
3. **如何使用 JGroups 组播方式（无法在云主机中使用）**  
首先修改 `j2cache.properties` 中的 `j2cache.broadcast` 值为 `jgroups`，然后在 maven 中引入
	
	```
	 
	     org.jgroups 
	     jgroups 
	     3.6.13.Final 
	 
	```
4. **如何使用 ehcache 作为一级缓存**  
首先修改 `j2cache.properties` 中的 `j2cache.L1.provider_class` 为 ehcache 或者 ehcache3，然后拷贝 ehcache.xml 或者 ehcache3.xml 到类路径，并配置好缓存，需要在项目中引入对 ehcache 的支持：  

	```
      
         net.sf.ehcache 
         ehcache 
         2.10.4 
         true 
     
    
      
         org.ehcache 
         ehcache 
         3.4.0 
         true 
     

	```

## 哪些项目在用 J2Cache ？

* www.oschina.net
* https://gitee.com/jfinal/jfinal
* https://gitee.com/fuhai/jboot
* https://gitee.com/tywo45/t-io
* 更多项目收集中，如果你的项目用了，请告诉我

## TODO ##


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)