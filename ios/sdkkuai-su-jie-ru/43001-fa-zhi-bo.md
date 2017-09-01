VHallLivePublish.h 发直播

1：发直播属性
/** 
*  推流连接的超时时间，单位为毫秒 默认5000 
*/
@property (nonatomic,assign)int publishConnectTimeout;

/**
 *  推流断开重连的次数 默认为 5 
 */
 @property (nonatomic,assign)int publishConnectTimes;
 
 
 /**
  *  用来显示摄像头拍摄内容的View
  */
  @property (nonatomic,strong,readonly)UIView * displayView;
  
  
/**
 *  视频采集的帧率 范围［10～30］ 
 */
  @property (nonatomic,assign)int videoCaptureFPS;
  
 /**
  *  代理
  */
 @property (nonatomic,assign)id <VHallLivePublishDelegate> delegate;
 
 
 
 /** 
   *  视频分辨率 默认值是kGeneralViodeResolution 960*540 
   */
  @property (nonatomic,assign)VHVideoResolution videoResolution;
  
  /**
   *  视频码率设置 
   */
   @property (nonatomic,assign)NSInteger videoBitRate;
   
   /**
    *  音频码率设置
    */
   @property (nonatomic,assign)NSInteger audioBitRate;
   
   
   /**
     *  设置静音
     */ 
   @property (assign,nonatomic)BOOL isMute; 

      
  /**
   *  判断用户使用是前置还是后置摄像头
   */
   @property (nonatomic,assign,readonly)AVCaptureDevicePosition captureDevicePosition;          
                  
   /**
    *  当前推流状态
    */                     
   @property (assign,nonatomic,readonly)BOOL isPublishing; 
   
   
   /**
    * 是否开启噪声消除，默认开启，最高支持32k的音频采样率,直播前设置，当采样率大于32k时，自动关闭噪声消除 
    * 注：开始直播后调用无效
    */
   @property(assign,nonatomic)BOOL isOpenNoiseSuppresion;
   

2：初始化直播引擎
/**
 *  初始化 直播引擎
 *  @param orientation视频拍摄方向
 *
 *  @return 是否成功
 */
 - (id)initWithOrientation:( VHDeviceOrientation)orientation;
 
3：设置采集设备
/**
 *  初始化 直播引擎
 *  @param orientation视频拍摄方向
 *
 *  @return 是否成功
 */
 - (id)initWithOrientation:( VHDeviceOrientation)orientation;
 
 4：初始化音频设备
 -(BOOL)initAudio;
 
 5：开始采集视频
 -(BOOL)startAudioCapture;
 
 6:停止采集视频
 - (BOOL)stopVideoCapture;
 
 7：开始发起直播
 /**
  *  开始发起直播 要在 initWithOrgiation initCaptureVideo initAudio startVideoCapture之后调用	 
  *  @param param 	
  *  param[@"id"] = 活动Id 必传 	
  *  param[@"access_token"] = 必传 	
  */
  - (void)startLive:(NSDictionary*)param;
  
  8：结束直播
  /**
 *  结束直播
 *  与startLive成对出现，如果调用startLive，则需要调用stopLive以释放相应资源
  */
  - (void)stopLive;
 
 9：断开推流
 /**
  *  断开推流的连接,注意app进入后台时要手动调用此方法 回到前台要reconnect重新直播		 
  */
  - (void)disconnect;
  
 10：重新推流
  /**
   * 重连流
  */
  -(void)reconnect;
  
  
  11：切换摄像头
  /**
  *  切换摄像头
  *
  *  @param captureDevicePosition
  * 
  *  @return 是否切换成功
  */
  -(BOOL)swapCameras:(AVCaptureDevicePosition)captureDevicePosition;
  
  12：手动对焦
  /**
  *手动对焦
  */
  -(void)setFoucsFoint:(CGPoint)newPoint;
  
  13：变焦
  /**
  *  变焦 
  * 
  *  @param zoomSize 变焦的比例
  *
  /-(void)captureDeviceZoom:(CGFloat)zoomSize;
  
  14：设置闪光灯模式
  /**
  *  变焦 
  * 
  *  @param zoomSize 变焦的比例
  *
  /-(void)captureDeviceZoom:(CGFloat)zoomSize;

   15：x销毁直播引擎
   /**
  *  销毁初始化数据
  *
  /-(void)destoryObject; 
  
  16：音频增益
  /*
* 设置音频增益大小，注意只有当开启噪音消除时可用
 @param size 音频增益的大小 [0.0,1.0]
*/
- (void)setVolumeAmplificateSize:(float)size;

17：发直播事件响应
1、添加代理事件
/**
 *  采集到第一帧的回调 
 *  @param image 第一帧的图片 
 */
 -(void)firstCaptureImage:(UIImage*)image;
 /**
  *  发起直播时的状态
  *
  *  @param liveStatus 直播状态 查看 文档中发直播枚举类型
  *  @param info  直播状态对应信息，字典格式 {@"code":xx,@"content"：xxx}
  *  code：状态码/错误码，如枚举值（0,1，…）content：对应的状态或错误说
  *  明,如播放缓冲开始、播放缓冲结束等
  */	
  
  -(void)publishStatus:( VHLiveStatus)liveStatus withInfo:(NSDictionary*)info;
  当liveStatus == VHLiveStatusPushConnectSucceed时，content代表出错原因
  
  4001   握手失败 
  4002   链接vhost/app失败 
  4003   网络断开 （预留，暂时未使用） 
  4004   无效token 
  4005   不再白名单中 
  4006   在黑名单中 
  4007   流已经存在 
  4008   流被禁掉 （预留，暂时未使用） 
  4009   不支持的视频分辨率（预留，暂时未使用） 
  4010   不支持的音频采样率（预留，暂时未使用） 
  4011   欠费
                         
                            
                               
---------------------------------------------------------------------
2:美颜功能

 2.1:配置是否开启美颜功能(如果启用美颜功能必须包含美颜功能滤镜库)  
 ![](/assets/图片 18.png)
 
 2.2:初始化VHallLivePublishFilter类,初始化方法参考VhallLivePublish
 ![](/assets/图片 19.png)
 
 2.3:开启美颜功能所需额外配置
![](/assets/图片 20.png)
注释：openFilter=YES为开启美颜


/**
 * setBeautifyFilterWithBilateral:Brightness:Saturation: 设置VHall美颜滤镜参数 GPUFilterDelegate == nil时有效
 *   @param distanceNormalizationFactor  // A normalization factor for the distance between central color and sample color.
 * @param brightness                   // The brightness adjustment is in the range [0.0, 2.0] with 1.0 being no-change.
 * @param saturation                   // The saturation adjustment is in the range [0.0, 2.0] with 1.0 being no-change.* return BOOL YES设置成功 NO 设置失败*/ 
 
 2.4:自定义滤镜代理id<VHallLivePublishFilterDelegate>GPUFilterDelegate
 GPUFilterDelegate 滤镜代理 ，在代理方法中添加您自己的滤镜
注释：
(1)	默认为nil,只有使用自己的滤镜的情况下设置此代理
(2)	必须发直播前设置
(3)	如果此属性不为nil时 ，SDK自带美颜功能失效，使用代理中设置的滤镜发起直播
 
 
 
 
 
 
   
                                    
                                          
                                                
                                                      
                                                            
                                                                  
                                                                        
                                                                              
                                                                                    
                                                                                                
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   