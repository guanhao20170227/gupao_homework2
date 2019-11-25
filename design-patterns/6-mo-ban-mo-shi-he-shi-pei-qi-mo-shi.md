作业大纲:

```
1、思考：模板模式除了继承以外，还有哪些实现方式？
2、使用适配模式，重构一段需要升级功能且兼容老系统的业务代码。
```

## 1 思考：模板模式除了继承以外，还有哪些实现方式？

```
模板模式还可以使用代理模式来实现;
```

## 2 使用适配模式，重构一段需要升级功能且兼容老系统的业务代码。

没有老系统的业务代码, 我就直接贴上我们例子中 扩展 登录方式的部分代码了

老代码:

```
public class SignInService {

    // 1 注册的方法;
    public ResultMsg register(String username, String password) {
        ResultMsg resultMsg = new ResultMsg(200, "注册成功", new Member());
        System.out.println(resultMsg.toString());
        return resultMsg;
    }

    // 2 登录的方法;
    public ResultMsg login(String username, String password) {
        System.out.println("Login Msg: username " +  username + " , password: " + password);
        return null;
    }

}
```

新代码

---



