### 索引
- [jvue-admin是什么？](#jvue-admin是什么)
- [前端技术栈](#前端技术栈)
- [后端技术栈](#后端技术栈)
- [授权设计](#授权设计)
- [测试地址](#测试地址)

### jvue-admin是什么
通过整合前端流行框架vue和相关组件，及后台的Spring boot，实现的权限管理及菜单动态生成最佳实践。

### 前端技术栈
vue, vuet, element-ui, axios

### 后端技术栈
spring boot, hazelcast, mybatis, postgresql, swagger2
PS: 如果需要hibernate(jpa)和mysql版本的话，请参考分支[jvue-admin-jpa](https://github.com/ccfish86/jvue-admin/tree/jvue-admin-jpa)。此外：两个分支对应的数据库字段有些不一样。

### 授权设计
传统的Struts，SpringMVC或类似的MVC架构下，页面和接口的权限是并行的，有的是以类型区分，有的是混着来的。
本项目中，以画面为单位，把接口和画面项目(按钮/组件)等绑定到画面，在给角色授权时，直观的可授予对应的接口和按钮的权限。
页面权限和后台接口权限分开加载，前台权限不持续再占用后台JVM内存，后台Spring Security启动时通过URL去DB加载并绑定角色，用户登录后直接通过ROLE和Spring Security匹配访问权限。
后续，可以结合工具，通过excel把画面定义好生成对应的vue和JAVA代码，或者后台JAVA实现类似功能，提高开发效率和统一的命名。

### 测试地址
线上测试地址：[http://jvue.ccfish.net/](http://jvue.ccfish.net/)
管理员：admin/admin
普通用户：user/user

PS: 正在努力开发中，预计春节以后会有一版Release

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)