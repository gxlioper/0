# DxTcpServer
Go语言的TCP网络通信框架，具备编码器和解码器接口，自己实现对应的编码器接口就行
# 思路原理与运行模式
  服务的整体编写思路，实际上都是Go的常规路子，然后做了一个编码解码的封装。先构建服务对象，然后指定编码解码结构对象，启动服务器，然后开启一个接收客户理解的协程acceptClients，在这个go routine中执行等待客户连接，客户连接上来之后，会开启用户的读取数据Go routine,读取在数据的过程中将数据根据编码器进行解码成对应的结构对象，然后投递到解析处理队列，另外一个专门解析的go routine专门负责从队列中获得客户发送的数据对象进行操作然后触发OnRecvData事件，我们编写服务端代码的时候，主要就是实现这个接收事件进行处理。这里有一个专门的go routine来负责检查心跳，从客户队列中获取解码对象执行OnRecvData操作，以及从发送队列中获取发送对象进行编码，然后发送到客户并触发OnSendData事件。服务器内部会不断的检查心跳，心跳机制是设定了TimeOutSeconds不为0的时候，会使用Go内部的ReadDeadLine等方法自动处理，如果达到了这个时间执行失败的，就关闭连接，表示失败了，如果设定了TimeOutSeconds=0，则会比对最后一次读取或者发送数据成功的时间和当前的时间差，超过2分钟的，视为心跳失败，则关闭连接。				
# 切记，使用了本服务框架之后，已经限定了实际的发送包格式，其格式为 
   发送对象编码后的长度+发送的对象编码
# 使用方法以及属性方法等
## DxTcpServer
  dxserver.DxTcpServer的LimitSendPkgCout表示限制的包的发送队列，如果指定的长度大于0，则会构建一个发送通道，所有的发送对象会先到通道，然后从通道进行数据发送，如果指定为0，则发送对象的时候，就直接立即发送数据了。    
  RequestCount表示请求数量    
  SendRequestCount表示发送的请求数量    
  SendDataSize表示发送的数据量大小    
  RecvDataSize表示接受的数据量大小    
  OnRecvData客户端发送数据包过来之后执行，其中包含有编码器自动解码的出来对象    
  OnClientConnect客户端连接事件   
  OnClientDisConnected客户断开事件   
  OnSendData数据发送触发事件   
  TimeOutSeconds超时设定，默认为0，采用自带的go routine判定心跳   
  SetCoder(encoder IConCoder)设定编码器   
  Open(addr string)打开一个服务，addr是服务地址比如":8340"   
## DxNetConnection客户端的连接对象结构
   RemoteAddr()对象的远程地址    
   Close()关闭连接    
   WriteObject(obj interface{})将对象编码之后发送回客户端    
# 编写一个简单的ECHO
```go
type EchoCoder struct {

}
//ECHO编码器编码，直接将内容写入到buf中
func (coder *EchoCoder)Encode(obj interface{},buf *bytes.Buffer) error  {
	buf.Write(obj.([]byte))
	return nil
}

func (coder *EchoCoder)Decode(bytes []byte)(result interface{},ok bool)  {
	return bytes,true
}

func (coder *EchoCoder)HeadBufferLen()uint16  {
	return 2
}

func (coder *EchoCoder)MaxBufferLen()uint16  {
	return 1024
}

func NewEchoServer()*dxserver.DxTcpServer{
	srv := new(dxserver.DxTcpServer)
	srv.LimitSendPkgCount = 20
	coder := new(EchoCoder)
	srv.SetCoder(coder)
	srv.OnRecvData = func(con *dxserver.DxNetConnection,recvData interface{}) {
		//直接发送回去
		con.WriteObject(recvData)
	}
	/*srv.OnClientConnect = func(con *dxserver.DxNetConnection){
		//客户端登录了
		fmt.Println("登录客户",srv.ClientCount())
	}*/
	return srv
}

//然后

func main(){
  srv = EchoDemo.NewEchoServer()
  srv.Open("127.0.0.1:8340")
}
```
以上的编码器是直接将发送的内容返回写入到了Buf中了，如果是其他的格式，比如，如果是Json，那么编码器的编码函数可以写为
```go
func (coder *JsonCoder)Decode(pkgbytes []byte)(result interface{},ok bool)  {
	buf := bytes.NewReader(pkgbytes[:])
	decoder := json.NewDecoder(buf)
  	jsonpkg := new(JSONPKG)
	ok = decoder.Decode(jsonpkg)==nil
	if ok{
		result = jsonpkg
	}else{
		result = nil
	}
	return
}
func (coder *JsonCoder)Encode(obj interface{},buf *bytes.Buffer) error  {
  encoder := json.NewEncoder(buf)
  return encoder.Encode(obj)
}
```
#  一个增加文件服务器的编码解码器扩展，简单用例如下
```go
//服务器端
srv = Filesrv.NewFileServer(curExecDir)
srv.Open("127.0.0.1:8340")

//客户端
func main()  {
	app := controls.NewApplication()
	app.ShowMainForm = false
	mainForm := app.CreateForm()
	PopMenu := NVisbleControls.NewPopupMenu(mainForm)

	fclient = FileClient.NewFileClient()
	fclient.OnDownLoad = func(client *FileClient.FileClient,FileName string,TotalSize,Position int64){
		fmt.Println(FileName,"正在文件下载",Position*100/TotalSize,"%")
	}
	mItem := PopMenu.Items().AddItem("下载文件")
	mItem.OnClick = func(sender interface{}) {
		fclient.DownLoadFile("第2版394860.pdf","d:\\2.pdf")
		fclient.DownLoadFile("游戏编程大师技巧(第二版.pdf","d:\\3.pdf")
	}
	mItem = PopMenu.Items().AddItem("-")
	mItem = PopMenu.Items().AddItem("退出")
	mItem.OnClick = func(sender interface{}) {
		fclient.Close()
		mainForm.Close()
	}
	trayicon := NVisbleControls.NewTrayIcon(mainForm)
	trayicon.PopupMenu = PopMenu
	trayicon.SetVisible(true)
	fclient.Connect("127.0.0.1:8340")
	app.Run()
}
```


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)