# easyAi
本包说明：
* 本包原名imageMarket,因为开始加入自然语言模块，所以之后更名为easyAi
* 本包对物体在图像中进行训练及识别，切割，定位的轻量级，面向小白的框架,功能在逐渐扩展中
* 本包对中文输入语句，对输入语句的类别进行分类，功能在逐渐扩展中
* 若有想扩充的功能请进群提意见，若是通用场景我会陆续补充，技术交流群：561433236
## 详细视频教程地址：
* 视频教程地址：https://www.bilibili.com/video/av89134035
## 框架效果演示结果:
* 因为是框架没有图像化界面，演示结果就是控制台输出的数据，只能用视频展示，想看演示结果请看教学视频
## 控制台输出演示
* 演示都是输出结果，详情请看具体视频教程，上有链接，这里就是展示一下控制台输出截图。
* 单物体识别效果：[点击查看](./src/test/image/end1.png)
* 多物体识别效果：[点击查看](./src/test/image/end2.png)
* 中文语言分类效果：[点击查看](./src/test/image/end3.png)
### 目前拥有的功能是
* 对单张图片单物体进行识别
* 对单张图片多物体进行识别与定位
* 对中文语言进行分类语义识别,判断用户说话的语义是什么，要做什么
* 若有想扩充的功能请进群提意见，若是通用场景我会陆续补充，技术交流群：561433236
### 目的是
* 低硬件成本，CPU可快速学习运行，面向jAVA开发的程序员，经过简单API调用就可实现物体在图像中的识别，定位及中文语言分类等功能
* 努力为中小企业提供AI场景解决技术方案
* 技术交流群：561433236
### 特点是
入手门槛低，简单配置，快速上手
#### 为什么做这个包
* 低门槛化：
现在随着人工智能技术的兴起，很多场景需要开发人员添加相应的功能，但是在二三线城市算法人才匮乏。
并且大多是JAVA开发程序员，业务做的更多，因为作者本人就是三线城市程序员，所以深知这一点。
所以我本人认为需要一款部署简单，不需要学习任何算法知识，
只通过最简单的API调用，就可以实现部分人工智能应用，并面向覆盖面最广的JAVA程序员使用的，且
能满足大部分AI业务场景实现的技术包。
* 面向用户：广大没接触过算法知识，人才相对匮乏的二三线JAVA业务开发程序员，实现人工智能应用
* 部署简单：
本包所有底层函数及数学库都是作者JAVA手写，不依赖任何第三方库，所以开发者只需要将本包下载到本地后，打成JAR包
引入到自己的POM文件中，就可以独立使用所有功能。
* 功能还在扩展：
本包现在的功能还在逐步扩展中
* 抛错捕获暂时还没有做全，若有抛错请进群交流：561433236，我来做一下错误定位
## 图像部分最简API 说明:
    public static void testPic() throws Exception {
           //测试SPEED模式学习过程
           //初始化图像转矩阵类:作用就是说将一个图片文件转化为矩阵类
           Picture picture = new Picture();
           //初始化配置模板类,设置模式为SPEED_PATTERN模式 即速度模式
           TempleConfig templeConfig = getTemple(true, StudyPattern.Speed_Pattern);
           //初始化计算类，并将配置模版和输出回调类载入计算类
           //运算类有两个构造一个是配置回调类，一个是不配置回调类
           //若使用定位功能，则无需配置回调类，若不启用，则要配置回调类
           //回调类要实现OutBack接口中的方法
           Ma ma = new Ma();
           Operation operation = new Operation(templeConfig, ma);
           //标注主键为 第几种分类，值为标注 1 是TRUE 0是FALSE
           //给训练图像进行标注，健是分类的ID,对应的就是输出结果的ID值，值要么写0要么写1
           // 1就是 是这种分类，0就是不是这种分类
           Map  rightTagging = new HashMap<>();//分类标注
           Map  wrongTagging = new HashMap<>();//分类标注
           rightTagging.put(1, 1.0);
           wrongTagging.put(1, 0.0);
           // 例如上面的标注了 只有一种分类，第一个MAP是true标注，第二个map是false标注
           for (int i = 1; i  > map = operation1.lookWithPosition(right, 4);
       }
   
       public static TempleConfig getTemple(boolean isFirst, int pattern) throws Exception {
           //创建一个配置模板类，作用：主要是保存及载入一些配置参数用
           TempleConfig templeConfig = new TempleConfig();
           //全连接层深度,选填可不填 不填默认值为2
           //这就像人类大脑的意识深度原理一样，深度学习越深，训练结果越准，但是训练量成几何倍数增加
           //比如默认深度是2 需要 正负模板各一千+张照片进行训练。识别率70%（数值只是举个例子，不是具体数值）
           //当深度改成3，则需要正负模板各三千+张照片进行训练,识别率 80%，深度4，八千+90%
           //以此类推，，内存允许的情况下，深度无限 识别率无限接近与百分之百
           //但是有极限，即超过某个深度，即使再增加深度，识别率反而会下降。需要具体不断尝试找到 合适的深度
           //注意：若深度提升，训练量没有成倍增长，则准确度反而更低！
           templeConfig.setDeep(2);
           //启用定位学习 注意启用在图片中对某个物体进行定位，要注意
           //学习的图片必须除了学习的物体以外，其他位置都是白色或者空白(即用PS扣空)。
           //即该图片除了这个物体，没有其他任何干扰杂色（一个像素的杂色都不可以有）
           //templeConfig.setHavePosition(true);
           //窗口类，就是用来扫描图片的窗口大小和移动距离的设定
           //Frame frame = new Frame();
           //初始化配置模版，参数说明(int studyPattern, boolean initPower, int width, int height
           //, int classificationNub)
           //studyPattern 学习模式：常量值 StudyPattern.Accuracy_Pattern;StudyPattern.Speed_Pattern
           //第一种模式精准模式，第二种模式是速度模式
           //精准模式顾名思义，准确相对高很多，但是缺点也很明显学习速度慢，不是一般的慢，CPU学习1000张图片
           //24小时都不够用！它学习速度比速度模式学习速度慢十倍都不止！但是执行识别速度上，却比速度模式还要快一点！
           //第二种速度模式，学习速度明显很快，一千张图片的学习大概一个半小时左右，但是精准度上差了一些
           //但是依然还是比较精准的，尤其做分类判断的时候，问题不大。
           //如何选择模式：在大部分情况下速度模式就够用了，在分类一张图片，比如这张图片有苹果的概率是多少
           //有橘子的概率是多少，精准度已经足够，它不是不精准，只是相对于精准模式要差一些
           //所以在大部分情况下，还是建议用速度模式，满足很多识别分类需求
           //initPower,是否是第一次初始化
           //学习就是学的模型参数，学完了要把模型参数类拿出来，序列化成JSON字符串，保存数据库
           //下次服务启动，读取JSON字符串，反序列化为MODEL模型 直接注入就可，无需再次学习
           //如果说你是要学习就写true,如果已经有学习结果了，你要注入之前的学习结果就是false
           //如果你选了false还没有进行注入的话，你取模型参数你可以看到所有参数都是0
           //width heigth ,要学习的图片宽高，注意：这个宽高不是严格图片尺寸，而是一个大致尺寸
           //要识别和学习的图片尺寸与这个宽高比 必要相差太大就好，而且宁长勿短
           //classificationNub 要识别的有几个分类，比如我就识别苹果，就是1 有两种苹果橘子就是 2
           templeConfig.init(pattern, isFirst, 3204, 4032, 1);
   
           return templeConfig;
       }
   
       public static void testPic2() throws Exception {
           //测试Accuracy_Pattern 模式学习过程，跟SPEED模式相同的部分就不再说明了
           Picture picture = new Picture();
           TempleConfig templeConfig = getTemple(true, StudyPattern.Accuracy_Pattern);
           Operation operation = new Operation(templeConfig);
           for (int i = 1; i   list = talk.talk("帮我配把锁");
        System.out.println(list);
        //这里做一个特别说明，语义分类的分类id不要使用"0",本框架约定如果类别返回数字0，则意味不能理解该语义，即分类失败
        //通常原因是模板量不足，或者用户说的话的语义，不在你的语义分类训练范围内
    }
## 神经网络最简API说明
     //创建一个DNN神经网络管理器
     NerveManager nerveManager = new NerveManager(...);
     //构造参数
     //sensoryNerveNub 感知神经元数量 即输入特征数量
     //hiddenNerverNub  每一层隐层神经元的数量
     //outNerveNub 输出神经元数量 即分类的类别
     //hiddenDepth 隐层神经元深度，即学习深度
     //activeFunction 激活函数
     //isDynamic 是否启用动态神经元数量(没有特殊需求建议为静态，动态需要专业知识)
     public NerveManager(int sensoryNerveNub, int hiddenNerverNub, int outNerveNub, int hiddenDepth, ActiveFunction activeFunction, boolean isDynamic)
     nerveManager.getSensoryNerves()获取感知神经元集合
     //eventId:事件ID
     //parameter:输入特征值
     //isStudy:是否是学习
     //E:特征标注
     //OutBack 回调类
     SensoryNerv.postMessage(long eventId, double parameter, boolean isStudy, Map  E, OutBack outBack)
     //每一次输出结果都会返回给回调类，通过回调类拿取输出结果，并通过eventId来对应事件
## 随机森林最简API说明
        //创建一个内存中的数据表
        DataTable dataTable = new DataTable(column);
        //构造参数是列名集合
        public DataTable(Set  key)
        //指定主列名集合中该表的主键
        dataTable.setKey("point");
        //创建一片随机森林
        RandomForest randomForest = new RandomForest(7);
        //构造参数为森林里的树木数量
        public RandomForest(int treeNub)
        //唤醒随机森林里的树木
        randomForest.init(dataTable);
        //将加入数据的实体类一条条插入森林中
        randomForest.insert(Object object);
        //森林进行学习
        randomForest.study();
        //插入特征数据，森林对该数据的最终分类结果进行判断
        randomForest.forest(Object objcet);
### 常见抛错
* error:Wrong size setting of image in templateConfig
* 原因是模版配置类图片宽高设置相差太大
> templeConfig.init(StudyPattern.Accuracy_Pattern, true, width, height, 1);
#### 最终说明
* TempleConfig()：配置模版类，一定要静态在内存中长期持有，检测的时候不要每次都NEW，
一直就使用一个配置类就可以了。
* Operation():运算类，除了学习可以使用一个以外，用户每检测一次都要NEW一次。
因为学习是单线程无所谓，而检测是多线程，如果使用一个运算类，可能会造成线程安全问题
#### 精准模式和速度模式的优劣
* 速度模式学习很快，但是检测速度慢，双核i3检测单张图片（1200万像素）单物体检测速度约800ms.
学习1200万像素的照片物体，1000张需耗时1-2小时。
* 精准模式学习很慢，但是检测速度快，双核i3检测单张图片（1200万像素）单物体检测速度约100ms.
学习1200万像素的照片物体，1000张需耗时5-7个小时。
#### 本包为性能优化而对AI算法的修改
* 本包的自然语言是通过内置分词器进行语句分词，然后再通过不同分词的时序进行编号成离散特征，最后进入随机森林分类
* 本包对图像AI算法进行了修改，为应对CPU部署。
* 卷积层不再使用权重做最终输出，而是将特征矩阵作出明显分层的结果。
* 卷积神经网络后的全连接层直接替换成了LVQ算法进行特征向量量化学习聚类，通过卷积结果与LVQ原型向量欧式距离来进行判定。
* 物体的边框检测通过卷积后的特征向量进行多元线性回归获得，检测边框的候选区并没有使用图像分割（cpu对图像分割算法真是超慢），
而是通过Frame类让用户自定义先验图框大小和先验图框每次移动的检测步长，然后再通过多次检测的IOU来确定是否为同一物体。
* 所以添加定位模式，用户要确定Frame的大小和步长，来替代基于图像分割的候选区推荐算法。
* 速度模式是使用固定的边缘算子进行多次卷积核，然后使用BP的多层神经网络进行强行拟合给出的结果（它之所以学习快，就是因为速度模式学习的是
全连接层的权重及阈值，而没有对卷积核进行学习）
* 本包检测使用的是灰度单通道，即对RGB进行降纬变成灰度图像来进行检测（RGB三通道都算的话，CPU有些吃不住）。
* 若使用本包还有疑问可自行看测试包内的HelloWorld测试案例类，或者联系作者Q：794757862


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)