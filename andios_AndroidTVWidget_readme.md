# Android TV 开发框架

使用说明: 

   https://git.oschina.net/hailongqiu/AndroidTVWidget/wikis/AndroidTVWidget-use-manual

键盘使用说明:
   
   https://git.oschina.net/hailongqiu/AndroidTVWidget/wikis/Android-TV-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8%E9%94%AE%E7%9B%98%E6%8E%A7%E4%BB%B6%28SkbContainer%29

项目导入说明:
   
   https://git.oschina.net/hailongqiu/AndroidTVWidget/wikis/AndroidTVWidget-use-manual%28Android-Studio%29

   https://git.oschina.net/hailongqiu/AndroidTVWidget/wikis/AndroidTVWidget-use-manual%28Eclipse%E5%AF%BC%E5%85%A5%29


 欢迎进入 TV开发，希望大家不断的分享代码，一起进步，谢谢. （hailongqiu 356752238@qq.com）
  
![输入图片说明](http://git.oschina.net/uploads/images/2016/0223/094451_e49419a7_111902.png "在这里输入图片标题")
 

天天加班加点，欢迎支持

![天天加班加点，欢迎支持](http://git.oschina.net/uploads/images/2016/0310/133650_1cc016cc_111902.png "天天加班加点，欢迎支持")


##Tab 测试DEMO图片.

![输入图片说明](http://git.oschina.net/uploads/images/2016/0229/221023_f9d44844_111902.jpeg "倒影效果")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0229/221031_38ff3206_111902.jpeg "倒影效果")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0227/220443_88e33e8c_111902.jpeg "在这里输入图片标题")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0227/211816_859f799a_111902.jpeg "在这里输入图片标题")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0227/211824_0fec2486_111902.jpeg "在这里输入图片标题")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0227/142535_a93ea19c_111902.jpeg "在这里输入图片标题")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0227/030817_cbece78a_111902.png "在这里输入图片标题")

![输入图片说明](http://git.oschina.net/uploads/images/2016/0223/190022_02e85c54_111902.png "ListVie的支持")

当ListView中有一些抢焦点的控件的时候，请使用 setDescendantFocusability ... ... 比如 Button，EditText

![输入图片说明](http://git.oschina.net/uploads/images/2016/0223/190048_e9e0be4c_111902.png "GridView的支持")

![标题栏](http://git.oschina.net/uploads/images/2016/0224/150241_7657d29b_111902.png "标题栏")

【MainUpView 部分API】
   
   private static int TRAN_DUR_ANIM = 300; // 控件动画的时间.(默认时间，建议不更改)
   
   public void setTranDurAnimTime(int time) { // 控件动画的时间.
   
   public void runTranslateAnimation(View toView, float scaleX, float scaleY) { // 边框移动到那个焦点控件.
   
   public void setFocusView(View view, float scale) { 设置焦点子控件的移动和放大.
   
   public void setUnFocusView(View view) { 设置无焦点子控件还原.
   
   public void setDrawUpRectPadding(int size) { 根据图片边框 自行 填写 相差的边距.

   public void setDrawUpRectPadding(Rect rect) { 根据图片边框 自行 填写 相差的边距.
   
   public void setShadowDrawable(Drawable shadowDrawable) {  当图片边框不自带阴影的话，可以自行设置阴影图片.
   
   public void setShadowResource(int resId) {
   
   public void setUpRectDrawable(Drawable upRectDrawable) { 设置移动边框，也是最上层的边框
   
   public void setUpRectResource(int resId) {
   
   // 设置 setDrawUpRectEnabled 类似图片中的小人，如果想让小人在最上面，需要设置这个属性.
   
   public void setDrawUpRectEnabled(boolean isDrawUpRect) { // 设置是否移动边框在最下层. true : 移动边框在最上层. 反之否.
   
   public void setTvScreenEnabled(boolean isTvScreen) { // 是否是TV的设备
   
   public boolean isTvScreenEnabled() {
   
   public void setInDraw(boolean isInDraw) { // 屏蔽 阴影，倒影，子控件的绘制.
   
【需要倒影功能 XML布局就可以设置 app:isReflect="false" 默认为 true ，有倒影，如果无法满足，请查看代码，自行修改】

  
 XiaoMi android_tv_metro  
 
 
 BorderViewDemo 
 

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)