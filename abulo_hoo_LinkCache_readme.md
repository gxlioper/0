# LinkCache - 一个灵活高效的PHP缓存工具库

LinkCache 是一个PHP编写的灵活高效的缓存工具库，提供多种缓存驱动支持，包括Memcache、Memcached、Redis、SSDB、文件缓存、APC、YAC等。通过LinkCache可以使不同缓存驱动实现操作统一，同时又可发挥不同缓存驱动各自的优势。LinkCache支持缓存 `object` 和 `array`，同时为防止产生惊群现象做了优化。

# 环境要求

- PHP >= 5.4
- 使用 Memcache 缓存需要安装[Memcache扩展](http://pecl.php.net/package/memcache)
- 使用 Memcached 缓存需要安装[Memcached扩展](http://pecl.php.net/package/memcached)
- 使用 Redis 缓存需要安装[Redis扩展](http://pecl.php.net/package/redis)
- 使用 APC 缓存需要安装[APC扩展](http://pecl.php.net/package/APC)
- 使用 YAC 缓存需要安装[YAC扩展](http://pecl.php.net/package/yac)

# 安装

## composer 安装
LinkCache 可以通过 `composer` 安装，使用以下命令从 `composer` 下载安装 LinkCache

``` bash
$ composer require dongnan/linkcache
```

## 手动下载安装
### 下载地址
- 在 `Git@OSC` 下载 http://git.oschina.net/dongnan/LinkCache/tags
- 在 `GitHub` 下载 https://github.com/dongnan/LinkCache/releases

### 安装方法
在你的入口文件中引入
```
  'files',
        //当前缓存驱动失效时，使用的备份驱动
        'fallback' => 'files',
        'memcache' => [
            'servers' => [
                ['host' => '127.0.0.1', 'port' => 11211, 'weight' => 1, 'persistent' => true, 'timeout' => 1, 'retry_interval' => 15, 'status' => true],
            ],
            'compress' => ['threshold' => 2000, 'min_saving' => 0.2],
        ],
        'memcached' => [
            'servers' => [
                ['host' => '127.0.0.1', 'port' => 11211, 'weight' => 1],
            ],
            //参考 Memcached::setOptions
            'options' => [],
        ],
        'redis' => [
            'host' => '127.0.0.1',
            'port' => 6379,
            'password' => '',
            'database' => '',
            'timeout' => ''
        ],
        'ssdb' => [
            'host' => '127.0.0.1',
            'port' => 8888,
            'password' => '',
            'timeoutms' => ''
        ],
	]
```

## instance

实例化缓存对象

```
  '127.0.0.1', 'port' => 6379]);
```

## getDriver

获取缓存驱动实例

所有缓存驱动都必须实现 `linkcache\interfaces\driver\Base` 接口的方法，获取到缓存驱动实例后，可直接使用缓存驱动的方法，包括缓存驱动中没有定义但缓存驱动扩展对象中已定义的方法。

## set

将参数中的 `value` 设置为 `key` 的值

#### 参数
- key - 字符串
- value	- 除了 resource 类型的所有的值
- time - (可选参数) key的生存时间，单位是秒(s)

#### 返回值
Boolean 如果设置成功，返回 `true`; 如果设置失败，返回 `false`

#### 例子

```
 set($key, $value);
	//设置有过期时间的缓存
	$status = $cache->set($key, $value, $time);
```

## setnx

当缓存中不存在 `key` 时，将参数中的 `value` 设置为 `key` 的值

#### 参数
- key - 字符串
- value	- 除了 resource 类型的所有的值
- time - (可选参数) key的生存时间，单位是秒(s)

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败，返回 `false`

#### 例子

```
 setnx($key, $value);
	//设置有过期时间的缓存
	$status = $cache->setnx($key, $value, $time);
```

## get

获取 `key` 对应的值

#### 参数
- key - 字符串

#### 返回值
Mixed - `key` 对应的值; 如果获取失败或 `key` 不存在，返回 `false`

#### 例子

```
 get($key);
```

## del

删除 `key`

#### 参数
- key - 字符串

#### 返回值
Boolean - 如果删除成功，返回 `true`; 如果删除失败，返回 `false`。**注意：** 当 `key` 不存在时，也会返回 `true`

#### 例子

```
 del($key);
```

## has

判断 `key` 是否存在

#### 参数
- key - 字符串

#### 返回值
Boolean - 如果 `key` 存在，返回 `true`；如果 `key` 不存在，返回 `false`

#### 例子

```
 has($key);
```

## ttl

获取 `key` 的生存时间(单位:s)

#### 参数
- key - 字符串

#### 返回值
Mixed - 生存剩余时间(单位:秒) `-1` 表示永不过期,`-2` 表示 `key` 不存在,失败返回 `false`

#### 例子

```
 ttl($key);
```

## expire

设置一个 `key` 的生存时间(单位:s)

#### 参数
- key - 字符串
- time - 整数，key的生存时间(单位:s)

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败或 `key` 不存在，返回 `false`

#### 例子

```
 expire($key, $time);
```

## expireAt

用UNIX时间戳设置一个 `key` 的过期时间

#### 参数
- key - 字符串
- time - UNIX时间戳(单位:s)

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败或 `key` 不存在，返回 `false`

#### 例子

```
 expireAt($key, $time);
```

## persist

删除一个 `key` 的生存时间，使其永不过期

#### 参数
- key - 字符串

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败或 `key` 不存在，返回 `false`

#### 例子

```
 persist($key);
```

## lock

对 `key` 设置锁标记（此锁并不对 `key` 做修改限制,仅为 `key` 的锁标记）

#### 参数
- key - 字符串
- time - 整数，`key锁标记` 的生存时间(单位:s)

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败，返回 `false`

#### 例子

```
 lock($key, $time);
```

## isLock

对 `key` 解除锁标记

#### 参数
- key - 字符串

#### 返回值
Boolean - 如果解除锁标记成功，返回 `true`; 如果设置失败，返回 `false`

#### 例子

```
 isLock($key);
```

## incr

设置 `key` 的值按整数递增

#### 参数
- key - 字符串
- step - (可选参数) 整数，递增步长，默认值为 `1`，可以为负值

#### 返回值
Mixed - 递增后的值，失败返回 `false`，如果 `key` 不存在，则按 `step` 设置新值

#### 例子

```
 incr($key, $step);
```

## incrByFloat

设置 `key` 的值按浮点数递增

#### 参数
- key - 字符串
- float - 浮点数，递增步长，可以为负值

#### 返回值
Mixed - 递增后的值，失败返回 `false`，如果 `key` 不存在，则按 `float` 设置新值

#### 例子

```
 incrByFloat($key, $float);
```

## decr

设置 `key` 的值按整数递减

#### 参数
- key - 字符串
- step - (可选参数) 整数，递减步长，默认值为 `1`，可以为负值

#### 返回值
Mixed - 递减后的值，失败返回 `false`，如果 `key` 不存在，则按 `-step` 设置新值

#### 例子

```
 decr($key, $step);
```

## mSet

批量设置多个 `key` 对应的值

#### 参数
- sets - `key` 和 `value` 组成的键值对数组

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败，返回 `false`

#### 例子

```
  'value1',
		'key2' => 'value2',
		'key3' => 'value3',
	];
	//批量设置多个key对应的值
	$status = $cache->mSet($sets);
```

## mSetNX

当缓存中不存在 `key` 时，批量设置多个 `key` 对应的值

#### 参数
- sets - `key` 和 `value` 组成的键值对数组

#### 返回值
Boolean - 如果设置成功，返回 `true`; 如果设置失败，返回 `false`

#### 例子

```
  'value1',
		'key2' => 'value2',
		'key3' => 'value3',
	];
	//当缓存中不存在key时，批量设置多个key对应的值
	$status = $cache->mSetNX($sets);
```

## mGet

获取所有给定key的值

#### 参数
- keys - 多个 `key` 组成的数组 

#### 返回值
array - 参数 `keys` 中的所有 `key` 与对应的 `value` 组成的数组，如果 `key` 不存在或是获取失败，对应的 `value` 值为 `false`

#### 例子

```
 mGet($keys);
```

# 开发

如果你觉得LinkCache还不错，但又不支持你想用的缓存驱动，不妨尝试在LinkCache新增该缓存驱动的支持。

## 1.增加新的缓存驱动

目前有两种方式可以方便的开发新的缓存驱动支持

- 继承 `linkcache\abstracts\DriverSimple` 抽象类
	1. 在 `src/linkcache/drivers` 目录下创建新的缓存驱动类 `Example.php`
		```
		 
			 * @copyright   (c) Dong Nan http://idongnan.cn All rights reserved.
			 * @link        http://git.oschina.net/dongnan/LinkCache
			 * @license     BSD (http://opensource.org/licenses/BSD-3-Clause)
			 */

			namespace linkcache\drivers;
			use linkcache\abstracts\DriverSimple;

			class Example extends DriverSimple {
			
			    /**
			     * 构造函数
			     * @param array $config 配置
			     */
			    public function __construct($config = []) {
			        $this->init($config);
					//TODO 完善这个方法
			    }
			
			    /**
			     * 检查驱动是否可用
			     * @return boolean      是否可用
			     */
			    public function checkDriver() {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 设置键值
			     * @param string $key
			     * @param string $value
			     * @return boolean
			     */
			    protected function setOne($key, $value) {
					//TODO 实现这个方法
					
			    }
			
			    /**
			     * 获取键值
			     * @param string $key
			     * @return mixed
			     */
			    protected function getOne($key) {
					//TODO 实现这个方法
			    }
			
			    /**
			     * 删除键值
			     * @param string $key
			     * @return boolean
			     */
			    protected function delOne($key) {
					//TODO 实现这个方法
			    }
			
			}

		```
	2. 实现 `linkcache\abstracts\DriverSimple` 抽象类中的抽象方法

- 实现接口 `linkcache\interfaces\driver\Base` (Base接口是必须的，你也可以实现更多的接口:Incr,Lock,Multi)
	1. 在 `src/linkcache/drivers` 目录下创建新的缓存驱动类 `Example.php`
		```
		 
			 * @copyright   (c) Dong Nan http://idongnan.cn All rights reserved.
			 * @link        http://git.oschina.net/dongnan/LinkCache
			 * @license     BSD (http://opensource.org/licenses/BSD-3-Clause)
			 */
			
			namespace linkcache\drivers;
			use linkcache\interfaces\driver\Base;
			
			class Example implements Base {
			
			    use \linkcache\traits\CacheDriver;
			
			    /**
			     * 构造函数
			     * @param array $config 配置
			     */
			    public function __construct($config = []) {
			        $this->init($config);
					//TODO 完善这个方法
			    }
			
			    /**
			     * 检查驱动是否可用
			     * @return boolean      是否可用
			     */
			    public function checkDriver() {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 设置键值
			     * @param string $key   键名
			     * @param mixed $value  键值
			     * @param int $time     过期时间,默认为-1,不设置过期时间;为0则设置为永不过期
			     * @return boolean      是否成功
			     */
			    public function set($key, $value, $time = -1) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 当键名不存在时设置键值
			     * @param string $key   键名
			     * @param mixed $value  键值
			     * @param int $time     过期时间,默认为-1,不设置过期时间;为0则设置为永不过期
			     * @return boolean      是否成功
			     */
			    public function setnx($key, $value, $time = -1) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 获取键值
			     * @param string $key   键名
			     * @return mixed|false  键值,失败返回false
			     */
			    public function get($key) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 删除键值
			     * @param string $key   键名
			     * @return boolean      是否成功
			     */
			    public function del($key) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 是否存在键值
			     * @param string $key   键名
			     * @return boolean      是否存在
			     */
			    public function has($key) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 获取生存剩余时间
			     * @param string $key   键名
			     * @return int|false    生存剩余时间(单位:秒) -1表示永不过期,-2表示键值不存在,失败返回false
			     */
			    public function ttl($key) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 设置过期时间
			     * @param string $key   键名
			     * @param int $time     过期时间(单位:秒)。不大于0，则设为永不过期
			     * @return boolean      是否成功
			     */
			    public function expire($key, $time) {
			        //TODO 实现这个方法
			    }
			
			    /**
			     * 移除指定键值的过期时间
			     * @param string $key   键名
			     * @return boolean      是否成功
			     */
			    public function persist($key) {
			        //TODO 实现这个方法
			    }
			
			}
		```
	2. 实现 `linkcache\interfaces\driver\Base` 接口中的方法

## 2.测试新增的驱动

为了保证代码的可靠性，不妨对新增的驱动做个测试吧。
我使用的是PHPUnit做的测试，版本：4.8.15

- 测试步骤
	1. 在 `tests` 目录新增测试类 `TestDriverExample.php` 
		```
		 
			 * @copyright   (c) Dong Nan http://idongnan.cn All rights reserved.
			 * @link        http://git.oschina.net/dongnan/LinkCache
			 * @license     BSD (http://opensource.org/licenses/BSD-3-Clause)
			 */
			
			namespace linkcacheTests;
			
			/**
			 * TestDriverExample
			 */
			class TestDriverExample extends TestDriverFiles
			{
			    protected $cacheDriver = 'example';
			}
		```
	2. 进入LinkCache项目目录，执行测试命令
		```
		phpunit --bootstrap autoload_dev.php tests/TestDriverExample
		```
		显示以下信息测试就通过啦~
		```
		PHPUnit 4.8.15 by Sebastian Bergmann and contributors.

		.................
		
		Time: 3.26 seconds, Memory: 8.50Mb
		
		OK (17 tests, 68 assertions)
		```

# LICENSE

使用非常灵活宽松的 [New BSD License](http://opensource.org/licenses/BSD-3-Clause) 协议





 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)