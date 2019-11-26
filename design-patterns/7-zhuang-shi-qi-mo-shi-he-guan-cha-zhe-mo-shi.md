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

---



