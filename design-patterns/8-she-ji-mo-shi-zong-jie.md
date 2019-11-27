作业大纲:

```
1、用一句自己的话总结学过的设计模式（要精准）。
2、列举SpringAOP、IOC、DI应用的代码片段。
```

## 1 用一句自己的话总结学过的设计模式:

| 设计模式 | 一句话归纳 | 举例 |
| :--- | :--- | :--- |
| 工厂模式\(Factory\) | 只对结果负责, 封装创建的过程. | BeanFactory, Calendar; |
| 单例模式\(Singleton\) | 保证独一无二 | ApplicationContext, Calendar; |
| 原型模式\(Prototype\) | 拔一根猴毛, 吹出千万个 | ArrayList, PrototypeBean |
| 代理模式\(Proxy\) | 找人办事, 增强职责 | ProxyFactoryBean, JdkDynamicAopProxy, CglibAopProxy; |
| 委派模式\(Delegate\) | 干活你的\(普通员工\), 功劳算我的\(项目经理\) | DispatcherServlet, BeanDefinitionParseDelegate; |
| 策略模式\(Strategy\) | 用户选择, 结果统一 | InstabtiationStrategy |
| 模板模式\(Template\) | 流程标准化, 自己实现定制 | JdbcTemplate, HttpServlet |
| 适配器模式\(Adapter\) | 兼容转接头 | AdvisorAdapter, HandlerAdapter |
| 装饰器模式\(Decorator\) | 包装, 同宗同源 | BufferReader, InputStream, OutputStream, HttpHeadResponseDecorator |
| 观察者模式\(Observer\) | 任务完成通知 | ContextLoaderListener |



2 列举SpringAOP、IOC、DI应用的代码片段:

