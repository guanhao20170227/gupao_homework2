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
[3] 订阅者：
        Jedis jedis = new Jedis("192.168.119.141", 6379);
        final MyListener listener = new MyListener();
        // 使用模式匹配的方式设置频道
        // 会阻塞
        jedis.psubscribe(listener, new String[]{"qingshan-*", "news-*"});
```



