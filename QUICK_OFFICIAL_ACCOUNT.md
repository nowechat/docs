# 快速开始

老流程，首先肯定是体验一把。
## 搞一个公众号
可以是自己的公众号，也可以申请一个测试公众号。

> 测试公众号申请地址： https://mp.weixin.qq.com/debug/cgi-bin/sandbox?t=sandbox/login
> 
> 也可以走接口测试流程：http://mp.weixin.qq.com/debug/cgi-bin/apiinfo

**记住上公众号的 AppId, AppSecret 等信息哦。**

## 写代码啦
### 首先要有配置
```Java
import cn.coding520.nowechat.kernel.Config;

...
public String test(){
    Config config = new Config();
    config.setAppId("xxx");
}
......
...
```
在接下来的实例化中要用到。（这个时候有 `Spring Boot` 就好了，直接注入，所以你也可以直接继承Config类注入，只是一个Bean）

### 然后处理消息有一个类
作为消息处理一大块，必须实现定义的 `MessageHandler` 接口。
```Java
import cn.coding520.nowechat.interfaces.MessageHandler;
import cn.coding520.nowechat.kernel.Message;
import cn.coding520.nowechat.kernel.TextMessage;

public class TestMessageHandler implements MessageHandler{
 
    @Override
    public Message handle(Message fromMessage){
        // 这里实现你自己的逻辑
        return new TextMessage("hello nowechat");
    }

}
```

### 最后可以设置接收啦

```Java
import cn.coding520.nowechat.kernel.Config;
import cn.coding520.nowechat.kernel.MessageServer;

...
public String test(){
    ...配置，获取HttpServletRequest
    MessageServer ms = new MessageServer(config);
    return ms.setMessageHandler(new TestMessageHandler()).getResponse();
    
    // 以下写法也可以
    // return ms.getResponse(new TextMessageHandler());
    
}
......
...
```

### 运行
在公众平台填上你的地址，愉快的事情就会出现～