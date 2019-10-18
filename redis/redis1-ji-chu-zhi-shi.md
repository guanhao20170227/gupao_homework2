作业大纲

```
1、Redis为什么要自己实现一个SDS？
2、基于Set如何实现用户关注模型？
3、总结Redis五大数据类型，和编码转换的条件
```

# 1 Redis 为什么要自己实现一个 SDS？

答:  由于 Redis 是用 C 语言编写的, 然而 C 语言是没有 string 类型的, C 中是用 以 '\0' 结束的字符串数组 char\[\] 来保存字符串数据的;

要是我们也用 char\[\] 数组来保存 string, 当 string 中保存 图片, 音频, 视频 等二进制文件的时候, 可能会出现 '\0' 而被截断, 从而出现二进制不安全的问题;

```
还有一些其他的原因:
1 char[] 数组需要先给出变量空间的大小, 可能会导致内存溢出的情况;
2 char[] 数组获取字符串的长度, 时间复杂度是 O(n);
3 char[] 长度的变更会导致内存需要重新分配
4 二进制安全;
```

实现 SDS 后的好处:

```
1 不用担心内存溢出;
2 获取字符长度的时间复杂度是 O(1);
3 通过 "空间预分配" 和 "惰性空间释放" 防止多次重分配内存;
4 判断结束的标志是 len 属性, 不是 '\0';
```

# 2 基于 Set 实现 用户关注模型:

我是基于 zset 来实现的

```
场景: 
人物: A, B; 人物的属性: 我的粉丝-fans, 我的关注-follow, 互粉-mutual;
--
(1) A 关注 B, B 不关注 A;
eg: A 关注 B
    1) zadd A:follow time B;
    2) zadd B:fans time A;
(2) A, B 相互关注:
    eg:
        A 关注 B;
            1) zadd A:follow time B;
            2) zadd B:fans time A;
        B 关注 A;
            1) zadd B:follow time A;
            2) zadd A:fans time B;
(3) 判断结果：
    1) 我(A)单向关注对方(B):
        zscore A:follow B #true
        zscore A:fans B #false
    2) 他(B)单向关注了我(A):
        zscore A:follow B #false
        zscore A:fans B #true
    3) A, B 相互关注:
        zscore A:follow B #true
        zscore A:fans B #true
```

# 3 总结Redis五大数据类型，和编码转换的条件

![](/assets/import_20191018212401.png)

---



