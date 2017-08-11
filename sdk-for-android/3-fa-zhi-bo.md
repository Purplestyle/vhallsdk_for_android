#### 1 准备工作

屏幕保持常亮

```
      getWindow().setFlags(WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON,
                WindowManager.LayoutParams.FLAG_KEEP_SCREEN_ON);
```

横竖屏发起视频

```
      /**
      * 如果竖屏发起设置ActivityInfo.SCREEN_ORIENTATION_REVERSE_PORTRAIT
      * 如果横屏发起设置ActivityInfo.SCREEN_ORIENTATION_REVERSE_LANDSCAPE
      */
      setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_REVERSE_PORTRAIT);
```

设置发起布局

```
      <com.vhall.vhalllive.CameraFilterView
        android:id="@+id/cameraview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
```

调用 init\(\)方法

```
      /**
      * pixel_type 发起的分辨率
      */
      getCameraView().init(pixel_type, Activity(), new RelativeLayout.LayoutParams(0, 0));
```

#### 2 发直播

Broadcast实例：  
Broadcast实例 这里需要将之前设置的信息传入Broadcast中 列如自定义view、帧率、码率 、发起事件回调、聊天，此处完整代码可以参考Demo

```
     Broadcast.Builder builder = new Broadcast.Builder()
    .cameraView(mView.getCameraView()).frameRate(param.frameRate)
    .chatCallback(new ChatCallback()) //如需要使用聊天 加上这个回调
    .videoBitrate(param.videoBitrate)
    .callback(new BroadcastEventCallback()); // 直播事件回调
    broadcast = builder.build();
```

一键发起直播，调用SDK initBroadcast方法，在这之前要先初始化观看实例。  
发起参数描述：  

| 参数字段 | 描述 |
| :--- | :--- |
| id | 活动ID(9位) |
| accessToken| 登陆密码不正确 |
| vhallID | 发起实例 |
| RequestCallback | 回调信息 |
备注： 子账号需要先创建，创建后会获取vhallID，当vhallID这个参数不为空时，使用子账号发起直播，使用的Token也需要用子账号重新生成，否则会返回身份验证失败。当vhallID这个参数为空时，默认使用主账号。
代码展示
```
     VhallSDK.getInstance().initBroadcast(param.id, param.token, getBroadcast(), 
	new VhallSDK.RequestCallback(){
            @Override
            public void success() {} // 发起成功
            @Override
            public void failed(int errorCode, String reason) {}
        });

```

#### 3 直播事件回调

```
     private class BroadcastEventCallback implements Broadcast.BroadcastEventCallback {
        @Override
        public void onError(int errorCode, String reason) {}
        @Override
        public void onStateChanged(int stateCode) {
            switch (stateCode) {
                case Broadcast.STATE_CONNECTED: /** 连接成功*/
                    break;
                case Broadcast.STATE_NETWORK_OK: /** 网络通畅*/
                    break;
                case Broadcast.STATE_NETWORK_EXCEPTION: /** 网络异常*/
                    break;
                case Broadcast.STATE_STOP:/** 直播停止*/
                    break;
            }
        }
        @Override
        public void uploadSpeed(String kbps) {/** 下载速度*/}
    }

```
| 状态码 | 描述 | 常量|
| :--- | :--- |:---|
| 20151 | 连接成功 |Broadcast.STATE_CONNECTED|
| 20152 | 网络通畅 |Broadcast.STATE_NETWORK_OK|
| 20153 | 网络异常 |Broadcast.STATE_NETWORK_EXCEPTION|
| 20154 | 直播停止 |Broadcast.STATE_STOP|

错误码

| 错误码 | 描述 |
| :--- | :--- |
| 10401| 活动结束失败 |
| 10402 | 当前活动ID错误 |
| 10403 | 活动不属于自己 |
| 10409 | 第三方用户对象不存在 |
| 10411 | 用户套餐余额不足 |
| 20101 | 正在直播 |
| 20102 | 初始化视频信息失败 |
| 20103 | 预览失败,无法直播 |
| 20104 | 直播地址有误 |
| 20105 | 连接服务器失败 |

#### 4 结束直播
获取VhallSDK的实例 调用finishBroadcast() 传入参数活动ID、TOKEN、Broadcast实例、结束回调 当直播结束时，需要调用此方法，此方法用于结束直播，生成回放，如果不调用，则无法生成回放。
参数说明：

| 参数字段 | 描述 |
| :--- | :--- |
| id | 活动ID(9位) |
| accessToken| 登陆密码不正确 |
| vhallID | 发起实例 |
| RequestCallback | 回调信息 |

以下是代码展示
```
VhallSDK.getInstance().finishBroadcast(param.id, param.token, getBroadcast(), new VhallSDK.RequestCallback() {
            @Override
            public void success() {// 停止成功}
            @Override
            public void failed(int errorCode, String reason) {// 停止失败}
});
```
































