  
   
    
    
 
**Albedo 2.0 pro - 企业信息化快速开发平台**   
- 基于 Spring Boot 、Spring Security、Mybatis 的RBAC权限管理系统  
- 基于数据驱动视图的理念封装 Element-ui，即使没有 vue 的使用经验也能快速上手  
- 提供 lambda 、stream api 、webflux 的生产实践   
- 微服务alibaba版本  albedo-cloud-alibaba   
- 微服务版本  albedo-cloud   
- 历史版本移步  1.3.1-SNAPSHOT    

   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_16-46-21.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-02-41.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-02-58.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-03-08.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-03-33.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-03-48.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-04-13.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-04-44.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-06-21.png)   
![](https://raw.githubusercontent.com/somowhere/albedo-source/master/albedo/Snipaste_2019-08-08_17-06-37.png)   

#### 核心依赖 


依赖 | 版本
---|---
Spring Boot |  2.1.9.RELEASE  
Mybatis Plus | 3.2.0
hutool | 4.6.8
Avue | 2.1.0
   


#### 模块说明
```lua
albedo
├── albedo-ui -- 前端工程[8080]
└── albedo-common -- 系统公共模块 
     ├── albedo-common-api --  服务基础api
     ├── albedo-common-core -- 公共工具类核心包
     ├── albedo-common-module -- 模块基础包
└── albedo-modules -- 功能模块
     ├── albedo-admin -- 通用用户权限管理系统业务处理模块[4000]
└── albedo-plugin  -- 插件模块 
     ├── albedo-data-mybatis -- mybatis 基础模块
     └── albedo-swagger-api -- swagger api
	 
```
#### 提交反馈

1. 欢迎提交 issue，请写清楚遇到问题的原因，开发环境，复显步骤。

2. 不接受`功能请求`的 issue，功能请求可能会被直接关闭。  

3.  somewhere0813@gmail.com     

4. QQ群: 685728393 

#### 开源协议


![](https://images.gitee.com/uploads/images/2019/0330/065147_e07bc645_410595.png)


#### 关注我们



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)