当用户在创建发起直播实例或者观看直播实例时的.ChatCallback中传入chatCallback回调，聊天服务器就已经开启了，具体参考快速接入介绍中的发起观看创建实例的描述  
以下是聊天服务器回调

```
    private class ChatCallback implements ChatServer.Callback {
        @Override
        public void onChatServerConnected() {}// 聊天服务器建立
        @Override
        public void onConnectFailed() {} // 聊天服务器连接失败
        @Override
        public void onChatMessageReceived(ChatServer.ChatInfo chatInfo) {//消息接收
            switch (chatInfo.event) {
                case ChatServer.eventMsgKey: // 聊天消息通知
                    break;
                case ChatServer.eventOnlineKey: // 上线消息通知
                    break;
                case ChatServer.eventOfflineKey: // 下线消息通知
                    break;
                case ChatServer.eventQuestion: // 问答消息
                    break;
            }
        }
        @Override
        public void onChatServerClosed() {}// 聊天服务器关闭
    }
```

| 字段 | 描述 |
| :--- | :--- |
| account_id |  用户ID|
| user_name |  用户昵称|
| avater |  用户头像|
| room |  用户ID|
| event|  消息类型 (用于区分消息用途)|
| time|  time|


getBroadcast().connectChatServer ();

getBroadcast().disconnectChatServer ();




备注：使用此功能默认聊天服务器已开启

#### 1、 上下线消息通知

消息体说明：chatInfo.event = “online offline”

| OnlineData | 描述 |
| :--- | :--- |
| role | 用户类型 host:主持人 guest：嘉宾 assistant：助手 user：观众|
| concurrent_user| 房间内当前用户数|
| is_gag | 是否被禁言|
| attend_count | 参会人数|

#### 2、 聊天消息

目前发起直播和观看直播中可以聊天。发起直播调用getBroadCast().sendChat()方法 。观看直播调用getWatchLive().sendChat()。

chatInfo.event = “msg”
参数说明：

| 参数字段 | 描述 |
| :--- | :--- |
| text| 聊天内容|
| VhallSDK.RequestCallback| 回调信息|

发起直播代码展示 && 观看直播代码展示：

```
    getBroadcast().sendChat(text, new VhallSDK.RequestCallback() { // 发起直播时聊天
            @Override
            public void success() {}
            @Override
            public void failed(int errorCode, String reason) {}
        });
    getWatchLive().sendChat(text, new VhallSDK.RequestCallback() {// 观看直播时聊天
            @Override
            public void success() {}
            @Override
            public void failed(int errorCode, String reason) {}
        });

```

#### 3、 聊天记录
获取SDK聊天记录。聊天记录只在观看直播时候获取，调用acquireChatRecord()
参数说明：

| 参数字段 | 描述 |
| :--- | :--- |
| showAll| 显示当次直播聊天最多为20条,true显示所有聊天最条为20条|
| ChatRecordCallback| 聊天记录回调|

```
    getWatchLive().acquireChatRecord(false, new ChatServer.ChatRecordCallback() {
            @Override
            public void onDataLoaded(List<ChatServer.ChatInfo> list) {}
            @Override
            public void onFailed(int errorcode, String messaage) {}
});


```


















