作业大纲:

```
1、举例Spring源码中你见过的委派模式，并画出类关系图。
2、利用策略模式重构一段业务代码。
```

## 1 举例Spring源码中你见过的委派模式，并画出类关系图

AbstractApplicationContext.obtainFreshBeanFactory\(\) --&gt; refreshBeanFactory\(\) 方法

AbstractRefreshableApplicationContext.refreshBeanFactory\(\) 方法

![](/assets/import_20191124115601.png)

c参考博客: [https://segmentfault.com/q/1010000016610781](https://segmentfault.com/q/1010000016610781)

## 2 利用策略模式重构一段业务代码

原始代码:

```
public class MyDispatcherServlet extends HttpServlet {

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //super.service(req, resp);
        // doDispatch(req, resp);
    }

    /**
     *  这一块也将在完成 策略模式的之后进行整改;
     * @param req
     * @param resp
     * @throws IOException
     */
    private void doDispatch(HttpServletRequest req, HttpServletResponse resp) throws IOException {
        String uri = req.getRequestURI();
        String mid = req.getParameter("mid");

        if (uri.contains("getMemberById")) {
            new MemberController().getMemberById(mid);
        } else if (uri.contains("getOrderById")) {
            new OrderController().getOrderById(mid);
        } else if (uri.contains("logout")) {
            new SystemController().logout(null);
        } else {
            resp.getWriter().write("404, Not Found My.");
        }
    }
}
```

重构后的代码:

```
public class MyDispatchServlet2 extends HttpServlet {

    private static Map<String, Object> mapController = new HashMap<String, Object>();
    private static Map<String, MyDispatchServlet2> mapInstance = new HashMap<String, MyDispatchServlet2>();

    static {
        mapController.put("getMemberById", new MemberController());
        mapController.put("getOrderById", new OrderController());
        mapController.put("logout", new SystemController());

        mapInstance.put(MyDispatchServlet2.class.getName(), new MyDispatchServlet2());
    }

    // 使用容器式单例吧，

    // web.xml 中
    // <servlet-class>com.haohao.designpatterns.f_delegate.demo2.MyDispatchServlet2</servlet-class>
    // 要求该类必须有默认的构造方法, 所有后面看这个地方还怎么处理的把.
    /*private MyDispatchServlet2() {
        // 1 防止反射破坏单例;
        if (mapController.get(MyDispatchServlet2.class.getName()) != null) {
            throw new RuntimeException("不能创建多个实例");
        }
    }*/

    // 2， 防止序列化破坏单例;
    public Object readResolve(){ return mapInstance.get(MyDispatchServlet2.class.getName()); }

    // 单例的全局访问点
    public static MyDispatchServlet2 getInstance() throws IllegalAccessException, InstantiationException {
        if (!mapInstance.containsKey(MyDispatchServlet2.class.getName())) {
            mapInstance.put(MyDispatchServlet2.class.getName(), MyDispatchServlet2.class.newInstance());
        }
        return mapInstance.get(MyDispatchServlet2.class.getName());
    }

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        try {
            doDispatch(req, resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void doDispatch(HttpServletRequest req, HttpServletResponse resp) throws NoSuchMethodException, 
            InvocationTargetException, IllegalAccessException {

        String uri = req.getRequestURI().replace("/web/", "");
        Object obj = mapController.get(uri);

        try {
            // 获取 Object 的方法并执行
            Method method = obj.getClass().getMethod(uri,String.class);
            System.out.println(method);
            method.invoke(obj, "12345");
        } catch(Exception ex) {
            try {
                resp.getWriter().write("404 Not Found.");
            } catch (IOException e) {
                e.printStackTrace();
            }
            ex.printStackTrace();
        }
    }
}
```

---



