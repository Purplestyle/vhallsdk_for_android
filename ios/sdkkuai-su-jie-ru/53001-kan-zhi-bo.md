1：观看直播属性
@property(nonatomic,assign)id <VHallMoviePlayerDelegate> delegate;
@property(nonatomic,strong,readonly)UIView * moviePlayerView;
@property(nonatomic,assign)int timeout;     //RTMP链接的超时时间 默认5秒，单位为毫秒
@property(nonatomic,assign)int reConnectTimes; //RTMP 断开后的重连次数 默认 2次
@property(nonatomic,assign)int bufferTime; //RTMP 的缓冲时间 默认 2秒 单位为秒 必须>0 值越小延时越小,卡顿增加
@property(assign,readonly)int realityBufferTime; //获取RTMP播放实际的缓冲时间
@property(nonatomic,assign,readonly)VHPlayerState playerState;//播放器状态



/**
 *  视频View的缩放比例 默认是自适应模式
 */
 @property(nonatomic,assign)VHRTMPMovieScalingMode movieScalingMode;
 
 
 /**
   *  当前视频观看模式 观看直播允许切换观看模式(回放没有) 
   *
   /
 @property(nonatomic,assign)VHMovieVideoPlayMode playMode;
 
 
 
 /**
   *  设置默认播放的清晰度 默认原画
   */
   @property(nonatomic,assign)VHMovieDefinition defaultDefinition;
   
   
   
   
 /*! @brief 直播视频清晰度 （只有直播有效） 
 * 
 *  @return 返回当前视频清晰度 如果和设置的不一致 设置无效保存原有清晰度 设置成功刷新直播，有可能设置失败，请再获取curDefinition查看       设置状态
 *  当前视频清晰度 观看直播允许切换清晰度(回放没有) 默认是defaultDefinition 
 */
 @property(nonatomic,assign)VHMovieDefinition curDefinition;
 
 
  /** 
   *  设置渲染视图 在VideoPlayMode:isVrVideo: 中设置 默认VHRenderModelNone 必须设置否则会    出现黑屏        
   */
   @property(nonatomic,assign)VHRenderModel renderViewModel;
   
   
 2：初始化VHMoviePlayer对象 
 /**
  *  初始化VHMoviePlayer对象
  * 
  *  @param delegate
  * 
  *  @return   返回VHMoviePlayer的一个实例 
  
  */
  -(instancetype)initWithDelegate:(id <VHallMoviePlayerDelegate>)delegate; 
  
  3:设置渲染模式
  /**
* 设置渲染视图 在VideoPlayMode:isVrVideo: 中设置 或在直播前设置
 */
- (void)setRenderViewModel:(VHRenderModel)renderModel;

  4：观看直播(RTMP)
 /**
 *  观看直播视频
 *
 *  @param param 
 *  param[@"id"] = 活动Id 必传 
 *  param[@"name"]  = 如已登录可以不传 
 *  param[@"email"] = 如已登录可以不传 
 *  param[@"pass"]  = 活动如果有K值或密码需要传 
 * 
 */
 -(BOOL)startPlay:(NSDictionary*)param;
 
 5:观看视频回放（仅HLS可用）
 /**
 *  观看回放视频   (仅HLS可用) 
 * 
 *  @param param 
 *  param[@"id"]    = 活动Id 必传 
 *  param[@"name"]  = 如已登录可以不传 
 *  param[@"email"] = 如已登录可以不传 
 *  param[@"pass"]  = 活动如果有K值或密码需要传 
 * 
 *  @param moviePlayerController MPMoviePlayerController 对象 
 */
 -(BOOL)startPlayback:(NSDictionary*)param moviePlayer:(MPMoviePlayerController *)moviePlayerController;
 
  6:暂停拉流播放
 /** 
  *  暂停直播播放,不会停止接收聊天 ppt等事件(只用直播活动) 
  */
  -(void)pausePlay;
  
  7：重新拉流播放
  /**
 * 播放出错/pausePlay后恢复直播播放(只用直播活动)
* @return NO 播放器不是暂停状态 或者已经结束
*/
 -(BOOL)reconnectPlay;
 
 8：停止观看直播
 /**
  *  停止直播 也会停止直播相关功能如聊天等 
 */
 -(void)stopPlay;
 
 9：设置静音
 /**
 *  设置静音
 * 
 *  @param mute 是否静音 
 */
 -(void)setMute:(BOOL)mute;
 
 10：设置系统声音大小
 /**
  *  设置系统声音大小
  *
  *  @param size float  [0.0~1.0]
  */
  +(void)setSysVolumeSize:(float)size;
  
 11：获取系统声音大小
 /**
  *  获取系统声音大小
  */
 +(float)getSysVolumeSize;
 
 12:销毁播放器
 /**
  *  销毁播放器 
  */
  -(void)destroyMoivePlayer;
  
  
  13：是否使用陀螺仪，仅VR播放时可用
  - (void)setUsingGyro:(BOOL)usingGyro;
  
  14：设置视屏布局方向，仅VR模式可用，要开启陀螺仪
  - (void)setUILayoutOrientation:(UIDeviceOrientation)orientation;
  
  15：观看直播视频（仅HLS可用，2.3.4以后不维护此功能）
  /**
 *  观看直播视频   (仅HLS可用)
 *
 *  @param param
 *  param[@"id"] = 活动Id 必传 
 *  param[@"name"] =未登录用户必须传值，用户昵称，已登录用户可传也可以不传
 *  param[@"email"] =未登录用户必须传值，用户邮箱，如果无邮箱需填写设备唯一标    识保证唯一性，已登录用户可传也可以不传
 *  param[@"pass"] = K值，已创建的活动如果有K值需要传，没有可不传
 * 
 *  @param moviePlayerController MPMoviePlayerController 对象 
 */
 -(void)startPlay:(NSDictionary*)param moviePlayer:(MPMoviePlayerController *)moviePlayerController;
 
 
 
 16:看直播事件响应
 VHallMoviePlayerDelegate
/**
* 播放连接成功
 * @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx}
* code：状态码，如枚举值（0,1，…）content：对应的状态说明
*/
- (void)connectSucceed:(VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info;
/**
* 缓冲开始回调
* @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx}
* code：状态码，如枚举值（0,1，…）content：对应的状态说明
*/
- (void)bufferStart:(VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info;
/**
 * 缓冲结束回调
 * @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx}
* code：状态码，如枚举值（0,1，…）content：对应的状态说明
*/
-(void)bufferStop:(VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info;
/**
* 下载速率的回调
 *
 * @param moviePlayer
* @param info 下载速率信息 单位kbps
* @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx}
* code：状态码，如枚举值（0,1，…）content：对应的状态说明
*/
- (void)downloadSpeed:(VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info;
/**
* cdn 发生切换时的回调
*
* @param moviePlayer
* @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx}
* code：状态码，如枚举值（0,1，…）content：对应的状态说明
*/
- (void)cdnSwitch:(VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info;
/**
* Streamtype
 *
* @param moviePlayer moviePlayer
* @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx}
* code：状态码，如枚举值（0,1，…）content：对应的状态说明
 */
- (void)recStreamtype:(VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info;
/**
* 播放时错误的回调
*
* @param livePlayErrorType 直播错误类型
* @param info 直播状态对应信息，字典格式{@"code":xx, @"content"：xxx} * code：状态码，如枚举值（0,1，…）content：对应的状态说明
 */
- (void)playError:(VHLivePlayErrorType)livePlayErrorType info:(NSDictionary*)info;
/**
 * 获取视频活动状态
*
 * @param playMode 视频活动状态
*/
- (void)ActiveState:(VHMovieActiveState)activeState;
/**
* 获取当前视频播放模式
*
* @param playMode 视频播放模式
*/
- (void)VideoPlayMode:(VHMovieVideoPlayMode)playMode isVrVideo:(BOOL)isVrVideo;
/**
* 获取当前视频支持的所有播放模式
*
* @param playModeList 视频播放模式列表
*/
- (void)VideoPlayModeList:(NSArray*)playModeList;
/**
* 该直播支持的清晰度列表
 *
* @param definitionList 支持的清晰度列表
*/
- (void)VideoDefinitionList:(NSArray*)definitionList;
/**
* 直播结束消息
 *
* 直播结束消息
 */
- (void)LiveStoped;
/**
 * 播主发布公告
 *
* 播主发布公告消息
*/
- (void)Announcement:(NSString*)content publishTime:(NSString*)time;
/**
 * 包含文档 获取翻页图片路径
 *
* @param changeImage 图片更新
*/
- (void)PPTScrollNextPagechangeImagePath:(NSString*)changeImagePath;

/**
* 画笔
*
*
*/
- (void)docHandList:(NSArray*)docList whiteBoardHandList:(NSArray*)boardList;
  
  
  
 --------------------------------------------------------------------
 
 2:观看VR视频功能
 2.1:实现VHallMoviePlayerDelegate 代理方法
 /**
 *  获取当前视频播放模式
 *
 *  @param playMode  视频播放模式
 */
-(void)VideoPlayMode:(VHallMovieVideoPlayMode)playMode isVrVideo:(BOOL)isVrVideo;根据isVideo返回值选择正确渲染视图模式（具体代码参见WatchLiveViewController）

2.2:陀螺仪设置是否开启（参见VHMoviePlayer.h）
/**
  *  是否使用陀螺仪，仅VR播放时可用
  */
  - (void)setUsingGyro:(BOOL)usingGyro;
  具体代码参见WatchLiveViewController

 
 
 
 
  
  
  
 
 
 
 
 
 
 
 
 
 
 
  
  
 
 

  
   
   
 