# 消息

## 消息类
在 package `cn.coding520.kernel.message` 中，包含了所有消息的类型。其中有 `@Repliable` 的是可以回复的，其他的都是公众平台不支持的回复类型。

## 消息解析
正如前文介绍的，我们不需要关心消息是否加密，xml 如何解析。nowechat 为你自动进行了处理。核心的处理类是 `cn.coding520.kernel.MessageManager` 。

当然，你也不需要关心它是怎么实现的，因为对外使用 `MessageServer` 就可以完成一切消息请求啦。

在你自己实现 MessageHandler 的类中， handle(Message fromMessage) 方法接收的参数就是解析后的参数，你可以通过 `fromMessage.getMsgType` 来判断消息类型，也可以使用 `fromMessage instanceof XXXMessage` 来判断。
```Java
if(fromMessage.getMsgType() == MsgType.TEXT.getValue()){
    System.out.pringln("收到文本消息");
} else if(fromMessage instanceof SubscribeEventMessage){
    System.out.println("这是一条关注消息");
}
```

**事件消息带有 `Event` 后缀。**

## 被动回复消息
只需要在 `MessageServer` 中设置好 `setMessageHandler` ， 就可以了。
如果有在外部获取消息的需求（比如写库等），下一个版本会在 `MessageServer` 中加一个方法来实现。