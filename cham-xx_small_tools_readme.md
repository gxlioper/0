[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu)
[![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)
# excel-poi


#### maven使用方式
```java
 
 
     com.github.stupdit1t 
     poi-excel 
     1.1 
 
```

### 导入
1. 支持严格的单元格校验
2. 支持数据行的图片导入
3. 3支持数据回调处理
4. 03和07都支持

### 导出
1. 动态表头+表尾
2. 支持List 数据
3. 支持图片导出，
4. 支持复杂对象的导出
5. 支持回调处理数据后再导出
6. 支持单元格的样式设置
7. 支持模板导出
8. 导出03和07都支持，默认为03，具体看以下使用方式


### 选择03还是07？
1. 03速度较快，单sheet最大65535行，体积大
2. 07速度慢，单sheet最大1048576行，体积小


## 主要功能：
### 导入
1. 简单的导入:
```java
// 1.获取源文件
Workbook wb = WorkbookFactory.create(new FileInputStream("src\\test\\java\\excel\\imports\\import.xlsx"));
// 2.获取sheet0导入
Sheet sheet = wb.getSheetAt(0);
// 3.生成VO数据
//参数：1.生成VO的class类型;2.校验规则;3.导入的sheet;3.从第几行导入;4.尾部非数据行数量
ImportRspInfo  list = ExcelUtils.parseSheet(ProjectEvaluate.class, EvaluateVerifyBuilder.getInstance(), sheet, 3, 2);
if (list.isSuccess()) {
	// 导入没有错误，打印数据
	System.out.println(JSON.toJSONString(list.getData()));
} else {
	// 导入有错误，打印输出错误
	System.out.println(list.getMessage());
}
```

2. 复杂导入，带图片导入，带回调处理
```java
// 1.获取源文件
Workbook wb = WorkbookFactory.create(new FileInputStream("src\\test\\java\\excel\\imports\\import.xlsx"));
// 2.获取sheet0导入
Sheet sheet = wb.getSheetAt(0);
// 3.生成VO数据
//参数：1.生成VO的class类型;2.校验规则;3.导入的sheet;3.从第几行导入;4.尾部非数据行数量;5.导入每条数据的回调
ImportRspInfo  list = ExcelUtils.parseSheet(ProjectEvaluate.class, ProjectVerifyBuilder.getInstance(), sheet, 3, 2, (row, rowNum) -> {
	//1.此处可以完成更多的校验
	if(row.getAreaName() == "中青旅"){
	    throw new POIException("第"+rowNum+"行，区域名字不能为中青旅！");
	}
	//2.图片导入，再ProjectEvaluate定义类型为byte[]的属性就可以，ProjectVerifyBuilder定义ImgVerfiy校验列.就OK了
});
if (list.isSuccess()) {
	// 导入没有错误，打印数据
	System.out.println(JSON.toJSONString(list.getData()));
	//打印图片byte数组长度
	byte[] img = list.getData().get(0).getImg();
	System.out.println(img);
} else {
	// 导入有错误，打印输出错误
	System.out.println(list.getMessage());
}
```

3. 自定义校验器，导入需要校验字段,必须继承AbstractVerifyBuidler

```java
public class ProjectVerifyBuilder extends AbstractVerifyBuidler {

	private static ProjectVerifyBuilder builder = new ProjectVerifyBuilder();

	public static ProjectVerifyBuilder getInstance() {
		return builder;
	}

	/**
	 * 定义列校验实体：提取的字段、提取列、校验规则
	 */
	private ProjectVerifyBuilder() {
		cellEntitys.add(new CellVerifyEntity("projectName", "B", new StringVerify("项目名称", true)));
		cellEntitys.add(new CellVerifyEntity("areaName", "C", new StringVerify("所属区域", true)));
		cellEntitys.add(new CellVerifyEntity("province", "D", new StringVerify("省份", true)));
		cellEntitys.add(new CellVerifyEntity("city", "E", new StringVerify("市", true)));
		cellEntitys.add(new CellVerifyEntity("people", "F", new StringVerify("项目所属人", true)));
		cellEntitys.add(new CellVerifyEntity("leader", "G", new StringVerify("项目领导人", true)));
		cellEntitys.add(new CellVerifyEntity("scount", "H", new IntegerVerify("总分", true)));
		cellEntitys.add(new CellVerifyEntity("avg", "I", new DoubleVerify("历史平均分", true)));
		cellEntitys.add(new CellVerifyEntity("createTime", "J", new DateTimeVerify("创建时间", "yyyy-MM-dd HH:mm", true)));
		cellEntitys.add(new CellVerifyEntity("img", "K", new ImgVerify("图片", false)));
		// 必须调用
		super.init();
	}
}

```


#### 导入示例图
![输入图片说明](https://images.gitee.com/uploads/images/2018/1118/104015_a439ba1a_1215820.png "QQ截图20181118104004.png")

### 导出
1. 简单导出
```java
// 1.获取导出的数据体
List  data = new ArrayList ();
for (int i = 0; i   data = new ArrayList ();
for (int i = 0; i   headerRules = new HashMap<>();
headerRules.put("1,1,A,K", "项目资源统计");
headerRules.put("2,3,A,A", "序号");
headerRules.put("2,2,B,E", "基本信息");
headerRules.put("3,3,B,B", "项目名称");
headerRules.put("3,3,C,C", "所属区域");
headerRules.put("3,3,D,D", "省份");
headerRules.put("3,3,E,E", "市");
headerRules.put("2,3,F,F", "项目所属人");
headerRules.put("2,3,G,G", "市项目领导人");
headerRules.put("2,2,H,I", "分值");
headerRules.put("3,3,H,H", "得分");
headerRules.put("3,3,I,I", "平均分");
headerRules.put("2,3,J,J", "创建时间");
headerRules.put("2,3,K,K", "项目图片");
// 3.尾部设置，一般可以用来设计合计栏
HashMap  footerRules = new HashMap<>();
footerRules.put("1,2,A,C", "注释:");
footerRules.put("1,2,D,K", "导出参考代码！");
// 4.导出hearder对应的字段设置
Column[] column = {

		Column.field("projectName"),
		// 4.1设置此列宽度为10
		Column.field("areaName")
			.width(10),
		// 4.2设置此列下拉框数据
		Column.field("province")
			.width(5)
			.dorpDown(new String[] { "陕西省", "山西省", "辽宁省" }),
		// 4.3设置此列水平居右
		Column.field("city")
			.align(HorizontalAlignment.RIGHT),
		// 4.4 设置此列垂直居上
		Column.field("people")
			.valign(VerticalAlignment.TOP),
		// 4.5 设置此列单元格 自定义校验 只能输入文本为数字文本，具体参考excel函数，不同的地方在于参数的下标从当前单元格A和1开始
		Column.field("leader")
			.verifyCustom("VALUE(F3:F500)","请输入数字！"),
		// 4.6设置此列单元格 整数 数据校验 ，同时设置背景色为棕色
		Column.field("scount")
			.verifyIntNum("10~20")
			.backColor(IndexedColors.BROWN),
		// 4.7设置此列单元格 浮点数 数据校验， 同时设置字体颜色红色
		Column.field("avg")
			.verifyFloatNum("10.0~20.0")
			.color(IndexedColors.RED),
		// 4.8设置此列单元格 日期 数据校验 ，同时宽度为20、限制用户表格输入、水平居中、垂直居中、背景色、字体颜色
		Column.field("createTime")
			.width(20)
			.verifyDate("2000-01-03 12:35~3000-05-06 23:23")
			.align(HorizontalAlignment.LEFT)
			.valign(VerticalAlignment.CENTER)
			.backColor(IndexedColors.YELLOW)
			.color(IndexedColors.GOLD),
		// 4.9项目图片
		Column.field("img")

};
// 5.执行导出到工作簿
// ExportRules:1.是否序号;2.列设置;3.标题设置可为空;4.表头设置;5.表尾设置可为空
Workbook bean = ExcelUtils.createWorkbook(data, new ExportRules(true, column, headerRules, footerRules), (fieldName, value, row, col) -> {
	if ("projectName".equals(fieldName) && row.getProjectName().equals("中青旅23")) {
		col.align(HorizontalAlignment.LEFT);
		col.valign(VerticalAlignment.CENTER);
		col.height(2);
		col.backColor(IndexedColors.RED);
		col.color(IndexedColors.YELLOW);
	}
	return value;
});
// 6.写出文件
bean.write(new FileOutputStream("src/test/java/excel/export/export2.xls"));
```

#### 2导出图
![输入图片说明](https://images.gitee.com/uploads/images/2018/1215/161814_61f83ff1_1215820.png "2.png")


3. 复杂的对象级联导出

```java
// 1.获取导出的数据体
List  data = new ArrayList ();
for (int i = 0; i   moreInfo = new HashMap<>();
	moreInfo.put("parent", new Parent("張無忌"));
	stu.setMoreInfo(moreInfo);
	stu.setName("张三");
	data.add(stu);
}
// 2.导出标题设置，可为空
String title = "學生基本信息";
// 3.导出的hearder设置
String[] hearder = { "學生姓名", "所在班級", "所在學校", "更多父母姓名" };
// 4.导出hearder对应的字段设置，列宽设置
Column[] column = { Column.field("name"), Column.field("classRoom.name"), Column.field("classRoom.school.name"), Column.field("moreInfo.parent.name"), };
// 5.执行导出到工作簿
// ExportRules:1.是否序号;2.字段信息;3.标题设置可为空;4.表头设置;5.表尾设置可为空
Workbook bean = ExcelUtils.createWorkbook(data, new ExportRules(false, column, title, hearder, null));
// 6.写出文件
bean.write(new FileOutputStream("src/test/java/excel/export/export3.xls"));
```

#### 3导出图
![输入图片说明](https://images.gitee.com/uploads/images/2018/1209/193615_b483f034_1215820.png "4.png")

4. map对象的简单导出

```java
// 1.获取导出的数据体
List > data = new ArrayList >();
for (int i = 0; i   map = new HashMap<>();
	map.put("name", "张三");
	map.put("classRoomName", "三班");
	map.put("school", "世纪中心");
	map.put("parent", "张无忌");
	data.add(map);
}
// 2.导出标题设置，可为空
String title = "學生基本信息";
// 3.导出的hearder设置
String[] hearder = { "學生姓名", "所在班級", "所在學校", "更多父母姓名" };
// 4.导出hearder对应的字段设置，列宽设置
Column[] column = { Column.field("name"), Column.field("classRoomName"), Column.field("school"), Column.field("parent"), };
// 5.执行导出到工作簿
// ExportRules:1.是否序号;2.字段信息;3.标题设置可为空;4.表头设置;5.表尾设置可为空
Workbook bean = ExcelUtils.createWorkbook(data, new ExportRules(false, column, title, hearder, null));
// 6.写出文件
bean.write(new FileOutputStream("src/test/java/excel/export/export4.xls"));
```

#### 4导出图
![输入图片说明](https://images.gitee.com/uploads/images/2018/1209/193608_c75b81ee_1215820.png "4.png")

5. 模板导出

```java
// 1.导出标题设置，可为空
String title = "客户导入";
// 2.导出的hearder设置
String[] hearder = { "宝宝姓名", "宝宝昵称", "家长姓名", "手机号码","宝宝生日","月龄","宝宝性别","来源渠道","市场人员","咨询顾问","客服顾问","分配校区","备注" };
// 3.导出hearder对应的字段设置，列宽设置
Column[] column = { 
		Column.field("宝宝姓名"),
		Column.field("宝宝昵称"), 
		Column.field("家长姓名"), 
		Column.field("手机号码").verifyText("11~11", "请输入11位的手机号码！"),
		Column.field("宝宝生日").verifyDate("2000-01-01~3000-12-31"), 
		Column.field("月龄").width(4).verifyCustom("VALUE(F3:F6000)", "月齡格式：如1年2个月则输入14"),
		Column.field("宝宝性别").dorpDown(new String[] {"男","女"}), 
		Column.field("来源渠道").width(12).dorpDown(new String[] { "品推", "市场" }), Column.field("市场人员").width(6).dorpDown(new String[] { "张三", "李四" }),
		Column.field("咨询顾问").width(6).dorpDown(new String[] { "张三", "李四" }), Column.field("客服顾问").width(6).dorpDown(new String[] { "大唐", "银泰" }),
		Column.field("分配校区").width(6).dorpDown(new String[] { "大唐", "银泰" }), 
		Column.field("备注")
	};
// 5.执行导出到工作簿
Workbook bean = ExcelUtils.createWorkbook(Collections.emptyList(), new ExportRules(false, column, title, hearder, null).setXlsx(true));
// 6.写出文件
bean.write(new FileOutputStream("src/test/java/excel/export/export5.xlsx"));
```

#### 5导出图
![输入图片说明](https://images.gitee.com/uploads/images/2018/1215/180646_50cc4004_1215820.png "5.png")


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)