# go_rocket_mq
go rocketmq client
#import
import rocketmq "github.com/didapinchegit/go_rocket_mq"

#example
	conf := &rocketmq.Config{
		Nameserver:   "192.168.1.234:9876",
		ClientIp:     "192.168.1.23",
		InstanceName: "DEFAULT",
	}
	consumer, err := rocketmq.NewDefaultConsumer("C_TEST", conf)
	if err != nil {
		log.Panic(err)
	}
	consumer.Subscribe("test2", "*")
	consumer.Subscribe("test3", "*")
	consumer.RegisterMessageListener(func(msgs []*rocketmq.MessageExt) error {
		for i, msg := range msgs {
			log.Print(i, string(msg.Body))
		}
		return nil
	})
	consumer.Start()


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)