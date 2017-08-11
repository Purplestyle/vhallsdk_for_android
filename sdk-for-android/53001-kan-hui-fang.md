#### 1 看回放
Watchplayback实例：
Watchplayback实例，和观看直播类似，传入Context , ContainerLayout(这里需要传入一个RelativeLayout,用于生成观看回放) ， callback获取观看回放时的一些状态。观看回放的操作和观看直播一样，请求的方法相同，参数相同。 代码可以参考上面的观看直播。

```
       WatchPlayback.Builder builder = new WatchPlayback.Builder()
    .context(playbackView.getmActivity())
    .containerLayout(playbackView.getContainer())
    .callback(new WatchCallback())
    .docCallback(new DocCallback());    //新增 回放绘制PPT和白板
watchPlayback = builder.build();


```

