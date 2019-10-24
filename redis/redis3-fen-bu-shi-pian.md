作业大纲:

```
1 在三台虚拟机安装 Sentinel 集群, 一主两从:
2 搭建 Redis Cluster 3主3从;
3 了解 ShardedJedis 是如何实现数据分片的;
```

## 1 搭建Sentinel 集群

```
[1] 计划将 128, 129, 130, 131 四台服务器当做一个整体来处理;(一般不建议用偶数的, 可能会出现脑裂现象)
[2] 主从:
        把 131 当做主 Redis-Sentinel 节点;
        把 128, 129, 130 当做从 服务器;
[3] 配置文件的改动:
        (1) redis.conf 配置文件:
                1) 修改 上面 3 说的配置, 保证 Redis 集群, 可以正常的启动起来;
        (2) sentinel.conf 配置文件:
---
测试了: 可以实现 failover 功能;
---
注意点: 需要先把 Redis 启动起来在启动 Redis-Sentinel;
```

## 2 搭建 Redis Cluster 集群

```
1 在 192.168.119.131 这一台机器上面, 使用不同的端口号来实现:
    端口分别是: 7291, 7292, 7293, 7294, 7295, 7296;

-- 
测试实现了:
127.0.0.1:7291> dbsize
(integer) 6652
127.0.0.1:7291>
[root@localhost redis-5.0.5]# ./src/redis-cli -p 7292
127.0.0.1:7292> dbsize
(integer) 6683
127.0.0.1:7292>
[root@localhost redis-5.0.5]# ./src/redis-cli -p 7293
127.0.0.1:7293> dbsize
(integer) 6665
127.0.0.1:7293>
[root@localhost redis-5.0.5]# ./src/redis-cli -p 7294
127.0.0.1:7294> dbsize
(integer) 6665
127.0.0.1:7294>
[root@localhost redis-5.0.5]# ./src/redis-cli -p 7295
127.0.0.1:7295> dbsize
(integer) 6652
127.0.0.1:7295>
[root@localhost redis-5.0.5]# ./src/redis-cli -p 7296
127.0.0.1:7296> dbsize
(integer) 6683
127.0.0.1:7296>
--- 
也实现了:
(1) master 宕机的时候, slave 会被选举为 master；
(2) 通过 ./redis-cli --cluster add-node new-host:new-port exist_host:exist_port 来添加新的节点;
```

## 3 了解 ShardedJedis 是如何实现分片的?

```
根据网上的参考:
(1) Sharded Jedis 是通过 TreeMap 来实现 哈希环的;
(2) 是使用一致性哈希来实现 数据分片的
```

参考博客: [https://www.jianshu.com/p/d240af4a671c](https://www.jianshu.com/p/d240af4a671c)

---



