![](http://git.oschina.net/uploads/images/2016/0510/122514_7d971a34_116083.jpeg)


[![](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![](https://maven-badges.herokuapp.com/maven-central/org.voovan/voovan-framework/badge.svg)](https://maven-badges.herokuapp.com/maven-central/org.voovan/voovan-framework)
![JDK 1.8](https://img.shields.io/badge/JDK-1.8-green.svg "JDK 1.8")
[![jar size 270K](https://img.shields.io/badge/size-270K-green.svg "size 270K")](https://git.oschina.net/helyho/Voovan/raw/master/voovan-framework.jar)

##### Voovan 是一个高性能异步网络框架和WEB服务器框架,同时支持HTTP客户端抓取、动态编译支持、数据库访问封装以及DateTime、String、Log、反射、对象工具、流操作、文件操作、异步双向通道等功能。旨在提供可靠、方便、可单元测试的代码。它是一个无任何依赖的独立工具包，希望能够方便广大开发者快速的实现应用。

---------------------

###Maven中央库支持:
```xml
 
     org.voovan 
     voovan-framework 
     1.5.1 
 
```

---------------------

###JDK支持:

 - 推荐使用 JDK1.8,懒人专用。
 - 如果仅使用 AIO 需要 JDK1.7。【[如何兼容到JDK1.7?](http://voovan.mydoc.io/?t=113242)】
 - 如果 WebServer 使用lambda 需要 JDK1.8,不使用 lambda 需要 JDK1.7。
 - 有能力的同学可以通过很简单几行修改使 WebServer 和 HTTPClient使用 NIO 那么就是 JDK1.6。

---------------------

###框架特点介绍:
 - 使用 JDK8 的 lambda 表达式,快速实现 HTTP/WebSocket 服务的开发。[【演示】](http://webserver.voovan.org/)/[【性能测试报告】](https://git.oschina.net/helyho/Voovan/issues/12)
 - 异步通信框架解决粘包问题,过滤器链等。
 - 独立无依赖的代码。
 - 源码注释丰富，方便码友学习、调试、使用。

---------------------

###一、高性能异步通信(AIO、NIO异步通信)

  类似 Netty 和 MINA 的异步 Socket 通信框架.但有有所不同。
  1. **可灵活解决Socket通信粘包的支持**（源码中包含 HTTP协议,字符串换行,定长报文的粘包实现）。
  1. **支持 SSL/TLS 加密通信。**
  1. **提供线程池依据系统负载情况自动动态调整。**
  1. 同时支持 NIO 和 AIO 特性。
  1. 采用非阻塞方式的异步传输。
  1. 事件驱动(Connect、Recive、Sent、Close、Exception)，采用回调的方式完成调用。
  1. **可灵活的加载过滤器机制。**
  
---------------------

###二、HTTP客户端和WEB服务器
###HTTP客户端特性:
  1. 基于 Voovan 异步通信框架实现。
  1. 客户端可以灵活自定义请求报文。
  1. 同步实现 HTTP请求(需要同步实现可参考)。
  1. 实现 WebSocket 客户端调用,可以连接任何支持 **WebSocket Version 13**的 WebSocket 服务。
  


###WEB服务器特性:
  1. 支持 **WebSocket Version 13**，并且保持 WebSocket请求参数。
  1. **使用 Lambda 实现更加方便的 Http 响应实现。**
  1. **支持路径参数自动抽取**  当路径定义/:name,在使用/jonh地址访问时，可以通过 name 参数获取 jonh 字符串。
  1. 重定向支持。
  1. 可灵活实现session共享。
  1. **异常统一展示**支持。
  1. MIME 配置支持。
  1. 支持基于 HTTP1.1 的 HTTPS 访问,默认采用TLS模式.
  1. 支持性能监控.  [[HTTP服务端性能监控演示](http://webserver.voovan.org/VoovanMonitor/Monitor.html)]

---------------------

###三、动态编译支持

  在内存中编一个保存有 java 代码的字符串,并将编译后的 byte 字节加入到 classloader 中,可灵活的动态定义类和使用。

---------------------

###四、数据库操作帮助类
提供类似Spring JDBCTemplate 的数据访问支持，但提供了更好更灵活易用的函数设计。
 - 支持的参数类型:
  - Map 参数
  - 不定参数
  - 对象作为参数
 - 支持存储过程调用。
 - 支持批量更新。
 - 数据库事务的支持。
 - 支持自动移除无匹配参数的条件。
 - 结果转换对象的时候使用模糊匹配。

---------------------

###五、DateTime、String、Log、反射、对象工具、流操作、文件操作、异步双向通道等

  1. 简单的 JSON 序列化和反序列化,效率比不过专业的序列化工具(如:FastJson),但重在轻量级好用。
  1. 日期类型和字符串和日期类型互转,日期类型加减操作。
  1. 反射的快捷实现,可直接通过反射取属性值,调用方法,实例化对象,**判断类的继承及实现**。
  1. 简单的日志记录类,支持指定输出流,日志报文自定义等。
  1. 简单的**自推导的对象类型强制转换**,根绝参数类型,运算类型自动退定强制转换类型。
  1. 流操作,读取定长、按行读取、**基于byte的split操作**等。
  1. 使用 ByteBuffer 实现的一个双向通道。
  1. 属性文件操作。
  1. 文件路径拼接、从绝对路径读取、从相对路径读取、从包路径读取、指定起始和结束位置内容读取等。
  1. List 和 Map 的快速初始化。
  
---------------------

###包结构说明

|  包名                      | 名称           |
| -------------             |:-------------: |
|org.voovan.db              |数据库操作类      |
|org.voovan.http            |HTTP工具包       |
|org.voovan.dynamicComplier |动态编译包        |
|org.voovan.network         |网络异步通信包    |
|org.voovan.tools           |基本工具包        |

---------------------

**文档入口: **【[开发手册](http://voovan.mydoc.io/)】

**交流QQ群：**454201740

**开源协议:**Apache v2 License

**Voovan开源项目源代码主要托管于 Git@OSC.**

**Issues地址:** [Git@OSC](http://git.oschina.net/helyho/Voovan/issues)

---------------------

## 贡献者名单
|  名称                      | 贡献内容           |
| -------------             |:-------------: |
|[愚民日记](https://git.oschina.net/helyho)             | 项目发起者      |
|[zhubibo](https://git.oschina.net/zhubibo)            | 应用与BUG提交      |


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)