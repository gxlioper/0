# kitty-cloud
Spring Cloud 架构搭建的开源社区技术网站


## 后端技术栈

**[Kitty](https://github.com/yinjihuan/kitty)**：Spring Cloud & Spring Cloud Alibaba 基础框架，内置了 Cat 监控，互联网公司落地 Spring Cloud 架构必备。

**[Spring Cloud](https://spring.io/projects/spring-cloud)**：Spring 微服务全家桶。

**[Spring Cloud Alibaba](https://github.com/alibaba/spring-cloud-alibaba)**：致力于提供微服务开发的一站式解决方案。

**[Sentinel](https://github.com/alibaba/Sentinel)**：把流量作为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性。

**[Nacos](https://github.com/alibaba/Nacos)**：一个更易于构建云原生应用的动态服务发现、配置管理和服务管理平台。

**[Dubbo](https://github.com/apache/dubbo)**：Apache Dubbo™ 是一款高性能 Java RPC 框架。

**[Cat](https://github.com/dianping/cat)**：基于 Java 开发的实时应用监控平台，为美团点评提供了全面的实时监控告警服务。

**[MyBatis-Plus](https://mp.baomidou.com)**：MyBatis的增强版。

**[Spring Data MongoDB](https://spring.io/projects/spring-data-mongodb)**：Spring 中对MongoDB操作的客户端框架。

**[JetCache](https://github.com/alibaba/jetcache)**：基于Java的缓存系统封装，提供统一的API和注解来简化缓存的使用。

**[ElasticSearch](https://github.com/elastic/elasticsearch)**：ElasticSearch 是一个开源，分布式，RESTful搜索引擎。

## 核心功能

* 微服务架构（Spring Cloud & Spring Cloud Alibaba）
* 支持RPC/HTTP双协议（Dubbo和Feign远程调用）
* 分布式链路跟踪（Sleuth + ELK）
* 熔断限流（基于Sentinel的熔断限流）
* Cat监控（Mybatis, Feign, Dubbo, MongoDB, ElasticSearch等都有埋点监控）
* 全局幂等（基于redisson的分布式锁 + 注解 + 多级存储的幂等组件）
* 分布式ID分发（基于Leaf改造，扩展了RPC获取ID服务）
* 分布式任务调度（基于XXL-JOB的任务调度）
* MongoDB，ElasticSearch的使用（业务服务中使用）

## 项目文档

* 文档地址：[http://cxytiandi.com](http://cxytiandi.com/blog/detail/36440)

## 项目模块

* kitty-cloud-common：公共模块，通用的工具类
* kitty-cloud-user：用户服务
* kitty-cloud-article：文章服务
* kitty-cloud-comment：评论服务
* kitty-cloud-gateway：Web网关
* kitty-cloud-search：搜索服务
* kitty-cloud-job：定时任务
* 开发中。。。。。。

## 项目演示

请大家不要随便改变配置内容，想要实验的自己本地安装就可以了，多谢合作。

* Nacos控制台：[http://47.105.66.210:8848/nacos](http://47.105.66.210:8848/nacos) nacos/nacos
* Cat控制台：[http://47.105.66.210:8080/cat](http://47.105.66.210:8080/cat)
* Sentinel控制台：[http://47.105.66.210:8300](http://47.105.66.210:8300) sentinel/sentinel
* XXL-JOB控制台：[http://47.105.66.210:8010/xxl-job-admin/](http://47.105.66.210:8010/xxl-job-admin/) admin/123456

# 公众号

公众号 ***猿天地*** 会持续更新Kitty Cloud 和 微服务相关技术文章，请关注。技术交流群请加我微信jihuan900

![](doc/images/2685774-17a60e1ead7fd232.png)



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)