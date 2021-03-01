# tensorflow2.0 for Chinese GPT2 

## 近期更新(持续修改中。。。)
打pb方法已经更新，可以参考我的另一个项目中的做法[ner打pb方法](https://github.com/Coder-nlper/chinese-ner-tf2)
## 说明
参考使用 HuggingFace的[transformers](https://github.com/huggingface/transformers)实现GPT2模型的编写与训练。
整体想法来源微软论文[Large-scale Pretrained Response Generation Model (DialoGPT)](https://arxiv.org/abs/1911.00536)原文实现[代码](https://github.com/microsoft/DialoGPT)
使用50W中文闲聊语料进行训练。
## 运行环境
python3.6、 tensorflow==2.1.0
## 训练说明
训练时，将一条训拼接，如 **"[SOS]四级过了没？[SEP]两次都只差多分。[SEP]心疼你三秒钟[SEP]不着急，慢慢来。急不来的，[SEP]
你慢慢吧我着急六级[SEP]人家四级没过你就要过六级了。[SEP]都加油[SEP]加油！[SEP]"**
```
四级过了没？
两次都只差多分。
心疼你三秒钟
不着急，慢慢来。急不来的，
你慢慢吧我着急六级
人家四级没过你就要过六级了。
都加油
加油！
```
50W条语料在data/目录下，data/ids目录是50W条语料转id后的结果

## 训练执行：
```
         python3 train.py
```
## inference执行:
```
         python3 infer.py
```
## 参考资料
感谢[GPT2-chitchat](https://github.com/yangjianxin1/GPT2-chitchat)项目中提供50W条聊天语料[百度网盘【提取码:osi6】](https://pan.baidu.com/s/1qDZ24VKLBU9GKARX9Ev65g)

openai的[GPT2](https://github.com/openai/gpt-2.git)源代码以及其inference代码


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)