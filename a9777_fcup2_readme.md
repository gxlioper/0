### 项目介绍

一个轻巧的js类库,用于在网页端上传大文件,大图片,可以设置多个上传参数,提供了多种回调.
可以任意绑定id,自动生成上传表单,可以自定义文件头,其它参数,设置最大上传,最小上传,以及判断上传类型.

官网地址：http://www.fcup.top

下载地址：https://gitee.com/lovefc/fcup2

![](https://www.showdoc.cc/server/api/common/visitfile/sign/20f40338081c1ea3b3a132955340c2f0?showdoc=.jpg)
### 安装教程
直接下载源码或者使用git克隆

### 使用方法

```javascript
  // 上传案例
  let up = new fcup({

    id: "upid", // 绑定id

    url: "./php/file.php", // url地址

    type: "jpg,png,jpeg,gif", // 限制上传类型，为空不限制

    shardsize: "0.01", // 每次分片大小，单位为M，默认1M

    minsize: '', // 最小文件上传M数，单位为M，默认为无

    maxsize: "50", // 上传文件最大M数，单位为M，默认200M
	
	// headers: {"version": "fcup-v2.0"}, // 附加的文件头
	  
	// apped_data: {}, //每次上传的附加数据
	
    // 定义错误信息
    errormsg: {
      1000: "未找到该上传id",
      1001: "类型不允许上传",
      1002: "上传文件过小",
      1003: "上传文件过大",
      1004: "请求超时"
    },

    // 开始事件                
    start: () => {
      console.log('开始上传');
    },

    // 等待上传事件，可以用来loading
    beforeSend: () => {
      console.log('等待请求中');
    },

    // 上传进度事件
    progress: (num, other) => {
      console.log(num);
      console.log('上传进度' + num);
      console.log("上传类型" + other.type);

      // 以下仅作参考,并不是太准确		 
      console.log("已经上传" + other.current);
      console.log("剩余上传" + other.surplus);
      console.log("已用时间" + other.usetime);
      console.log("预计时间" + other.totaltime);
    },

    // 错误提示
    error: (msg) => {
      alert(msg);
    },

    // 上传成功回调，回调会根据切片循环，要终止上传循环，必须要return false，成功的情况下要始终要返回true;
    success: (res) => {

      let data = res ? eval('(' + res + ')') : '';

      let url = data.url + "?" + Math.random();

      if (data.status == 2) {
        alert('上传完成');
      }

      if (data.status == 3) {
        alert('已经上传过了');
        return false;
      }

      // 如果接口没有错误，必须要返回true，才不会终止上传循环
      return true;
    }
  });
```

### 前端参数详细

| 参数 |类型| 空 | 默认 | 备注 |
|----    |-------    |--- |---|------      | 
|id | string | 否 | 无 |     dom的id        | 
|url |string | 否 | 无  |   上传到服务器的url  |
|type |string | 是  |  空 |  限制上传类型，多个用,号分割(不区分大小写),为空不限制  |
|shardsize    | int,float | 否   | 2   |     每次分片的大小,单位为M,因为要计算md5,所以如果条件允许,不要设定的太小     |
|minsize    | int,float | 是   | 空   |  上传文件的最小M数   |
|maxsize    | int,float | 是   | 空   |  上传文件的最大M数   |
|headers |object   |是   | 空  |  每次上传附带的文件头  |
|apped_data |object   |是   | 空  |  每次上传附带的其它参数,传递到后台  |
|timeout |int   |否   | 3000 |  ajax超时时间  |
|errormsg |object   |否   | object |  错误提示 | 
|start |function   |是   | fucntion |  实例化类后的开始事件  |
|beforeSend |function   |是   | fucntion |  等待上传事件  |
|progress |function   |是   | fucntion |  上传进度事件  |
|error |function   |是   | fucntion |  内部的错误提示函数  |
|success |function   |是   | fucntion |  数据成功传递到后端的事件,这是一个循环事件 |


### 后端参数详情

|参数名|注释|
|----    |------  |
|file_data |分段的文件|
|file_name |文件名称|
|file_total |文件的总片数|
|file_index |当前片数|
|file_md5 |文件的md5|
|file_size |文件的总大小|
|file_chunksize |当前切片的文件大小|
|file_suffix |文件的后缀名|
- 备注：以post的方式传递到后端

### 更新日志

2018/1/8 : 添加了对于接口返回结果的回调，添加了对于上传表单id的指定

2018/1/10 : 添加了node.js的上传接口，基于express框架

2018/1/17 : 优化了分片异步处理,队列执行接口,修复细节

2018/5/02 : 添加了文件大小的判断,添加了对于文件md5的计算,添加了终止函数,传值到后台使用,优化细节部分

2019/5/21 : 分离了原来的进度动画，现在用户可以自定义自己的动画和按钮，分别提供了各种回调事件以便处理

2019/8/12 : 修复了获取md5值的bug，感谢Matty的提醒

2019/10/22: 修改了终止事件循环执行的bug

2020/01/05: 重新封装类库,优化性能,改掉了以前的bug 

2020/01/30: 优化了时间计算,添加了可自定义header头的功能

2020/02/01: 多实例化,可以在同一个页面添加多个上传功能


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)