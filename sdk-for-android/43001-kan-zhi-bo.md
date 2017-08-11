#### 1 看直播
WatchLive 实例：
watchLive 实例 , 这里需要将一些设置信息传入 列如Context、containerLayout(这里需要传入一个RelativeLayout,用于生成观看)、回调callback, MessageEventCallback 消息回调 ，ChatCallback 聊天回调

```
      WatchLive.Builder builder = new WatchLive.Builder()
               .context()
               .containerLayout() // 传入观看布局
               .bufferDelay() // 缓冲几秒的BUFFER
               .callback(new WatchCallback())
               .messageCallback(new MessageEventCallback())
               .chatCallback(new ChatCallback());//如果使用聊天就加这个回调
      watchLive = builder.build();

```

一键观看直播：
一键观看直播，当Activity 被创建 观看界面Activity必须包涵一个RelativeLayout布局 此布局需要往VhallSDK中传递 用于一键生成回放，获取VhallSDK的实例 调用initWatch() 这里传入参数WatchLive实例、活动ID(必填)、用户名、用户邮箱、vhall_id、K值校验等参数。
参数描述

| 参数字段 | 描述 |
| :--- | :--- |
| id | 活动ID(9位) |
| nickname| 用户名 |
| email| 用户邮箱 |
| vhall_id| VhallId (登陆后获取,没有传空) |
| password| K值 |
| WatchLive| 观看直播实例 |
| RequestCallback| 请求通用回调 |

备注：如果用户名和密码为空，则vhall_id 不能为空，
      如果vhall_id为空，则用户名和密码不能为空，
      如果都传，默认取vhall_id的值。

```
      VhallSDK.getInstance().initWatch(param.id, "test", "test@vhall.com", vhallId , param.k, getWatchLive(), 
new VhallSDK.RequestCallback() {
            @Override
            public void success() {// 获取观看信息成功}
            @Override
            public void failed(int errorCode, String reason) { 失败}
        });

```

#### 2 观看事件回调


错误码

| 错误码 | 描述 |
| :--- | :--- |
| 10030 | 身份验证出错 |
| 10402 | 当前活动ID错误 |
| 10049 | 访客数据信息不全 |
| 10404 | KEY值验证出错 |
| 10046 | 当前活动已结束 |
| 10405 | 微吼用户ID出错 |
| 10047 | 您已被踢出，请联系活动组织者 |
| 10048 | 活动现场太火爆，已超过人数上限 |
| 10410 | 用户信息不存在 |

#### 3 停止直播
当用户停止观看时，需要调用VhallSDK中停止观看直播方法，调用此方法，SDK会断开拉流。
代码展示如下
getWatchLive().stop();

#### 4 开启弹幕
	弹幕实现依赖第三方库B站的弹幕引擎•烈焰弹幕 DanmakuFlameMaster 
第一步，在我们视频view布局的上方再覆盖一个显示弹幕的View， 弹幕的View必须要做成完全透明的, 这样即使覆盖在视频界面的上方也不会影响到视频的正常观看，布局如下：

```
      <master.flame.danmaku.ui.widget.DanmakuView
        android:id="@+id/sv_danmaku"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

第二步，找到build.gradle添加如下依赖

```
      dependencies {
        compile 'com.github.ctiao:DanmakuFlameMaster:0.6.4'
        compile 'com.github.ctiao:ndkbitmap-armv7a:0.6.4'
        compile 'com.github.ctiao:ndkbitmap-armv5:0.6.4'
        compile 'com.github.ctiao:ndkbitmap-x86:0.6.4'
    }
```

第三步，初始化弹幕所需的信息，设置回调详情参考Demo，

```
      HashMap<Integer, Integer> maxLinesPair = new HashMap<Integer, Integer>();
       maxLinesPair.put(BaseDanmaku.TYPE_SCROLL_RL, 5); // 滚动弹幕最大显示5行
      
        // 设置是否禁止重叠
        HashMap<Integer, Boolean> overlappingEnablePair = new HashMap<Integer, Boolean>();
        overlappingEnablePair.put(BaseDanmaku.TYPE_SCROLL_RL, true);

```






















