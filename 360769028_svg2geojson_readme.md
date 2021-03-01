# svg转geojson(gulp插件)
***

[TOC]

## 使用方法
	
### 1.下载 
	git clone http://10.19.157.229:3000/tools/geojson.git

### 2.安装 
```bash
cd geojson
cnpm i
```
### 3.使用
+ 将svg文件直接放在 ** svg/ ** 目录下
+ 输入命令
```
gulp
```
+ 在 ** dist/ ** 目录下将生产对应的目录,目录下有转换后的geojson文件以及行政中心的坐标文件和svg原文件



## 制作地图geojson数据的所有步骤
+ 设计地图草稿
+ 根据设计稿使用ai画矢量地图
+ 导出svg
+ 使用gulp将svg转换为geojson
+ 使用图表库制作地图

### 设计地图草稿
设计师设计地图草稿(只需明确行政划分区域即可),如下图
![](http://ww1.sinaimg.cn/large/82eaf5a8gw1fb5hdct8ucj20br0e5abw.jpg)

### 使用AI描出矢量图

* 将设计草稿导入AI
* 新建图层,在图层内跟据设计稿使用钢笔工具描出一个行政区的行政(使用多边形描边)
* 将该图层取名为行政区名字
* 重复第2步,描出所有行政区

![](http://ww2.sinaimg.cn/large/82eaf5a8gw1fb5he2yb4kj20jo0dbjto.jpg)

* 选择所有描点,转换尖角,去除不小心画出的曲线(导出的svg不是由polygon组成的而是path的时候使用这个方法,建议描完后就使用一次)
![](http://ww2.sinaimg.cn/large/82eaf5a8gw1fb5hevxtdrj20ht0fpjty.jpg)
* 在每个图层中心处再画一个圆形或者椭圆
![](http://ww4.sinaimg.cn/large/82eaf5a8gw1fb5hf9spu6j20k70c7q5d.jpg)
* 删除设计草稿的图层导出svg，没有出错的话格式应该如下
![](http://ww3.sinaimg.cn/large/82eaf5a8gw1fb5hfo9pytj20hp0ao794.jpg)

* 如果发现poluygon标签变成了path,请注意第4步骤

** 注意:导出的svg转换出的geojson制作的地图将会是垂直颠倒的(可能是坐标轴不一样,
一个左上角一个右下角),所以我们要把我们制作的AI图垂直翻转后再导出svg **

![](http://ww2.sinaimg.cn/large/82eaf5a8gw1fb5hgx82ouj20bw0dgmyg.jpg)

### 将svg转换为geojson

### 实例

#### [echarts (echarts会将地图横向压扁,需要设置宽高,不能自适应)](http://jsrun.net/iNpKp/embedded/all/light/)
  

#### [highcharts](http://jsrun.cn/ZNpKp/result/light/)

  

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)