作业大纲

```
1、运用原型模式重构一段业务代码。
```

## 1 利用原型模式重构一段业务代码：

由于现在没有业务代码, 所以我就贴上 深度克隆和单例的代码吧.

\[1\] 单例类: 继承 Closeable, 重写 clone\(\) 方法, 返回单实例;

```
public class DeepCloneSingleton implements Cloneable {

    // 方法1, 继承 Cloneable, 重写 clone 方法;
    private static final DeepCloneSingleton INSTANCE = new DeepCloneSingleton();

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return INSTANCE;
    }

    private DeepCloneSingleton() {
        if (INSTANCE != null) {
            throw new RuntimeException("不能创建多个实例");
        }
    }

    public static DeepCloneSingleton getInstance() {
        return INSTANCE;
    }
}
```

--

