# mnet

## 后端

#### 安装memcached
```
> sudo apt-get install memcached
```

#### 安装Mysql mysqlclient必备的依赖
```
> sudo apt-get install libmysqlclient-dev
```

#### 安装package
```
> pip install -r requirements.txt
```

#### pre-commit 安装
```
> pre-commit install
> pre-commit autoupdate
```

#### 运行服务器
```
> ./run.sh server
> ./run.sh migration_all
> ./run.sh migrate_all

# 单独app操作
> ./run.sh migration netflow
> ./run.sh migrate netflow
```

## 前端
安装SASS
```
1. install ruby:
    https://github.com/oneclick/rubyinstaller2/releases/download/2.4.1-2/rubyinstaller-2.4.1-2-x64.exe

2. open terminal and install sass:
    gem install sass
    sass -v
```

安装项目
```
1. clone 项目:
    git clone https://github.com/zhexiao/mnet.git

2. run sass:
    cd web
    sass --watch sass:css --no-cache --style compressed
```

编程工具和运行
```
1. 安装pycharm专业版
2. 右键web/app/index.html -> open in browser
```

挂载到nginx
```
> sudo apt-get install nginx
> sudo vim /etc/nginx/sites-enabled/default
------
# if the static file encode has problem, set it
sendfile off;
root /vagrant/mnet/web;
------

> sudo service nginx restart
```


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)