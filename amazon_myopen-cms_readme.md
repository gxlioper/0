# 项目介绍
项目逐步完善中。
# 快速开始
构建项目以后，从SQL文件夹下倒入初始化SQL。配置文件在config.txt里。找到AppConfig类，右键Debug即可运行。
访问地址 http://IP:8000/admin  账号：admin/123456,端口在 AppConfig可以修改

# 目录介绍
2 本项目，前台使用了layui,官网http://www.layui.com，后台使用了jfinal3.3,官网http://www.jfinal.com
3 本项目，主要封装了一下功能，权限，字典，定时任务
4
	权限，自己定义了权限拦截器，便于改造，主要思路是把后台配置过的url都进行认证，如果后台没有配置过改权限，那么就不会认证。同时封装了权限标签，详细使用见/admin/user/index.html 里面的 auth ，建议配置按钮的权限，设置成最终提交的url，而不是跳转的URL
5 字典，
	字典使用方式见 /admin/user/index.html 状态查询参数，通过页面设置map对象传入参数，然后生成select
6 	定时任务，
	可以直接添加定时任务，定时任务可以立即执行一次，等等
7 使用了 jfinal自带的模板，而非jsp，模板使用方式参见jfinal文档
8 目前项目html结构
	/admin，后台管理的页面，/admin/common 里面是后台模板的几个通用的部分,不想使用通用的布局，参考/admin/login.html或者使用部分布局，参考/admin/my_password.html
	/common 整个项目的通用模板m 目前包含了字典的模板
	/plugins 包含了各种js插件等
	/upload  默认上传的文件会保存在这里
	
##部署注意事项
1 nginx的时候，反向代理配置
location / {
	proxy_pass http://127.0.0.1:8282 ; 
	proxy_connect_timeout 60s;
	proxy_read_timeout 5400s;
	proxy_send_timeout 5400s;
	client_max_body_size    1000m; 
				
	proxy_set_header Host $http_host;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header X-Forwarded-Proto $scheme;
}
	
2 需要在config里面配置 主域名的信息


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)