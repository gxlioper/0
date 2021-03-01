node-forward-proxy
===============

P2P HTTP and SOCKS forward webproxy based on [AppNet.io](https://github.com/InstantWebP2P/appnet.io) and Node.js

### Features

* HTTP / SOCKS proxy server as forward-proxy import service
* HTTP CONNECT tunnel over AppNet.io STUN session as forward-proxy export service
* multi-hop relay over STUN session
* secure P2P proxy tunnel to build user-defined WebVPN service
* high UDP data transfer performance

### Install manually
* npm install forward-proxy, or git clone [forward-proxy](https://github.com/InstantWebP2P/forward-proxy.git) && cd forward-proxy && npm install
* forward-proxy depend on node-httpp, just build it from repo [node-httpp](https://github.com/InstantWebP2P/node-httpp)
* setup your own AppNet.io backend controller services refer to [AppNet.io-controller](https://github.com/InstantWebP2P/appnet.io-controller)

### Install with prebuilt packages, just download and unzip it
* [Windows package](https://github.com/InstantWebP2P/node-forward-proxy/archive/pkg-release-windows.zip)
* [OSx package](https://github.com/InstantWebP2P/node-forward-proxy/archive/pkg-release-osx.zip)
* [Linux x86 package](https://github.com/InstantWebP2P/node-forward-proxy/archive/pkg-release-linux32.zip)
* [Linux x86_64 package](https://github.com/InstantWebP2P/node-forward-proxy/archive/pkg-release-linux64.zip)
* [RaspberryPi package](https://github.com/InstantWebP2P/node-forward-proxy/archive/pkg-release-pi.zip)

### Usage/API
* for export service, refer to demo/export.js. to start it, just node demo/export.js
* for http proxy server, refer to demo/webproxy.js. to start it, just node demo/webproxy.js
* for socks proxy server, refer to demo/socksproxy.js. to start it, just node demo/export.js
* for http/socks server, please fill export service vURL in options.export, when create Proxy instance
* web browser is http proxy / socks proxy client
* after setup export service and start http or socks server, then set web browser proxy settings point to http/socks server
* for forward-proxy util, refer to bin/forward-proxy. to start it, just node bin/forward-proxy --key usrkey(MUST) --http_port xxx --socks_port xxx --export_vurl vURL --enable_export
* export/import service's usrkey MUST same

### License

(The MIT License)

Copyright (c) 2012-present Tom Zhou(appnet.link@gmail.com)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.



 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)