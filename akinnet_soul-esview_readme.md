 
   中文 
 
  Esview 



 
     
    
 
  

# Introduction
Esview is a vue page code generator based on iview-ui.  

You can get .vue file code by dnd components on esview.

Also you can customize your own draggable components.

![QQ图片20171027113639.png](http://chuantu.biz/t6/121/1509463255x2890191685.gif)

# Online Demo

http://47.94.2.0:9090

#  Doc 

1 generate code:

You can assemble page by dragging components on the left side and drop them into the middle section.

Click 'code' on the action bar to see generated code and click copy to get code.

2 customize own draggable components:

You should know how to register components on vue,so this is the first step,

second step is to go to page 'Develop->ManageControl',copy code of 'Div',

and modify exports.* according to your own components,click save and you will see it on assemble page.


# Install
frontend: Esview uses vue and iview，so the code generated must rely on vue and iview.

backend: Java（springboot）,so you must install jdk firstly.

database:mysql,the sql file is on directory 'server',named 'soul-esview.sql'.

# Theory
How to implement dnd：I use html api，the code is in dnd.js .

How to generate code：The data structure behind assembled page is a syntax tree,

I use recursive downward parsing to get the final .vue code.  

# License
[MIT](https://opensource.org/licenses/MIT)

Copyright (c) 2017-present,  SunZhengJie(Furioussoulk)


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)