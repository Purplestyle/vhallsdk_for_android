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
调用 init()方法
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
| id| 活动ID(9位) |
| accessToken| 登陆密码不正确 |



































