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