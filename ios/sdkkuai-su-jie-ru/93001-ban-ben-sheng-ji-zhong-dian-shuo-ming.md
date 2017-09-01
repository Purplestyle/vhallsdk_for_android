1：V2.9.0到v3.0.0升级说明  
a、删除App工程中VHallSDK文件夹下所有文件 重新添加VHallSDK  
b、工程中所有 VHMoviePlayer 类替换为VHallMoviePlayer  
c、去掉 VHMoviePlayer 类中setDefinition 方法 统一使用 curDefinition 属性 注意：setCurDefinition 若果参数是视频不支持的分辨率 设置无效 调用此属性    get方法获取当前分辨率  
d、去掉 VHMoviePlayer 类中liveFormat属性  
e、一些枚举定义已不再推荐使用建议尽快更新 特别注意：VHDeviceOrientation 原有意义错误已修正

f、发起端CameraEngineRtmpDelegate 替换为VHallLivePublishDelegate

2:v2.7.0到v2.8.0、v2.9.0升级说明  
a、libVinnyLive.a -&gt; libVhallLiveApi.a  
b、需要删除原来的libVinnyLive.a库  
c、添加 libVhallLiveApi.a  
d、如果出现黑屏但有声音 请查看观看是否调用了

* \(void\)setRenderViewModel:\(VHRenderModel\)renderModel;

3:v2.3.0到v2.4.0升级说明  
a、绑定应用签名信息

b、使用SDK前集成前，务必先配置好此签名信息，否则使用时会出现“身份验证失败”提示信息。

c、进入[http://e.vhall.com/home/vhallapi/authlist](http://e.vhall.com/home/vhallapi/authlist) ，API/SDK使用权限信息页面。  
选择已开通的应用进行编辑操作。  
点下一步进入应用绑定页面。  
选择IOS-SDK切页后输入安全码BundleID项。（Bundle Identifier在项目Targets的General中找到，如下图）  
![](/assets/图片 25.png)

AppDelegate.m

# import "VHallApi.h"

-\(BOOL\)application:\(UIApplication_\)application didFinishLaunchingWithOptions:\(NSDictionary _\)launchOptions  
    {  
                \[VHallApi registerApp:AppKey SecretKey:AppSecretKey\];//新增  
      }

VHallLivePublish.h

* \(void\)startLive:\(NSDictionary\*\)param;//参数发生变化，去掉AppKey和AppSecretKey
* \(void\)stopLive; //结束直播 用于替换原来disconnect方法 与startLive成对出现，如果调用startLive，则需要调用stopLive以释放相应资源
* \(void\)disconnect; //方法不再用于结束直播，只用于手动断开直播流， 断开推流的连接,注意app进入后台时要手动调用此方法、切回到前台需reconnect重新推流。（注：特别需要使用disconnect的地方都改成stopLive）  
  bitRate -&gt; videoBitRate  //比特率属性变为videoBitRate

  VHallMoviePlayer.h  
  -\(BOOL\)startPlay:\(NSDictionary_\)param;//参数发生变化,去掉AppKey和AppSecretKey  
  -\(void\)startPlayback:\(NSDictionary_\)param moviePlayer:\(MPMoviePlayerController \*\)moviePlayerController;  //参数发生变化，去掉AppKey和AppSecretKey



