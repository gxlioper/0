 
     
 

 
     
         
     
     
         
     
     
         
     
 
     
     顺手点个 Star，支持我们更好发展并持续维护此项目，感谢！ 
 

## 简介

HoServer 是基于Node.js开发开箱即用的后台服务和管理平台脚手架，可视化对象定义，一行代码实现增删改查所有接口，内置用户、权限等基本功能。基于 HoServer 可在短时间内开发出高质量的 RESTful API 服务和管理平台，助您大幅缩短项目开发周期，降低开发成本。是您产品占领窗口快速推向市场、接项目提升客户满意度的利器。

:house_with_garden: 官方网站: [HoServer 官网](http://hos.helloreact.cn)

:globe_with_meridians: 演示地址: [演示站点](http://hosdemo.helloreact.cn)

:book: 使用文档: [开发文档](http://hos.helloreact.cn/docs) | [部署文档](http://hos.helloreact.cn/docs/#deploy)

:arrow_forward: 视频教程: [HoServer 视频教程](http://hos.helloreact.cn/docs/tutorials_video.html)

![04_api_list.png](http://assets.helloreact.cn/screens/webp/ori/04_api_list.png)

## 功能特性

**简单高效**

- 开箱即用，一行代码实现增删改查所有接口，支持批量更新删除，以及聚合查询。
- 基于Node.js Express 框架，不发明新轮子，学习成本低，快速上手。

**功能强大**

- 对象、接口全部可视化管理。
- 内置短信、支持阿里云存储。
- 内置基于Ant Design Pro管理平台，包括用户管理、系统管理、内容管理等常用功能。
- 支持数据批量导入导出。

**安全可靠**

- 所有接口默认基于 JWT 进行安全校验，防止非法请求。
- 所有接口可独立设置操作权限，确保核心数据安全。
- 所有接口都有完善的参数校验。

**灵活方便**

- 独有的 Hook 机制可方便扩展和改写默认接口功能。
- 所有接口都是无状态的，可方便进行集群扩展。
- 基于 MongoDb 数据库，部署维护成本相对较低。

**高性能**

- 支持接口缓存，并支持内存、Redis等不同缓存实现。
- 内置服务性能指标接口，方便集成监控系统。

**高质量**

- 所有代码默认采用 ESLint Standard JS + Prettier 代码检查。
- 典型的三层架构。
- 适当的架构约束确保低级别开发者也能实现高质量代码。

***
## HoServer Pro 特性 :gem: 

>  HoServer Pro 是 HoServer 的商业版本，在社区版基础上增加了Api文档自动生成、客户端SDK自动生成、系统监控、内置公众号模板、支付等更多高级功能。

**自动生成 Api 文档**

- 一键生成在线 Api 文档，自动生成参数列表以及输入输出示例代码。
- 支持导出 Markdown 格式，即将支持导出 Pdf / Word 等格式。

**自动生成 Postman 集合**

- 自动生成 Postman 测试集合文件，并预填充所有输入参数模拟数据。

- 支持 Postman 直接在线导入。

**自动生成客户端 Sdk**

- 自动生成客户端 Sdk代码，客户端不需要再写繁琐的 request 代码了，就像调用本地服务层代码一样透明调用服务端接口。支持 Javascript、React Native、Java 和 ObjectC等常用语言。

**更多三方平台集成**

- 支持微信、QQ、微博三方登录。
- 内置公众号模板包含自定义菜单、自动微信账号授权及获取当前微信用户开放信息等。
- 内置微信、支付宝支付服务端集成，以及支付订单流水查询管理。

**自动生成增删改查管理页面**

- 一行代码实现增、删、改、查、批量导入导出数据页面，自动生成表单，并可通过代码对默认页面功能进行定制。

**服务监控告警系统**

- 基于 Prometheus + Grafana 搭建，可查看服务响应时间、并发数、调用次数等服务关键指标，以及系统负载、内存、硬盘、网络等多项指标。

- 可配置短信邮件等多种告警方式。

## 支持

QQ 交流群: 720338887

![输入图片说明](http://assets.helloreact.cn/images/qq_qr.png "qq_qr.png")

微信交流群: 

![输入图片说明](http://assets.helloreact.cn/images/wx_qr.png "wx_qr.png")


## 开源版使用须知

> 允许用于商业项目中，必须保留版权信息，请自觉遵守。

> 禁止将本项目的代码和资源进行任何形式的出售，产生的一切任何后果责任由侵权者自负。

## 快速开始

> git clone https://gitee.com/hello-react/HoServer.git

> cd ./HoServer

**后台服务**

> cd src/server

> yarn install 或 npm install

> yarn start 或 npm run start 启动服务

**管理平台**

另开一个终端窗口进入 `src/manager`, 
如未安装umi 请先 `yarn global add umi` 或 `npm install -g umi`

> yarn install 或 npm install

> yarn start 或 npm start 启动管理平台

> 打开浏览器访问: http://localhost:8000

> 默认用户名密码: admin / 123456

注: 

演示站点连接的是 HoServer 演示数据库，此数据库只读，所有更新操作将被取消。可自行在本地搭建 MongoDB 数据库环境，参考部署文档在本地部署数据库。

[更多文档请参考官方文档](http://hos.helloreact.cn/docs)。


## 系统功能截图

![01_dict.png](http://assets.helloreact.cn/screens/webp/ori/01_dict.png)

![02_model.png](http://assets.helloreact.cn/screens/webp/ori/02_model.png)

![03_model_properties.png](http://assets.helloreact.cn/screens/webp/ori/03_model_properties.png)

![05_sys_announce.png](http://assets.helloreact.cn/screens/webp/ori/05_sys_announce.png)

![06_log.png](http://assets.helloreact.cn/screens/webp/ori/06_log.png)

![07_config.png](http://assets.helloreact.cn/screens/webp/ori/07_config.png)

![08_users.png](http://assets.helloreact.cn/screens/webp/ori/08_users.png)

![09_permission.png](http://assets.helloreact.cn/screens/webp/ori/09_permission.png)

![10_role.png](http://assets.helloreact.cn/screens/webp/ori/10_role.png)

![20_api_doc.png](http://assets.helloreact.cn/screens/webp/ori/20_api_doc.png)

![21_postman.png](http://assets.helloreact.cn/screens/webp/ori/21_postman.png)

![22_sdk.png](http://assets.helloreact.cn/screens/webp/ori/22_sdk.png)

![23_content.png](http://assets.helloreact.cn/screens/webp/ori/23_content.png)

![24_payment.png](http://assets.helloreact.cn/screens/webp/ori/24_payment.png)

![25_monitor1.png](http://assets.helloreact.cn/screens/webp/ori/25_monitor1.png)

![26_monitor2.png](http://assets.helloreact.cn/screens/webp/ori/26_monitor2.png)



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)