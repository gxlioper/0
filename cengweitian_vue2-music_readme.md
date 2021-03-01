# vue2.0-music

[![标签](https://img.shields.io/teamcity/codebetter/bt428.svg)]() [![标签](https://img.shields.io/npm/v/@cycle/core.svg)]() [![标签](https://img.shields.io/npm/dm/localeval.svg)]()


> Vue.js 打造高级实战——音乐 App
>Vue2.0 云音乐播放器，QQ音乐API，可听QQ音乐高品质付费歌曲。 


## 项目截图

![vue2-music](https://upload-images.jianshu.io/upload_images/4340772-6388d1448806267e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 安装与运行

```
git clone https://github.com/HuangCongqing/vue2-music.git

cd vue-music

npm install

npm run dev //服务端运行 访问 http://localhost:8080

npm run build 项目打包 

感兴趣的童鞋可以来个star

```

### TO DO

* listview.vue下的scrollY函数

* 部分接口线上404错误

* 

技术栈

【前端】

* Vue：用于构建用户界面的 MVVM 框架。它的核心是响应的数据绑定和组系统件
* vue-router：为单页面应用提供的路由系统，项目上线前使用了 Lazy Loading Routes 技术来实现异步加载优化性能
* vuex：Vue 集中状态管理，在多个组件共享某些状态时非常便捷
* vue-lazyload：第三方图片懒加载库，优化页面加载速度
* better-scroll：iscroll 的优化版，使移动端滑动体验更加流畅
* Sass(Scss)：css 预编译处理器
* ES6：ECMAScript 新一代语法，模块化、解构赋值、Promise、Class 等方法非常好用

【后端】

* Node.js：利用 Express 起一个本地测试服务器
* jsonp：服务端通讯。抓取 QQ音乐(移动端)数据
* axios：服务端通讯。结合 Node.js 代理后端请求，抓取 QQ音乐(PC端)数据

【自动化构建及其他工具】

* vue-cli：Vue 脚手架工具，快速初始化项目代码
* eslint：代码风格检查工具，规范代码书写
* vConsole：移动端调试工具，在移动端输出日志




## 项目树
```
.
├── README.md
├── build
│   ├── build.js
│   ├── check-versions.js
│   ├── dev-client.js
│   ├── dev-server.js
│   ├── utils.js
│   ├── vue-loader.conf.js
│   ├── webpack.base.conf.js
│   ├── webpack.dev.conf.js
│   └── webpack.prod.conf.js
├── config
│   ├── dev.env.js
│   ├── index.js
│   └── prod.env.js
├── index.html
├── package.json
├── prod.server.js
├── src
│   ├── App.vue
│   ├── api                       // 获取的数据及处理都在api其中
│   │   ├── config.js
│   │   ├── rank.js
│   │   ├── recommend.js
│   │   ├── search.js
│   │   ├── singer.js
│   │   └── song.js
│   ├── base
│   │   ├── confirm
│   │   │   └── confirm.vue
│   │   ├── listview
│   │   │   └── listview.vue
│   │   ├── loading
│   │   │   ├── loading.gif
│   │   │   └── loading.vue
│   │   ├── no-result
│   │   │   ├── no-result.vue
│   │   │   ├── no-result@2x.png
│   │   │   └── no-result@3x.png
│   │   ├── progress-bar
│   │   │   └── progress-bar.vue
│   │   ├── progress-circle
│   │   │   └── progress-circle.vue
│   │   ├── scroll
│   │   │   └── scroll.vue
│   │   ├── search-box
│   │   │   └── search-box.vue
│   │   ├── search-list
│   │   │   └── search-list.vue
│   │   ├── slider
│   │   │   └── slider.vue
│   │   ├── song-list                 //歌曲列表，复用
│   │   │   ├── first@2x.png
│   │   │   ├── first@3x.png
│   │   │   ├── second@2x.png
│   │   │   ├── second@3x.png
│   │   │   ├── song-list.vue
│   │   │   ├── third@2x.png
│   │   │   └── third@3x.png
│   │   ├── switches
│   │   │   └── switches.vue
│   │   └── top-tip
│   │       └── top-tip.vue
│   ├── common
│   │   ├── fonts
│   │   │   ├── music-icon.eot
│   │   │   ├── music-icon.svg
│   │   │   ├── music-icon.ttf
│   │   │   └── music-icon.woff
│   │   ├── image
│   │   │   └── default.png
│   │   ├── js                        // 组件中用到的一些方法
│   │   │   ├── cache.js
│   │   │   ├── config.js
│   │   │   ├── dom.js
│   │   │   ├── jsonp.js
│   │   │   ├── mixin.js
│   │   │   ├── singer.js
│   │   │   ├── song.js
│   │   │   └── util.js
│   │   └── stylus
│   │       ├── base.styl
│   │       ├── icon.styl
│   │       ├── index.styl
│   │       ├── mixin.styl
│   │       ├── reset.styl
│   │       └── variable.styl
│   ├── components
│   │   ├── add-song
│   │   │   └── add-song.vue
│   │   ├── disc
│   │   │   └── disc.vue
│   │   ├── m-header
│   │   │   ├── logo@2x.png
│   │   │   ├── logo@3x.png
│   │   │   └── m-header.vue
│   │   ├── music-list
│   │   │   └── music-list.vue         // 列表，是singer-detail中的子组件
│   │   ├── player
│   │   │   └── player.vue
│   │   ├── playlist
│   │   │   └── playlist.vue
│   │   ├── rank
│   │   │   └── rank.vue
│   │   ├── recommend
│   │   │   └── recommend.vue
│   │   ├── search
│   │   │   └── search.vue
│   │   ├── singer
│   │   │   └── singer.vue
│   │   ├── singer-detail
│   │   │   └── singer-detail.vue
│   │   ├── suggest
│   │   │   └── suggest.vue
│   │   ├── tab
│   │   │   └── tab.vue
│   │   ├── top-list
│   │   │   └── top-list.vue
│   │   └── user-center
│   │       └── user-center.vue
│   ├── main.js
│   ├── router
│   │   └── index.js
│   └── store
│       ├── actions.js
│       ├── getters.js
│       ├── index.js
│       ├── mutation-types.js
│       ├── mutations.js
│       └── state.js
└── static
    ├── 1.png
    ├── 2.png
    ├── 3.png
    ├── 4.png
    └── 5.png

```

###开源许可证 License AGPLv3

>开源是一种精神，vue2-music的开源更是人的一种进步

>开源是自由的，而不是免费的。Free(自由) is not free(免费)
请认真阅读并遵守以下开源协议

AGPLv3 [GNU Affero General Public License v3.0](https://github.com/HuangCongQing/vue2-music/blob/master/LICENSE)

此外，代码仅作学习vue所用，禁止私用，违者必究


# vue2-music


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)