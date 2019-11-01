作业大纲:

```
1、一个任务10秒钟触发一次，但是每次执行需要60秒，在第20秒的时候，会同时运行两个任务吗？怎么禁止一个任务并发运行？
2、现在有三个任务，任务A、任务B、任务C，怎么让多个任务串行执行，例如A执行完了之后再执行B，B执行完了再执行C？
3、除了执行本地的代码之外，怎么调用其他系统的任务？
4、任务在什么时候会错过触发？错过触发怎么办？
```

## 1 会执行两个任务吗？ 怎么样禁止任务的并发执行?

答:  在 20 秒的时候, 回执行第二个任务的, Quartz 默认是多线程的;

如果想要将 Job 变成单线程 需要在 Job 实现类上加上 @DisallowConcurrentExecution 注解;

如果是 spring 工程, 需要给 Job Bean 添加: &lt;property name="concurrent" value="true"&gt;&lt;/property&gt;

c参考博客: [https://www.cnblogs.com/Rozdy/p/4220186.html](https://www.cnblogs.com/Rozdy/p/4220186.html)

--

具体的实现:

job:

test:



## 2 怎样使多个任务串行执行?


