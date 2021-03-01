# xvp demo


##项目介绍 
小V铺是完全开源的项目，通过提供商城源码、商城开放API、RUI前端开源组件库三大核心功能，方便二次开发，帮助开发者简单高效降低二次开发成本，满足专注业务深度开发的需求。

##环境依赖 
spring-boot-starter-parent v1.4.3.RELEASE  
spring-boot-starter-web v1.4.3.RELEASE  
spring-boot-starter-aop v1.4.3.RELEASE  
jfinal v3.0  
druid v1.0.15  
tutils2 v1.3.3 (`git clone https://github.com/CZ-chen/tutils2.git`)  
rop-sdk v1.0  

##License
 
BSD 2-Clause License

Copyright (c) 2017, lktech
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 

##融数开放平台 

###1.登录融数开放平台 http://open.rongcapital.cn/  
![](https://github.com/lktech/xvp_demo/raw/master/image/01.png) 

###2.点击右上角`未登录`，按照要求进行注册，`成为开发者`  
![](https://github.com/lktech/xvp_demo/raw/master/image/02.png) 
![](https://github.com/lktech/xvp_demo/raw/master/image/03.png) 
![](https://github.com/lktech/xvp_demo/raw/master/image/04.png) 

###3.注册后,加入QQ群451528860，联系平台人员，立马为您审批 

###4.登录后，点击右上角昵称，选择`应用管理`，进入应用列表页面  
![](https://github.com/lktech/xvp_demo/raw/master/image/05.png) 

###5.添加应用 
![](https://github.com/lktech/xvp_demo/raw/master/image/06.png) 
![](https://github.com/lktech/xvp_demo/raw/master/image/07.png) 

###6.点击账号信息，查看详情信息 
![](https://github.com/lktech/xvp_demo/raw/master/image/08.png) 

###7.审核通过后，申请小微铺核心API 
①点API信息；②选择未申请；③选择小微铺核心API；④选中需要申请的API；⑤申请API 
![](https://github.com/lktech/xvp_demo/raw/master/image/09.png) 

###8.申请API审批通过后，点击API信息，选择已申请，点击API，查看API详细信息(入参，返回结果示例，错误码等) 
![](https://github.com/lktech/xvp_demo/raw/master/image/10.png) 
![](https://github.com/lktech/xvp_demo/raw/master/image/11.png) 

###9.申请API审核通过后，点击左侧`文档与工具`-->`SDK下载`，下载SDK  
![](https://github.com/lktech/xvp_demo/raw/master/image/12.png) 

##RUI 
###关于RUI [线上访问地址](http://rui.lingketech.com/) 

RUI 是一套基于 Vue2.0 的完整的前端解决方案，不仅包含PC组件库和移动端组件库，还包含了完整的项目脚手架已及组件配套原型，可零配置直接启动脚手架。 

在项目根目录配置了Mockjax本地接口模拟依赖库，可在mockapi里配置模拟接口，实现前后端同步进行。 

RUI，不止于UI。

###安装 

通过`npm`安装本地服务第三方依赖模块(需要已安装[Node.js](https://nodejs.org/))

```
npm install
```
启动服务(http://localhost:8090)

```
node server.js
```
发布代码
```
npm run dist
```

##项目部署 

###1.下载xvp_demo项目源代码(`git clone`) 
```shell
git clone https://github.com/lktech/xvp_demo.git
```
###2.解压SDK，将RopExSdk.jar放在项目lib文件夹下 
![](https://github.com/lktech/xvp_demo/raw/master/image/13.png) 

###3.修改src/main/resources下的application.properties配置文件为开发者模式，配置如下 
spring.profiles.active=dev

###4.修改src/main/resources下的application-dev.properties配置文件 
![](https://github.com/lktech/xvp_demo/raw/master/image/08.png) 

```java
server.tomcat.access-log-enabled=true
server.port=端口号
server.session.cookie.max-age=7200
server.session.timeout=7200
#rop
com.lingke.xvp.rop.url=参考上图，替换为您的调用地址
com.lingke.xvp.rop.key=参考上图，替换为您的App Key
com.lingke.xvp.rop.secret=参考上图，替换为您的App Secret

#db
com.lingke.xvp.db.url=替换为您的数据库URL
com.lingke.xvp.db.user=替换为您的数据库user
com.lingke.xvp.db.password=替换为您的数据库password
com.lingke.xvp.db.name=替换为您的数据库name

#isv
#当开发者申请账号为沙箱时，com.xiaovpu.openapi.isv.url值应为http://sit-open.xiaovpu.com/isv/
#当开发申请账号为正式时，com.xiaovpu.openapi.isv.url值为http://open.xiaovpu.com/isv/

com.xiaovpu.openapi.isv.url=http://sit-open.xiaovpu.com/isv/
```

###5.在项目根目录下，执行打包 
```
mvn clean package
```
###6.在src/main/resources下创建一个static文件夹，将项目根目录下target/web下的mall和seller文件下复制到src/main/resources/static目录下 

![](https://github.com/lktech/xvp_demo/raw/master/image/15.png) 

###7.找到XvpApp.java文件，执行此类中的main方法 

###8.访问页面http://主机:端口/seller/index.html 


##创建数据库 

###1.安装MySQL 

官方下载地址http://dev.mysql.com/downloads/mysql/#downloads 

###2.创建数据库 

```
CREATE DATABASE 数据库名;  //创建数据库
```

###3.执行sql脚本 

在数据库执行sql文件下面的*.sql脚本， 

![](https://github.com/lktech/xvp_demo/raw/master/image/14.png) 

##目录结构
                               
├── src
│   └── main
│       └── java
│           └── com
│               └── lingke
│                   └── xvp
│                       └── demo
│                           ├── controller
│                           │   ├── request                         // request body
│                           │   ├── response                        // response body
│                           │   ├── seller                  
│                           │   │   ├── OrderController.java        // 订单相关业务处理
│                           │   │   ├── ProductController.java      // 商品相关业务处理
│                           │   │   ├── SellerController.java       // 卖家相关业务处理
│                           │   │   └── StoreController.java        // 店铺相关业务处理
│                           │   ├── user                    
│                           │   │   ├── OrderController.java        // 订单相关业务处理
│                           │   │   ├── ProductController.java      // 商品相关业务处理
│                           │   │   ├── StoreController.java        // 店铺相关业务处理
│                           │   │   └── UserController.java         // 普通用户相关业务处理
│                           │   └── CommonController.java           // 通用类相关业务处理
│                           ├── db                          
│                           │   ├── codegen                 
│                           │   │   └── ActiveRecordGen             // 使用jFinal动态生成代码
│                           │   └── dao
│                           ├── utils                               // 工具方法
│                           ├── XvpApp.java                         // 项目的mainClass，用于启动服务
│                           ├── XvpAspect.java                      // 事务控制
│                           ├── XvpConstants.java                   // 常量
│                           ├── XvpDbConfig.java                    // 获取数据库连接
│                           ├── XvpInterceptorConfig.java           // 配置需要拦截的请求
│                           └── XvpRopClient.java                   // rop客户端
├── src
│   └── main
│       └── resources
│           ├── application.properties						        // 配置文件
│           └── logback-online.xml							        // logback配置文件
├── lib          
│   └── RopExSdk.jar										        // SDK
├── sql                                                             // sql脚本
├── src                
│   └── main
├── web														        // 前端页面
│   ├── mall                                                        // 商城页面
│   │   ├── README.md           
│   │   ├── dist                                                    // 项目build目录
│   │   ├── index.html                                              // 项目入口文件
│   │   ├── package.json                                            // 项目配置文件
│   │   ├── src                                                     // 生产目录
│   │   │   ├── assets                                              // css js 和图片资源
│   │   │   ├── components                                          // 各种组件
│   │   │   ├── views                                               // 各种页面
│   │   │   ├── filters.js                                          // 各种过滤器
│   │   │   └── main.js                                             // Webpack 预编译入口
│   │   ├── server.js                                               // webpack-dev-server服务配置
│   │   └── webpack.constants.js                                    // Webpack 配置文件
│   └── seller                                                      // 卖家页面
│       ├── README.md           
│       ├── dist                                                    // 项目build目录
│       ├── index.html                                              // 项目入口文件
│       ├── package.json                                            // 项目配置文件
│       ├── src                                                     // 生产目录
│       │   ├── assets                                              // css js 和图片资源
│       │   ├── components                                          // 各种组件
│       │   ├── views                                               // 各种页面
│       │   ├── filters.js                                          // 各种过滤器
│       │   └── main.js                                             // Webpack 预编译入口
│       ├── server.js                                               // webpack-dev-server服务配置
│       └── webpack.constants.js                                    // Webpack 配置文件
├── LICENSE														    // 版权
├── pom.xml														    // pom文件
└── README.md
 


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)