knife4j是为Java MVC框架集成Swagger生成Api文档的增强解决方案,前身是swagger-bootstrap-ui,取名kni4j是希望她能像一把匕首一样小巧,轻量,并且功能强悍!

knife4j的前身是`swagger-bootstrap-ui`，为了契合微服务的架构发展,由于原来`swagger-bootstrap-ui`采用的是后端Java代码+前端Ui混合打包的方式,在微服务架构下显的很臃肿,因此项目正式更名为`knife4j`

更名后主要专注的方面

- 前后端Java代码以及前端Ui模块进行分离,在微服务架构下使用更加灵活
- 提供专注于Swagger的增强解决方案,不同于只是改善增强前端Ui部分

**效果：**[http://swagger-bootstrap-ui.xiaominfo.com/doc.html](http://swagger-bootstrap-ui.xiaominfo.com/doc.html)

**示例:**[https://gitee.com/xiaoym/swagger-bootstrap-ui-demo](https://gitee.com/xiaoym/swagger-bootstrap-ui-demo)

**交流：**[![](https://img.shields.io/badge/加入QQ1群-608374991(满)-red.svg)](//shang.qq.com/wpa/qunwpa?idkey=16b81902c23fbca82780fa107da1b6612e2ee44a05c4103c9176ad9d61c2f6bf)  [![](https://img.shields.io/badge/加入QQ2群-621154782-red.svg)](//shang.qq.com/wpa/qunwpa?idkey=11e0a1453a6a3695bd8ed709fbc8359c9c48dd8538aaafbece7b84ecd325b91c)


**文档**:[https://doc.xiaominfo.com/](https://doc.xiaominfo.com/)

**源码分析**:[https://www.xiaominfo.com/2019/05/20/springfox-0/](https://www.xiaominfo.com/2019/05/20/springfox-0/)

## 项目模块

目前主要的模块包括：

| 模块名称             | 说明                                                         |
| -------------------- | ------------------------------------------------------------ |
| knife4j              | 为Java MVC框架集成Swagger的增强解决方案                      |
| knife4j-admin        | 云端Swagger接口文档注册管理中心,集成gateway网关对任意微服务文档进行组合集成 |
| knife4j-extension    | chrome浏览器的增强swagger接口文档ui,快速渲染swagger资源      |
| knife4j-service      | 为swagger服务的一系列接口服务程序                            |
| knife4j-front        | knife4j-spring-ui的纯前端静态版本,用于集成非Java语言使用     |
| swagger-bootstrap-ui | knife4j的前身,最后发布版本是1.9.6                            |



## 业务场景

### 不使用增强功能,纯粹换一个swagger的前端皮肤

不使用增强功能,纯粹换一个swagger的前端皮肤，这种情况是最简单的,你项目结构下无需变更

可以直接引用swagger-bootstrap-ui的最后一个版本1.9.6或者使用knife4j-spring-ui

老版本引用

```xml
 
     com.github.xiaoymin 
     swagger-bootstrap-ui 
     1.9.6 
 
```

新版本引用

```xml
 
     com.github.xiaoymin 
     knife4j-spring-ui 
     ${lastVersion} 
 
```

### Spring Boot项目单体架构使用增强功能

在Spring Boot单体架构下,knife4j提供了starter供开发者快速使用

```xml
 
     com.github.xiaoymin 
     knife4j-spring-boot-starter 
     ${knife4j.version} 
 
```

该包会引用所有的knife4j提供的资源，包括前端Ui的jar包

### Spring Cloud微服务架构

在Spring Cloud的微服务架构下,每个微服务其实并不需要引入前端的Ui资源,因此在每个微服务的Spring Boot项目下,引入knife4j提供的微服务starter

```xml
 
     com.github.xiaoymin 
     knife4j-micro-spring-boot-starter 
     ${knife4j.version} 
 
```

在网关聚合文档服务下,可以再把前端的ui资源引入

```xml
 
     com.github.xiaoymin 
     knife4j-spring-boot-starter 
     ${knife4j.version} 
 
```

## 另外说明

不管是knife4j还是swagger-bootstrap-ui

对外提供的地址依然是doc.html

访问：http://ip:port/doc.html

即可查看文档

**这是永远不会改变的**



## 提ISSUES必看

虽然建立了QQ交流群,但是很多没用加群的朋友会通过ISSUES来反馈问题,提ISSUES本身是一个很好的技术习惯，这有助于帮助我能很好的定位问题所在,但因为我并不是实时关注,所以经常在我处理issues的时候，看到很多朋友提的问题却也无从着手，写下一些建议,希望提ISSUES的朋友能在提的时候都有涉及到：

1、swagger-bootstrap-ui和springfox-swagger的版本号,这个尤为重要,很多低版本出现的问题有可能我在新发布的版本中已经解决了,每个版本都有更新日志,可以参考这篇文档：https://doc.xiaominfo.com/changelog/

2、提ISSUES时贴图、贴代码,代码不用贴逻辑，只需要贴接口层即可,还有相关的实体类(如果有涉及的话)，这些信息有助于我快速定位问题,省去了来回沟通的成本,提高大家的效率

3、在QQ交流群沟通的朋友我也希望能通过提ISSUE来记录下我们沟通的过程,我并非实时处理此问题，这让我集中再处理issues的时候有助于拉回我们彼此沟通时的场景，最终在新版本解决问题

4、swagger-bootstrap-ui使用的是传统的JS技术,jQuery+Dom操作,打包后的源码也并没有压缩处理,代码注释部分我也有说明,应该是能理解的，如果我没有及时处理碰到的问题,欢迎大家提交pr，毕竟众人拾柴火焰高嘛

## 项目Demo示例

Demo示例见另外项目地址：[https://gitee.com/xiaoym/swagger-bootstrap-ui-demo](https://gitee.com/xiaoym/swagger-bootstrap-ui-demo)

| 模块                            | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| knife4j-spring-boot-demo        | 在Spring Boot架构下集成knife4j的项目示例                     |
| knife4j-spring-boot-single-demo | 在Spring Boot单体架构下集成knife4j的项目示例                 |
| knife4j-spring-cloud-gateway    | 在Spring Cloud微服务架构下通过gateway网集成knife4j的示例     |
| swagger-bootstrap-ui-demo-mvc   | 在Spring MVC模式下集成swagger-bootstrap-ui                   |
| swagger-bootstrap-ui-demo       | 在Spring Boot单体架构下集成swagger-bootstrap-ui              |
| swagger-bootstrap-ui-gateway    | 在Spring Cloud微服务架构下通过gateway网关集成swagger-bootstrap-ui |
| swagger-bootstrap-ui-zuul       | 在Spring Cloud微服务架构下通过zuul网关集成swagger-bootstrap-ui |

## 界面效果

![接口说明](static/des.png)

![接口调试](static/debug.png)

![个性化设置](static/settings.png)

![接口离线文档](static/markdown.png)

![SwaggerModels](static/models.png)

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)