![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Cover.jpg)

# Nepxion Discovery 框架指南
[![Total lines](https://tokei.rs/b1/github/Nepxion/DiscoveryGuide?category=lines)](https://tokei.rs/b1/github/Nepxion/Discovery?category=lines)  [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?label=license)](https://github.com/Nepxion/Discovery/blob/master/LICENSE)  [![Maven Central](https://img.shields.io/maven-central/v/com.nepxion/discovery.svg?label=maven%20central)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.nepxion%22%20AND%20discovery)  [![Javadocs](http://www.javadoc.io/badge/com.nepxion/discovery-plugin-framework.svg)](http://www.javadoc.io/doc/com.nepxion/discovery-plugin-framework)  [![Build Status](https://travis-ci.org/Nepxion/Discovery.svg?branch=master)](https://travis-ci.org/Nepxion/Discovery)  [![Codacy Badge](https://api.codacy.com/project/badge/Grade/8e39a24e1be740c58b83fb81763ba317)](https://www.codacy.com/project/HaojunRen/Discovery/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Nepxion/Discovery&amp;utm_campaign=Badge_Grade_Dashboard)

每一个访问路过的朋友，如果您觉得这个开源框架不错，请顺手在页面右上角帮它[**Star**]一下

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Star2.jpg)

如果本文档由于Github网速原因无法完整阅读，请访问
- [Nepxion Discovery【探索】微服务企业级解决方案(PDF版)](http://nepxion.gitee.io/docs/link-doc/discovery-solution-pdf.html)
- [Nepxion Discovery【探索】指南篇(PDF版)](http://nepxion.gitee.io/docs/link-doc/discovery-guide-pdf.html) 或 [Nepxion Discovery【探索】指南篇(HTML版)](http://nepxion.gitee.io/docs/link-doc/discovery-guide.html)

Nepxion Discovery【探索】，基于Spring Cloud Discovery服务注册发现、Ribbon负载均衡、Feign和RestTemplate调用等组件全方位增强的企业级微服务开源解决方案，更贴近企业级需求，更具有企业级的插件引入、开箱即用特征
- 支持阿里巴巴Nacos、Eureka、Consul和Zookeeper四个服务注册发现中心
- 支持阿里巴巴Nacos、携程Apollo和Redis三个远程配置中心
- 支持阿里巴巴Sentinel和Hystrix两个熔断隔离限流降级中间件
- 支持Uber Jaeger、Apache Skywalking等符合OpenTracing调用链中间件
- 支持Java Agent 解决异步跨线程ThreadLocal上下文传递
- 支持Prometheus、Grafana和Spring Boot Admin监控中间件
- 支持Spring Cloud Gateway、Zuul网关和微服务三大模块的灰度发布和路由等一系列功能
- 支持和兼容Spring Cloud Edgware版、Finchley版、Greenwich版和Hoxton版

Nepxion Discovery【探索】框架指南，基于Spring Cloud Greenwich版、Finchley版和Hoxton版而制作（对于Edgware版，使用者需要自行修改）。使用指南主要涉及的功能包括：
- 基于Header传递的全链路灰度路由，网关为路由触发点。采用配置中心配置路由规则映射在网关过滤器中植入Header信息而实现，路由规则传递到全链路服务中。路由方式主要包括版本和区域的匹配路由、版本和区域的权重路由、IP地址和端口的路由
- 基于规则订阅的全链路灰度发布。采用配置中心配置灰度规则映射在全链路服务而实现，所有服务都订阅某个共享配置。发布方式主要包括版本和区域的匹配发布、版本和区域的权重发布
- 基于多方式的规则和策略推送。包括基于远程配置中心的规则和策略订阅推送（本文以Nacos为例）、基于Swagger和Rest的规则和策略推送
- 基于Group的全链路服务隔离。包括注册隔离、消费端隔离和提供端服务隔离，示例仅提供基于Group隔离。除此之外，不在本文介绍内的，还包括：
    - 注册隔离：黑/白名单的IP地址的注册隔离、最大注册数限制的注册隔离
    - 消费端隔离：黑/白名单的IP地址的消费端隔离
- 基于Env的全链路环境隔离和路由。包括基于元数据Metadata的env参数进行隔离，当调用端实例和提供端实例的元数据Metadata环境配置值相等才能调用。环境隔离下，调用端实例找不到符合条件的提供端实例，把流量路由到一个通用或者备份环境。支持网关独立部署和非独立部署两种场景下，动态调度子环境的能力
- 全链路服务限流熔断降级权限。集成阿里巴巴Sentinel，有机整合灰度路由，扩展LimitApp的机制，通过动态的Http Header方式实现组合式防护机制，包括基于服务名、基于灰度组、基于灰度版本、基于灰度区域、基于IP地址和端口等防护机制，支持自定义任意的业务参数组合实现该功能。支持原生的流控规则、降级规则、授权规则、系统规则、热点参数流控规则。除此之外，也集成Hystrix限流熔断组件
- 全链路监控。包括全链路调用链监控（Tracing）、全链路日志（Logging）、全链路指标监控（Metrics），CNCF技术委员会通过OpenTelemetry规范整合基于Tracing的OpenTracing规范（官方推荐Jaeger做Backend）和基于Metrics的OpenSensus规范（官方推荐Prometheus做Backend）。框架支持OpenTracing、Uber Jaeger、Apache Skywalking
    - 全链路调用链监控（Tracing）包括Header方式、调用链方式、日志方式等单个或者组合式的全链路灰度调用链，支持对Sentinel自动埋点。调用链方式不支持Edgware版（Spring Boot 1.x.x）
    - 全链路指标监控（Metrics）包括Prometheus、Grafana、Spring Boot Admin
- 全链路Header传递
- 全链路服务侧注解
- 全链路服务侧API权限
- 元数据Metadata自动化策略。包括基于服务名前缀自动创建灰度组名和基于Git插件自动创建灰度版本号
- 元数据Metadata运维平台策略
- 同城双活多机房切换支持。它包含在“基于Header传递的全链路灰度路由”里
- 数据库灰度发布。内置简单的数据库灰度发布策略，它不在本文的介绍范围内
- 灰度路由和发布的自动化测试
- Docker容器化和Kubernetes平台的无缝支持部署

[**Nacos**] 阿里巴巴中间件部门开发的新一代集服务注册发现中心和配置中心为一体的中间件。它是构建以“服务”为中心的现代应用架构 (例如微服务范式、云原生范式) 的服务基础设施，支持几乎所有主流类型的“服务”的发现、配置和管理，更敏捷和容易地构建、交付和管理微服务平台

[**Sentinel**] 阿里巴巴中间件部门开发的新一代以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性的分布式系统的流量防卫兵。它承接了阿里巴巴近10年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等

[**Spring Cloud Alibaba**] 阿里巴巴中间件部门开发的Spring Cloud增强套件，致力于提供微服务开发的一站式解决方案。此项目包含开发分布式应用微服务的必需组件，方便开发者通过Spring Cloud编程模型轻松使用这些组件来开发分布式应用服务。依托Spring Cloud Alibaba，只需要添加一些注解和少量配置，就可以将Spring Cloud应用接入阿里微服务解决方案，通过阿里中间件来迅速搭建分布式应用系统

[**OpenTracing**] OpenTracing已进入CNCF，正在为全球的分布式追踪系统提供统一的概念、规范、架构和数据标准。它通过提供平台无关、厂商无关的API，使得开发人员能够方便的添加（或更换）追踪系统的实现。对于存在多样化的技术栈共存的调用链中，OpenTracing适配Java、C、Go和.Net等技术栈，实现全链路分布式追踪功能。迄今为止，Uber Jaeger、Twitter Zipkin和Apache Skywalking已经适配了OpenTracing规范

本框架成为阿里巴巴中间件Nacos和Spring Cloud Alibaba项目的相关开源
  

示例以Nacos为服务注册中心和配置中心（使用者可自行换成其它服务注册中心和配置中心），集成Spring Cloud Alibaba，通过Gateway和Zuul调用两个版本或者区域的服务，模拟网关灰度路由和服务灰度权重的功能

如果使用者需要更强大的功能，请参考[源码主页](https://github.com/Nepxion/Discovery)。规则策略很多，请使用者选择最适合自己业务场景的方式

## 目录
- [请联系我](#请联系我)
- [相关版本](#相关版本)
- [相关链接](#相关链接)
    - [源码主页](#源码主页)
    - [指南主页](#指南主页)
    - [文档主页](#文档主页)
- [相关图示](#相关图示)
    - [部署架构拓扑图](#部署架构拓扑图)
    - [服务治理架构图](#服务治理架构图)
    - [灰度方式区别图](#灰度方式区别图)
- [环境搭建](#环境搭建)
- [启动服务](#启动服务)
- [环境验证](#环境验证)
- [基于Header传递方式的灰度路由策略](#基于Header传递方式的灰度路由策略)
    - [灰度路由架构图](#灰度路由架构图)
        - [多版本灰度路由架构图](#多版本灰度路由架构图)
        - [多区域灰度路由架构图](#多区域灰度路由架构图)
        - [多IP和端口灰度路由架构图](#多IP和端口灰度路由架构图)
    - [配置网关灰度路由策略](#配置网关灰度路由策略)
        - [版本匹配灰度路由策略](#版本匹配灰度路由策略)
        - [版本权重灰度路由策略](#版本权重灰度路由策略)
        - [区域匹配灰度路由策略](#区域匹配灰度路由策略)
        - [区域权重灰度路由策略](#区域权重灰度路由策略)
        - [IP地址和端口匹配灰度路由策略](#IP地址和端口匹配灰度路由策略)
    - [配置全链路灰度条件命中和灰度匹配组合式策略](#配置全链路灰度条件命中和灰度匹配组合式策略)
    - [配置全链路灰度条件权重和灰度匹配组合式策略](#配置全链路灰度条件权重和灰度匹配组合式策略)
    - [配置前端灰度和网关灰度路由组合式策略](#配置前端灰度和网关灰度路由组合式策略)
    - [通过其它方式设置灰度路由策略](#通过其它方式设置灰度路由策略)
        - [通过前端传入灰度路由策略](#通过前端传入灰度路由策略)
        - [通过业务参数在过滤器中自定义灰度路由策略](#通过业务参数在过滤器中自定义灰度路由策略)
        - [通过业务参数在策略类中自定义灰度路由策略](#通过业务参数在策略类中自定义灰度路由策略)	
- [基于订阅方式的全链路灰度发布规则](#基于订阅方式的全链路灰度发布规则)
    - [配置全链路灰度匹配规则](#配置全链路灰度匹配规则)
        - [版本匹配灰度规则](#版本匹配灰度规则)
        - [区域匹配灰度规则](#区域匹配灰度规则)
    - [配置全链路灰度权重规则](#配置全链路灰度权重规则)
        - [全局版本权重灰度规则](#全局版本权重灰度规则)
        - [局部版本权重灰度规则](#局部版本权重灰度规则)
        - [全局区域权重灰度规则](#全局区域权重灰度规则)
        - [局部区域权重灰度规则](#局部区域权重灰度规则)
    - [配置全链路灰度权重和灰度匹配组合式规则](#配置全链路灰度权重和灰度匹配组合式规则)
- [基于多方式的规则和策略推送](#基于多方式的规则和策略推送)
    - [基于远程配置中心的规则和策略订阅推送](#基于远程配置中心的规则和策略订阅推送)
    - [基于Swagger和Rest的规则和策略推送](#基于Swagger和Rest的规则和策略推送)	
- [基于Group的全链路服务隔离](#基于Group的全链路服务隔离)
    - [注册服务隔离](#注册服务隔离)
    - [消费端服务隔离](#消费端服务隔离)
    - [提供端服务隔离](#提供端服务隔离)
- [基于Env的全链路环境隔离和路由](#基于Env的全链路环境隔离和路由)
    - [环境隔离](#环境隔离)
    - [环境路由](#环境路由)
- [基于Sentinel的全链路服务限流熔断降级权限和灰度融合](#基于Sentinel的全链路服务限流熔断降级权限和灰度融合)
    - [原生Sentinel注解](#原生Sentinel注解)
    - [原生Sentinel规则](#原生Sentinel规则)
        - [流控规则](#流控规则)
        - [降级规则](#降级规则)
        - [授权规则](#授权规则)
        - [系统规则](#系统规则)
        - [热点参数流控规则](#热点参数流控规则)	
    - [基于灰度路由和Sentinel-LimitApp扩展的防护机制](#基于灰度路由和Sentinel-LimitApp扩展的防护机制)
        - [基于服务名的防护机制](#基于服务名的防护机制)
        - [基于灰度组的防护机制](#基于灰度组的防护机制)
        - [基于灰度版本的防护机制](#基于灰度版本的防护机制)
        - [基于灰度区域的防护机制](#基于灰度区域的防护机制)
        - [基于IP地址和端口的防护机制](#基于IP地址和端口的防护机制)
        - [自定义业务参数的组合式防护机制](#自定义业务参数的组合式防护机制)
- [基于Hystrix的全链路服务限流熔断和灰度融合](#基于Hystrix的全链路服务限流熔断和灰度融合)
- [全链路监控](#全链路监控)
    - [全链路调用链监控-Tracing](#全链路调用链监控-Tracing)
        - [Header输出方式](#Header输出方式)
        - [调用链输出方式](#调用链输出方式)
        - [日志输出方式](#日志输出方式)
    - [全链路指标监控-Metrics](#全链路指标监控-Metrics)
        - [Prometheus监控方式](#Prometheus监控方式)
        - [Grafana监控方式](#Grafana监控方式)
        - [Spring-Boot-Admin监控方式](#Spring-Boot-Admin监控方式)
- [全链路Header传递](#全链路Header传递)
- [全链路侦测](#全链路侦测)
- [全链路服务侧注解](#全链路服务侧注解)
- [全链路服务侧API权限](#全链路服务侧API权限)
- [异步跨线程Agent](#异步跨线程Agent)
- [元数据Metadata自动化策略](#元数据Metadata自动化策略)
    - [基于服务名前缀自动创建灰度组名](#基于服务名前缀自动创建灰度组名)
    - [基于Git插件自动创建灰度版本号](#基于Git插件自动创建灰度版本号)
- [元数据Metadata运维平台策略](#元数据Metadata运维平台策略)
- [内置配置文件](#内置配置文件)
- [Docker容器化和Kubernetes平台支持](#Docker容器化和Kubernetes平台支持)
- [Star走势图](#Star走势图)

## 请联系我
微信、公众号和文档

![Alt text](https://github.com/HaojunRen/Docs/raw/master/zxing-doc/微信-1.jpg)![Alt text](https://github.com/HaojunRen/Docs/raw/master/zxing-doc/公众号-1.jpg)![Alt text](https://github.com/HaojunRen/Docs/raw/master/zxing-doc/文档-1.jpg)

## 相关版本
支持如下版本：

| 框架版本 | 框架分支 | 框架状态 | Spring Cloud版本 | Spring Boot版本 | Spring Cloud Alibaba版本 |
| --- | --- | --- | --- | --- | --- |
| 6.0.2 | master | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status1.png) | Hoxton Greenwich Finchley | 2.2.x.RELEASE 2.1.x.RELEASE 2.0.x.RELEASE | 2.2.x.RELEASE 2.1.x.RELEASE 2.0.x.RELEASE |
| ~~5.6.0~~ | ~~5.x.x~~ | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status2.png) | Greenwich | 2.1.x.RELEASE | 2.1.x.RELEASE |
| ~~4.15.0~~ | ~~4.x.x~~ | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status2.png) | Finchley | 2.0.x.RELEASE | 2.0.x.RELEASE |
| 3.16.2 | master-3.x.x | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status1.png) | Edgware | 1.5.x.RELEASE | 1.5.x.RELEASE |
| ~~2.0.x~~ | ~~2.x.x~~ | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status3.png) | Dalston | 1.x.x.RELEASE | N/A |
| ~~1.0.x~~ | ~~1.x.x~~ | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status3.png) | Camden | 1.x.x.RELEASE | N/A |

![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status1.png) 表示迭代中 | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status2.png) 表示不维护，但可用 | ![](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Status3.png) 表示不维护，不可用，已废弃

注意：
- 6.x.x版本（同时适用于Finchley、Greenwich和Hoxton以及未来的更高版本），将继续维护
- 5.x.x版本（适用于Greenwich）不再维护，并入到6.x.x版本，对应的5.6.0是最后一个稳定版本
- 4.x.x版本（适用于Finchley）不再维护，并入到6.x.x版本，对应的4.15.0是最后一个稳定版本
- 3.x.x版本（适用于Edgware）为了照顾老的技术栈公司，将继续维护
- 2.x.x版本（适用于Dalston）已废弃
- 1.x.x版本（适用于Camden）已废弃

## 相关链接

### 源码主页
[源码主页](https://github.com/Nepxion/Discovery)

### 指南主页
[指南主页](https://github.com/Nepxion/DiscoveryGuide)

### 文档主页
[文档主页](https://gitee.com/Nepxion/Docs/tree/master/web-doc)

## 相关图示

### 部署架构拓扑图
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/BasicTopology.jpg)

### 服务治理架构图
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Govern.jpg)

### 灰度方式区别图
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Difference.jpg)

## 环境搭建
- 下载代码
    - Git clone https://github.com/Nepxion/DiscoveryGuide.git 
- 代码导入IDE
- 下载Nacos服务器
    - 从[https://github.com/alibaba/nacos/releases](https://github.com/alibaba/nacos/releases)获取nacos-server-x.x.x.zip，并解压
- 启动Nacos服务器
    - Windows环境下，运行bin目录下的startup.cmd
    - Linux环境下，运行bin目录下的startup.sh

## 启动服务 
- 在IDE中，启动四个应用服务和两个网关服务，控制平台服务和监控平台服务可选，如下： 

| 类名 | 微服务 | 服务端口 | 版本 | 区域 |
| --- | --- | --- | --- | --- |
| DiscoveryGuideServiceA1.java | A1 | 3001 | 1.0 | dev |
| DiscoveryGuideServiceA2.java | A2 | 3002 | 1.1 | qa |
| DiscoveryGuideServiceB1.java | B1 | 4001 | 1.0 | qa |
| DiscoveryGuideServiceB2.java | B2 | 4002 | 1.1 | dev |
| DiscoveryGuideGateway.java | Gateway | 5001 | 1.0 | 无 |
| DiscoveryGuideZuul.java | Zuul | 5002 | 1.0 | 无 |
| DiscoveryGuideConsole.java | Console | 6001 | 1.0 | 无 |
| DiscoveryGuideAdmin.java | Admin | 6002 | 1.0 | 无 |

## 环境验证
- 导入Postman的测试脚本，[脚本地址](https://github.com/Nepxion/DiscoveryGuide/raw/master/postman.json)

- 在Postman中执行目录结构下 ”Nepxion“ -> ”Discovery指南网关接口“ -> ”Gateway网关调用示例“，调用地址为[http://localhost:5001/discovery-guide-service-a/invoke/gateway](http://localhost:5001/discovery-guide-service-a/invoke/gateway)，相关的Header值已经预设，供开发者修改。测试通过Spring Cloud Gateway网关的调用结果，结果为如下格式：
```
gateway -> [ID=discovery-guide-service-a][H=192.168.0.107:3001][V=1.0][R=dev][E=env1][G=discovery-guide-group][TID=48682.7508.15870951148324081][SID=49570.77.15870951148480000] 
-> [ID=discovery-guide-service-b][H=192.168.0.107:4001][V=1.0][R=qa][E=env1][G=discovery-guide-group][TID=48682.7508.15870951148324081][SID=49571.85.15870951189970000]
```

- 在Postman中执行目录结构下 ”Nepxion“ -> ”Discovery指南网关接口“ -> ”Zuul网关调用示例“，调用地址为[http://localhost:5002/discovery-guide-service-a/invoke/zuul](http://localhost:5002/discovery-guide-service-a/invoke/zuul)，相关的Header值已经预设，供开发者修改。测试通过Zuul网关的调用结果，结果为如下格式：
```
zuul -> [ID=discovery-guide-service-a][H=192.168.0.107:3001][V=1.0][R=dev][E=env1][G=discovery-guide-group][TID=48682.7508.15870951148324081][SID=49570.77.15870951148480000] 
-> [ID=discovery-guide-service-b][H=192.168.0.107:4001][V=1.0][R=qa][E=env1][G=discovery-guide-group][TID=48682.7508.15870951148324081][SID=49571.85.15870951189970000]
```

- 上述步骤在下面每次更改规则策略的时候执行，并验证结果和规则策略的期望值是否相同

## 基于Header传递方式的灰度路由策略

本章节通过网关为触发点来介绍灰度路由策略功能，使用者也可以不通过网关，直接以微服务为触发点进行实施

### 灰度路由架构图

#### 多版本灰度路由架构图

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/RouteVersion.jpg)

#### 多区域灰度路由架构图

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/RouteRegion.jpg)

#### 多IP和端口灰度路由架构图

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/RouteAddress.jpg)

### 配置网关灰度路由策略
在Nacos配置中心，增加网关灰度路由策略

#### 版本匹配灰度路由策略
增加Spring Cloud Gateway的基于版本匹配路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-gateway，策略内容如下，实现从Spring Cloud Gateway发起的调用都走版本为1.0的服务：
```xml
 
 
     
         1.0 
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-1.jpg)

每个服务调用的版本都可以自行指定，见下面第二条。当所有服务都选同一版本的时候，可以简化成下面第一条
```
1.  1.0 
2.  {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"} 
```

如果上述表达式还未满足需求，也可以采用通配符（具体详细用法，参考Spring AntPathMatcher）
```
* - 表示调用范围为所有服务的所有版本
1.* - 表示调用范围为所有服务的1开头的所有版本
```
或者
```
"discovery-guide-service-b":"1.*;1.2.?"
```
表示discovery-guide-service-b服务的版本调用范围是1开头的所有版本，或者是1.2开头的所有版本（末尾必须是1个字符）

#### 版本权重灰度路由策略
增加Spring Cloud Gateway的基于版本权重路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-gateway，策略内容如下，实现从Spring Cloud Gateway发起的调用1.0版本流量调用为90%，1.1流量调用为10%：
```xml
 
 
     
         1.0=90;1.1=10 
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-2.jpg)

每个服务调用的版本权重都可以自行指定，见下面第二条。当所有服务都选相同版本权重的时候，可以简化成下面第一条
```
1.  1.0=90;1.1=10 
2.  {"discovery-guide-service-a":"1.0=90;1.1=10", "discovery-guide-service-b":"1.0=90;1.1=10"} 
```

#### 区域匹配灰度路由策略
增加Zuul的基于区域匹配路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现从Zuul发起的调用都走区域为dev的服务：
```xml
 
 
     
         dev 
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-3.jpg)

每个服务调用的区域都可以自行指定，见下面第二条。当所有服务都选同一区域的时候，可以简化成下面第一条
```
1.  dev 
2.  {"discovery-guide-service-a":"dev", "discovery-guide-service-b":"dev"} 
```

如果上述表达式还未满足需求，也可以采用通配符（具体详细用法，参考Spring AntPathMatcher）
```
* - 表示调用范围为所有服务的所有区域
d* - 表示调用范围为所有服务的d开头的所有区域
```
或者
```
"discovery-guide-service-b":"d*;q?"
```
表示discovery-guide-service-b服务的区域调用范围是d开头的所有区域，或者是q开头的所有区域（末尾必须是1个字符）

#### 区域权重灰度路由策略
增加Zuul的基于区域权重路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现从Zuul发起的调用dev区域流量调用为85%，qa区域流量调用为15%：
```xml
 
 
     
         dev=85;qa=15 
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-4.jpg)

每个服务调用的区域权重都可以自行指定，见下面第二条。当所有服务都选相同区域权重的时候，可以简化成下面第一条
```
1.  dev=85;qa=15 
2.  {"discovery-guide-service-a":"dev=85;qa=15", "discovery-guide-service-b":"dev=85;qa=15"} 
```

#### IP地址和端口匹配灰度路由策略
增加Zuul的基于IP地址和端口匹配的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现从Zuul发起的调用走指定IP地址和端口，或者指定IP地址，或者指定端口（下面策略以端口为例）的服务：
```xml
 
 
     
         127.0.0.1:3001  -->
         127.0.0.1  -->
         3001 
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-5.jpg)

每个服务调用的端口都可以自行指定，见下面第二条。当所有服务都选同一端口的时候，可以简化成下面第一条（单机版不适用于该策略）
```
1.  3001 
2.  {"discovery-guide-service-a":"3001", "discovery-guide-service-b":"3001"} 
```

如果上述表达式还未满足需求，也可以采用通配符（具体详细用法，参考Spring AntPathMatcher）
```
* - 表示调用范围为所有服务的所有端口
3* - 表示调用范围为所有服务的3开头的所有端口
```
或者
```
"discovery-guide-service-b":"3*;400?"
```
表示discovery-guide-service-b服务的端口调用范围是3开头的所有端口，或者是4开头的所有端口（末尾必须是1个字符）

### 配置全链路灰度条件命中和灰度匹配组合式策略
属于全链路蓝绿部署的范畴。既适用于Zuul和Spring Cloud Gateway网关，也适用于Service微服务，一般来说，网关已经加了，服务上就不需要加，当不存在的网关的时候，服务就可以考虑加上

支持Spel表达式进行自定义规则，支持所有标准的Spel表达式，包括==，!=，>，>=，  '2'，但a作为Header未传递进来，即为null，判断结果为true
- null满足不等于。当某个Header未传值，但又指定了该Header大于的表达式，那么正则结果是true。例如，表达式为#H['a'] != '2'，但a作为Header未传递进来，即为null，判断结果为true

增加组合式的灰度策略，支持版本匹配、区域匹配、IP地址和端口匹配、版本权重匹配、区域权重匹配。以版本匹配为例，Group为discovery-guide-group，Data Id为discovery-guide-gateway，或者，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现功能：
```
1. 当外部调用带有的Http Header中的值a=1同时b=2
    节点中header="#H['a'] == '1' &amp;&amp; #H['b'] == '2'"对应的version-id="version-route1"，找到下面
    节点中id="version-route1" type="version"的那项，那么路由即为：
   {"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"}

2. 当外部调用带有的Http Header中的值a=1
    节点中header="#H['a'] == '1'"对应的version-id="version-route2"，找到下面
    中id="version-route2" type="version"的那项，那么路由即为：
   {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.1"}

3. 当外部调用带有的Http Header中的值都不命中，那么执行顺序为
   1）如果配置了权重路由（ 节点下）的策略，则执行权重路由
   2）如果权重路由策略未配置，则执行 节点中的全局缺省路由，那么路由即为：
   {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}
   3）如果全局缺省路由未配置，则执行Spring Cloud Ribbon轮询策略
   
4. 必须带有Header。假如不愿意从网关外部传入Header，那么可以通过策略中配置条件表达式中的Header来决策蓝绿和灰度，可以代替外部传入Header，参考如下配置：
    
        
    

5. 策略总共支持5种，可以单独一项使用，也可以多项叠加使用：
   1）version 版本路由
   2）region 区域路由
   3）address IP地址和端口路由
   4）version-weight 版本权重路由
   5）region-weight 区域权重路由

6. 策略支持Spring Spel的条件表达式方式

7. 策略支持Spring Matcher的通配符方式

8. 支持并行实施。通过namespace（可以自定义）的Http Header进行发布隔离
```

```xml
 
 
     
     
         {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"} 
     
    
     
     
         
         
         
             
             
         

         
             {"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"} 
             {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.1"} 
         

         
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-8.jpg)

内置基于Swagger的Rest接口，可以校验策略的条件表达式、校验策略的全链路路由

### 配置全链路灰度条件权重和灰度匹配组合式策略
属于全链路灰度发布的范畴。既适用于Zuul和Spring Cloud Gateway网关，也适用于Service微服务，一般来说，网关已经加了，服务上就不需要加，当不存在的网关的时候，服务就可以考虑加上

增加组合式的灰度策略，支持版本匹配、区域匹配、IP地址和端口匹配。以版本匹配为例，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现功能：
- a服务1.0版本向网关提供90%的流量，1.1版本向网关提供10%的流量
- a服务1.0版本只能访问b服务1.0版本，1.1版本只能访问b服务1.1版本

该功能的意义是，网关随机权重调用服务，而服务链路按照版本匹配方式调用

```
1. version-route1链路配比90%的流量，version-route2链路配比10%的流量

2. 策略总共支持3种，可以单独一项使用，也可以多项叠加使用：
   1）version 版本路由
   2）region 区域路由
   3）address IP地址和端口路由

3. 当带有Header的时候，根据Header的表达式来选择相应的全链路权重策略；如果不带Header，执行默认无条件的全链路权重策略

4. 策略支持Spring Spel的条件表达式方式，用法跟上面一致

5. 策略支持Spring Matcher的通配符方式，用法跟上面一致

6. 支持并行实施。通过namespace（可以自定义）的Http Header进行发布隔离
```

```xml
 
 
     
     
         {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"} 
     

     
     
         
         
         
             
             
             
         

         
             {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"} 
             {"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"} 
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-9.jpg)

### 配置前端灰度和网关灰度路由组合式策略
当前端（例如：APP）和后端微服务同时存在多个版本时，可以执行“前端灰度&网关灰度路由组合式策略”

例如：前端存在1.0和2.0版本，微服务存在1.0和2.0版本，由于存在版本不兼容的情况（前端1.0版本只能调用微服务的1.0版本，前端2.0版本只能调用微服务的2.0版本），那么前端调用网关时候，可以通过Header传递它的版本号给网关，网关根据前端版本号，去路由对应版本的微服务

该场景可以用“通过业务参数在过滤器中自定义灰度路由策略”的方案来解决，如下：

```xml
 
 
     
         
             
             
         

         
             {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"} 
             {"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"} 
         
     
 
```

上述配置，模拟出全链路中，两条独立不受干扰的调用路径：

```
1. APP v1.0 -> 网关 -> A服务 v1.0 -> B服务 v1.0
2. APP v1.1 -> 网关 -> A服务 v1.1 -> B服务 v1.1
```

### 通过其它方式设置灰度路由策略
除了上面通过配置中心发布灰度规路由则外，还有如下三种方式，这三种方式既适用于Zuul和Spring Cloud Gateway网关，也适用于Service微服务

#### 通过前端传入灰度路由策略
通过前端（Postman）方式传入灰度路由策略，来代替配置中心方式，传递全链路路由策略。注意：当配置中心和界面都配置后，以界面传入优先

- 版本匹配策略，Header格式如下任选一个：
```
1. n-d-version=1.0
2. n-d-version={"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}
```

- 版本权重策略，Header格式如下任选一个：
```
1. n-d-version-weight=1.0=90;1.1=10
2. n-d-version-weight={"discovery-guide-service-a":"1.0=90;1.1=10", "discovery-guide-service-b":"1.0=90;1.1=10"}
```

- 区域匹配策略，Header格式如下任选一个：
```
1. n-d-region=qa
2. n-d-region={"discovery-guide-service-a":"qa", "discovery-guide-service-b":"qa"}
```

- 区域权重策略，Header格式如下任选一个：
```
1. n-d-region-weight=dev=99;qa=1
2. n-d-region-weight={"discovery-guide-service-a":"dev=99;qa=1", "discovery-guide-service-b":"dev=99;qa=1"}
```

- IP地址和端口匹配策略，Header格式如下任选一个：
```
1. n-d-address={"discovery-guide-service-a":"127.0.0.1:3001", "discovery-guide-service-b":"127.0.0.1:4002"}
2. n-d-address={"discovery-guide-service-a":"127.0.0.1", "discovery-guide-service-b":"127.0.0.1"}
3. n-d-address={"discovery-guide-service-a":"3001", "discovery-guide-service-b":"4002"}
```

- 环境隔离下动态环境匹配策略：
```
1. n-d-env=env1
```

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-6.jpg)

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide2-7.jpg)

当外界传值Header的时候，网关也设置并传递同名的Header，需要决定哪个Header传递到后边的服务去。需要通过如下开关做控制：
```vb
# 当外界传值Header的时候，网关也设置并传递同名的Header，需要决定哪个Header传递到后边的服务去。如果下面开关为true，以网关设置为优先，否则以外界传值为优先。缺失则默认为true
spring.application.strategy.gateway.header.priority=false
# 当以网关设置为优先的时候，网关未配置Header，而外界配置了Header，仍旧忽略外界的Header。缺失则默认为true
spring.application.strategy.gateway.original.header.ignored=true

# 当外界传值Header的时候，网关也设置并传递同名的Header，需要决定哪个Header传递到后边的服务去。如果下面开关为true，以网关设置为优先，否则以外界传值为优先。缺失则默认为true
spring.application.strategy.zuul.header.priority=false
# 当以网关设置为优先的时候，网关未配置Header，而外界配置了Header，仍旧忽略外界的Header。缺失则默认为true
spring.application.strategy.zuul.original.header.ignored=true
``` 

#### 通过业务参数在过滤器中自定义灰度路由策略
通过过滤器传递Http Header的方式传递全链路灰度路由策略
下面代码既适用于Zuul和Spring Cloud Gateway网关，也适用于Service微服务，一般来说，网关已经加了，服务就不需要加，当不存在的网关的时候，服务上就可以考虑。继承GatewayStrategyRouteFilter、ZuulStrategyRouteFilter或者ServiceStrategyRouteFilter，覆盖掉如下方法中的一个或者多个，通过@Bean方式覆盖框架内置的过滤类
```java
public String getRouteVersion();

public String getRouteRegion();

public String getRouteAddress();

public String getRouteVersionWeight();

public String getRouteRegionWeight();
```

GatewayStrategyRouteFilter示例

在代码里根据不同的Header选择不同的路由路径，示例提供全链路条件命中和全链路随机权重两种方式
```java
// 适用于A/B Testing或者更根据某业务参数决定灰度路由路径。可以结合配置中心分别配置A/B两条路径，可以动态改变并通知
// 当Header中传来的用户为张三，执行一条路由路径；为李四，执行另一条路由路径
public class MyGatewayStrategyRouteFilter extends DefaultGatewayStrategyRouteFilter {
    private static final String DEFAULT_A_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.0\", \"discovery-guide-service-b\":\"1.1\"}";
    private static final String DEFAULT_B_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.1\", \"discovery-guide-service-b\":\"1.0\"}";

    @Value("${a.route.version:" + DEFAULT_A_ROUTE_VERSION + "}")
    private String aRouteVersion;

    @Value("${b.route.version:" + DEFAULT_B_ROUTE_VERSION + "}")
    private String bRouteVersion;

    // 全链路条件命中
    @Override
    public String getRouteVersion() {
        String user = strategyContextHolder.getHeader("user");

        if (StringUtils.equals(user, "zhangsan")) {
            return aRouteVersion;
        } else if (StringUtils.equals(user, "lisi")) {
            return bRouteVersion;
        }

        return super.getRouteVersion();
    }

    // 全链路随机权重
    /*@Override
    public String getRouteVersion() {
        List > list = new ArrayList >();
        list.add(new ImmutablePair (DEFAULT_A_ROUTE_VERSION, 30D));
        list.add(new ImmutablePair (DEFAULT_B_ROUTE_VERSION, 70D));
        MapWeightRandom  weightRandom = new MapWeightRandom (list);
        
        return weightRandom.random();
    }*/
}
```
在配置类里@Bean方式进行过滤类创建，覆盖框架内置的过滤类
```java
@Bean
public GatewayStrategyRouteFilter gatewayStrategyRouteFilter() {
    return new MyGatewayStrategyRouteFilter();
}
```

ZuulStrategyRouteFilter示例

在代码里根据不同的Header选择不同的路由路径，示例提供全链路条件命中和全链路随机权重两种方式
```java
// 适用于A/B Testing或者更根据某业务参数决定灰度路由路径。可以结合配置中心分别配置A/B两条路径，可以动态改变并通知
// 当Header中传来的用户为张三，执行一条路由路径；为李四，执行另一条路由路径
public class MyZuulStrategyRouteFilter extends DefaultZuulStrategyRouteFilter {
    private static final String DEFAULT_A_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.0\", \"discovery-guide-service-b\":\"1.1\"}";
    private static final String DEFAULT_B_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.1\", \"discovery-guide-service-b\":\"1.0\"}";

    @Value("${a.route.version:" + DEFAULT_A_ROUTE_VERSION + "}")
    private String aRouteVersion;

    @Value("${b.route.version:" + DEFAULT_B_ROUTE_VERSION + "}")
    private String bRouteVersion;

    // 全链路条件命中
    @Override
    public String getRouteVersion() {
        String user = strategyContextHolder.getHeader("user");

        if (StringUtils.equals(user, "zhangsan")) {
            return aRouteVersion;
        } else if (StringUtils.equals(user, "lisi")) {
            return bRouteVersion;
        }

        return super.getRouteVersion();
    }

    // 全链路随机权重
    /*@Override
    public String getRouteVersion() {
        List > list = new ArrayList >();
        list.add(new ImmutablePair (DEFAULT_A_ROUTE_VERSION, 30D));
        list.add(new ImmutablePair (DEFAULT_B_ROUTE_VERSION, 70D));
        MapWeightRandom  weightRandom = new MapWeightRandom (list);
        
        return weightRandom.random();
    }*/
}
```
在配置类里@Bean方式进行过滤类创建，覆盖框架内置的过滤类
```java
@Bean
public ZuulStrategyRouteFilter zuulStrategyRouteFilter() {
    return new MyZuulStrategyRouteFilter();
}
```

ServiceStrategyRouteFilter示例

在代码里根据不同的Header选择不同的路由路径，示例提供全链路条件命中和全链路随机权重两种方式
```java
// 适用于A/B Testing或者更根据某业务参数决定灰度路由路径。可以结合配置中心分别配置A/B两条路径，可以动态改变并通知
// 当Header中传来的用户为张三，执行一条路由路径；为李四，执行另一条路由路径
public class MyServiceStrategyRouteFilter extends DefaultServiceStrategyRouteFilter {
    private static final String DEFAULT_A_ROUTE_VERSION = "{\"discovery-guide-service-b\":\"1.1\"}";
    private static final String DEFAULT_B_ROUTE_VERSION = "{\"discovery-guide-service-b\":\"1.0\"}";

    @Value("${a.route.version:" + DEFAULT_A_ROUTE_VERSION + "}")
    private String aRouteVersion;

    @Value("${b.route.version:" + DEFAULT_B_ROUTE_VERSION + "}")
    private String bRouteVersion;

    // 全链路条件命中
    @Override
    public String getRouteVersion() {
        String user = strategyContextHolder.getHeader("user");

        if (StringUtils.equals(user, "zhangsan")) {
            return aRouteVersion;
        } else if (StringUtils.equals(user, "lisi")) {
            return bRouteVersion;
        }

        return super.getRouteVersion();
    }

    // 全链路随机权重
    /*@Override
    public String getRouteVersion() {
        List > list = new ArrayList >();
        list.add(new ImmutablePair (DEFAULT_A_ROUTE_VERSION, 30D));
        list.add(new ImmutablePair (DEFAULT_B_ROUTE_VERSION, 70D));
        MapWeightRandom  weightRandom = new MapWeightRandom (list);
        
        return weightRandom.random();
    }*/
}
```
在配置类里@Bean方式进行过滤类创建，覆盖框架内置的过滤类
```java
@Bean
public ServiceStrategyRouteFilter serviceStrategyRouteFilter() {
    return new MyServiceStrategyRouteFilter();
}
```

#### 通过业务参数在策略类中自定义灰度路由策略
通过策略方式自定义灰度路由策略。下面代码既适用于Zuul和Spring Cloud Gateway网关，也适用于Service微服务，同时全链路中网关和服务都必须加该方式，DefaultDiscoveryEnabledStrategy可以有多个，框架会组合判断
```java
// 实现了组合策略，版本路由策略+区域路由策略+IP和端口路由策略+自定义策略
public class MyDiscoveryEnabledStrategy extends DefaultDiscoveryEnabledStrategy {
    private static final Logger LOG = LoggerFactory.getLogger(MyDiscoveryEnabledStrategy.class);

    // 对REST调用传来的Header参数（例如：mobile）做策略
    @Override
    public boolean apply(Server server) {
        String mobile = strategyContextHolder.getHeader("mobile");
        String serviceId = pluginAdapter.getServerServiceId(server);
        String version = pluginAdapter.getServerVersion(server);
        String region = pluginAdapter.getServerRegion(server);
        String environment = pluginAdapter.getServerEnvironment(server);
        String address = server.getHostPort();

        LOG.info("负载均衡用户定制触发：mobile={}, serviceId={}, version={}, region={}, env={}, address={}", mobile, serviceId, version, region, environment, address);

        if (StringUtils.isNotEmpty(mobile)) {
            // 手机号以移动138开头，路由到1.0版本的服务上
            if (mobile.startsWith("138") && StringUtils.equals(version, "1.0")) {
                return true;
                // 手机号以联通133开头，路由到2.0版本的服务上
            } else if (mobile.startsWith("133") && StringUtils.equals(version, "1.1")) {
                return true;
            } else {
                // 其它情况，直接拒绝请求
                return false;
            }
        }

        return true;
    }
}
```
在配置类里@Bean方式进行策略类创建
```java
@Bean
public DiscoveryEnabledStrategy discoveryEnabledStrategy() {
    return new MyDiscoveryEnabledStrategy();
}
```
在网关和服务中支持基于Rest Header传递的自定义灰度路由策略，除此之外，服务还支持基于Rpc方法参数传递的自定义灰度路由策略，它包括接口名、方法名、参数名或参数值等多种形式。下面的示例表示在服务中同时开启基于Rest Header传递和Rpc方法参数传递的自定义组合式灰度路由策略，DefaultDiscoveryEnabledStrategy可以有多个，框架会组合判断
```java
// 实现了组合策略，版本路由策略+区域路由策略+IP和端口路由策略+自定义策略
public class MyDiscoveryEnabledStrategy implements DiscoveryEnabledStrategy {
    private static final Logger LOG = LoggerFactory.getLogger(MyDiscoveryEnabledStrategy.class);

    @Autowired
    private PluginAdapter pluginAdapter;

    @Autowired
    private ServiceStrategyContextHolder serviceStrategyContextHolder;

    @Override
    public boolean apply(Server server) {
        boolean enabled = applyFromHeader(server);
        if (!enabled) {
            return false;
        }

        return applyFromMethod(server);
    }

    // 根据REST调用传来的Header参数（例如：mobile），选取执行调用请求的服务实例
    private boolean applyFromHeader(Server server) {
        String mobile = serviceStrategyContextHolder.getHeader("mobile");
        String serviceId = pluginAdapter.getServerServiceId(server);
        String version = pluginAdapter.getServerVersion(server);
        String region = pluginAdapter.getServerRegion(server);
        String environment = pluginAdapter.getServerEnvironment(server);
        String address = server.getHostPort();

        LOG.info("负载均衡用户定制触发：mobile={}, serviceId={}, version={}, region={}, env={}, address={}", mobile, serviceId, version, region, environment, address);

        if (StringUtils.isNotEmpty(mobile)) {
            // 手机号以移动138开头，路由到1.0版本的服务上
            if (mobile.startsWith("138") && StringUtils.equals(version, "1.0")) {
                return true;
                // 手机号以联通133开头，路由到2.0版本的服务上
            } else if (mobile.startsWith("133") && StringUtils.equals(version, "1.1")) {
                return true;
            } else {
                // 其它情况，直接拒绝请求
                return false;
            }
        }

        return true;
    }

    // 根据RPC调用传来的方法参数（例如接口名、方法名、参数名或参数值等），选取执行调用请求的服务实例
    // 本示例只作用在discovery-guide-service-a服务上
    @SuppressWarnings("unchecked")
    private boolean applyFromMethod(Server server) {
        Map  attributes = serviceStrategyContextHolder.getRpcAttributes();
        String serviceId = pluginAdapter.getServerServiceId(server);
        String version = pluginAdapter.getServerVersion(server);
        String region = pluginAdapter.getServerRegion(server);
        String environment = pluginAdapter.getServerEnvironment(server);
        String address = server.getHostPort();

        LOG.info("负载均衡用户定制触发：attributes={}, serviceId={}, version={}, region={}, env={}, address={}", attributes, serviceId, version, region, environment, address);

        if (attributes.containsKey(DiscoveryConstant.PARAMETER_MAP)) {
            Map  parameterMap = (Map ) attributes.get(DiscoveryConstant.PARAMETER_MAP);
            String value = parameterMap.get("value").toString();
            if (StringUtils.isNotEmpty(value)) {
                // 输入值包含dev，路由到dev区域的服务上
                if (value.contains("dev") && StringUtils.equals(region, "dev")) {
                    return true;
                    // 输入值包含qa，路由到qa区域的服务上
                } else if (value.contains("qa") && StringUtils.equals(region, "qa")) {
                    return true;
                } else {
                    // 其它情况，直接通过请求
                    return true;
                }
            }
        }

        return true;
    }
}
```
需要通过如下开关开启该功能
```vb
# 启动和关闭路由策略的时候，对RPC方式的调用拦截。缺失则默认为false
spring.application.strategy.rpc.intercept.enabled=true
```

## 基于订阅方式的全链路灰度发布规则
在Nacos配置中心，增加全链路灰度发布规则
注意：该功能和网关灰度路由和灰度权重功能会叠加，为了不影响演示效果，请先清除网关灰度路由的策略

### 配置全链路灰度匹配规则

#### 版本匹配灰度规则
增加版本匹配的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现a服务1.0版本只能访问b服务1.0版本，a服务1.1版本只能访问b服务1.1版本：
```xml
 
 
     
         
             
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide3-1.jpg)

#### 区域匹配灰度规则
增加区域匹配的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现dev区域的a服务只能访问dev区域的b服务，qa区域的a服务只能访问qa区域的b服务：
```xml
 
 
     
         
             
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide3-2.jpg)

### 配置全链路灰度权重规则

#### 全局版本权重灰度规则
增加全局版本权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现版本为1.0的服务提供90%的流量，版本为1.1的服务提供10%的流量：
```xml
 
 
     
         
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide4-1.jpg)

#### 局部版本权重灰度规则
增加局部版本权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现a服务1.0版本提供90%的流量，1.1版本提供10%的流量；b服务1.0版本提供20%的流量，1.1版本提供80%的流量：
```xml
 
 
     
         
             
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide4-2.jpg)

#### 全局区域权重灰度规则
增加全局区域权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现区域为dev的服务提供90%的流量，区域为qa的服务提供10%的流量：
```xml
 
 
     
         
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide4-3.jpg)

#### 局部区域权重灰度规则
增加局部区域权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现a服务dev区域提供90%的流量，qa区域提供10%的流量；b服务dev区域提供20%的流量，qa区域提供80%的流量：
```xml
 
 
     
         
             
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide4-4.jpg)

注意：局部权重优先级高于全局权重，版本权重优先级高于区域权重

请执行Postman操作，请仔细观察服务被随机权重调用到的概率

### 配置全链路灰度权重和灰度匹配组合式规则
增加组合式的灰度规则，支持版本匹配和区域匹配。以版本匹配为例，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现功能：
- a服务1.0版本向网关提供90%的流量，1.1版本向网关提供10%的流量
- a服务1.0版本只能访问b服务1.0版本，1.1版本只能访问b服务1.1版本

该功能的意义是，网关随机权重调用服务，而服务链路按照版本匹配方式调用

```xml
 
 
     
         
             
             
         

         
             
             
         
     
 
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide5-1.jpg)

图形化界面验证
- 下载[源码主页](https://github.com/Nepxion/Discovery)的工程，并导入IDE
- 启动源码工程下的discovery-springcloud-example-console/ConsoleApplication
- 启动源码工程下的discovery-console-desktop/ConsoleLauncher
- 通过admin/admin登录，点击“显示服务拓扑”按钮，将呈现如下界面
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide5-2.jpg)
- 在加入上述规则前，选中网关节点，右键点击“执行灰度路由”，在弹出路由界面中，依次加入“discovery-guide-service-a”和“discovery-guide-service-b”，点击“执行路由”按钮，将呈现如下界面
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide5-3.jpg)
- 在加入上述规则后，在路由界面中，再次点击“执行路由”按钮，将呈现如下界面
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide5-4.jpg)

## 基于多方式的规则和策略推送

### 基于远程配置中心的规则和策略订阅推送

Nacos订阅推送界面

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Nacos2.jpg)

Apollo订阅推送界面

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Apollo1.jpg)

### 基于Swagger和Rest的规则和策略推送

服务侧单个推送界面

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Swagger1.jpg)

控制平台批量推送界面

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Swagger2.jpg)

## 基于Group的全链路服务隔离

元数据中的Group在一定意义上代表着系统ID或者系统逻辑分组，基于Group策略意味着只有同一个系统中的服务才能调用

### 注册服务隔离
基于Group黑/白名单的策略，即当前的服务所在的Group，不在Group的黑名单或者在白名单里，才允许被注册。只需要在网关或者服务端，开启如下配置即可：
```vb
# 启动和关闭注册的服务隔离（基于Group黑/白名单的策略）。缺失则默认为false
spring.application.strategy.register.isolation.enabled=true
```
黑/白名单通过如下方式配置
```vb
spring.application.strategy.register.isolation.group.blacklist=
spring.application.strategy.register.isolation.group.whitelist=
```

### 消费端服务隔离
基于Group是否相同的策略，即消费端拿到的提供端列表，两者的Group必须相同。只需要在网关或者服务端，开启如下配置即可：
```vb
# 启动和关闭消费端的服务隔离（基于Group是否相同的策略）。缺失则默认为false
spring.application.strategy.consumer.isolation.enabled=true
```
通过修改discovery-guide-service-b的Group名为其它名称，执行Postman调用，将发现从discovery-guide-service-a无法拿到discovery-guide-service-b的任何实例。意味着在discovery-guide-service-a消费端进行了隔离

### 提供端服务隔离
基于Group是否相同的策略，即服务端被消费端调用，两者的Group必须相同，否则拒绝调用，异构系统可以通过Header方式传递n-d-service-group值进行匹配。只需要在服务端（不适用网关），开启如下配置即可：
```vb
# 启动和关闭提供端的服务隔离（基于Group是否相同的策略）。缺失则默认为false
spring.application.strategy.provider.isolation.enabled=true

# 灰度路由策略的时候，需要指定对业务RestController类的扫描路径。此项配置作用于RPC方式的调用拦截和消费端的服务隔离两项工作
spring.application.strategy.scan.packages=com.nepxion.discovery.guide.service.feign
```

在Postman调用，执行[http://localhost:4001/invoke/abc](http://localhost:4001/invoke/abc)，去调用discovery-guide-service-b服务，将出现如下异常。意味着在discovery-guide-service-b提供端进行了隔离
```
Reject to invoke because of isolation with different service group
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide6-1.jpg)
如果加上n-d-service-group=discovery-guide-group的Header，那么两者保持Group相同，则调用通过。这是解决异构系统调用微服务被隔离的一种手段
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide6-2.jpg)

## 基于Env的全链路环境隔离和路由

基于元数据Metadata的env参数进行隔离，当调用端实例和提供端实例的元数据Metadata环境配置值相等才能调用。环境隔离下，调用端实例找不到符合条件的提供端实例，把流量路由到一个通用或者备份环境

支持两种方式的环境隔离，动态调度子环境的能力
- 网关独立部署
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/IsolationEnvironment1.jpg)

- 网关非独立部署
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/IsolationEnvironment2.jpg)

### 环境隔离

在网关或者服务端，配置环境元数据，在同一套环境下，env值必须是一样的，这样才能达到在同一个注册中心下，环境隔离的目的
- 当网关配置了env元数据，网关和服务同处于一套环境下，会自动执行隔离
- 当网关未配置env元数据，网关管辖多个子环境，那么可以通过外部传入n-d-env的Header方式，让网关去调度子环境。如果外部未传入n-d-env的Header，网关则执行Spring Cloud Ribbon轮询策略
```vb
spring.cloud.nacos.discovery.metadata.env=env1
```

需要在调用端开启如下配置：
```vb
# 启动和关闭环境隔离，环境隔离指调用端实例和提供端实例的元数据Metadata环境配置值相等才能调用。缺失则默认为false
spring.application.environment.isolation.enabled=true
```

### 环境路由

需要在调用端开启如下配置：
```vb
# 启动和关闭环境路由，环境路由指在环境隔离下，调用端实例找不到符合条件的提供端实例，把流量路由到一个通用或者备份环境，例如：元数据Metadata环境配置值为common（该值可配置，但不允许为保留值default）。缺失则默认为false
spring.application.environment.route.enabled=true
# 流量路由到指定的环境下。不允许为保留值default，缺失则默认为common
spring.application.environment.route=common
```

## 基于Sentinel的全链路服务限流熔断降级权限和灰度融合

通过集成Sentinel，在服务端实现该功能

封装NacosDataSource和ApolloDataSource，支持Nacos和Apollo两个远程配置中心，零代码实现Sentinel功能。更多的远程配置中心，请参照Sentinel官方的DataSource并自行集成
```
1. Nacos的Key格式：Group为元数据中配置的[组名]，Data Id为[服务名]-[规则类型]
2. Apollo的Key格式：[组名]-[服务名]-[规则类型]
```

支持远程配置中心和本地规则文件的读取逻辑，即优先读取远程配置，如果不存在或者规则错误，则读取本地规则文件。动态实现远程配置中心对于规则的热刷新

支持如下开关开启该动能，默认是关闭的
```vb
# 启动和关闭Sentinel限流降级熔断权限等原生功能的数据来源扩展和调用链埋点输出。缺失则默认为false
spring.application.strategy.sentinel.enabled=true
```

### 原生Sentinel注解

参照下面代码，为接口方法增加@SentinelResource注解，value为sentinel-resource，blockHandler和fallback是防护其作用后需要执行的方法

```java
@RestController
@ConditionalOnProperty(name = DiscoveryConstant.SPRING_APPLICATION_NAME, havingValue = "discovery-guide-service-b")
public class BFeignImpl extends AbstractFeignImpl implements BFeign {
    private static final Logger LOG = LoggerFactory.getLogger(BFeignImpl.class);

    @Override
    @SentinelResource(value = "sentinel-resource", blockHandler = "handleBlock", fallback = "handleFallback")
    public String invoke(@PathVariable(value = "value") String value) {
        value = doInvoke(value);

        LOG.info("调用路径：{}", value);

        return value;
    }

    public String handleBlock(String value, BlockException e) {
        return value + "-> B server sentinel block, cause=" + e.getClass().getName() + ", rule=" + e.getRule() + ", limitApp=" + e.getRuleLimitApp();
    }

    public String handleFallback(String value) {
        return value + "-> B server sentinel fallback";
    }
}
```

### 原生Sentinel规则

原生Sentinel规则的用法，请参照Sentinel官方文档

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Sentinel3.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Sentinel4.jpg)

#### 流控规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-flow，规则内容如下：
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "default",
        "grade": 1,
        "count": 1,
        "strategy": 0,
        "refResource": null,
        "controlBehavior": 0,
        "warmUpPeriodSec": 10,
        "maxQueueingTimeMs": 500,
        "clusterMode": false,
        "clusterConfig": null
    }
]
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-1.jpg)

#### 降级规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-degrade，规则内容如下：
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "default",
        "count": 2,
        "timeWindow": 10,
        "grade": 0,
        "passCount": 0
    }
]
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-2.jpg)

#### 授权规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下：
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "discovery-guide-service-a",
        "strategy": 0
    }
]
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-3.jpg)

#### 系统规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-system，规则内容如下：
```
[
    {
        "resource": null,
        "limitApp": null,
        "highestSystemLoad": -1.0,
        "highestCpuUsage": -1.0,
        "qps": 200.0,
        "avgRt": -1,
        "maxThread": -1
    }
]
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-4.jpg)

#### 热点参数流控规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-param-flow，规则内容如下：
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "default",
        "grade": 1,
        "paramIdx": 0,
        "count": 1,
        "controlBehavior": 0,
        "maxQueueingTimeMs": 0,
        "burstCount": 0,
        "durationInSec": 1,
        "paramFlowItemList": [],
        "clusterMode": false
    }
]
```
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-5.jpg)

### 基于灰度路由和Sentinel-LimitApp扩展的防护机制

该方式对于上面5种规则都有效，这里以授权规则展开阐述

授权规则中，limitApp，如果有多个，可以通过“,”分隔。"strategy": 0 表示白名单，"strategy": 1 表示黑名单

#### 基于服务名的防护机制

修改配置项Sentinel Request Origin Key为服务名的Header名称，修改授权规则中limitApp为对应的服务名，可实现基于服务名的防护机制

配置项，该配置项默认为n-d-service-id，可以不配置
```vb
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-id
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示所有discovery-guide-service-a服务允许访问discovery-guide-service-b服务
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "discovery-guide-service-a",
        "strategy": 0
    }
]
```

#### 基于灰度组的防护机制

修改配置项Sentinel Request Origin Key为灰度组的Header名称，修改授权规则中limitApp为对应的组名，可实现基于组名的防护机制

配置项
```vb
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-group
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示隶属my-group组的所有服务都允许访问服务discovery-guide-service-b
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "my-group",
        "strategy": 0
    }
]
```

#### 基于灰度版本的防护机制

修改配置项Sentinel Request Origin Key为灰度版本的Header名称，修改授权规则中limitApp为对应的版本，可实现基于版本的防护机制

配置项
```vb
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-version
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示版本为1.0的所有服务都允许访问服务discovery-guide-service-b
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "1.0",
        "strategy": 0
    }
]
```

#### 基于灰度区域的防护机制

修改配置项Sentinel Request Origin Key为灰度区域的Header名称，修改授权规则中limitApp为对应的区域，可实现基于区域的防护机制

配置项
```vb
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-region
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示区域为dev的所有服务都允许访问服务discovery-guide-service-b
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "dev",
        "strategy": 0
    }
]
```

#### 基于IP地址和端口的防护机制

修改配置项Sentinel Request Origin Key为灰度区域的Header名称，修改授权规则中limitApp为对应的区域值，可实现基于IP地址和端口的防护机制

配置项
```vb
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-address
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示地址和端口为192.168.0.88:8081和192.168.0.88:8082的服务都允许访问服务discovery-guide-service-b
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "192.168.0.88:8081,192.168.0.88:8082",
        "strategy": 0
    }
]
```

支持如下开关开启该动能，默认是关闭的
```vb
# 启动和关闭Sentinel LimitApp限流等功能。缺失则默认为false
spring.application.strategy.service.sentinel.limit.app.enabled=true
```

#### 自定义业务参数的组合式防护机制

通过适配类实现自定义业务参数的组合式防护机制
```java
// 自定义版本号+用户名，实现组合式熔断
public class MyServiceSentinelRequestOriginAdapter extends DefaultServiceSentinelRequestOriginAdapter {
    @Override
    public String parseOrigin(HttpServletRequest request) {
        String version = request.getHeader(DiscoveryConstant.N_D_SERVICE_VERSION);
        String user = request.getHeader("user");

        return version + "&" + user;
    }
}
```
在配置类里@Bean方式进行适配类创建
```java
@Bean
public ServiceSentinelRequestOriginAdapter ServiceSentinelRequestOriginAdapter() {
    return new MyServiceSentinelRequestOriginAdapter();
}
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示版本为1.0且传入的Http Header的user=zhangsan，同时满足这两个条件下的所有服务都允许访问服务discovery-guide-service-b
```
[
    {
        "resource": "sentinel-resource",
        "limitApp": "1.0&zhangsan",
        "strategy": 0
    }
]
```

运行效果

- 当传递的Http Header中user=zhangsan，当全链路调用中，API网关负载均衡discovery-guide-service-a服务到1.0版本后再去调用discovery-guide-service-b服务，最终调用成功

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-6.jpg)

- 当传递的Http Header中user=lisi，不满足条件，最终调用在discovery-guide-service-b服务端被拒绝掉

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-7.jpg)

- 当传递的Http Header中user=zhangsan，满足条件之一，当全链路调用中，API网关负载均衡discovery-guide-service-a服务到1.1版本后再去调用discovery-guide-service-b服务，不满足version=1.0的条件，最终调用在discovery-guide-service-b服务端被拒绝掉

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/DiscoveryGuide7-8.jpg)

## 基于Hystrix的全链路服务限流熔断和灰度融合

通过引入Hystrix组件实现服务限流熔断的功能。灰度路由Header和调用链Span在Hystrix线程池隔离模式（信号量模式不需要引入）下传递时，通过线程上下文切换会存在丢失Header的问题，通过下述步骤解决，同时适用于网关端和服务端

- Pom引入
```xml
 
 
     com.nepxion 
     discovery-plugin-strategy-starter-hystrix 
     ${discovery.version} 
 
```

- 配置开启
```vb
# 开启服务端实现Hystrix线程隔离模式做服务隔离时，必须把spring.application.strategy.hystrix.threadlocal.supported设置为true，同时要引入discovery-plugin-strategy-starter-hystrix包，否则线程切换时会发生ThreadLocal上下文对象丢失。缺失则默认为false
spring.application.strategy.hystrix.threadlocal.supported=true
```

该方案也可以被异步跨线程Agent代替

## 全链路监控

### 全链路调用链监控-Tracing

调用链监控，在本文主要指灰度调用链监控。快速入门操作，请访问操作视频[Nepxion Discovery 灰度发布路由调用链](https://pan.baidu.com/s/1PbksbZKVY7reBrnVb3RS6Q)，注意一定要下载下来看，不要在线看，否则不清晰

灰度调用链主要包括如下12个参数，以n-d-service开头的是必须的，其它是可选的或者按照场景而定。使用者可以自行定义要传递的调用链参数，例如：traceId, spanId等；也可以自行定义要传递的业务调用链参数，例如：mobile, user等
```
1. n-d-service-group - 服务所属组或者应用
2. n-d-service-type - 服务类型，分为“网关”和“服务”
3. n-d-service-id - 服务ID
4. n-d-service-address - 服务地址，包括Host和Port
5. n-d-service-version - 服务版本
6. n-d-service-region - 服务所属区域
7. n-d-service-env - 服务所属环境
8. n-d-version - 版本路由值
9. n-d-region - 区域路由值
10. n-d-address - 地址路由值
11. n-d-version-weight - 版本权重路由值
12. n-d-region-weight - 区域权重路由值
```
灰度调用链输出分为Header方式、调用链方式、日志MDC方式，三种方式可以并存使用。调用链方式支持WebMvc和WebFlux

#### Header输出方式

- Spring Cloud Gateway网关端自行会传输Header值（参考Discovery源码中的AbstractGatewayStrategyRouteFilter.java）
- Zuul网关端自行会传输Header值（参考Discovery源码中的AbstractZuulStrategyRouteFilter.java）
- 服务端通过Feign和RestTemplate拦截器传输Header值（参考Discovery源码中的FeignStrategyInterceptor.java和RestTemplateStrategyInterceptor.java）

#### 调用链输出方式

调用链输出方式以OpenUber Jaeger为例来说明

1. 从[网盘文档](https://pan.baidu.com/s/1i57rXaNKPuhGRqZ2MONZOA)获取，Windows操作系统下解压后运行jaeger.bat，Mac和Lunix操作系统请自行研究
2. 执行Postman调用后，访问[http://localhost:16686](http://localhost:16686)查看灰度调用链
3. 灰度调用链支持WebMvc和WebFlux两种方式，以GRAY字样的标记来标识
4. 支持对Sentinel自动埋点

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Jaeger1.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Jaeger2.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Jaeger3.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Jaeger4.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Jaeger5.jpg)

集成Sentinel + 灰度全链路监控
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Jaeger6.jpg)

集成主流中间件 + 灰度全链路监控

代码请从[指南示例高级版](https://github.com/Nepxion/DiscoveryGuide)获取，分支为premium。运行出下图强大效果的前提，需要事先搭建Nacos、Jaeger、ActiveMQ、MongoDB、RabbitMQ、Redis、RocketMQ以及MySQL数据库等环境
使用者如果不想搭建环境，想直接观看效果，可以直接把[离线数据](https://github.com/Nepxion/DiscoveryGuide/raw/master/tracing.json)导入到Jaeger界面（JSON File栏，拖进去即可），观看到下图效果
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/JaegerPremium1.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/JaegerPremium2.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/JaegerPremium3.jpg)

附录 Skywalking
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Skywalking1.jpg)
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Skywalking2.jpg)

请注意如下配置，将决定终端界面的显示
1. 如果开启，灰度信息输出到独立的Span节点中，意味着在界面显示中，灰度信息通过独立的GRAY Span节点来显示。优点是信息简洁明了，缺点是Span节点会增长一倍
2. 如果关闭，灰度信息输出到原生的Span节点中，意味着在界面显示中，灰度信息会和原生Span节点的调用信息、协议信息等混在一起，缺点是信息庞杂混合，优点是Span节点数不会增长
```vb
# 启动和关闭调用链的灰度信息以独立的Span节点输出，如果关闭，则灰度信息输出到原生的Span节点中（Skywalking不支持原生模式）。缺失则默认为true
spring.application.strategy.tracer.separate.span.enabled=true
```

自定义调用链上下文参数的创建（该类不是必须的），继承DefaultStrategyTracerAdapter
```java
// 自定义调用链上下文参数的创建
// 对于getTraceId和getSpanId方法，在OpenTracing等调用链中间件引入的情况下，由调用链中间件决定，在这里定义不会起作用；在OpenTracing等调用链中间件未引入的情况下，在这里定义才有效，下面代码中表示从Http Header中获取，并全链路传递
// 对于getCustomizationMap方法，表示输出到调用链中的定制化业务参数，可以同时输出到日志和OpenTracing等调用链中间件，下面代码中表示从Http Header中获取，并全链路传递
public class MyStrategyTracerAdapter extends DefaultStrategyTracerAdapter {
    @Override
    public String getTraceId() {
        return StringUtils.isNotEmpty(strategyContextHolder.getHeader(DiscoveryConstant.TRACE_ID)) ? strategyContextHolder.getHeader(DiscoveryConstant.TRACE_ID) : StringUtils.EMPTY;
    }

    @Override
    public String getSpanId() {
        return StringUtils.isNotEmpty(strategyContextHolder.getHeader(DiscoveryConstant.SPAN_ID)) ? strategyContextHolder.getHeader(DiscoveryConstant.SPAN_ID) : StringUtils.EMPTY;
    }

    @Override
    public Map  getCustomizationMap() {
        Map  customizationMap = new HashMap ();
        customizationMap.put("mobile", StringUtils.isNotEmpty(strategyContextHolder.getHeader("mobile")) ? strategyContextHolder.getHeader("mobile") : StringUtils.EMPTY);
        customizationMap.put("user", StringUtils.isNotEmpty(strategyContextHolder.getHeader("user")) ? strategyContextHolder.getHeader("user") : StringUtils.EMPTY);

        return customizationMap;
    }
}
```
在配置类里@Bean方式进行调用链类创建，覆盖框架内置的调用链类
```java
@Bean
public StrategyTracerAdapter strategyTracerAdapter() {
    return new MyStrategyTracerAdapter();
}
```

自定义类方法上入参和出参输出到调用链（该类不是必须的），继承ServiceStrategyMonitorAdapter
```java
// 自定义类方法上入参和出参输出到调用链
// parameterMap格式：
// key为入参名
// value为入参值
public class MyServiceStrategyMonitorAdapter implements ServiceStrategyMonitorAdapter {
    @Override
    public Map  getCustomizationMap(ServiceStrategyMonitorInterceptor interceptor, MethodInvocation invocation, Map  parameterMap, Object returnValue) {
        Map  customizationMap = new HashMap ();
        customizationMap.put(DiscoveryConstant.PARAMETER, parameterMap.toString());
        customizationMap.put(DiscoveryConstant.RETURN, returnValue != null ? returnValue.toString() : null);

        return customizationMap;
    }
}
```
在配置类里@Bean方式进行创建
```java
@Bean
public ServiceStrategyMonitorAdapter serviceStrategyMonitorAdapter() {
    return new MyServiceStrategyMonitorAdapter();
}
```

业务方法上获取TraceId和SpanId
```java
public class MyClass {
    @Autowired
    private StrategyMonitorContext strategyMonitorContext;

    public void doXXX() {
        String traceId = strategyMonitorContext.getTraceId();
        String spanId = strategyMonitorContext.getSpanId();
        ...
    }
}
```

对于调用链功能的开启和关闭，需要通过如下开关做控制：
```vb
# 启动和关闭监控，一旦关闭，调用链和日志输出都将关闭。缺失则默认为false
spring.application.strategy.monitor.enabled=true
# 启动和关闭日志输出。缺失则默认为false
spring.application.strategy.logger.enabled=true
# 日志输出中，是否显示MDC前面的Key。缺失则默认为true
# spring.application.strategy.logger.mdc.key.shown=true
# 启动和关闭Debug日志打印，注意每调用一次都会打印一次，会对性能有所影响，建议压测环境和生产环境关闭。缺失则默认为false
spring.application.strategy.logger.debug.enabled=true
# 启动和关闭调用链输出。缺失则默认为false
spring.application.strategy.tracer.enabled=true
# 启动和关闭调用链的灰度信息以独立的Span节点输出，如果关闭，则灰度信息输出到原生的Span节点中（Skywalking不支持原生模式）。缺失则默认为true
# spring.application.strategy.tracer.separate.span.enabled=true
# 启动和关闭调用链的灰度规则策略信息输出。缺失则默认为true
# spring.application.strategy.tracer.rule.output.enabled=true
# 启动和关闭调用链的异常信息是否以详细格式输出。缺失则默认为false
spring.application.strategy.tracer.exception.detail.output.enabled=true
# 启动和关闭类方法上入参和出参输出到调用链。缺失则默认为false
# spring.application.strategy.tracer.method.context.output.enabled=false
```

对于灰度Span输出在调用链界面上的显示，提供如下配置
```vb
# 显示在调用链界面上灰度Span的名称，建议改成具有公司特色的框架产品名称。缺失则默认为NEPXION
# spring.application.strategy.tracer.span.value=NEPXION
# 显示在调用链界面上灰度Span Tag的插件名称，建议改成具有公司特色的框架产品的描述。缺失则默认为Nepxion Discovery
# spring.application.strategy.tracer.span.tag.plugin.value=Nepxion Discovery
```

对Sentinel自动埋点，有如下两个参数默认处于关闭状态，但因为原生的Sentinel不是Spring技术栈，下面参数必须通过-D方式或者System.setProperty方式等设置进去
```vb
# 启动和关闭Sentinel调用链上规则在Span上的输出，注意：原生的Sentinel不是Spring技术栈，下面参数必须通过-D方式或者System.setProperty方式等设置进去。缺失则默认为true
# spring.application.strategy.tracer.sentinel.rule.output.enabled=true
# 启动和关闭Sentinel调用链上方法入参在Span上的输出，注意：原生的Sentinel不是Spring技术栈，下面参数必须通过-D方式或者System.setProperty方式等设置进去。缺失则默认为false
# spring.application.strategy.tracer.sentinel.args.output.enabled=false
```

注意，OpenTracing对Finchley版的Spring Cloud Gateway的reactor-core包存在版本兼容性问题，如果使用者希望Finchley版的Spring Cloud Gateway上使用OpenTracing，需要做如下改造
```java
 
     com.nepxion 
     discovery-plugin-strategy-starter-gateway 
     ${discovery.version} 
     
         
             io.projectreactor 
             reactor-core 
         
     
 

 
     io.projectreactor 
     reactor-core 
     3.2.3.RELEASE 
 
```
上述方式也适用于其它引入了低版本reactor-core包版本兼容性的场景

#### 日志输出方式

可以单独输出，也可以结合调用链一起组合输出，使用方式跟调用链方式类似 

参考在IDE控制台打印的结果
![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Tracer.jpg)

### 全链路指标监控-Metrics

#### Prometheus监控方式

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Prometheus.jpg)

#### Grafana监控方式

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Grafana.jpg)

#### Spring-Boot-Admin监控方式

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Admin7.jpg)

## 全链路Header传递

框架会默认把相关的Header，进行全链路传递，可以通过如下配置进行。除此之外，凡是以“n-d-”开头的任何Header，框架都会默认全链路传递
```vb
# 启动和关闭路由策略的时候，对REST方式的调用拦截。缺失则默认为true
spring.application.strategy.rest.intercept.enabled=true
# 启动和关闭Header传递的Debug日志打印，注意每调用一次都会打印一次，会对性能有所影响，建议压测环境和生产环境关闭。缺失则默认为false
spring.application.strategy.rest.intercept.debug.enabled=true
# 灰度路由策略的时候，对REST方式调用拦截的时候（支持Feign或者RestTemplate调用），希望把来自外部自定义的Header参数（用于框架内置上下文Header，例如：trace-id, span-id等）传递到服务里，那么配置如下值。如果多个用“;”分隔，不允许出现空格
spring.application.strategy.context.request.headers=trace-id;span-id
# 灰度路由策略的时候，对REST方式调用拦截的时候（支持Feign或者RestTemplate调用），希望把来自外部自定义的Header参数（用于业务系统子定义Header，例如：mobile）传递到服务里，那么配置如下值。如果多个用“;”分隔，不允许出现空格
spring.application.strategy.business.request.headers=user;mobile
```

## 全链路侦测

通过内置基于LoadBalanced RestTemplate方式的/inspector/inspect接口方法，实现全链路侦测，可以查看全链路中调用的各个服务的版本、区域、子环境、IP地址等是否符合预期，是否满足灰度条件，该接口可以集成到使用者的界面中，就可以规避通过Postman工具或者调用链系统去判断，有利于节省人工成本。使用方式：
```
1. 执行Post请求
2. 请求的路径：http://[网关URL]/[服务名1]/inspector/inspect
3. 请求的内容：{"serviceIdList":["服务名2", "服务名3", ....]}。服务名不分前后次序
```

## 全链路服务侧注解

服务侧对于RPC方式的调用拦截、消费端的服务隔离和调用链三项功能，默认映射到RestController类（含有@RestController注解），并配合如下的扫描路径才能工作
```vb
# 灰度路由策略的时候，需要指定对业务RestController类的扫描路径。此项配置作用于RPC方式的调用拦截、消费端的服务隔离和调用链三项功能
spring.application.strategy.scan.packages=com.nepxion.discovery.guide.service.feign
```
当使用者不希望只局限于RestController类（含有@RestController注解）方式，而要求在任何类中实现上述功能，那么框架提供@ServiceStrategy注解，使用者把它加在类头部即可，可以达到和@RestController注解同样的效果

## 全链路服务侧API权限

服务侧对于RPC方式的调用，可以加入API权限控制，通过在接口或者类名上加@Permission注解，或者在接口或者类的方法名上加@Permission注解，实现API权限控制。如果两者都加，以前者为优先
- 实现权限自动扫描入库
- 实现提供显式基于注解的权限验证，参数通过注解传递；实现提供基于Rest请求的权限验证，参数通过Header传递
- 实现提供入库方法和权限判断方法的扩展，这两者需要自行实现

请参考[权限代码](https://github.com/Nepxion/DiscoveryGuide/blob/master/discovery-guide-service/src/main/java/com/nepxion/discovery/guide/service/permission)

## 异步跨线程Agent

灰度路由Header和调用链Span在Hystrix线程池隔离模式下或者线程池异步调用Feign或者RestTemplate时，通过线程上下文切换会存在丢失Header的问题，通过下述步骤解决，同时适用于网关端和服务端

方案实现中…

## 元数据Metadata自动化策略

### 基于服务名前缀自动创建灰度组名

通过指定长度截断或者标志截断服务名的前缀来自动创建灰度组名，这样就可以避免使用者手工维护灰度组名。当两者都启用的时候，截断方式的组名优先级要高于手工配置的组名

- 增加配置项
```vb
# 开启和关闭使用服务名前缀来作为服务组名。缺失则默认为false
spring.application.group.generator.enabled=false
# 服务名前缀的截断长度，必须大于0
spring.application.group.generator.length=15
# 服务名前缀的截断标志。当截断长度配置了，则取截断长度方式，否则取截断标志方式
spring.application.group.generator.character=-
```

### 基于Git插件自动创建灰度版本号

通过集成插件git-commit-id-plugin，通过产生git信息文件的方式，获取git.commit.id（最后一次代码的提交ID）或者git.build.version（对应到Maven工程的版本）来自动创建灰度版本号，这样就可以避免使用者手工维护灰度版本号。当两者都启用的时候，Git插件方式的版本号优先级要高于手工配置的版本号

- 增加Git编译插件

需要在4个工程下的pom.xml里增加git-commit-id-plugin

默认配置
```xml
 
     pl.project13.maven 
     git-commit-id-plugin 
     
         
             
                 revision 
             
         
     
     
         
         true 
         
         yyyyMMdd 
         yyyy-MM-dd-HH:mm:ss  -->
     
 
```

特色配置
```xml
 
     pl.project13.maven 
     git-commit-id-plugin 
     
         
             
                 revision 
             
         
     
     
         
         true 
         
         ${project.basedir}/.git 
         
         ${project.build.outputDirectory}/git.json 
         ${project.basedir}/git.json  -->
         
         json 
         
         true 
         
         false 
         
         false 
         yyyyMMdd 
         yyyy-MM-dd-HH:mm:ss  -->
     
 
```

更多的配置方式，参考[https://github.com/git-commit-id/maven-git-commit-id-plugin/blob/master/maven/docs/using-the-plugin.md](https://github.com/git-commit-id/maven-git-commit-id-plugin/blob/master/maven/docs/using-the-plugin.md)

可能需要增加下面的配置，保证git相关文件被打包进去
```xml
 
     
         src/main/java 
         
             **/*.xml 
             **/*.json 
             **/*.properties 
         
     
     
         src/main/resources 
         
             **/*.xml 
             **/*.json 
             **/*.properties 
         
     
 
```

- 增加配置项
```vb
# 开启和关闭使用Git信息中的字段单个或者多个组合来作为服务版本号。缺失则默认为false
spring.application.git.generator.enabled=true
# 插件git-commit-id-plugin产生git信息文件的输出路径，支持properties和json两种格式，支持classpath:xxx和file:xxx两种路径，这些需要和插件里的配置保持一致。缺失则默认为classpath:git.properties
spring.application.git.generator.path=classpath:git.properties
# spring.application.git.generator.path=classpath:git.json
# 使用Git信息中的字段单个或者多个组合来作为服务版本号。缺失则默认为{git.commit.time}-{git.total.commit.count}
# spring.application.git.version.key={git.commit.id.abbrev}-{git.commit.time}
# spring.application.git.version.key={git.build.version}-{git.commit.time}
```

下面是可供选择的Git字段，比较实际意义的字段为git.commit.id，git.commit.id.abbrev，git.build.version，git.total.commit.count
```vb
git.branch=master
git.build.host=Nepxion
git.build.time=2019-10-21-10\:07\:41
git.build.user.email=1394997@qq.com
git.build.user.name=Nepxion
git.build.version=1.0.0
git.closest.tag.commit.count=
git.closest.tag.name=
git.commit.id=04d7e45b11b975db37bdcdbc5a97c02e9d80e5fa
git.commit.id.abbrev=04d7e45
git.commit.id.describe=04d7e45-dirty
git.commit.id.describe-short=04d7e45-dirty
git.commit.message.full=\u4FEE\u6539\u914D\u7F6E
git.commit.message.short=\u4FEE\u6539\u914D\u7F6E
git.commit.time=2019-10-21T09\:09\:25+0800
git.commit.user.email=1394997@qq.com
git.commit.user.name=Nepxion
git.dirty=true
git.local.branch.ahead=0
git.local.branch.behind=0
git.remote.origin.url=https\://github.com/Nepxion/DiscoveryGuide.git
git.tags=
git.total.commit.count=765
```

注意：一般情况下，上述两个地方的配置都同时保持默认即可。对于一些特色化的用法，两个地方的配置项用法必须保持一致，例如：
```vb
# 输出到工程根目录下
 ${project.basedir}/git.json 
# 输出成json格式
 json 
```
下面配置项必须上面两个配置项的操作逻辑相同
```vb
# 输出到工程根目录下的json格式文件
spring.application.git.generator.path=file:git.json
```

内置基于Swagger的Rest接口，可以供外部查询当前服务的Git信息

## 元数据Metadata运维平台策略

外部系统（例如：运维发布平台）在远程启动微服务的时候，可以通过参数传递来动态改变元数据或者增加运维特色的参数，最后注册到远程配置中心。有如下两种方式：
- 通过Program arguments来传递，它的用法是前面加“--”。支持Eureka、Zookeeper和Nacos的增量覆盖，Consul由于使用了全量覆盖的tag方式，不适用改变单个元数据的方式。例如：--spring.cloud.nacos.discovery.metadata.version=1.0
- 通过VM arguments来传递，它的用法是前面加“-D”。支持上述所有的注册组件，它的限制是变量前面必须要加“metadata.”，推荐使用该方式。例如：-Dmetadata.version=1.0
- 两种方式尽量避免同时用

## 内置配置文件

框架提供内置配置文件spring-application-default.properties。如果使用者希望对框架做封装，并提供相应的默认配置，可以在src/main/resources目录下放置spring-application-default.properties。注意：该文件在整个服务目录和包中只能出现一次

## Docker容器化和Kubernetes平台支持

### Docker容器化

- 搭建Windows10操作系统或者Linux操作系统下的Docker环境
    - Windows10环境下，具体步骤参考[Docker安装步骤](https://github.com/Nepxion/Thunder/blob/master/thunder-spring-boot-docker-example/README.md)
    - Linux环境请自行研究
- 需要在4个工程下的pom.xml里增加spring-boot-maven-plugin和docker-maven-plugin
```xml
 
     org.springframework.boot 
     spring-boot-maven-plugin 
     
         true 
         com.nepxion.discovery.guide.gateway.DiscoveryGuideGateway 
         JAR 
     
     
         
             
                 repackage 
             
             
                 false 
             
         
     
 
 
     com.spotify 
     docker-maven-plugin 
     
         ${ImageName} 
         openjdk:8-jre-alpine 
         ["java", "-jar", "/${project.build.finalName}.jar"] 
         
             ${ExposePort} 
         
         
             
                 / 
                 ${project.build.directory} 
                 ${project.build.finalName}.jar 
             
         
     
 
```
- 拷贝discovery-guide-docker目录下的所有脚本文件到根目录下
- 所有脚本文件下的MIDDLEWARE_HOST=10.0.75.1改成使用者本地物理IP地址（Docker是不能去连接容器外地址为localhost的中间件服务器）
- 全自动部署和运行Docker化的服务。在根目录下
    - 一键运行install-docker-gateway.bat或者.sh，把Spring Cloud Gateway网关全自动部署且运行起来
    - 一键运行install-docker-zuul.bat或者.sh，把Zuul网关全自动部署且运行起来
    - 一键运行install-docker-service-xx.bat或者.sh，把微服务全自动部署且运行起来。注意，必须依次运行，即等上一个部署完毕后才能执行下一个
    - 一键运行install-docker-console.bat或者.sh，把控制平台全自动部署且运行起来
    - 一键运行install-docker-admin.bat或者.sh，把监控平台全自动部署且运行起来	
- 上述步骤为演示步骤，和DevOps平台结合在一起，更为完美

![Alt text](https://github.com/HaojunRen/Docs/raw/master/discovery-doc/Docker.jpg)

### Kubernetes平台支持

请自行研究

## Star走势图

[![Stargazers over time](https://starchart.cc/Nepxion/Discovery.svg)](https://starchart.cc/Nepxion/Discovery)

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)