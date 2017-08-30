#### 1 看回放
Watchplayback实例：
Watchplayback实例，和观看直播类似，传入Context , ContainerLayout(这里需要传入一个RelativeLayout,用于生成观看回放) ， callback获取观看回放时的一些状态。观看回放的操作和观看直播一样，请求的方法相同，参数相同。 代码可以参考上面的观看直播。

```
    WatchPlayback.Builder builder = new                        WatchPlayback.Builder()
    .context(playbackView.getmActivity())
    .containerLayout(playbackView.getContainer())
    .callback(new WatchCallback())
    .docCallback(new DocCallback());    //新增 回放绘制PPT和白板
     watchPlayback = builder.build();

```
一键观看回放：（参数和观看直播相同）
一键观看回放，参数和观看直播相同，传递的观看实例变成WatchedPlayBack

| 参数字段 | 描述 |
| :--- | :--- |
| id | 活动ID(9位) |
| nickname| 用户名 |
| email| 用户邮箱 |
| vhall_id| VhallId (登陆后获取,没有传空) |
| password| K值 |
| recordId| 回放片段ID（只在观看回放使用） |
| WatchPlayBack| 观看回放实例 |
| RequestCallback| 回调信息 |


```
    VhallSDK.getInstance().initWatch(param.id, "test", "test@vhall.com", vhallId, param.k, , recordId getWatchPlayback(), 
       new VhallSDK.RequestCallback() {
            @Override
            public void success() {// 获取观看信息成功}
            @Override
            public void failed(int errorCode, String reason) { 失败}
        });
```


#### 2 观看回放事件回调

```
    VhallSDK.getInstance().initWatch(param.id, "test", "test@vhall.com", vhallId , param.k, recordId , getWatchPlayback(), 
private class WatchCallback implements WatchPlayBack.WatchEventCallback {
        @Override
        public void onError(int errorCode, String errorMsg) {// 错误返回错误码}
        @Override
        public void onStateChanged(boolean playWhenReady, int playbackState) {/
                 switch (playbackState) {/播放器过程中的状态信息
                       case VhallHlsPlayer.STATE_IDLE:// 闲置状态
                           break;
                       case VhallHlsPlayer.STATE_PREPARING:// 准备状态
                           break;
                       case VhallHlsPlayer.STATE_BUFFERING:// 正在加载
                           break;
                       case VhallHlsPlayer.STATE_READY:// 正在加载
                           break;
                       case VhallHlsPlayer.STATE_ENDED:// 准备就绪
                           break;
                       case VhallHlsPlayer.STATE_ENDED:// 结束
                       default:
                           break;
                   }
               }
        @Override
        public void uploadSpeed(String kbps) { // 速度}
	@Override
        public void onStartFailed(String errorMsg) {// 初始化观看播放器时的错误}
}

```
#### 3 播放器方法

当观看信息请求成功，虽然和观看直播请求的是相同的方法，但是逻辑处理不同，SDK会默认得到播放地址并设置进播放器中，用户只需调用watchPlayback实例中的各种方法来获取想要得到的信息。

开始播放

```
    getWatchPlayback().start();
```


暂停播放


```
    getWatchPlayback().pause();
```
停止播放

```
    getWatchPlayback().stop();
```
获取播放进度

```
     getWatchPlayback().seekTo(playerCurrentPosition);
```
获取当前播放进度
```
    getWatchPlayback().getCurrentPosition();
```

获取播放时长：
```
    getWatchPlayback().getDuration();
```

是否正在播放
```
    getWatchPlayback().isPlaying();
```

#### 4 发送/获取评论信息

发送消息

| 参数字段 | 描述 |
| :--- | :--- |
| text| 评论内容 |
| user_id| 用户登陆返回的唯一标识 |
| RequestCallback| 回调信息 |

代码展示
```
    getWatchPlayback().sendComment(text, user_id, new VhallSDK.RequestCallback() {
            @Override
            public void success() {  //接口请求成功
                chatView.clearInputContent();
                chatView.clearChatData();
		}
             @Override
            public void failed(int errorCode, String reason) {}
        });

```
| 错误码 | 描述 |
| :--- | :--- |
| 10010| 活动不存在 |
| 10011| 不是该平台下的活动 |
| 10017| 活动ID不能为空 |
| 10806| 内容不能为空 |
| 10807| 用户ID不能为空 |
| 10808| 当前用户未参会 |

获取历史聊天评论

| 参数字段 | 描述 |
| :--- | :--- |
| webinar_id| 活动id |
| limit| 每页的数量(取条目最多为50条) |
| pos| 偏移量(如果从0开始就是最新的一条) |
| ChatServer.ChatRecordCallback()| 回调信息 |



```
   watchPlayback.requestCommentHistory(webinar_id, String.valueOf(limit), String.valueOf(pos), new ChatServer.ChatRecordCallback() {
            @Override
            public void onDataLoaded(List<ChatServer.ChatInfo> list) {//接口请求成功}
            @Override
            public void onFailed(int errorcode, String messaage) {}
        });

```

| 错误码 | 描述 |
| :--- | :--- |
| 10030| 身份验证出错 |
| 10402| 当前活动ID错误 |
| 10403| 活动不属于自己 |
| 10407| 查询数据为空|
| 10412| 直播中，获取失败 |
| 10413| 获取条目最多为50条 |
| 10409| 参会信息不存在 |
| 10410| 活动开始时间不存在 |



#### 5 观看回放绘制PPT和白板
1	回调WatchPlayBack.DocumentEventCallback

```
    private class DocCallback implements WatchPlayback.DocumentEventCallback {
        @Override
        public void onEvent(String key, List<MessageServer.MsgInfo> msgInfos) {
            if (msgInfos != null && msgInfos.size() > 0) {
                documentView.paintPPT(key, msgInfos);
                documentView.paintBoard(key, msgInfos);
            }
        }
        @Override
        public void onEvent(MessageServer.MsgInfo msgInfo) {
            documentView.paintPPT(msgInfo);
            documentView.paintBoard(msgInfo);
        }
}

```
备注： 在Builder观看回放实例的时候加入 docCallback()

























































































































