作业大纲

```
1、思考并总结装饰者模式和适配器模式的根本区别。
2、用Guava API实现GPer社区提问通知的业务场景。
```

## 1 思考并总结装饰者模式和适配器模式的根本区别。

```
                装饰器模式                                适配器模式
形式                是一种非常特别的适配器模式                 没有层级关系, 装饰器模式有层级关系
定义                装饰器类和被装饰器类继承同一个接口          适配器与适配者之间没有关系, 通常采用
                      主要是为了扩展之后依旧保留 OOP 关系         继承或是代理进行包装;
关系                 满足 is-a 关系(继承)                          满足 has-a 关系(持有引用)
功能                 注重覆盖, 扩展                                注重兼容, 转换
设计                 前置考虑                                      后置考虑                     
```

## 2 用Guava API实现GPer社区提问通知的业务场景。

EventBusCenter

```
public class EventBusCenter {

    private static EventBus eventBus = new EventBus();

    private EventBusCenter() {}

    public static EventBus getInstance() {
        return eventBus;
    }

    public static void register(Object obj) {
        eventBus.register(obj);
    }

    public static void unregister(Object obj) {
        eventBus.unregister(obj);
    }

    public static void post(Object obj) {
        eventBus.post(obj);
    }

}
```

teacher1:

```
public class Teacher1 {

    private String name;

    public Teacher1(String name) {
        this.name = name;
    }

    @Subscribe
    public void getQuestion(Question question) {
        System.out.printf("%s 老师, 接受到 来自 %s 的问题， 具体的问题是: \n %s",
                this.name, question.getUsername(), question.getContent());
    }
}
```

teacher2:

```
public class Teacher2 {

    private String name;

    public Teacher2(String name) {
        this.name = name;
    }

    @Subscribe
    public void getQuestion(Question question) {
        System.out.printf("%s 老师, 接受到 来自 %s 的问题， 具体的问题是: \n %s",
                this.name, question.getUsername(), question.getContent());
    }
}
```

Question:

```
public class Question {

    private String username;// 提出问题人
    private String content; // 问题的内容



    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```

Test:

```
public class Test {

    public static void main(String[] args) {

        Teacher1 teacher1 = new Teacher1("Tom");
        Teacher2 teacher2 = new Teacher2("Mic");

        Question question = new Question();
        question.setUsername("小明");
        question.setContent("请老师详细的讲解 观察者设计模式.\n");

        EventBusCenter.register(teacher1);
        EventBusCenter.register(teacher2);

        EventBusCenter.post(question);
    }
}
```

c参考博客: [https://blog.csdn.net/u010739551/article/details/80482701](https://blog.csdn.net/u010739551/article/details/80482701)

---



