#pragma mark - 新版版使用的常量定义如下


{
     VHLogType_ON    = 1,   //开启日志
     VHLogType_ALL   = 2,   //开启全部日志
};


#pragma mark - 发起端常量定义

  * 发直播状态
  *
  * 当kLiveStatusPushConnectError时，content代表出错原因 及具体错误码查看下方错误码定义
 
 
 
 typedef NS_ENUM(NSInteger,VHLiveStatus)
 VHLiveStatusNone                    = kLiveStatusNone,
 VHLiveStatusPushConnectSucceed      = kLiveStatusPushConnectSucceed,    //直播连接成功
 VHLiveStatusPushConnectError        = kLiveStatusPushConnectError,      //直播连接失败
 VHLiveStatusParamError              = kLiveStatusParamError,            //参数错误
 VHLiveStatusSendError               = kLiveStatusSendError,             //直播发送数据错误
 VHLiveStatusUploadSpeed             = kLiveStatusUploadSpeed,           //直播上传速率
 VHLiveStatusAudioRecoderError       = kLiveStatusAudioRecoderError,     //音频采集失败，提示用户查看权限或者重新推流，切记此事件会回调多次，直到音频采集正常为止
 VHLiveStatusUploadNetworkException  = kLiveStatusUploadNetworkException,//发起端网络环境差
 VHLiveStatusUploadNetworkOK         = kLiveStatusUploadNetworkOK,       //发起端网络环境恢复正常
 VHLiveStatusGetUrlError             = kLiveStatusGetUrlError,           //获取推流地址失败
 
 
 
 /**
  * 摄像头取景方向
 
 
 typedef NS_ENUM(NSInteger,VHDeviceOrientation)
 VHDevicePortrait                    = kDevicePortrait,
 VHDeviceLandSpaceLeft              = kDeviceLandSpaceRight,
 VHDeviceLandSpaceRight             = kDeviceLandSpaceLeft
 
 
 
 
 /**
 
 
 typedef NS_ENUM(NSInteger,VHVideoResolution)
 VHLowVideoResolution                = kLowVideoResolution,      //低分边率  352*288
 VHGeneralVideoResolution            = kGeneralVideoResolution,  //普通分辨率 640*480
 VHHVideoResolution                  = kHVideoResolution,        //高分辨率  960*540
 VHHDVideoResolution                 = kHDVideoResolution        //超高分辨率 1280*720
 
 
 
 #pragma mark - 观看端常量定义
 
 /**
   * 观看端错误事件
   * 当VHLivePlayGetUrlError时， content代表出错原因 及具体错误码查看下方错误码定义
 
 typedef NS_ENUM(NSInteger,VHLivePlayErrorType)
 VHLivePlayErrorNone                 = kLiveStatusNone,
 VHLivePlayGetUrlError               = kLivePlayGetUrlError,     //获取服务器rtmpUrl错误
 VHLivePlayParamError                = kLivePlayParamError,      //参数错误
 VHLivePlayRecvError                 = kLivePlayRecvError,       //接受数据错误
 VHLivePlayCDNConnectError           = kLivePlayCDNConnectError, //CDN链接失败
 
 
 /**
   * 直播播放器视频填充模式，回放使用MPMoviePlayerController 自带填充模式设置
 
 
 
typedef NS_ENUM(NSInteger,VHRTMPMovieScalingMode)
VHRTMPMovieScalingModeNone          = kRTMPMovieScalingModeNone,        //填充满video显示view
VHRTMPMovieScalingModeAspectFit     = kRTMPMovieScalingModeAspectFit,   //在保持长宽比的前提下，缩放图片，使得图片在容器内完整显示出来 可能留有黑边
VHRTMPMovieScalingModeAspectFill    = kRTMPMovieScalingModeAspectFill,  //在保持长宽比的前提下，缩放图片，使图片充满容器








/**
 
 
 
 typedef NS_ENUM(NSInteger,VHStreamType)
 VHStreamTypeNone                    = kVHallStreamTypeNone,         //未知
 VHStreamTypeVideoAndAudio           = kVHallStreamTypeVideoAndAudio,//音视频
 VHStreamTypeOnlyVideo               = kVHallStreamTypeOnlyVideo,    //纯视频无音频
 VHStreamTypeOnlyAudio               = kVHallStreamTypeOnlyAudio,    //纯音频
 
 
 
 /**
  
  

typedef NS_ENUM(NSInteger,VHRenderModel){
 VHRenderModelNone                   = kVHallRenderModelNone,
 VHRenderModelOrigin                 = kVHallRenderModelOrigin,      //普通视图的渲染
 VHRenderModelDewarpVR               = kVHallRenderModelDewarpVR,    //VR视图的渲染
 
 
 
 
 
 
 /**
   *  播放器状态 直播状态 回放状态由于用户创建的 MPMoviePlayerController 实例获取
 
 typedef NS_ENUM(NSInteger,VHPlayerState) {
 VHPlayerStateStoped                 = 0,    //停止   可调用startPlay: startPlayback: 状态转为VHallPlayerStateStarting
 VHPlayerStatePlaying                = 2,    //播放中 可调用stopPlay pausePlay 状态转为VHallPlayerStateStoped/VHallPlayerStatePaused
 
 
 
 
 /**
 
  */
typedef NS_ENUM(NSInteger,VHMovieVideoPlayMode) {
VHMovieVideoPlayModeNone            = 0,    //不存在
VHMovieVideoPlayModeMedia           = 1,    //单视频
VHMovieVideoPlayModeTextAndVoice    = 2,    //文档＋声音
VHMovieVideoPlayModeTextAndMedia    = 3,    //文档＋视频
VHMovieVideoPlayModeVoice           = 4,    //单音频



/**
 
  */
 typedef NS_ENUM(NSInteger,VHMovieDefinition) {
 VHMovieDefinitionOrigin             = 0,    //原画
 VHMovieDefinitionUHD                = 1,    //超高清
 VHMovieDefinitionHD                 = 2,    //高清
 VHMovieDefinitionSD                 = 3,    //标清
 VHMovieDefinitionAudio              = 4,    //纯音频
 
 
 
 /**
   *  活动状态
   */
 
 typedef NS_ENUM(NSInteger,VHMovieActiveState) {
  VHMovieActiveStateNone              = 0,
  VHMovieActiveStateLive              = 1,    //直播
  VHMovieActiveStateReservation       = 2,    //预约
  VHMovieActiveStateEnd               = 3,    //结束
  VHMovieActiveStateReplay            = 4,    //回放or点播
  
  
 #endif /*VHallConst.h */
 //错误信息info中 错误码code 及 content错误信息
 
 以下是推流连接失败错误码
 4001 | 握手失败
 4002 | 链接vhost/app失败
 4003 | 网络断开 （预留，暂时未使用）
 4004 | 无效token
 4005 | 不再白名单中
 4006 | 在黑名单中
 
 4008 | 流被禁掉 （预留，暂时未使用）
 
 
 

以下是所有网络接口请求错误的错误码及错误内容
10010 | 活动不存在

10017 | 活动id 不能为空
10030 | 身份验证出错

10046 | 当前活动已结束
10047 | 您已被踢出，请联系活动组织者

10049 | 访客数据信息不全
10401 | 活动开始失败
10401 | 活动结束失败
10402 | 当前活动ID错误
10403 | 活动不属于自己

10405 | 录播不存在


10408 | 当前活动非直播状态
10409 | 参会ID不能为空
10410 | 抽奖ID不能为空



10411 | 用户名称不能为空


10412 | 直播中，获取失败
10413 | 获取条目最多为50
10501 | 用户不存在
10502 | 登陆密码不正确





 以下是所有业务逻辑错误
 20001 | AppKey 或 SecretKey 未设置
 20002 | 后台接口api错误
 
 
 
 20006 | 当前活动已为回放/点播
 
 
 20009 | 未参会
 
 20011 | 发直播token为空
 20012 | 结束活动失败
 
 
 20015 | 未获取到签到ID
 20016 | 签到已结束
 20017 | 未获取到问卷ID
 20018 | 请求参数错误
 
 
 以下是网络错误信息
 
30001 | 请求参数错误
30002 | 网络错误
30003 | 请求错误


30006 | 请求返回错误
 
 
 
 
 
 
 
 
 
 
 
 
 
 