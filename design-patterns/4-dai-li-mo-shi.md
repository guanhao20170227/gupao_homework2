作业大纲:

```
1、仿JDK动态代理实现原理，自己手写一遍。
2、思考：为什么JDK动态代理中要求目标类实现的接口数量不能超过65535个？
3、结合自身的业务场景用代理模式进行重构。
```

## 1 模仿 JDK 动态代理, 自己手写一遍:

github： [https://github.com/guanhao20170227/gupao\_test\_code/tree/master/java\_design/src/main/java/com/haohao/e\_proxy/dynamicproxy/gpself](https://github.com/guanhao20170227/gupao_test_code/tree/master/java_design/src/main/java/com/haohao/e_proxy/dynamicproxy/gpself)

```
--- 生成的class 文件
// Decompiled by Jad v1.5.8g. Copyright 2001 Pavel Kouznetsov.
// Jad home page: http://www.kpdus.com/jad.html
// Decompiler options: packimports(3) 
// Source File Name:   $Proxy0.java

package com.haohao.e_proxy.dynamicproxy.gpself;


// Referenced classes of package com.haohao.e_proxy.dynamicproxy.gpself:
//            Person, GPInvocationHandler

public class $Proxy0
    implements Person
{

    public $Proxy0(GPInvocationHandler gpinvocationhandler)
    {
        handler = gpinvocationhandler;
    }

    public void findLove()
    {
        try
        {
            java.lang.reflect.Method method = com/haohao/e_proxy/dynamicproxy/gpself/Person
                .getMethod("findLove", new Class[0]);
            handler.invoke(this, method, new Object[0]);
        }
        catch(Throwable throwable)
        {
            throwable.printStackTrace();
        }
    }

    public GPInvocationHandler handler;
}
```

2 思考：为什么JDK动态代理中要求目标类实现的接口数量不能超过65535个？

     1



c参考博客:  [https://blog.csdn.net/weixin\_44402359/article/details/95447277](https://blog.csdn.net/weixin_44402359/article/details/95447277)

