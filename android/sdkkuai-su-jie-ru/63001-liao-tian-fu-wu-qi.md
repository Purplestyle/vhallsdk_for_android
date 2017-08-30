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



