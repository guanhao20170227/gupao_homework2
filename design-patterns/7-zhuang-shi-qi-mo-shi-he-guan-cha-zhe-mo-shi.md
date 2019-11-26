作业大纲

```
1、思考并总结装饰者模式和适配器模式的根本区别。
2、用Guava API实现GPer社区提问通知的业务场景。
```

## 1 思考并总结装饰者模式和适配器模式的根本区别。

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

    1

---



