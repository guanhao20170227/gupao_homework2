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
1
```

---



