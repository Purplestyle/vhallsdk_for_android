1：下载SDK&使用准备
从github下载：https://github.com/vhall/vhallsdk_live_ios/releases 
-----------------------------------------------------------------------------------------
2:开发环境要求
最低支持iOS版本：iOS 7.0
最低支持iPhone型号：iPhone 5
支持CPU架构： armv7, arm64
含有i386和x86_64模拟器版本的库文件，推流功能无法在模拟器上工作，播放功能完全支持模拟器。

-----------------------------------------------------------------------------------------
3:ATS支持情况:支持
----------------------------------------------------------------------------------------
4:添加依赖库
添加系统库
libc++.tbd
libz2.1.0.tbd
libicucore.tbd
libz.tbd
libiconv.tbd
CoreTelephony.framework
MediaPlayer.framework
AVFoundation.framework
VideoToolbox.framework
AssetsLibrary.framework
OpenAL.framework
OpenGLES.framework
QuartzCore.framework
CoreMedia.framework
Security.framework
JavaScriptCore.framework
将VHallSDK文件夹添加到工程中，添加后的效果如下图所示：
![](/assets/图片 3.png)

-----------------------------------------------------------------------------------------

5:Demo简介：DEMO只针对核心功能进行演示，不包括UI界面设计。
-----------------------------------------------------------------------------------------
6：Demo基础设置
  6.1、工程中任意 *.m 文件修改为 *.mm
  6.2、关闭bitcode 设置
  6.3、plist 中 App Transport Security Settings -> Allow Arbitrary Loads 设置为YES
  6.4、注册AppKey [VHallApi registerApp:AppKey SecretKey:AppSecretKey]; 
  6.5、检查工程 Bundle ID 是否与AppKey对应 
  6.6、 plist 中 Privacy - Camera Usage Description 是否允许使用相机
  6.7、plist  中 Privacy - Microphone Usage Description是否允许使用麦克风
-----------------------------------------------------------------------------------------
7:Demo结构介绍
  通过 VHSDKDemo.xcworkspace  打开demo源码 包括两部分 
  
  
-----------------------------------------------------------------------------------------
8：主要测试参数说明
  1）活动ID：指的是客户创建的一个直播活动的唯一标识，Demo测试时可从e.vhall.com的控制台页面上获取到
  2）Token：Demo测试时可从http://e.vhall.com/api/test页面，调用接口verify/access-token获取到，有效期为24小时
  
  4）缓冲时间：延时观看时间
  
  6）K值： 默认为空，指的是控制直播观看权限的参数，具体使用说明参考第三方K值验证



  

基础参数配置填写：

![](/assets/图片 4.png)

用户登录：

帐号和密码：微吼直播官网的帐号名称和登录密码，可通过以下方式获得



















