作业大纲:

```
1、布隆过滤器为什么不支持删除？如何让BF支持删除的功能？
2、绘制一张Redis知识脑图，放在git，贴地址？
```

## 1 布隆过滤器为什么不支持删除？如何让BF支持删除的功能？

```
布隆过滤器存储的是一种函数关系，不是存储的真实数据，如果要删除，需要修改函数关系，而且还不只是一个函数，
是一组函数，因此实现起来困难，所以不支持删除。
如果要让BF支持删除的功能，使用带计数器的布隆过滤器，现在已经有第三方实现了CountingBloomFilter，
原理就是当删除时计数减一。
--
有人提出了一种基于 D-left Hash 方法实现支持删除操作的布隆过滤器，同时空间效率也比Counting filters高。
```

参考文档: 主要参考了 zelioer 同学 和 秦啸 同学的作业:

## 2 绘制一张Redis知识脑图，放在git，贴地址？

github : [https://github.com/guanhao20170227/gupao\_homework2/blob/master/xmindfile/Redis.xmind](https://github.com/guanhao20170227/gupao_homework2/blob/master/xmindfile/Redis.xmind)



