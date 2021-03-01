#flyray-data
飞雷数据平台

### 平台架构

![平台架构](flyray-data-doc/UI/architecture.jpg)

 
  
 **工程名**    **描述**    **端口** 
 
 
 flyray-data-eureka-server    服务发现与注册中心    7070 
 
 
 flyray-dataconfig-server    配置管理中心    7072 
 
 
 flyray-data-gateway    动态路由器    7073 
 
 
 flyray-data-service-A    A服务，用来测试服务间调用与路由    7074 
 
 
 flyray-data-service-B    B服务，整合Mybatis、PageHelper、Redis，整合接口限速方案，可选google Guava RateLimiter与自实现    7075 
 
 
 flyray-data-service-B2    B2服务，与B服务serviceId相同，用来测试负载均衡和容错    7076 
 
 
 flyray-data-hystrix-ribbon    负载均衡器的容错测试    7077 
 
 
 flyray-data-hystrix-feign    feign的容错测试    7079 
 
 
 flyray-data-hystrix-dashboard    hystrix可视化监控台    7080 
 
 
 flyray-data-turbine    集群下hystrix可视化监控台    7081 
 
 
 flyray-data-sleuth    服务链路追踪    7082 
 
 
 flyray-data-service-admin    spring boot admin监控台    7088 
 
  


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)