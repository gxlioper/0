# ExcelKit

> 简单、好用且轻量级的海量Excel文件导入导出解决方案。

### 注意：从2.0开始,进行了代码重构,不再兼容1.x

#### 重构内容：
1. @ExportConfig重构,支持convert转换器.
2. Excel读取性能优化,由usermodel包下的API重构为eventusermode包下的API,以SAX的方式,边读边处理,性能得到了极大的提升,可轻松实现百万级别的海量数据处理.
3. 写Excel文件的API重构为streaming包下的API，同时支持多sheet导出.
4. 取消了对Excel2003以及以下版本的excel文件支持.
5. 包结构重构,便于以后的版本扩展和升级,不再兼容1.x版本.


# 编译环境：
> 使用``` jdk1.6.0_45 ``` 和```maven-3.2.5```进行项目构建,理论上支持```jdk6+```。

# 使用效果：
> ExcelKit-Example完整示例程序 ([https://github.com/wuwz/ExcelKit-Example][1])

![image](https://raw.githubusercontent.com/wuwz/ExcelKit-Example/master/example.gif)

# 如何使用？


1.引入Maven依赖或下载jar包([下载最新版jar包][2])

> 使用本工具无需关注poi依赖问题（只需引入以下相关jar包)。

``` xml
		 
			 org.wuwz 
			 ExcelKit 
			 2.0 
		 
		 
			 xml-apis 
			 xml-apis 
			 1.4.01 
		 
		
		 
		 
			 log4j 
			 log4j 
			 1.2.9 
		 
		 
			 javax.servlet 
			 javax.servlet-api 
			 3.0.1 
		 
```

> ExcelKit集成的jar:
``` xml
	 3.8 
	 1.9.3 
	 1.6.1 
	 1.1.6 
	 2.11.0 
```

       

2.导出项配置（通过注解）：
 
``` java
	public class User {

    	@ExportConfig("UID")
		private Integer uid;
	
		@ExportConfig("用户名")
		private String username;
	
		@ExportConfig(value = "密码", replace = "******", color = HSSFColor.RED.index)
		private String password;
	
		@ExportConfig(value = "性别", width = 50, convert = "s:1=男,2=女")
		private Integer sex;
	
		@ExportConfig(value = "年级", convert = "c:org.wuwz.poi.test.GradeIdConvert")
		private Integer gradeId;
        
       // getter setter...
   }
```

2.1.实现ExportConvert（如果配置了convert属性,参考gradeId字段）：

> convert属性说明:

将单元格值进行转换后再导出：
目前支持以下几种场景：

1. 固定的数值转换为字符串值（如：1代表男，2代表女）

	表达式: ```"s:1=男,2=女"```
	
	
2. 数值对应的值需要查询数据库才能进行映射 (用的机会不多,一般这种情况直接在DAO处理)

   需要实现org.wuwz.poi.convert.ExportConvert接口
   
   表达式: ```"c:org.wuwz.poi.test.GradeIdConvert"```
	

``` java

	public class GradeIdConvert implements ExportConvert {
		
		static Map  records;
		static {
			//默认数据库字典查询 select * from tb_grades
			records = new HashMap ();
			records.put(1, "一年级学生");
			records.put(2, "二年级学生");
			records.put(3, "三年级学生");
		}
	
		@Override
		public String handler(Integer val) {
			return records.get(val) != null ? records.get(val) : "无记录";
		}
	
	}
```

        

3.一行代码执行浏览器导出：

``` java
	@RequestMapping("/export");
	public void export(HttpServletResponse response) {
		List  users = dao.getUsers();
		
		// 生成Excel并使用浏览器下载
		ExcelKit.$Export(User.class, response).toExcel(users, "用户信息");
	}
```

		

	

# 常用例子：

1.海量数据Excel文件读取（边读边处理）：

	

``` java
	ExcelKit.$Import()
		.setEmptyCellValue(null) // 设置空单元格的值,默认为null,可不设置
		.readExcel(new File("c:/bigexcel.xlsx"), new ReadHandler() {
		
		@Override
		public void handler(int sheetIndex, int rowIndex, List  row) {
			if(rowIndex == 0) return; //排除第一行..
			
			System.out.println("当前行："+rowIndex);
			System.out.println("行数据："+row);
			System.out.println();
			
			// 入库解析
			if(row.get(0) != null) {
				// UID...
			} 
			
			if(row.get(1) != null) {
				// 用户名..
			}
		}
	});
```


 

2.生成Excel文件到本地：
 

``` java
	ExcelKit.$Builder(User.class)
		.setMaxSheetRecords(10000) //设置每个sheet的最大记录数,默认为10000,可不设置
		.toExcel(records, "用户数据", new FileOutputStream(new File("c:/test001.xlsx")));
```
	
	

  [1]: https://github.com/wuwz/ExcelKit-Example
  [2]: https://github.com/wuwz/ExcelKit/blob/master/compile-jar/ExcelKit-2.0.jar?raw=true

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)