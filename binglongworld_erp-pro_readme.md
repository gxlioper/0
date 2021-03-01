# erp_pro

> 基于SpringBoot 2.X框架，为中小企业打造开源好用的多租户ERP软件，专注进销存+财务功能，`目前正在新增生产模块`。主要模块有零售管理、采购管理、销售管理、仓库管理、财务管理、报表查询、系统管理等。支持预付款、收入支出、仓库调拨、组装拆卸、订单等特色功能。拥有库存状况、出入库统计等报表。对权限进行精确划分，同时支持多系统集成方案，可与OA，CRM，知识库等多个系统进行集成使用。`项目长期更新，觉得不错的点下star吧`

#### 介绍
基于SpringBoot框架和SaaS模式，立志为中小企业提供开源好用的多租户ERP软件，目前专注进销存+财务功能。主要模块有零售管理、采购管理、销售管理、仓库管理、财务管理、报表查询、系统管理等。支持预付款、收入支出、仓库调拨、组装拆卸、订单等特色功能。拥有库存状况、出入库统计等报表。同时对角色和权限进行了细致全面控制，精确到每个按钮和菜单。

> 价格介绍：开源版只包含基础功能，架构不支持高并发，容易出现问题，如想使用，签订使用协议即可。商业版包含所有功能，一直在更新，价格也在随时变化，目前价格是六万五千元【2020/02/27更新】(需要发票另外算)，负责半年的现有功能维护，提供开发文档、技术支持、疑难问题的解决方案，可根据需要进行功能整合（整合后费用跟着变化），一次性付费，全部源码。商业版包含的功能:https://gitee.com/doc_wei01/skyeye 。单独的ERP授权价格是8000

- 代码是没问题的，请下载`发行版`，环境版本请参照下面云盘提供的版本进行对应的修改
- [面试专题](https://gitee.com/doc_wei01/skyeye/blob/master/Java%E5%AD%A6%E4%B9%A0%E7%9B%AE%E5%BD%95.md)
- 小白勿入，不会度娘的勿入
- 项目交流群：(群一(满)：[696070023](http://shang.qq.com/wpa/qunwpa?idkey=e9aace2bf3e05f37ed5f0377c3827c6683d970ac0bcc61b601f70dc861053229))(群二：[836039567](https://shang.qq.com/wpa/qunwpa?idkey=7bb6f29b27f772aadca9c7c4e384f7833c64e9c3c947b5e946c7b303d1fe174a))(群三：[887391486](https://shang.qq.com/wpa/qunwpa?idkey=a65f2e0292eb1048bb13abb7adca302bd83e3465974861ec1f04c2f7fffc4d99))；有问题请提Issues，优先回答Issues问题
- 请不要重复加群，一个群就可以了，把机会留给更多人
- 百度云盘群（3676101838）提供环境安装文档和软件。请用手机版云盘自行搜索进群。
-  **进群先看公告！！！进群先看公告！！！进群先看公告！！！**  重要的事情说三遍
- 开发环境对应的文档以及安装包地址：链接：https://pan.baidu.com/s/1msVBhDcf_I_VN63YCcS-kA 提取码：w8sr；不要告诉我你没有云盘
- 经常有一些二货不知道发行版怎么下，不会下还说不能运行，这里把发行版链接给出来：[发行版](https://gitee.com/doc_wei01/erp-pro/releases)
- 如有定制需求，可入群或将需求发送至邮箱`598748873@qq.com`。
- [OA地址](https://gitee.com/doc_wei01/skyeye)
- [掘金文档地址](https://juejin.im/post/5db28c1e51882560613501cf)

> 体验地址服务器因为一些原因没再续费关了，需要体验的，请联系作者远程查看

#### 启动方式
直接运行com.SkyeyeErpApplication即可，启动完成后，访问`http://localhost:8086`即可。 初始化账号密码：root/123456

#### 功能介绍

- 用户管理：用户是系统操作者，该功能主要完成系统用户配置
- 部门管理：配置系统组织机构（公司、部门、小组），树结构展现支持数据权限
- 岗位管理：配置系统用户所属担任职务
- 菜单管理：配置系统菜单，操作权限，按钮权限标识等
- 角色管理：角色菜单权限分配、设置角色按机构进行数据范围权限划分
- 操作日志：系统正常操作日志记录和查询；系统异常信息日志记录和查询
- 聊天：用户可以像QQ一样与系统内容人员进行聊天
- 基础设置：包含背景图片设置、锁屏图片设置等
- 仓库管理：管理用户所拥有的仓库
- 计量单位：产品规格单位管理
- 产品信息：管理用户所拥有的产品信息
- 结算账户：自定义账户的结算方式以及结算明细的查看
- 收支(科目)项目：自定义除了采购/销售等产生的费用外，其他产生费用的项目
- 基本资料：包含客户管理、会员管理、供应商管理
- 采购管理：包含采购单、转入库单、采购入库、采购退货等功能
- 销售管理：包含销售单、转出库单、销售出库、销售退货等功能
- 仓库管理：包含其他入库、其他出库、调拨、组装单、拆分单等功能
- 零售管理：包含零售出库、零售退货等功能
- 报表管理：包含入库/出库明细、入库/出库汇总、库存状况、客户/供应商/会员对账等报表
- 财务管理：收入单、支出单、收付款单、转账单等
- 代码生成器：用户可自行提供模板，一键生成主要代码
- 租户群管理：系统可建立多个租户群体，各自管理各自的数据
- 配件管理：管理系统中的配件，用于产品维修等


#### 技术选型

##### 后端技术:

技术|名称|版本
---|---|---
[SpringBoot](http://spring.io/projects/spring-boot)|核心框架|2.0.3
[MyBatis](http://www.mybatis.org/mybatis-3/zh/index.html)|ORM框架
[Druid](https://github.com/alibaba/druid)|数据库连接池|
[Maven](http://maven.apache.org/)|项目构建管理|
[redis](https://redis.io/)|key-value存储系统|3.2集群（不要问我单机的能不能行）
[webSocket](http://www.runoob.com/html/html5-websocket.html)|浏览器与服务器全双工(full-duplex)通信|
[quartz 2.2.2](http://www.quartz-scheduler.org/)|定时任务|
[ActiveMQ](http://activemq.apache.org/replicated-leveldb-store.html)|消息队列|
[Java]()|Java|1.8
[MySQL]()|数据库|5.5.28

##### 前端技术：

技术|名称
---|---
[jQuery](http://jquery.com/)|函式库
[zTree](http://www.treejs.cn/v3/)|树插件
[layui](https://www.layui.com/)|模块化前端UI
[winui](https://gitee.com/doc_wei01/skyeye)|win10风格UI(自己做的前端架构)
[handlebars](http://www.ghostchina.com/introducing-the-handlebars-js-templating-engine/)|js模板引擎
[webSocket](http://www.runoob.com/html/html5-websocket.html)|浏览器与服务器全双工(full-duplex)通信

#### 代码描述
##### 前后台接口映射

```
 
	 
 
```

##### 后台代码编写规范

###### 控制层

```
@RequestMapping("后台接口")
public void 方法名(InputObject inputObject, OutputObject outputObject) throws Exception{
	服务层接口对象.方法名(inputObject, outputObject);
}
```

###### 服务层

```
@Override
public void 方法名(InputObject inputObject, OutputObject outputObject) throws Exception {
	Map  map = inputObject.getParams();//接收参数
	Map  user = inputObject.getLogParams();//获取当前登录用户信息
	/**
	 * 业务逻辑
	 */
	outputObject.setBean(bean);//返回单个实体Bean
	outputObject.setBeans(beans);//返回集合
	outputObject.settotal(total);//返回数量
	outputObject.setreturnMessage("信息");//返回前端的错误信息
	outputObject.setreturnMessage("信息", 错误码);//返回前端的错误信息，同时抛出异常（不常用）
}
```

#### 效果图

|效果图|效果图|
| ------------- | ------------- |
|![](https://images.gitee.com/uploads/images/2019/1011/084458_e0c2e256_1541735.png "")|![](https://s2.ax1x.com/2019/10/11/uHSaY8.png "")|
|![](https://images.gitee.com/uploads/images/2019/1011/084630_9326c93d_1541735.png "")|![](https://s2.ax1x.com/2019/10/11/uHpkh8.png "")|
|![](https://images.gitee.com/uploads/images/2019/1011/084706_8c921d85_1541735.png "")|![](https://s2.ax1x.com/2019/10/11/uHpeXj.png "")|
|![](https://images.gitee.com/uploads/images/2019/1015/091741_4030a2f0_1541735.png "")|![](https://s2.ax1x.com/2019/10/15/K9meR1.png "")|
|![输入图片说明](https://images.gitee.com/uploads/images/2019/1022/165203_457e90a8_1541735.png "在这里输入图片标题")|![输入图片说明](https://images.gitee.com/uploads/images/2019/1022/165318_c88d74e3_1541735.png "在这里输入图片标题")|
|![输入图片说明](https://images.gitee.com/uploads/images/2019/1022/165355_a7090ee3_1541735.png "在这里输入图片标题")|![输入图片说明](https://images.gitee.com/uploads/images/2019/1022/165505_0f5c5162_1541735.png "在这里输入图片标题")|
|![输入图片说明](https://images.gitee.com/uploads/images/2019/1022/165537_fbb78be8_1541735.png "在这里输入图片标题")|![输入图片说明](https://images.gitee.com/uploads/images/2019/1023/152325_95480f53_1541735.png "在这里输入图片标题")|


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)