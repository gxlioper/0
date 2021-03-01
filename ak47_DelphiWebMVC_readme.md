# DelphiWebMVC使用说明:
	运行时使用管理员权限。
	项目主页：http://www.delphiwebmvc.com
	讨论QQ群: 685072623

	开发工具:delphi xe10.3
	注意:win10系统以管理员权限运行
	数据库支持MySQL,SQLite,MSSQL,Oracle,其它数据库可自行进行添加。
	
	Controller  : 控制器类存放目录
	Config 		: 项目配置相关代码
	Publish 	: 视图页面js,css,html,数据库配置相关资源
	Project 	: 工程文件
	
	数据库与服务配置(可加密配置)：
	Publish/config.json文件
	例：
	{
	"Server": {
		"Port": "8004",
		"Compress":"deflate",
		"HTTPQueueLength":1000,
		"ChildThreadCount":10
	},
	"Redis":{
		"Host":"",
		"Port":6379,
		"PassWord":"admin",
		"InitSize":5,
		"TimeOut":60,
		"ReadTimeOut":10
	},
	"Config":{
		"__APP__":"",
		"__WebRoot__":"WebRoot",
		"template":"view",
		"template_type":".html",
		"document_charset":"utf-8",
		"sessoin_name":"__guid_session",
		"Route_suffix":"",
		"session_start":true,
		"session_timer":30,
		"bpl_Reload_timer":5,
		"bpl_unload_timer":10,
		"open_package":false,
		"open_log":false,
		"open_cache":true,
		"cache_max_age":"315360000",
		"open_interceptor":true,
		"show_sql":false,
		"open_debug":true,
		"directory":[
			{
				"path":"/view/data/",
				"permission":false
			}
		]
	},	
	"DBConfig":{
		"MYSQL": {
			"DriverID": "MySQL",
			"Server": "127.0.0.1",
			"Port": "3306",
			"Database": "test",
			"User_Name": "root",
			"Password": "root",
			"CharacterSet": "utf8",
			"Compress": "False",
			"Pooled": "True",
			"POOL_CleanupTimeout": "30000",
			"POOL_ExpireTimeout": "90000",
			"POOL_MaximumItems": "50"
		},
		"SQLite": {
			"DriverID": "SQLite",
			"Database": "sqlite.db",
			"User_Name": "",
			"Password": "",
			"OpenMode": "CreateUTF8",
			"Pooled": "True",
			"POOL_CleanupTimeout": "30000",
			"POOL_ExpireTimeout": "90000",
			"POOL_MaximumItems": "50"
		},
		"MSSQL": {
			"DriverID": "MSSQL",
			"Server": "127.0.0.1",
			"Port": "1433",
			"Database": "Northwind",
			"User_Name": "sa",
			"Password": "",
			"Pooled": "True",
			"POOL_CleanupTimeout": "30000",
			"POOL_ExpireTimeout": "90000",
			"POOL_MaximumItems": "50"
		},
		"ORACLE": {
			"DriverID": "Ora",
			"CharacterSet": "UTF8",
			"Database": "192.168.178.102:1521\\orcl",
			"User_Name": "",
			"Password": "",
			"Pooled": "True",
			"POOL_CleanupTimeout": "30000",
			"POOL_ExpireTimeout": "90000",
			"POOL_MaximumItems": "50"
		}
	}
	

	



	路由配置：
	Config/uRouteMap.pas配置相关路由
	例:
	unit uRouteMap;

	interface

	uses
	  Route;

	type
	  TRouteMap = class(TRoute)
	  public
		constructor Create(); override;
	  end;

	implementation

	uses
	  MainController, CaiWuController, FirstController, IndexController, KuCunController, LoginController, UsersController, XiaoShouController;

	constructor TRouteMap.Create;
	begin
	  inherited;
	//路径,控制器,视图目录,是否拦截
	//SetRoute(name: string; ACtion: TClass; path: string = '';isInterceptor:Boolean=True);
	  SetRoute('', TLoginController, 'login');
	  SetRoute('Main', TMainController, 'main');
	  SetRoute('Users', TUsersController, 'users');
	end;

	end.


	控制器开发：
	存放在Controller文件夹
	例:
	unit LoginController;

	interface

	uses
	  System.SysUtils, System.Classes, FireDAC.Stan.Intf, Data.DB, superobject,
	  BaseController;

	type
	  TLoginController = class(TBaseController)
	  public
		procedure index();
		procedure check();
		procedure checknum();
	  end;

	implementation

	uses
	  uTableMap;

	procedure TLoginController.check();
	var
	  json: string;
	  sdata, ret, wh: ISuperObject;
	  username, pwd: string;
	  sql: string;
	begin
	  ret := SO();
	  with View do
	  begin
		try
		  username := Input('username');
		  pwd := Input('pwd');
		  Sessionset('username', username);
		  json := Sessionget('username');
		  wh := SO();
		  wh.S['username'] := username;
		  wh.S['pwd'] := pwd;
		  sdata := Db.FindFirst(tb_users, wh);
		  if (sdata <> nil) then
		  begin
			json := sdata.AsString;
			Sessionset('username', username);
			Sessionset('name', sdata.S['name']);
			ret.I['code'] := 0;
			ret.S['message'] := '登录成功';
		  end
		  else
		  begin
			ret.I['code'] := -1;
			ret.S['message'] := '登录失败';
		  end;
		  ShowJson(ret);
		except
		  on e: Exception do
			ShowText(e.ToString);
		end;

	  end;
	end;

	procedure TLoginController.checknum;
	var
	  num: string;
	begin
	  Randomize;
	  num := inttostr(Random(9)) + inttostr(Random(9)) + inttostr(Random(9)) + inttostr(Random(9));
	  View.ShowCheckIMG(num, 60, 30);
	end;

	procedure TLoginController.index();
	begin
	  with View do
	  begin
		ShowHTML('Login');
	  end;
	end;

	end.


	拦截器配置：
	Config/uInterceptor.pas
	例：
	unit uInterceptor;

	interface

	uses
	  System.SysUtils, View, System.Classes;

	type
	  TInterceptor = class
		urls: TStringList;
		function execute(View: TView; error: Boolean): Boolean;
		constructor Create;
		destructor Destroy; override;
	  end;

	implementation

	{ TInterceptor }

	constructor TInterceptor.Create;
	begin
	  urls := TStringList.Create;
	  //拦截器默认关闭状态uConfig文件修改
	  //不需要拦截的地址添加到下面
	  urls.Add('/');
	  urls.Add('/check');
	  urls.Add('/checknum');
	end;

	function TInterceptor.execute(View: TView; error: Boolean): Boolean;
	var
	  url: string;
	begin
	  Result := false;
	  with View do
	  begin
		if (error) then
		begin
		  Result := true;
		  exit;
		end;
		url := LowerCase(Request.PathInfo);
		if urls.IndexOf(url)  window.location.href=''/''; ';
			Response.SendResponse;
		  end;
		end;
	  end;
	end;

	destructor TInterceptor.Destroy;
	begin
	  urls.Free;
	  inherited;
	end;

	end.


	
	框架标记：
	__APP__ 应用路径
    setAttr('ls',list.AsString);
    setAttr('key1','1');
    setAttr('key2','2');
	setAttr('key3','3');
    setAttr('username','admin');
    setAttr('user',jo.ToString);
	
	 
	#{username}
	#{user.name}
	 
	 
		 
			 #{d.name} 
			 男   女   未知    

		 
	 
	 
	   不存在
	 
	
	条件类别
	'neq', '!=='	
	'eq', '=='
	'and', '&&'
	'or', '||'
	'gte', '>='
	'ge', '>='
	'gt', '>='
	'lte', '<='
	'le', '<='
	'lt', '<'

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)