## 项目说明
# king-admin
king-admin是一个超酷的前后端分离的基础权限管理后台，前端：angularJs+bootstrap+gulp，后端：spring-boot+mybatis-plus(分java版和kotlin版)

## [项目演示](http://112.74.40.9)
账号：kt
密码：kt

## 项目部署

执行 king-admin.sql

前端：
```
cd king-admin-angularjs

npm install -g gulp cnpm bower

cnpm install

bower install

gulp serve
```
http://localhost:5000

后端：

```
cd king-admin-java  或者 cd king-admin-kotlin

mvn install -Dmaven.test.skip=true
```
运行 KingAdminJavaApplication.java 或者 KingAdminKotlinApplication.kt

http://localhost:8080

## 注：
java用了lombok注解简化代码，请下载lombok插件
如果不前后端分离部署，可以cd king-admin-angularjs 运行 gulp 命令打包生成static 
然后替换到java或kotlin的resource里

## 未完成
angular4版本
king-admin-angular ：Angular + Bootstrap4 + Webpack 

vue版本
king-admin-vue : vue2 + es6 + webpack

## 效果展示

![image](http://112.74.40.9//screenshots/login.png)
![image](http://112.74.40.9//screenshots/home.png)
![image](http://112.74.40.9//screenshots/userlist.png)
![image](http://112.74.40.9//screenshots/user.png)
![image](http://112.74.40.9//screenshots/role.png)
![image](http://112.74.40.9//screenshots/menu.png)
![image](http://112.74.40.9//screenshots/phone1.png)
![image](http://112.74.40.9//screenshots/phone2.png)


## 鸣谢

[Blur Admin](http://akveo.github.io/blur-admin/)

[mybatis-plus](https://git.oschina.net/baomidou/mybatis-plus)

## License
[MIT](LICENSE.txt) license.




 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)