###更新：
V1.1 2015-08-02

加入BAE支持，修改cookie_secret设定。

V1.0:

2015-07-30 项目发布

###1.简介
WLBLOG是一个由Python+Tornado实现的静态博客生成系统。采用markdown撰写文章。开发初衷一是为了Tornado框架的学习，二是作者对WordPress的繁琐和臃肿十分不满。目前还很粗糙，持续改进中。

###2.技术架构

* 演示地址：[http://wangxun.me](http://wangxun.me "http://wangxun.me")
* 开发语言：Python
* 服务框架：Tornado
* 前端技術：Bootstrap、Jquery、Highlight,editor.md
* 文章编辑：markdown

###3.技术特性
* 动静分离：用户访问到的是纯静态的页面，只有写博客和编译静态文件时才需要后端支援。
* 可灵活部署：可以只部署静态内容（只需要支持静态页面的WEB环境即可），也可以前后端都部署（需要Python环境）。
* 文档编辑使用了叛道的[Editor.md](https://git.oschina.net/pandao/editor.md "Editor.md") 


###4.普通部署
环境要求：
> 系统最好是Linux（Tornado在Windows下基于select速度很low）
> 
> 需要Mysql数据库
> 
> 需要MySQLdb模块（[http://sourceforge.net/projects/mysql-python/files/?source=navbar](http://sourceforge.net/projects/mysql-python/files/?source=navbar "http://sourceforge.net/projects/mysql-python/files/?source=navbar")）

- 1.首先将数据（data.sql）导入mysql
- 2.修改db.py的MySQL数据库连接设定。
- 3.安装Python环境、MySQLdb模块后执行server.py
- 4.后台地址：/admin
- 5.默认用户名密码：用户名：admin  密码：admin

###5.BAE部署
BAE.py可以直接支持部署到BAE环境下，配置完数据库连接之后即可直接部署。

###6.后台截图：

![](http://wangxun.me/static/image/2015082721392420150827213734.png)
![](http://wangxun.me/static/image/2015082721394620150827213804.png)
![](http://wangxun.me/static/image/2015082721401120150827213826.png)


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)