#Mybatis分页插件 - PageHelper   

如果你也在用Mybatis，建议尝试该分页插件，这一定是 最方便 使用的分页插件。  

该插件目前支持以下数据库的 物理分页 :

 1. `Oracle`
 2. `Mysql`
 3. `MariaDB`
 4. `SQLite`
 5. `Hsqldb`
 6. `PostgreSQL`
 7. `DB2`
 8. `SqlServer(2005+)`

##最新版本为3.6.0

###Maven坐标

```xml  
 
     com.github.pagehelper 
     pagehelper 
     3.6.0 
 
```  

###下载JAR包

分页插件pagehelper.jar： 

 - https://oss.sonatype.org/content/repositories/releases/com/github/pagehelper/pagehelper/
 
 - http://repo1.maven.org/maven2/com/github/pagehelper/pagehelper/

由于使用了sql解析工具，你还需要下载jsqlparser.jar（这个文件完全独立，不依赖其他）：  

 - http://repo1.maven.org/maven2/com/github/jsqlparser/jsqlparser/0.9.1/
 
 - http://git.oschina.net/free/Mybatis_PageHelper/attach_files
 
##3.6.0更新日志：

 - 支持db2数据库
 
 - 支持sqlserver(2005+)数据库
 
 - sqlserver注意事项： 
   - 请先保证你的SQL可以执行
   - sql中最好直接包含order by，可以自动从sql提取
   - 如果没有order by，可以通过入参提供，但是需要自己保证正确
   - 如果sql有order by，可以通过orderby参数覆盖sql中的order by
   - order by的列名不能使用别名(`UNION,INTERSECT,MINUS,EXCEPT`等复杂sql不受限制，具体可以自己尝试)
   - 表和列使用别名的时候不要使用单引号(')

 - 简单修改结构
 
 - `startPage`方法返回值从`void`改为`Page`，获取`Page`后可以修改参数值
 
 - `Page`增加一个针对sqlserver的属性`orderBy`，用法看上面的 注意事项 
 
 - `Page`增加了一个链式赋值的方法，可以像下面这样使用：
   `PageHelper.startPage(1,10).count(false).reasonable(true).pageSizeZero(false)`
   
 - `PageHelper`增加了`startPage(int pageNum, int pageSize,String orderBy)`方法，针对sqlserver

##项目文档[wiki](http://git.oschina.net/free/Mybatis_PageHelper/wikis/home)：  

###&gt;[如何使用分页插件](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/HowToUse.markdown)  

###&gt;[更新日志](http://git.oschina.net/free/Mybatis_PageHelper/blob/master/wikis/Changelog.markdown) 

###&gt;[提交(gitosc)BUG](http://git.oschina.net/free/Mybatis_PageHelper/issues/new?issue%5Bassignee_id%5D=&issue%5Bmilestone_id%5D=)

##相关链接

对应于oschub的项目地址：http://git.oschina.net/free/Mybatis_PageHelper

对应于github的项目地址：https://github.com/pagehelper/Mybatis-PageHelper

Mybatis-Sample（分页插件测试项目）：[http://git.oschina.net/free/Mybatis-Sample](http://git.oschina.net/free/Mybatis-Sample)

Mybatis项目：https://github.com/mybatis/mybatis-3

Mybatis文档：http://mybatis.github.io/mybatis-3/zh/index.html  

Mybatis专栏： 

- [Mybatis示例](http://blog.csdn.net/column/details/mybatis-sample.html)

- [Mybatis问题集](http://blog.csdn.net/column/details/mybatisqa.html)  

作者博客：  

- http://my.oschina.net/flags/blog

- http://blog.csdn.net/isea533   

作者QQ： 120807756  

作者邮箱： abel533@gmail.com  

Mybatis工具群： 211286137 (Mybatis相关工具插件等等)

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)