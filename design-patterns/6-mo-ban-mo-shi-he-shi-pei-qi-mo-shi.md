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

新代码: 

```
public class PasswordForThirdAdapter extends SignInService implements IPasswordForThird {

    @Override
    public ResultMsg loginForQQ(String id) {
        return processLogin(id, LoginForQQAdapter.class);
    }

    @Override
    public ResultMsg loginForWechat(String id) {
        return processLogin(id, LoginForWechatAdapter.class);
    }

    @Override
    public ResultMsg loginForToken(String id) {
        return processLogin(id, LoginForTokenAdapter.class);
    }

    @Override
    public ResultMsg loginForTelephone(String telephone, String code) {
        return processLogin(telephone, LoginForTelephoneAdapter.class);
    }

    // 统一上面的公共方法, 根据传递过来的值, 执行各自的逻辑  是 简单工厂方法;
    //    --> 登录的各个方式是不同的, 但是结果都是可以登录进入  是 策略方法;

    // 这种写法是 模仿的 Sprig AOP 里面的写法写的, 希望多多的思考
    private ResultMsg processLogin(String key, Class<? extends ILoginAdapter> clazz) {
        try {
            ILoginAdapter adapter = clazz.newInstance();
            if (adapter.support(adapter)) {
                return adapter.login(key, adapter);
            }
        } catch(Exception ex) {
            ex.printStackTrace();
        }
        return null;
    }
}
```

---



