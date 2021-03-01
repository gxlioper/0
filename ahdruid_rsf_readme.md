
# 请注意：RSF 项目回归 Hasor。为了方便后续开发维护，此代码库暂停维护。请您更新 Fork 和 Star 到下面两个地址：
## 源码和历史版本已迁移到：http://git.oschina.net/zycgit/hasor or https://github.com/zycgit/hasor
----------

# RSF

&emsp;&emsp;一个高可用、高性能、轻量级的分布式服务框架。支持容灾、负载均衡、集群。一个典型的应用场景是，将同一个服务部署在多个`Server`上提供 request、response 消息通知。

&emsp;&emsp;使用RSF可以点对点调用，也可以分布式调用。部署方式上：可以搭配注册中心，也可以独立使用。

----------
### 工作原理
![工作原理](http://project.hasor.net/resources/224933_BV6Q_1166271.jpg)

----------
### RSF架构设计
![RSF架构](http://project.hasor.net/resources/002011_mz60_1166271.jpg)

----------
### RoadMap
![RoadMap](http://project.hasor.net/resources/120213_9S4m_1166271.jpg)

----------
### 介绍
##### 特色功能:
01. 支持服务热插拔：支持服务动态发布、动态卸载
02. 支持服务分组：支持服务分组、分版本
03. 支持多种方式调用：同步、异步、回调、接口代理
04. 支持多种模式调用：RPC模式调用、Message模式调用
        &emsp;&emsp;RPC     模式: 远程调用会等待并返回执行结果。适用于一般方法。遇到耗时方法会有调用超时风险
        &emsp;&emsp;Message 模式: 远程调用当作消息投递到远程机器，不会产生等待，可以看作是一个简单的 MQ。适合于繁重的耗时方法
05. 支持点对点调用。RSF的远程调用可以点对点定向调用，也可以集群大规模部署集中提供同一个服务
06. 支持虚拟机房。通过配置虚拟机房策略可以降低跨机房远程调用
07. 支持泛化调用。简单的理解，泛化调用就是不依赖二方包，通过传入方法名，方法签名和参数值，就可以调用服务
08. 支持隐式传参。可以理解隐式传参的含义为，不需要在接口上明确声明参数。在发起调用的时传递到远端
09. 内置 Telnet 控制台，可以命令行方式直接管理机器
10. 支持 offline/online 动作

##### 扩展性:
01. 支持第三方集成，可以独立使用,也可以和 Spring、Jfinal等第三方框架整合使用
02. 支持拦截器RsfFilter，开发者可以通过扩展 Filter 实现更多需求
03. 支持自定义序列化。默认使用内置 Hessian 4.0.7 序列化库
04. 支持Telnet控制台自定义指令。通过扩展控制台指令，可以发挥更大想象空间

##### 稳定性(参数可配置):
01. 最大发并发请求数配置（默认:200）
02. 最大发起请求超限制策略设置: A-等待1秒重试、B-抛异常（默认:B-抛异常）
03. Netty线程数配置（默认: 监听请求线程数: 1，IO线程数: 8）
04. 提供者调用队列容量配置（默认: 队列容量: 4096）
05. Work线程数配置（默认: 处理调用线程数: 4）
06. 请求超时设置。支持服务提供者，服务订阅者独立配置各自的超时参数（默认 6000毫秒）
07. 双向通信。RSF会合理利用Socket连接，双向通信是指当A机器发起远程调用请求之后，RSF会建立长连接
        &emsp;&emsp;-- 如果B机器有调用A机器的需求则直接使用这个连接不会重新创建新的连接，双向通信会大量降低集群间的连接数
08. 支持优雅停机。应用停机，Center会自动通知整个集群。即便所有 Center 离线，RSF也会正确处理失效地址

##### 健壮性:
01. 每小时地址本动态备份。当所有注册中心离线，即便在没有注册中心的情况下应用程序重启，也不会导致服务找不到提供者的情况
02. 当某个地址失效之后，RSF会冻结一段时间，在这段时间内不会有请求发往这个地址
03. 支持请求、响应分别使用不同序列化规则

##### 可维护性:
01. 支持QoS流量控制。流控可以精确到：接口、方法、地址
02. 支持动态路由脚本。路由可以精确到：接口、方法、参数
03. 通过路由脚本可以轻松实现接口灰度发布

##### 安全性:
01. 支持发布服务授权
02. 支持服务订阅授权
03. 支持匿名应用

----------
### Demo
	 
	 
		 net.hasor 
		 hasor-rsf 
		 1.1.0 
	 

	 
	 
	 
     
         
             rsf:// :2180 
         
     

    // 服务接口
    public interface EchoService {
        public String sayHello(String echo) throws InterruptedException;
    }
    
    // 服务接口实现
    public class EchoServiceImpl implements EchoService {
        public String sayHello(String echo) throws InterruptedException {
            return "you say " + echo;
        }
    }
    
	// 服务提供者
	Hasor.createAppContext("server-config.xml", new RsfModule() {
        public void loadModule(RsfApiBinder apiBinder) throws Throwable {
			EchoService echoService = new EchoServiceImpl();
			apiBinder.rsfService(EchoService.class).toInstance(echoService).register();
		}
	});

	// 服务消费者
	AppContext clientContext = Hasor.createAppContext("client-config.xml", new RsfModule() {
        public void loadModule(RsfApiBinder apiBinder) throws Throwable {
			apiBinder.rsfService(EchoService.class).register();
		}
	});
	RsfClient client = clientContext.getInstance(RsfClient.class);
	EchoService echoService = client.wrapper(EchoService.class);
	String echoMessage = echoService.sayHello("Hello Word");
	System.out.println(echoMessage);

----------
### 未来版本计划支持的项目（粗略计划）
* 细节优化
- 整个 static-config.xml 的配置都可以被主配置文件进行覆盖。
- RsfCenter 数据订阅，方便不同版本Center之间数据同步。为Hasor版本升级可能存在的不兼容性考虑。

----------
### 相关连接

* WebSite：[http://www.hasor.net](http://www.hasor.net)
* Docs : [http://hasor-guide.mydoc.io/](http://hasor-guide.mydoc.io/)
* Issues：[http://git.oschina.net/teams/hasor/issues](http://git.oschina.net/teams/hasor/issues)
* Team：[http://team.oschina.net/hasor](http://team.oschina.net/hasor)
* Demo工程：[http://git.oschina.net/zycgit/hasor-example](http://git.oschina.net/zycgit/hasor-example)
* QQ群：193943114
* [![License](https://img.shields.io/badge/license-Apache%202-4EB1BA.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/net.hasor/hasor-rsf/badge.svg)](https://maven-badges.herokuapp.com/maven-central/net.hasor/hasor-rsf)
[![Build Status](https://travis-ci.org/zycgit/rsf.svg?branch=master)](https://travis-ci.org/zycgit/rsf)
[![Build Status](https://travis-ci.org/zycgit/rsf.svg?branch=dev)](https://travis-ci.org/zycgit/rsf)

### 正式发布

* mvn release:prepare -P release
* ./deploy.sh -P release
* ./build.sh && docker build -t debug . && docker run debug

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)