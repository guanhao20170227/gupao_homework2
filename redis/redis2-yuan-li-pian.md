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

```



