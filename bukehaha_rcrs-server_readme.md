# `rcrs-server` Robocup Rescue Simulation Server

(Linux) Instructions to download, build and run the RoboCup Rescue Simulator (RCRS)

## 1. Software Pre-Requisites

- Git
- Gradle 6.1.1+
- OpenJDK Java 8+

## 2. Download project from GitHub

```bash

$ git clone git@github.com:roborescue/rcrs-server.git
```

## 3. Compile

```bash

$ ./gradlew clean

$ ./gradlew completeBuild
```

## 4. Execute

Open a terminal window, navigate to the ```rcrs-server``` root directory and execute

```bash

$ cd boot

$ ./start.sh -m ../maps/gml/test/map -c ../maps/gml/test/config
```

Open another terminal window, navigate to the ```rcrs-server``` root directory and execute

```bash

$ cd boot

$ ./sampleagent.sh
```

## 5. Support

To report a bug, suggest improvements or request support, please open an issue at GitHub  .

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)