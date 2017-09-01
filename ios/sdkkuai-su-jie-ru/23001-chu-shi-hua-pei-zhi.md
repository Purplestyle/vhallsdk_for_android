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
  7.1、UIModel 此部分是微吼对发起和观看端进行了简单封装，并提供源码，客户可以直接修改使用，也可作为微吼SDK   调用demo 做参考使用，注：此模块先编译
  7.2、VHSDKDemo demo层只有登录、设置 、直播入口，所有直播相关都在uimodel中用户可以修改UIModel 完成页面快速定制
-----------------------------------------------------------------------------------------
8：主要测试参数说明
  1）活动ID：指的是客户创建的一个直播活动的唯一标识，Demo测试时可从e.vhall.com的控制台页面上获取到
  2）Token：Demo测试时可从http://e.vhall.com/api/test页面，调用接口verify/access-token获取到，有效期为24小时
  3）码率设置：主要用于视频编码设置，码率与视频的质量成正比，默认值300，单位Kbps
  4）缓冲时间：延时观看时间
  5）分辨率： 352*288/640*480/960*540/1280*720
  6）K值： 默认为空，指的是控制直播观看权限的参数，具体使用说明参考第三方K值验证

客户Server端需要提供如下信息：
  1）活动Id: 通过客户Server端接口获取到，此接口需调用VHALL接口webinar/list获取
  2）AccessToken：通过客户Server端接口获取到，此接口需调用VHALL接口verify/access-token获取。 

基础参数配置填写：
找到Demo中CONSTS.h文件，找到以下代码进行每一项的填写。
![](/assets/图片 4.png)

用户登录：
有些功能模块需要用户登录后才可正常使用，比如聊天、问答。
帐号和密码：微吼直播官网的帐号名称和登录密码，可通过以下方式获得
接口调用注册：[http://e.vhall.com/home/vhallapi/active#user_register_第三方创建用户 ](http://e.vhall.com/home/vhallapi/active#user_register_%E7%AC%AC%E4%B8%89%E6%96%B9%E5%88%9B%E5%BB%BA%E7%94%A8%E6%88%B7)



















