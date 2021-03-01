家聊
====
轻量级IM开源项目，基于环信Sdk
------

**由于项目中集成了友盟统计，是为了方便搜集崩溃日志，还请fork该项目的朋友在进行二次开发的时候删除友盟或者更换渠道名，以免和我的项目混淆，谢谢配合** 
想直接体验项目运行效果的可[点击这里下载apk](http://ogqrscjjw.bkt.clouddn.com/FC_DebugV1.5.apk) 编译项目需要Android Studio2.2以上!
 
###更新日志： 
####V1.5: 
①更新环信库到最新版本V3.3.0【自环信3.2.3版本就不再支持armeabi，所以这个版本已移除相关库】 
②修复部分bug 
####V1.4: 
①添加检测更新的功能 
②更新环信库到最新版本3.2.3（吐槽下环信，老是变sdk方法名字） 
③修复bug，微调某些界面 
####V1.3: 
①更新环信库到最新版本3.2.2 
②添加实时通话记录 
③修复小bug 
####V1.2: 
①修复部分机型启动崩溃、无法发起实时通话的bug 
②集成小米推送和华为推送 
③统一签名文件 
####V1.1: 
①添加友盟统计，方便搜索崩溃信息 
②更新环信库到最新版本 
③修复部分bug 
####V1.0： 
正式发布

###初衷 
很久之前想教家里老人学习使用智能机，让他们能用App和家人交流沟通，但是发现市面上流行的社交软件对于他们来说学习成本太高，毕竟他们从来没使用过智能手机，这些社交软件中很多功能都是不需要的，所以就产生了自己做一个轻量级IM软件的想法。起初没想做成开源的，后来发现其实这也是一个锻炼总结的好机会，所以就有了这个开源项目：家聊 
 
###项目特点 
个人偏向使用原生技术，所以在开发过程中倾向于自己写实现过程，当然也有使用到一些第三方库和控件（在此感谢那些为开源做出贡献的先驱者们，站在前人的肩膀上，必须时刻保持感恩之心！）项目中基础架构类似MVP，但不是按照安卓官方标准来的，而是在自己的理解上精简了部分，且没有做整体的MVP封装，但是应该不会影响代码理解。 
核心通讯组件是使用的环信3.X版本，官网地址：http://www.easemob.com/ ，在此感谢环信！ 
 
###主要功能： 
1.聊天模块，包含文字聊天、语音聊天、发送图片、短视频、实时音频通话、实时视频通话。 
2.通讯录：可获取系统通讯录，和环信好友关系整合。 
3.拨号器：自定义的简单拨号盘，方便老人直接拨打电话 
 
###项目截图： 
![](https://github.com/Vanish136/FamilyChat/raw/master/screenshoot/FC01.png)
![](https://github.com/Vanish136/FamilyChat/raw/master/screenshoot/FC02.png)
![](https://github.com/Vanish136/FamilyChat/raw/master/screenshoot/FC03.png)
![](https://github.com/Vanish136/FamilyChat/raw/master/screenshoot/FC04.png)
![](https://github.com/Vanish136/FamilyChat/raw/master/screenshoot/FC05.png)
![](https://github.com/Vanish136/FamilyChat/raw/master/screenshoot/FC06.png)
 
###开源引用
1.EventBus:https://github.com/greenrobot/EventBus 
2.Ormlite:https://github.com/j256/ormlite-android 
3.Pinyin4j:https://github.com/belerweb/pinyin4j 
4.PermissionDispatcher:https://github.com/hotchemi/PermissionsDispatcher 
5.SelectableroundedImageview:https://github.com/pungrue26/SelectableRoundedImageView 
6.SectorProgressView:https://github.com/timqi/SectorProgressView 
7.Android-ScalableVideoView:https://github.com/yqritc/Android-ScalableVideoView 
8.FlatUI:https://github.com/eluleci/FlatUI 
9.Glide:https://github.com/bumptech/glide 
10.Android-Crop:https://github.com/jdamcd/android-crop 
11.PhotoView:https://github.com/chrisbanes/PhotoView 
项目中某些库也有引用到一些别人的代码片段（例如PtrView、QrCode库中部分代码是参考网上资料），但是由于无法找到具体出处，在此暂不贴出引用链接，如果有人能提供详细出处，还请联系我，谢谢！
 
####联系作者
如果发现项目bug或者对项目有好的建议，欢迎提交issue，或者通过下面的联系方式联系我. 
*QQ：505515031  746604151 
*邮箱：505515031@qq.com 
*微信：Vanish520136 
######注：联系我时请注明来意！！！

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)