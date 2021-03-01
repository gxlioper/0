# ieaseMusic

[![Current Release](https://img.shields.io/github/release/trazyn/ieaseMusic.svg?style=flat-square)](https://github.com/trazyn/ieaseMusic/releases)
![License](https://img.shields.io/github/license/trazyn/ieaseMusic.svg?style=flat-square)
[![Travis CI status](https://img.shields.io/travis/trazyn/ieaseMusic/dev.svg?style=flat-square)](https://travis-ci.org/trazyn/ieaseMusic/branches)
[![Dependencies Status](https://david-dm.org/trazyn/ieaseMusic/status.svg?style=flat-square)](https://david-dm.org/trazyn/ieaseMusic)
[![DevDependencies Status](https://david-dm.org/trazyn/ieaseMusic/dev-status.svg?style=flat-square)](https://david-dm.org/trazyn/ieaseMusic?type=dev)
[![JS Standard Style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat-square)](http://standardjs.com)


 

> Elegant NeteaseMusic desktop app, Rock with NeteaseMusic :metal:

> Built by Electron, React, MobX, JSS

`API` 由 [Binaryify/NeteaseCloudMusicApi](https://github.com/Binaryify/NeteaseCloudMusicApi) 提供。


## Preview

![PREVIEW](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/preview.gif?raw=true)

## Feature
- 帅
- 很帅
- 非常帅
- JSS Theme support
- OSX Friendly
- Cross Platform
- Keyboard support
- Desktop notifications
- Modern UI design
- High quality music(FLAC)
- Track your listen to Last.fm
- Fix dead music link [#3](https://github.com/trazyn/ieaseMusic/issues/3)(QQ music, Xiami music, Kugou music, Kuwo music, MiGu music, Biadu music all in one)
- Share music to Facebook, Twitter, Google+, WeChat
- WeChat scan to log in
- Download music 🍭

  ![Downloader](https://raw.githubusercontent.com/trazyn/ieaseMusic/dev/screenshots/downloader.png)
- Alfred 3 workflow([alfred-ieasemusic](https://github.com/trazyn/alfred-ieasemusic)), required [v1.2.6+](https://github.com/trazyn/ieaseMusic/releases/latest)

  ![Alfred](https://github.com/trazyn/alfred-ieasemusic/raw/master/screenshots/menu.png?raw=true)

## Install

Download the last version on the [website](https://github.com/trazyn/ieaseMusic/releases/latest) or below.

#### Mac(10.9+)
[Download](https://github.com/trazyn/ieaseMusic/releases/download/v1.3.4/ieaseMusic-1.3.4-mac.dmg) the `.dmg` file, Or use `homebrew`:
```
brew cask install ieasemusic
```

#### Linux

[Download](https://github.com/trazyn/ieaseMusic/releases/download/v1.3.4/ieaseMusic-1.3.4-linux-amd64.deb) the `.deb` file for 'Debian / Ubuntu':
```
$ sudo dpkg -i ieaseMusic-1.3.4-linux-amd64.deb
```

[Download](https://github.com/trazyn/ieaseMusic/releases/download/v1.3.4/ieaseMusic-1.3.4-linux-x86_64.rpm) the `.rpm` file for 'Centos/RHEL':
```
$ sudo yum localinstall ieaseMusic-1.3.4-linux-x86_64.rpm
```

[Download](https://github.com/trazyn/ieaseMusic/releases/download/v1.3.4/iease-music-1.3.4-x86_64.AppImage) the `.Appimage` file for other distribution:
```
$ chmod u+x iease-music-1.3.4-x86_64.AppImage
$ ./iease-music-1.3.4-x86_64.AppImage
```

Archlinux `pacman` install:
```
$ pacman -S iease-music
```
or
```
$ pacman -S iease-music-git
```

## Screenshots

![Home](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/home.png?raw=true)
![FM](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/fm.png?raw=true)
![PLAYER](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/player.png?raw=true)
![PLAYER2](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/player-2.png?raw=true)
![USER](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/user.png?raw=true)
![ARTIST](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/artist.png?raw=true)
![COMMENTS](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/comments.png?raw=true)
![LYRICS](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/lyrics.png?raw=true)
![COVER](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/cover.png?raw=true)
![TOP](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/top.png?raw=true)
![CMDP](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/cmd+p.png?raw=true)
![MENU](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/menu.png?raw=true)
![UPNEXT](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/upnext.png?raw=true)
![PLAYLIST](https://github.com/trazyn/ieaseMusic/blob/dev/screenshots/playlist.png?raw=true)

## Development
```
git submodule init
git submodule update --remote --merge
$ npm install
$ npm run dev
```

## UNBLOCK
修改`/etc/hosts`添加
```
158.199.142.239 music.163.com
163.171.98.219  p1.music.126.net
163.171.98.219  p3.music.126.net
163.171.98.219  p4.music.126.net
202.122.146.83  m10.music.126.net
```
>上面是日本反代节点[fengjueming/unblock-NetEaseMusic](https://github.com/fengjueming/unblock-NetEaseMusic)
>
>新加坡节点（本屌太穷有需要还是尽量用上面的节点吧）
>```
>52.221.201.48 music.163.com
>```

关于优化`IP`地址，p开头的是图片CDN服务器，m开头的是音乐资源CDN服务器。可以通过
```
ping ws.acgvideo.com
```
来寻找最优的音乐资源CDN服务器。通过
```
ping cdnetworks.com
```
来寻找最优的图片资源CDN服务器。

## Keyboard shortcuts

Description            | Keys
-----------------------| -----------------------
暂停/播放              |  Space 
上一曲                 |  Left 
下一曲                 |  Right 
音量加                 |  Up 
音量减                 |  Down 
喜欢歌曲               |  Cmd   L 
播放历史记录           |  Cmd   0  ...  9 
搜索                   |  Cmd   F 
显示下载歌曲               |  Shift   Cmd   D 
跳转首页               |  Shift   Cmd   H 
查看榜单               |  Shift   Cmd   T 
所有歌单               |  Shift   Cmd   P 
我的电台               |  Shift   Cmd   F 
菜单                   |  Shift   Cmd   L 
播放列表               |  Cmd   P 
偏好设置               |  Cmd   , 
偏好设置               |  鼠标右键 

## TODO:
- [x] Home
- [x] Playlist
- [x] Top
- [x] My FM
- [x] User
- [x] Artist
- [x] Album
- [x] Search
- [x] Login
- [x] Pllylist subscribe
- [x] Follow
- [x] Flac high quality audio
- [x] Fix dead music link([#3](https://github.com/trazyn/ieaseMusic/issues/3))
- [x] Scrobble to Last.fm
- [x] Comment（Read only）
- [x] Lyrics
- [x] Auto update
- [x] Alfred supports
- [x] Download manager
- [x] Wechat QR code login
- [x] Weibo QR code login
- [ ] Resize window（New UI）

## 参考列表
- UNBLOCK

  [fengjueming/unblock-NetEaseMusic](https://github.com/fengjueming/unblock-NetEaseMusic)
  
   [acgotaku/NetEaseMusicWorld](https://github.com/acgotaku/NetEaseMusicWorld)
- 高品质音乐
  [YongHaoWu/NeteaseCloudMusicFlac](https://github.com/YongHaoWu/NeteaseCloudMusicFlac)
- 添加其他曲库，解决死链问题
  [ITJesse/UnblockNeteaseMusic](https://github.com/ITJesse/UnblockNeteaseMusic)

## License
还是 MIT 吧，懒得改了

![DONATE](https://github.com/trazyn/ieaseMusic/blob/dev/resource/donate.png?raw=true)


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)