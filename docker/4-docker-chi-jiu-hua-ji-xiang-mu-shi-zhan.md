作业大纲:

```
01 MySQL高可用集群搭建，采用percona xtradb cluster的方案
02 Nginx+3个Spring Boot项目[这个放到了网盘源码的目录]+MySQL[sql语句也放到了网盘源码的目录] 容器化方案的搭建
```

## 1 pxc 搭建 Mysql 的高可用的方案:

pxc 的8888 端口的监控:

![](/assets/import_20191108213601.png)

## 2 搭建 多个 spring-boot 项目的实例:

\[1\] weaveworks/scope 来监控的实例：

![](/assets/import_20191109114501.png)

将 nginx 的ip 172.22.0.11/12/13 换成 sb01/sb02/sb03 是可以的, 但是要保留 8080 的端口, 但是在 spring-boot 项目中 my-mysql 替换 aliyun\_ip:3306 中 my-mysql 后面是不要添加端口的;

---

