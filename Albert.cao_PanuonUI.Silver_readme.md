   
   

# Panuon.UI.Silver
Panuon.UI optimized version. A beautiful wpf ui library using templates &amp; attached properties.  
Panuon.UI的优化版本。一个漂亮的、使用样式与附加属性的WPF UI控件库。

You can download Panuon.UI.Silver (pre-release) from nuget now. Check "include pre-release" option before query.  
Panuon.UI.Silver(预发行版)现已加入Nuget平台。在搜索"Panuon.UI.Silver"前，请在Nuget包管理器中勾选“包括预发行版”。  

Email : zeoun@qq.com  
QQ Group : 718778191  
Zhihu : @末城via

# News 动态  

## 2.0版本即将到来
更多样式，更好的表现，更少的BUG。  
2.0版本提供对Net Core 3.0的完全支持。几乎每种控件都增加了至少一种样式，或是进行了现有样式调整。  
全新的UIBrowser，帮助你快速设计控件，并生成样式或控件代码（尚在准备和优化中，可能会迟到）。  
2.0版本对现有控件库的代码进行了完全的重构，从根源上解决了一些BUG，并大幅减少了可能出现的Exception。从1.0版本升级到2.0版本需要修改约30%控件库相关代码，但这值得一试。  
请注意，2.0版本中不再集成FontAwesome，改为内置Panuon独家设计的IconFont字体库。目前已有200多个图标，你可以在UIBrowser中看到它们。Panuon IconFont会保持更新。  
提供完备的开发文档、代码示例与1.0升级指南（文档将转移到阿里的语雀平台）。https://www.yuque.com/mochengvia/silver2.0   
下载方式：你可以在上方的Branch中切换2.0.0分支并下载开发版代码，但控件尚不齐全。开发版Nuget已经发行。  

#### 2020-3-25 v1.0.9.9
[Re] 修复了Badge的Background和Foreground的绑定初始值未生效的BUG。  
将PasswordBoxHelper.Password属性更改为默认双向绑定。

#### 2020-3-11 v1.0.9.8
修复了Badge的Background和Foreground的绑定初始值未生效的BUG。  
修复了ContextMenu中的MenuItem无法识别AccessKey的BUG。  
修复了WindowX会在SizeToContent="WidthAndHeight"时出现白边的BUG。  
修复了DateTimePicker的SelectedDate赋值为new DateTime时会报错的问题。SelectedDate的年份最小值已被限定为5（与MinDate无关）。  

#### 2020-2-17 v1.0.9.6
修复了部分控件可能会在后台抛出错误的问题。
新增了MessageBoxX的Question图标。

# ReleaseNote 发布文档  

https://github.com/Panuon/Panuon.Documents/blob/master/Documents/PanuonUI.Silver/release-note.zh-cn.md

# Document 文档

Chinese document(English document is still being written, you can translate it by google or other translators):  
中文文档：  
https://github.com/Panuon/Panuon.Documents/blob/master/Documents/PanuonUI.Silver/zh-cn.md

# Case 案例  

### Morin 魔音

http://www.huanghunxiao.com/  
  
![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/case_morin_4.png)  

### Collector 

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/case_collector_1.png)  

# Examples 示例  

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/window_1.png)

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/window_2.png)

# Donate  捐赠
Panuon.UI.Silver is an open source library.Your support will motivate me to continue Panuon.UI.Silver development.    
Panuon.UI.Silver是一个完全开源的控件库。您的支持是项目得以发展的根本保证。

Zhifubao:  
支付宝：

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/zhifubao.jpg)

Paypal:  
paypal.me/Zeoun  


## Where is the exmaple ? （示例在哪？）
After downloading this repository, launch "Panuon.UI.Silver.Browser" project , and you will find it .  
当您下载该仓库后，只需启动"Panuon.UI.Silver.Browser"项目，即可看到示例。

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/step1.png)

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/temp.jpg)
### Work with helper （需要使用Helper的控件）:
Button / CheckBox / RadioButton / TextBox / PasswordBox / ComboBox / Expander / GroupBox / Expander

### Dependent custom controls （独立自定义控件）:
Calendar / Carousel / Loading / MultiSelector / ImageCuter / TagPanel / NeonLabel / Clock / DateTimePicker

### Styles only （仅样式）:
DataGrid / ScrollViewer (MiniScrollViewer)

# Button 

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/button.jpg)

# TextBox / PasswordBox

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/textbox.jpg)

# CheckBox

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/checkbox.jpg)

# RadioButton

![](https://panuonui-silver-1252047526.cos.ap-chengdu.myqcloud.com/radiobutton.jpg)


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)