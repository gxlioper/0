# vue-form-making
基于Vue,ElementUI快速创建表单，进行数据校验，获取表单数据

演示地址：http://tools.xiaoyaoji.cn/form-marking

## CDN
``` html
 
 
 
  
```

## Hello world
``` html
 
 
 
   
   
   
   
 
 
   
      
   
 
   
    
   
    
    
   
    new Vue({
      el: '#app'
    })
   
 
```

## Install
```shell
npm install form-making -S
```

## Quick Start
``` javascript
import Vue from 'vue'
import Element from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import FormMaking from 'form-making'
import 'form-making/dist/FormMaking.css'
Vue.use(ElementUI, { size: 'small' })
Vue.use(FormMaking)

// or
import {
  MakingForm
} from 'form-making'
import 'form-making/dist/FormMaking.css'

Vue.component(MakingForm.name, MakingForm)
```

## Template
``` html
  
```

## 功能介绍

工具提供两个组件 MakingForm(表单配置)，GenerateForm(表单渲染)

首先看看 MakingForm 的功能介绍

![](https://user-gold-cdn.xitu.io/2018/9/14/165d7578d36b0654?w=2878&h=1108&f=png&s=233664)

![](https://user-gold-cdn.xitu.io/2018/9/14/165d75fc8f26c49c?w=2266&h=1402&f=png&s=255307)

预览可以实时预览你编辑表单的表单渲染的效果，并可以查看获取到填写的数据结构

![](https://user-gold-cdn.xitu.io/2018/9/14/165d762ed2d9ec62?w=1966&h=836&f=png&s=137285)

生成JSON操作为渲染组件生成JSON数据
![](https://user-gold-cdn.xitu.io/2018/9/14/165d76fd6941702a?w=1552&h=982&f=png&s=142989)


接下来就是 GenerateForm 如何使用，这里默认你已经将该组件正确引入项目

``` html
 
 
```
``` javascript
new Vue({
    ...
    data () {
        return {
            jsonData: {}, // 表单配置中生成的json数据
            values: {}, // 表单需要显示的表单数据
            remoteFuncs: {
                // 组件配置时配置的远端方法,保持和配置时输入的名称一致
                func_test (resolve) {
                  // 模拟接口请求
                  setTimeout(() => {
                    const options = [
                      {id: '1', name: '1111'},
                      {id: '2', name: '2222'},
                      {id: '3', name: '3333'}
                    ]
                    
                    // 获取到的值和标签可以通过配置页远端配置
                    // 值:id  标签：name
        
                    resolve(options) // 将后端获取的数据放入回调函数中
                  }, 2000)
                }，
                func_test2....
            }
        }
    },
    methods: {
        ...{
            // 调用此方法验证表单数据和获取表单数据
            this.$refs.generateForm.getData().then(data => {
                // 数据校验成功
                // data 为获取的表单数据
            }).catch(e => {
                // 数据校验失败
            })
        }
    }
})
```

自此一个表单就制作完毕

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)