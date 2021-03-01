# MT_Timer（MT译为Multiple或Multi）

#### 一、介绍

一个Linux下的超级简洁的定时器：*利用epoll机制和timerfd新特性实现的多重、多用、多个定时任务实现*。只需要使用TIMER_CREATE()接口创建一个定时器实体，即**可向其添加成千上万个定时任务，定时任务可达到纳秒级别的精度，且可在同一时间点添加不同的定时任务！**。

#### 二、软件接口

整个定时器包含如下几类接口。

1. **创建和声明定时器实例**：使用定时器的第一步就是使用TIMER_CREATE()创建一个定时器实例，在其它文件使用到该定时器时，使用TIMER_DECLEAR()进行声明：
```
TIMER_CREATE(name);
TIMER_DECLEAR(name);
```

2. **初始化和反初始化定时器**：在正式使用定时器之前，首先使用TIMER_INIT()初始化前面创建的定时器实例，name是实例名称，max是创建定时器要检测的定时任务数量；当不再使用定时器时，可使用TIMER_DEINIT()反初始化定时器（退出定时器，并释放所有资源）：
```
TIMER_INIT(name, max);
TIMER_DEINIT(name);
```

3. **添加和删除定时任务**：
```
TIMER_ADD(name, itimespec, repeat, cb, data, rb);
TIMER_DEL(name, timerfd);
```

TIMER_ADD()用于向定时器实例name中添加一个定时任务，其参数描述如下：
- ittimespec是定时任务的定时时间和循环时间，其结构体类型如下：
```
struct timespec {
    time_t tv_sec;  // seconds
    long   tv_nsec; // nanoseconds
};
struct itimerspec {
    struct timespec it_value;
    struct timespec it_interval;
};
```

其中it_value即是超时时间（相对时间），若想定义周期定时任务，则设置it_interval成员；若不想定义周期定时任务，则需设置it_interval成员都为0。因此，第一次超时和后面周期定时任务是可以使用不同时间的。

- repeat是周期定时任务的重复次数，若设置为**-1，代表永远重复；0，代表一次都不执行**；因此repeat应至少为1，或者使用-1；
- cb为定时任务超时回调函数，其类型为：void (*timer_callback_t)(void *data)；
- data为定时任务回调函数的参数，为void *类型，用户可指定为自己定义的结构体；

TIMER_ADD()添加定时任务成功返回新定时任务的文件描述符，失败返回  
#include  
#include  

#include "mt_timer.h"

void timeout_handle(void *arg)
{
    printf("[%ld]:timeout1\n", time(NULL));
}

void timeout_handler(void *arg)
{
    printf("[%ld]:timeout2\n", time(NULL));
}

TIMER_CREATE(test);

int main(void)
{
    int timer;
    struct itimerspec itimespec;

    TIMER_INIT(test, 10);
    itimespec.it_value.tv_sec = 3;
    itimespec.it_value.tv_nsec = 0;
    itimespec.it_interval.tv_sec = 1;
    itimespec.it_interval.tv_nsec = 0;
    
    timer = TIMER_ADD(test, &itimespec, 8, timeout_handle, NULL);
    TIMER_ADD(test, &itimespec, 3, timeout_handler, NULL);
    printf("[%ld]:timer_add : %d\n", time(NULL), TIMER_COUNT(test));
    
    sleep(4);//getchar();
    TIMER_DEL(test, timer);
    printf("[%ld]:timer_del : %d\n", time(NULL), TIMER_COUNT(test));
    TIMER_CLEAR(test);
    printf("[%ld]:timer_clear : %d\n", time(NULL), TIMER_COUNT(test));
    getchar();

    TIMER_DEINIT(test);
    
    return 0;
}
```

#### 四、赞赏作者

![image](https://images.gitee.com/uploads/images/2019/0510/144101_bc93efba_3026819.jpeg)

#### 五、参与贡献

1. Fork 本仓库
2. 新建 Feat_xxx 分支
3. 提交代码
4. 新建 Pull Request


#### 六、码云特技

1. 使用 Readme\_XXX.md 来支持不同的语言，例如 Readme\_en.md, Readme\_zh.md
2. 码云官方博客 [blog.gitee.com](https://blog.gitee.com)
3. 你可以 [https://gitee.com/explore](https://gitee.com/explore) 这个地址来了解码云上的优秀开源项目
4. [GVP](https://gitee.com/gvp) 全称是码云最有价值开源项目，是码云综合评定出的优秀开源项目
5. 码云官方提供的使用手册 [https://gitee.com/help](https://gitee.com/help)
6. 码云封面人物是一档用来展示码云会员风采的栏目 [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)

 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)