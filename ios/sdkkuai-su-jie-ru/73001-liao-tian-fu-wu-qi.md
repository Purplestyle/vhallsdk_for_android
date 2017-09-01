1：聊天

 如果使用聊天和问答功能，需要用户提前调用WebApi进行注册用户操作。否则提示用户不存在。详细接口  说明，查看 http://e.vhall.com/home/vhallapi/active#user_register_第三方创建用户。   VHallChat.h

1.1：创建聊天实例
_chat = [[VHallChat alloc] initWithMoviePlayer:_moviePlayer];//看直播
_chat = [[VHallChat alloc] initWithLivePublish:self.engine];//发直播


1.2：设置代理
_chat.delegate = self; 

1.3：发送聊天内容
/**
 *  发送聊天内容
 *  成功回调成功Block 
 *  失败回调失败Block 
 *  失败Block中的字典结构如下：
 *  key:code 表示错误码
 *  value:content 表示错误信息
 */	
 - (void)sendMsg:(NSString *)msg success:(void(^)())success failed:(void (^)(NSDictionary* failedData))reslutFailedCallback;
 
 1.4：接受上下线消息（代理方法）
 /**
  *  接收上下线消息
  *  代理方法先设置delegate属性
  *  接收到的VHallOnlineStateModel实例数组
  */
 - (void)reciveOnlineMsg:(NSArray *)msgs;
 
 1.5：接收聊天消息（代理方法）
 /**
 *  接收聊天消息
 *  代理方法先设置delegate属性 
 *  接收到的VHallChatModel实例数组 
 */
 - (void)reciveChatMsg:(NSArray *)msgs;
 
 
 
 
 -------------------------------------------------------------------------
2: 问答
如果使用聊天和问答功能，需要用户提前调用WebApi进行注册用户操作。否则提示用户不存在。详细接口说明，查看 http://e.vhall.com/home/vhallapi/active#user_register_第三方创建用户。   VHallQAndA.h 

2.1 设置代理
_QA.delegate = self;

2.2 发送问题 
/**
  *  发送问题
  *  成功回调成功Block 
  *  失败回调失败Block
  *  失败Block中的字典结构如下：
  *  key:code 表示错误码
  *  value:content 表示错误信息
  */		
  - (void)sendMsg:(NSString *)msg success:(void(^)())success failed:(void (^)(NSDictionary* failedData))reslutFailedCallback;
  
 2.3  接收问答消息(代理方法)
 /**
  *  接收问答消息
  *  代理方法先设置delegate属性
  *  接收到的VHallQAModel实例数组
  */
 - (void)reciveQAMsg:(NSArray *)msgs;
  
 -----------------------------------------------------------------------
3:抽奖功能  请详见VHallLottery.h文件的说明

3.1 设置代理
_lottery.delegate = self;

3.2 提交个人中奖信息
/**
  *  提交个人中奖信息 	
  *  @param info   个人信息 	
  * key:user_name 用户名 	
  * key:phone     电话 	
  *  成功回调成功Block 	
  *  失败回调失败Block 	
  *  失败Block中的字典结构如下： 	
  * key:code 表示错误码 	
  * value:content 表示错误信息 	
  */	 
  - (void)submitLotteryInfo:(NSDictionary *)info success:(void(^)())success failed:(void (^)(NSDictionary *failedData))reslutFailedCallback;

3.3接收抽奖开始消息(代理方法)
/**
 *  接收抽奖开始消息
 *  代理方法先设置delegate属性
 *  接收到的VHallStartLotteryModel实例
 */
 - (void)startLottery:(VHallStartLotteryModel *)msg;
 
 
3.4接收抽奖结果消息(代理方法)
/**
 *  接收抽奖结果消息 
 *  代理方法先设置delegate属性
 *  接收到的VHallEndLotteryModel实例 
 */
 - (void)endLottery:(VHallEndLotteryModel *)msg;
--------------------------------------------------------------------------

4:公告功能

4.1公告代理方法(VHallMoviePlayerDelegate)
/**
  *  播主发布公告
  *
  *  播主发布公告消息
  */
  - (void)Announcement:(NSString*)content publishTime:(NSString*)time;
  
4.2实例化公告展示UI
![](/assets/图片 21.png)



------------------------------------------------------------------------
5：文档演示功能
5.1: 新增枚举
![](/assets/图片6.png)

5.2 新增代理方法
![](/assets/图片7.png)

5.3 代理方法使用
注释：新增代理方法，只在视频直播和回放请求成功后会返回对应返回值；请求失败，返回值为nil；遵从的方法如下图：文件位置  VHallMoviePlayer.h
![](/assets/图片 9.png)
代理方法实现：
请参考SDK demo 文件：
以下文件均可
![](/assets/图片 11.png)
![](/assets/图片 12.png)
![](/assets/图片 13.png)


方法实现：
注释：
-(void)PPTScrollNextPagechangeImagePath:(NSString*)changeImagePath,此方法中，图片缓存处理请开发者根据自己需求处理图片缓存
![](/assets/图片 14.png)

---------------------------------------------------------------------------
6：签到功能  请详见VHallSign.h文件的说明需实现 （VHallSignDelegate）
 
 6.1:开始签到代理方法
 /**
 *  开始签到
 *
 *  开始签到消息
 */
 - (void)startSign;
 
 6.2:距离签到结束剩余时间代理方法
 /**
  *  距签到结束剩余时间
  *
  *  距签到结束剩余时间 
  */
  - (void)signRemainingTime:(NSTimeInterval)remainingTime;
  
  6.3:签到结束代理方法
  /**
  *  签到结束
  *
  *  签到结束消息
  */
  - (void)stopSign;
  
  6.4: 签到
  /**
 *  签到
 *  成功回调成功Block 
 *  失败回调失败Block 
 *  失败Block中的字典结构如下： 
 *  key:code 表示错误码 
 *  value:content 表示错误信息
 * 10010  活动不存在
 * 10011  不是该平台下的活动 
 * 10017  活动id 不能为空
 * 10807  用户id不能为空 
 * 10813  签名ID不能为空 
 * 10814  用户名称不能为空 
 * 10815  当前用户已签到 
 */
 -(BOOL)signSuccess:(void(^)())success failed:(void (^)(NSDictionary* failedData))reslutFailedCallback;
 ![](/assets/图片 23png.png)
 
 6.5：取消签到
 /**
  *  取消签到
  * 
  *  取消签到
 */
 - (void)cancelSign;
 
 ------------------------------------------------------------------------
 
7：问卷功能
 
 7.1: 获取问卷消息(需实现VhallSurveyDelegate)
 /**
  *  接收问卷消息
  *
  * 
  */
  -(void)receiveSurveryMsgs:(NSArray*)msg;
  
 7.2:根据问卷ID获取问卷详情
  /**
* 获取问卷内容
*
* @param surveyId 调查问卷Id
* @param webId 当前活动Id
* @param success 成功回调成功Block 返回问卷内容
* @param reslutFailedCallback 失败回调失败Block
* 失败Block中的字典结构如下：
* key:code 表示错误码
* value:content 表示错误信息 */- (void)getSurveryContentWithSurveyId:(NSString*)surveyId webInarId:(NSString*)webId success:(void(^)(VHallSurvey* msgs))survey failed:(void (^)(NSDictionary* failedData))reslutFailedCallback;

7.3:发送问卷结果
/**
  * 发送完成问卷
  * 
  * 成功回调成功Block
  * 失败回调失败Block
  * 		失败Block中的字典结构如下：
  * 		key:code 表示错误码 
  *		value:content 表示错误信息 
  */
  - (void)sendMsg:(NSArray *)msg success:(void(^)())success failed:(void (^)(NSDictionary* failedData))reslutFailedCallback;
  --------------------------------------------------------------------------
  
8：画笔白板功能
  8.1:初始化VHDocumentView
  VHDocumentView 负责展示PPT、白板以及画笔渲染，使用之前需要初始化。初始化位置为收到PPT翻页消息代理方法中（-（void）PPTScrollNextPagechangeImagePath:(NSString*)changeImagePath（具体看demo实例）
  
  8.2:接收画笔以及白板绘制消息
  需要实现VHallMoviePlayerDelegate中的协议（docList为文档画笔数据,boardList为白板画     笔数据）
/**
* 画笔
*
 *
 */
- (void)docHandList:(NSArray*)docList whiteBoardHandList:(NSArray*)boardList
--------------------------------------------------------------------------

8:回放评论功能
 8.1: 发表评论
 /**    
  *  发表评论内容
  *  成功回调成功Block      
  *  失败回调失败Block      
  *  失败Block中的字典结构如下：      
  *  key:code 表示错误码      
  *  value:content 表示错误信息      
  */
  - (BOOL)sendComment:(NSString *)comment success:(void(^)())success failed:(void (^)(NSDictionary* failedData))reslutFailedCallback;
  
  8.2: 获取历史评论
  /** 注意（当A用户发完一条评论，B立即拉取评论内容，此时数据库会返回一条重复数据，第三方用户可以根据返回模型里面的commentId 进行去重处理）
*获取历史评论记录 在进入回放活动后调用
*@param limit         每次拉取数据条数，默认每次20条，最多50条
*@param pos          从第几条数据开始获取，默认0       
*  成功回调成功Block       
*  失败回调失败Block       
*  失败Block中的字典结构如下：       
*  key:code 表示错误码      
*  value:content 表示错误信息-(void)getHistoryCommentPageCountLimit:(NSInteger)limit offset:((NSInteger) pos  success(void(^)(NSarray *msgs))success  failed:(void(^)(NSDictionary * faileData))reslutFailedCallback
  

  


  
 
 
  
  
 
 








 


