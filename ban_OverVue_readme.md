 
   
   
  OverVue (Beta)
 

  Prototyping Tool for Vue Developers  

 OverVue is a prototyping tool that allows developers to  dynamically  create and visualize a Vue application, implementing a real-time intuitive  tree display  of component hierarchy and a live-generated  code preview . The resulting boilerplate can be  exported  as a template for further development. 

 这个程序能帮你生成Vue 组件, 设置 routes , 也可以帮你显像Component Parent-Child组件树。你只要做一些小配置然后可以下载code boilerplate. 这样你就可以很方便简洁地生成Vue前台APP了！ 

![](https://raw.githubusercontent.com/jeisele2/OverVue/master/src/assets/gifs/screenshot.png)

#### Features
+ Upload a frontend mockup image
+ Visualize draggable and resizable components
+ Create parent-child hierarchy of components
+ Add html elements to components
+ Create routes to be used by Vue Router
+ Live-generated previewable code snippets for each component
+ Live-generated tree view to aid in visualizing parent-child hierarchy
+ Save projects and open previous projects
+ Export full boilerplate code for a working frontend


#### How to use
+ Opening the application will create by default a root App component and a root route called "HomeView"
+ Upload a mockup from your filesystem if you'd like. Remove the mockup and choose a new one if needed.
![](https://raw.githubusercontent.com/jeisele2/OverVue/master/src/assets/gifs/upload-image-drawers.gif)

+ To add a new component, type its name in the component name box and select any HTML elements that should be rendered by that component.
+ HTML elements can also be added after creation by selecting the component in the display, then selecting HTML elements.
+ Select a parent component for the new component if needed.
+ After adding, you can move and resize the component in the display.
![alt text](https://raw.githubusercontent.com/jeisele2/OverVue/master/src/assets/gifs/component_creation.gif)

+ You can also add children to components by right-clicking the component to add children to, and you can see the tree re-render as you create new components or change the hierarchy.
![](https://raw.githubusercontent.com/jeisele2/OverVue/master/src/assets/gifs/HTML-elements-tree-rerender.gif)

+ The dashboard shows info about each component (code snippets and HTML elements). Click a component in the display to see its properties.                                               
![](https://raw.githubusercontent.com/jeisele2/OverVue/master/src/assets/gifs/snippets-active-component.gif)

+ You can add new routes and view all components and routes in the sidebar.
![](https://raw.githubusercontent.com/jeisele2/OverVue/master/src/assets/gifs/sidebar-components-routes.gif)

+ When finished creating, you can export to a file location of your choice. Below is the exported file structure:

```
public/
  index.html
src/
  assets/
  components/
    UserCreatedComponent1.vue
    UserCreatedComponent2.vue
    ...
  views/
    HomeView.vue
    UserCreatedRouteComponent1.vue
    UserCreatedRouteComponent2.vue
    ...
  App.vue
  main.js
  router.js
babel.config.js
package.json
```

#### Running a local version
This app was developed using the Quasar framework, so first you will need to install the Quasar cli
```
npm i -g @quasar/cli
```
Install dependencies
```
npm i
```
To run electron app in dev mode
```
quasar dev -m electron
```
To build a new .dmg
```
quasar build -m electron
```

#### Contributing
We'd love for you to test this application out and submit any issues you encounter. Also feel free to fork to your own repo and submit PRs.
Here are some features we're thinking about adding:
+ Vuex state prototyping and boilerplate export
+ Ability to add additional mockup images for more routes
+ Ability to nest HTML elements
+ Option to export files in TypeScript

#### Authors
```
Contributors:
Joseph Eisele @jeisele2
Dean Chung @deanfchung
Dean Ohashi @dnohashi
Drew Nguyen @drewngyen
```
Inspired by [PreVue](https://github.com/open-source-labs/PreVue)


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)