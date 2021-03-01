#EleAdmin

使用饿了么前端搭建的可配置化后台，[手册在这里](http://www.kancloud.cn/jixzfw/ele_admin)。

2017/1/10
  优化了实现流程
  提供了表格按钮操作列的动态效果，可以没有操作列 @chris.liu 
  实现了表格初选功能 : 在表格数据中返回selected :[3,4]，则row中id为3,4的行默认选中。


2017/1/8
  **提取出自定义按钮元素，按钮定义更高级、更灵活。**对原有的按钮进行了优化，对一些定义建重新命名: IsSelector、canDisable、disableKey、switch、switchKey，简单易用。
  增加了变化按钮功能，根据行数据，显示不同的按钮，比如 【开启】和【关闭】的切换。
  

2107/1/6
  **树状表格**

2016/12/26
  修正了表格查询、翻页、排序功能。在翻页、远程排序时，依旧保持查询效果；新查询从0页开始，并保持排序效果。

2016/12/25
   **增加了password一致性和远程唯一性数据校验功能。**(下面有说明，一看就了然) 拓展了element原有的数据校验功能，使数据校验的定义更加直观，简单。

2016/12/24 
  表格组件新增本地排序、服务器排序、搜索表单配置项
  优化了监视器组件

  
##先看看效果
![树状表格](http://git.oschina.net/uploads/images/2017/0106/134305_b9dff11b_45533.jpeg "树表格")
![表格效果](http://git.oschina.net/uploads/images/2016/1224/083631_6b448b48_45533.jpeg "表格示例")
![表单效果](http://git.oschina.net/uploads/images/2016/1221/150557_9ba5805b_45533.jpeg "表单示例")

## 使用方法
本后台高度配置化，后台显示的内容都是通过Ajax获取json数据动态生成的。当前包括菜单、表格页面、表单页面
###菜单结构
```javascript
 //页面首次加载时会从后台读取菜单数据，后台地址在index.html中定义
 // 入口地址
 window.bench     = "/hello.txt";
```
数据结构如下
```javascript
return {
  "title":"JPHP-ELEMENT管理后台", //后台标题
  "menus": [ // 菜单列表
        {
            "index" : "1", //菜单索引
            "title" : "文章中心",//菜单标题
            "submenus" : [ //子菜单，可以没有
                {
                    "index" : "1", 
                    "title" : "栏目AA",
                    "url":"/table.txt" //菜单路由地址，参见Vue-router
                },{
                    "index" : "2",  "title" : "栏目BB","url":"/form.txt"
                },{
                    "index" : "3",  "title" : "栏目CC","url":"/table.txt"
                }
            ]
        } //，{}...
    ],
    "current": 1 //默认选中的菜单
}
```
### 表格结构
点击菜单后，系统会根据路由信息读取数据，从而决定如何渲染页面
```javascript

return {
  "mate" : {//渲染定义
    "columns" : [//列定义
      {
        "label":"姓名", 
        "name" :"name",
        "width":"120"
      }//,{}...
    ],
    "rows"  : [//数据定义
      {
        "id":1,
        "date": "2016-05-03",
        "name": "王小虎",
        "address": "上海市普陀区金沙江路 1518 弄"
      }//, {}
    ],
    "btns" :[//表格顶部按钮定义
        {
            "action"   :"add",
            "url"      : "/form.txt",
            "label"    : "增加元素",
            "type"     : "success",
            "isApi"    : false,    //重新读取数据还是重新渲染
            "useId"    : -1,  // -1 不用， 0 当前行，1 选中行
            "isSelector" : false  //复选框0选中时是否禁用
        }//,{}
    ],
    "actions" :[//行按钮
        {
            "action":"edit",
            "url"   : "/form.txt",
            "label" : "修改",
            "type"  : "success",
            "isApi" : false,
            "useId" : 0 
        }//,{}
    ],
    "search" : {
        "inline" : true //,其他参考form配置
       
    },
    "page"  : 1, //当前页
    "total" : 40  // 数据总条数
  },
  "title": "表格中心",
  "currentView" : "Tabler" //渲染格式
}
```
###表单结构
```javascript

return {
  "mate" : {
    "values": {//默认值
        "name": ""//,...
    
    },
    "fields" : [//域定义
            {
                "holder"      :"select",//参见Element组件
                "name"        :"name",
                "label"       :"活动区域",
                "placeholder" :"请选择活动区域",
                "options"     :[ //如果有的话
                    {
                        "label"   :"区域一",
                        "value"   :"shanghai"
                    },{
                        "label"   :"区域二",
                        "value"   :"beijing"
                    }
                ]
            }//,{}
        ],
        "rules": {//验证规则
          "name": [
            { "required": true, "message": "请输入活动名称", "trigger": "blur" },
            { "min": 3, "max": 5, "message": "长度在 3 到 5 个字符", "trigger": "blur" }
          ]//, ...
        }
  },
  "title" : "表单中心",
  "currentView" : "Formor" //渲染格式
}

```

###数据校验
```javascript
return {
    //...
    "rules": {
        "pass": [
          { "required": true, "message": "请输入密码", "trigger": "blur" }
        ],
        "checkPass": [
          { "validator": "validatePassword", "trigger": "blur","name":"pass","message":"请检查密码"}
        ],
        "onlyOne":[
          { "validator": "validateAsync", "trigger": "blur","url":"/data/only.php" }
        ]
      }
     //,...
}
```

##使用方法

git clone git@git.oschina.net:bfgdqch/EleAdmin.git

cd EleAdmin

npm install

npm run dev

浏览器中看效果 http://localhost:8080

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)