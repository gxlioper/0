# WebServiceDataProvider
[![NuGet](https://img.shields.io/badge/NuGet-Scottxu.WebServiceDataProvider-yellow.svg)](https://www.nuget.org/packages/Scottxu.WebServiceDataProvider/)
[![Packagist](https://img.shields.io/packagist/l/doctrine/orm.svg)](https://mit-license.org/)

WebServiceDataProvider是一个用于动态调用WebService的C#类库，使用此类库，不仅可以仅通过两三条语句来调用WebService提供的方法，还可以使用动态编译的代码来调用这些方法。你无需在编译前添加好WebService的引用，只用添加这个类库，你就可以在需要时轻松使用WebService提供的服务。

## 依赖
* Newtonsoft.json >= 11.0.2

## 快速开始
在你的项目中搜索并添加名为“Scottxu.WebServiceDataProvider”的NuGet程序包，即可使用。

## 如何使用
只需简单的几行代码，就可以调用任何WebService。

>### 使用方法名调用
```C#
using Scottxu.WebServiceDataProvider;
var connection = new Connection("http://xxxx/xxxx.asmx");
var command = connection.GetMethodCommand("WebService方法名", "WebService名称");
string returnString = connection.Query();
```

>### 使用动态编译的C#代码调用
```C#
using Scottxu.WebServiceDataProvider;
var connection = new Connection("http://xxxx/xxxx.asmx");
var command = connection.GetCSharpCommand(
  "var webService = new WebService名称();" +
  "return webService.WebService方法名();" +
  );
string returnString = connection.Query();
```
## 联系作者
如果有任何问题请写Issus。 
Email：xyc0714@aliyun.com


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)