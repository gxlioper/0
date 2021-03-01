# ExcelKit

> 简单,好用且轻量级Excel文件导入导出工具。

> ExcelKit-Example完整示例程序 ([https://github.com/wuwz/ExcelKit-Example][1])

# 如何使用？


 1. 引入Maven依赖或下载jar包([点我下载ExcelKit-0.1.jar][2])
 

           
			 org.wuwz 
			 ExcelKit 
			 1.0 
		 

         
		 
			 javax 
			 javaee-api 
			 7.0 
		 
		 
			 javax.servlet 
			 javax.servlet-api 
			 3.1.0 
		 

 2. 导出项配置（通过注解）：
 

        public class User {

        	@ExportConfig(value = "UID", width = 150)
        	private Integer uid;
        
        	@ExportConfig(value = "用户名", width = 200)
        	private String username;
        
        	@ExportConfig(value = "密码(不可见)", width = 120, isExportData = false)
        	private String password;
        
        	@ExportConfig(value = "昵称", width = 200)
        	private String nickname;
        
        	private Integer age;
        
        	// getter setter...
        }

 3. 一行代码导出：
 

		List  users = dao.getUsers();
		
		// 生成Excel并使用浏览器下载
		ExcelKit.$Export(User.class, response).toExcel(users, "用户信息");
		
 3. 导出效果预览：
	![image](https://raw.githubusercontent.com/wuwz/ExcelKit/master/example.png)
	

# 其他使用例子

 1. 导入Excel读取数据：

    	List  users = Lists.newArrayList();
		
		final List  users = Lists.newArrayList();
		
		//导入数据。
		File excelFile = new File("C:\\Users\\Administrator\\Desktop\\excel.xlsx");
		ExcelKit.$Import().readExcel(excelFile, new OnReadDataHandler() {
			
			@Override
			public void handler(List  rowData) {
				User u = new User();
				u.setUid(Integer.valueOf(rowData.get(0)));
				u.setUsername(rowData.get(1));
				u.setPassword(rowData.get(2));
				u.setNickname(rowData.get(3));
				
				u.setAge(18);
				users.add(u);
				
			}
		});
		
		System.out.println(users);

 

 2. 生成Excel文件到本地、生成导入模版文件：
 

        // 生成本地文件
		File excelFile = new File("C:\\Users\\Administrator\\Desktop\\excel.xlsx");
		ExcelKit.$Builder(User.class).toExcel(users, "用户信息", new FileOutputStream(excelFile));
		
		// 生成Excel导入模版文件。
		users.clear();
		File templateFile = new File("C:\\Users\\Administrator\\Desktop\\import_template.xlsx");
		ExcelKit.$Builder(User.class).toExcel(users, "用户信息", new FileOutputStream(templateFile));
		
		
		
		


  [1]: https://github.com/wuwz/ExcelKit-Example
  [2]: https://github.com/wuwz/ExcelKit/blob/master/target/ExcelKit-1.0.jar?raw=true

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)