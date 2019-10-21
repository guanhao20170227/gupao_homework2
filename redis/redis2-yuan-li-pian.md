作业大纲:

```
1、    Jedis中，如何取消对频道的订阅？
2、    为什么在一个事务中存在错误，Redis不回滚？
3、    Redis不是只有一个线程吗？它已经卡死了，怎么接受spript kill指令的？
4、    基于一个数据结构，如何设计一个传统的LRU算法？
```

## 1 Jedis 如何取消对频道的订阅？

```
[1] 需要引入一个监听器： MyListener extends JedisPubSub;
[2] 发布者:
        Jedis jedis = new Jedis("192.168.119.141", 6379);
        jedis.publish("qingshan-123", "666");
        jedis.publish("qingshan-abc", "pengyuyan");
        jedis.publish("news-weather", "rain");
        jedis.publish("news-sport", "yaoming");
[3] 订阅者：
        Jedis jedis = new Jedis("192.168.119.141", 6379);
        final MyListener listener = new MyListener();
        // 使用模式匹配的方式设置频道
        // 会阻塞
        jedis.psubscribe(listener, new String[]{"qingshan-*", "news-*"});

---
源码位置: G:\BaiduNetdiskDownload\Java\咕泡学习\5_分布式与微服务\02.redis\
                        redis_2 原理\3_课堂源码\gupao-jedis\src\main\java\pubsub>
```

参考博客:  [https://www.cnblogs.com/excellencesy/p/11696580.html](https://www.cnblogs.com/excellencesy/p/11696580.html)

## 2 为什么在一个事务中存在错误，Redis不回滚？

```
答:
-- 不需要回滚 
只有发生语法错误的时候, Redis 命令才会执行失败, 或是对 keys 赋予一个类型错误的数据,
    这就意味着这些程序是有问题的, 所以是需要修改程序, 这个问题是不会出现在生产的环境上的。
-- 不能回滚:
Redis 事务主要用于不间断的执行多条命令, 即是存在引发错误额命令. Redis 先执行命令, 命令成功后,
    才会记录日志, 所以出现错误时无法回滚.
```

参考博客: [https://baijiahao.baidu.com/s?id=1613631210471699441픴=spider&for=pc](https://baijiahao.baidu.com/s?id=1613631210471699441&wfr=spider&for=pc)

[https://www.oschina.net/question/2426118\_2303633](https://www.oschina.net/question/2426118_2303633)

## 3 Redis不是只有一个线程吗？它已经卡死了，怎么接受spript kill指令的？

```
使用 script kill, 是在 调用 Lua 脚本超时的时候使用的;
(1) script 还可以使用是由于在 redis.conf 配置文件中配置了 lua-time-limit 5000; 5 秒;
      5 秒内是不接受任何命令, 5 秒后是可以接受命令的, 但是不执行命令;
(2) 由于 Lua 脚本的引擎功能比较强大, 他会提供各种各样的钩子函数, 它允许在内部虚拟机执行指令时运行钩子代码,
      Redis 正是使用了这个钩子函数。
      Redis 在发现Lua 脚本超时后, 就会在钩子函数里面去处理客服端的请求;
```

参考博客：[https://blog.csdn.net/qq\_16605855/article/details/83305942](https://blog.csdn.net/qq_16605855/article/details/83305942)

## 4 基于一个数据结构，如何设计一个传统的LRU算法？

```
方法1： 基于 Redis 的 List, 加上 rpush, lpop 就可以实现 LRU 了;

方法2: Cache 链表 + hashMap 实现:
```

方法2参考博客: [https://www.cnblogs.com/lzrabbit/p/3734850.html\#f2](https://www.cnblogs.com/lzrabbit/p/3734850.html#f2)

---

