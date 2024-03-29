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
        if (INSTANCE != null) { // 添加判断后, 反射就不能创建对象
            throw new RuntimeException("不能创建多个实例");
        }
    }

    public static DeepCloneSingleton getInstance() {
        return INSTANCE;
    }

    // 防止序列化破坏单例
    public  Object readResolve() {
        return INSTANCE;
    }
}
```

\[2\] 测试类:

```
public class Test {
    public static void main(String[] args) throws Exception {
        // 1 使用反射获取 实例， 在构造方法添加判断
        Class clazz = DeepCloneSingleton.class;
        Constructor c = clazz.getDeclaredConstructor(null);
        c.setAccessible(true);
        //DeepCloneSingleton deep1 = (DeepCloneSingleton) c.newInstance();

        // 2 直接获取对象
        DeepCloneSingleton deep2 = DeepCloneSingleton.getInstance();

        // 3 克隆的
        DeepCloneSingleton deep3 = (DeepCloneSingleton) deep2.clone();

        // System.out.println(deep1 == deep2);
        // System.out.println(deep1 == deep3);
        System.out.println(deep2 == deep3);
    }
}
```

---

