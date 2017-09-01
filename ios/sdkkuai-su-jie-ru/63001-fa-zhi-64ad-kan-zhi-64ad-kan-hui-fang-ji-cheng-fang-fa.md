1：注册AppKey
#import "VHallApi.h"
-application: didFinishLaunchingWithOptions: {
… 			
[VHallApi registerApp: XXXXXX SecretKey:XXXXXX]; 
…
}
--------------------------------------------------------------------------
2:发直播
（1）在viewDidLoad添加推流引擎初始化代码
  self.engine = [[VHallLivePublish alloc] initWithOrientation: deviceOrientation]; 
   [self.engine initCaptureVideo:AVCaptureDevicePositionBack];    
   [self.engine initAudio];   
   self.engine.delegate = self;    
   self.engine.displayView.frame = self.view.bounds;    
   [self.view insertSubview:self.engine.displayView atIndex:0]; 
      //开始视频采集、并显示预览界面    [
  self.engine startVideoCapture];
  
  
  
  （2）发起直播推流代码
  
   NSMutableDictionary * param = [[NSMutableDictionary alloc]init];    
   param[@"id"] =@"123456789" ;  //直播id	    
   param[@"access_token"] = @"XXXXXXX";//直播token
   [_engine startLive:param];
   
   
   （3）发直播事件代理CameraEngineDelegate
   -(void)firstCaptureImage:(UIImage *)image{ 
   NSLog(@"第一帧");
   }
   
   -(void)publishStatus:( VHLiveStatus)liveStatus withInfo:(NSDictionary *)info{    
   if(liveStatus == VHLiveStatusPushConnectSucceed)        
   NSLog(@"----------------发起成功");    	
   NSLog(@"liveStatus：%d content：%@",liveStatus,info[@"content"]);}
-----------------------------------------------------------------------
3：看直播
（1）在viewDidLoad里面初始化播放器
 self.moviePlayer = [[VHallMoviePlayer alloc]initWithDelegate:self];    
 [self.moviePlayer  setRenderViewModel: VHRenderModelOrigin];
 [self.view addSubview: self.moviePlayer.moviePlayerView];
 self.moviePlayer.moviePlayerView.frame = self.view.bounds;
 
 （2）观看直播活动
  NSMutableDictionary * param = [[NSMutableDictionary alloc]init];    
  param[@"id"] = @"296380230";    
  param[@"name"]=[UIDevice currentDevice].name;    
  param[@"email"]=[[[UIDevice currentDevice]identifierForVendor] UUIDString];
  [self.moviePlayer startPlay:param];
  
  
  （3）观看直播事件代理VHallMoviePlayerDelegate
  -(void)playError:( VHLivePlayErrorType)livePlayErrorType info:(NSDictionary *)info;{NSLog(@"%@",info);}
  - (void)connectSucceed:( VHallMoviePlayer*)moviePlayer info:(NSDictionary *)info{NSLog(@"连接成功");}
  - (void)bufferStart:( VHallMoviePlayer*)moviePlayer info:(NSDictionary *)info{}
  - (void)bufferStop:( VHallMoviePlayer*)moviePlayer info:(NSDictionary *)info{}
  - (void)downloadSpeed:( VHallMoviePlayer*)moviePlayer info:(NSDictionary *)info{}
  - (void)recStreamtype:( VHallMoviePlayer*)moviePlayer info:(NSDictionary*)info{}
  ---------------------------------------------------------------------------
 4：看回放
 （1）在viewDidLoad里面初始化播放器
self.moviePlayer = [[VHallMoviePlayer alloc]initWithDelegate:self];    
self.hlsMoviePlayer =[[MPMoviePlayerController alloc] init];    
[self.hlsMoviePlayer.view setFrame:self.view.bounds];  // player的尺寸
[self.view addSubview:self.hlsMoviePlayer.view];   


（2）点击开始播放事件
NSMutableDictionary * param = [[NSMutableDictionary alloc]init];    
param[@"id"] = @"890355280" ;    
param[@"name"] = [UIDevice currentDevice].name;    
param[@"email"] = [[[UIDevice currentDevice] identifierForVendor] UUIDString];
[_moviePlayer startPlayback:param moviePlayer:self.hlsMoviePlayer]; 


-----------------------------------------------------------------------

 












