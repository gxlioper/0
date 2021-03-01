# timePHP

## timePHP用途？
   timePHP是一个基于php cli开发的定时脚本框架,可以实现简单的配置,自己的逻辑代码纯php无需写shell脚本
易管理,易开发,支持自定义多进程,时间周期可以按（月日,星期几,天,小时,分钟,秒）来执行,等功能。
简单的配置一下就可以根据需求开发自己的逻辑代码【此框架暂只支持liunx系统】。

## timePHP操作命令

## 全部启动命令

``` python
[root@FX-DEBUG taskphp]# php ./start.php start

----------------------- timePHP -----------------------------
timePHP version:1.0          PHP version:5.6.9
------------------------ timePHP -------------------------------
pid           name          status
14524         backup          [OK] 
14525         clearmeesage    [OK] 
14526         clearrom        [OK] 
-----------------------------------------------------------

```

## 查看任务列表

``` python
[root@FX-DEBUG taskphp]# php ./start.php status

----------------------- timePHP -----------------------------
timePHP version:1.0          PHP version:5.6.9
------------------------ timePHP -------------------------------
pid           name          status
14524         backup          [OK] 
14525         clearmeesage    [OK] 
14526         clearrom        [OK] 
-----------------------------------------------------------

```
## 退出程序

``` python
[root@FX-DEBUG taskphp]# php ./start.php kill  

 [退出成功] 
 
``` 

## 目录结构

```
./start.php						入口启动文件
./app							任务主目录
./app/任务名						独立任务目录			
./app/任务名/config.php			该任务的配置文件	 
./app/任务名/function.php			该任务的函数
./app/任务名/任务名Task.class.php	任务入口文件
./app/任务名/Demo.php				自定义封装类可以不要	
./extend						第三方插件目录
./timephp						框架核心文件

```

## 配置文件规范

``` php
 
 * @copyright  TimePHP
 * @license    https://github.com/qq1985277517/timePHP
 *   */
return [
    "TASK"=>array(//任务相关配置【必填项】
        "name"=>"backup",//进程名
        "count"=>1,//进程数 默认为1，如果要开启多进程 请开启redis 使用队列
        "status"=>1,//1 启动 -1停止
        "processType"=>false,//默认false  （该选项只有系统进程才会用到）
        /**
         * 格式
         * m    1,3,5,12,25 12:20:00      每个月的几号几点执行
         * w    1,3,5 12:20:00      一周的1,3,5 12:20:00执行一次     0是星期天
         * d    12:20:00            每天12:20:00执行一次
         * h    2                   每2小时执行一次
         * i    2                   每2分钟执行一次
         * s    3                   每3秒执行一次
         *   */
        "timeType"=>"s",//时间类型  m号  w周  d天  h小时     i分钟 s秒
        "timePeriod"=>"5",//时间
    ),
    /**  数据库连接配置  */
    'DB_TYPE'   => "mysql", // 数据库类型
    'DB_HOST'   => "127.0.0.1", // 服务器地址
    'DB_NAME'   => "demo", // 数据库名
    'DB_USER'   => "root", // 用户名
    'DB_PWD'    => "root",  // 密码
    'DB_PORT'   => 3306, // 端口
    'DB_PREFIX' => "tourism_", // 数据库表前缀
    'DB_PARAMS'=>array('persist'=>true),//是否支持长连接  true是  false 否
];
?>

```

## 数据库操作

## 数据库操作和ThinkPHP一样

``` php
namespace app\backup;
use lib\Task;
use lib\common\SystemFun;
/**
 * @author     Bililovy 
 * @copyright  TimePHP
 * @license    https://github.com/qq1985277517/timePHP
 */
class backupTask extends Task{
    public function run(){
        //初始化数据库配置信息
        SystemFun::Config($this->getConfig());
        //实例化模型   和 thinkphp的M()方法一样，操作也是一样
        $model=SystemFun::model("gameActivity");
        //执行查询一条数据
        $res=$model->where(array("id"=>1))->find();
        var_dump($res);
    }
}

```

## 获取配置文件信息

``` php

$config=$this->getConfig();
var_dump($config);

```
## 引用第三方插件

``` php
如:
 
 * @copyright  TimePHP
 * @license    https://github.com/qq1985277517/timePHP
 */
class clearmeesageTask extends Task{
    public function run(){
        SystemFun::import("extend@PHPMailer@PHPMailerAutoload");
        $mail             = new \PHPMailer(); //PHPMailer对象
    }
}
?>

```










 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)