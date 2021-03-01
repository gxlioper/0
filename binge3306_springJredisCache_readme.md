#基于jedis+spring的简易封装 redis缓存。

#1.配置redis客户端操作以及spring，启动redis;
#2.测试用例详见Test测试结果如下;
![eeee](http://git.oschina.net/uploads/images/2014/0214/162636_89b3b797_1052.png)

#序列化方案 ：
1.jdk原生序列化方案;     
2.基于kryo序列化方案 ;    
3.基于 FST序列化方案 ;    
4.基于 protobuffer序列化方案 ;    
5.基于redis的订阅/发布方案； 
6.基于messagePack序列化方案；

#序列化测试性能对比 10w次序列化 反序列化：
![QQ截图20140625141711](http://git.oschina.net/uploads/images/2014/0625/141810_8c03a33c_1052.png)
#fst kryo都是不错的选择！
#其中kyro默认采用了UsafeInput 和UsafeOutPut流 ，直接操作内存，提供更快的序列化方案
#测试protobuffer相当的优秀  只是该序列化方案要在特定的环境中 且只适合pb内置的消息格式，
#不适合大众化的javabean序列化 有局限性；
#kyro是纯java中应该最快的，同fst相比 在10W次的序列化 反序列中测试相差30ms,
#现有项目中使用Kyro序列化方案。
#ps:该组件已经在某手机游戏服务器中得到了验证与应用 请放心使用！

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)