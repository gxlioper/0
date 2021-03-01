# Axure_Js_Inject v3.0
可以在产品原型（RP）中加入你想要的js代码，这些js代码会用浏览器浏览产品原型的时候执行

---


## 软件要求

- Axure rp 9.0 
- Chrome 浏览器 73版 及以上的浏览器

## 可运行的地方

- [通过蓝湖axure插件上传到蓝湖平台](https://lanhuapp.com/)
- axure 自带的生成 html 文件

## 不可运行的地方

* axure cloud

------

## 用法（图文版）

[Axure_js_inject 的使用说明](https://lanhuapp.com/url/zGWVj)

## 用法（纯文字版）

#### 安装

1. 前往发布页下载 axure_js_inject.zip : [下载方式1(github)](https://github.com/cxwithyxy/Axure_Js_Inject/releases)  |  [下载方式2(gitee)](https://gitee.com/cxwithyxy/Axure_Js_Inject/releases)
2. 关闭运行中的 axure9
3. 解压到 axure9 的根目录 （可能是这个路径：D:\Axure\Axure RP 9\）
4. 启动 axure9
5. 在元件库中找到 Axure_Js_Inject_V3 ，则证明安装成功了

#### 使用{{}}占位符执行代码

- 在可以使用[[]]的地方，便可以使用{{}}

- 如“设置文本”成当前时间:

- 用[[]]方法时，输入的是[[Now]]

- 用{{}}方法时，输入的是{{new Date()}}

- 但是{{}}占位符可以实现更多的功能

- 如展示浏览器UA

- {{navigator.userAgent}}

#### 使用code_Box执行代码

- 从Axure_Js_Inject元件库中拖拽code_Box到你的页面上

- 把js代码粘贴到code_Box中

#### 使用case_Expose

case_Expose 用于把axure中的事件处理的case提取接口给外部js调用

- 从Axure_Js_Inject元件库中拖拽case_Expose到你的页面上

- case_Expose中设置文本为你想要的接口名称(如: 移动那个东西)

- 设置case_Expose的交互--鼠标单击时--case为: 移动另一个元件

- 在任意可以执行js代码的地方(如: code_Box)调用你想要的接口名称(如: 移动那个东西();)




 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)