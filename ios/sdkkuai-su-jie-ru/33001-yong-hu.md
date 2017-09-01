如果使用聊天和问答功能，需要用户提前调用WebApi进行注册用户操作。否则提示用户不存在。详细接口说明，查看 http://e.vhall.com/home/vhallapi/active#user_register_第三方创建用户。

1：登陆
/*!
 *  登录 (如使用聊天，问答等功能必须登录)
 * 
 *  @param aAccount         账号  需服务器调用微吼注册API 注册该用户账号密码 
 *  @param aPassword        密码
 *  @param aSuccessBlock    成功的回调 
 *  @param aFailureBlock    失败的回调
 * 
 */
 + (void)loginWithAccount:(NSString *)aAccount   password:(NSString *)aPassword  success:(void (^)())aSuccessBlock                failure:(void (^)(NSError *error))aFailureBlock;
 
 
2：退出当前账号
/*!
 *  登录 (如使用聊天，问答等功能必须登录)
 * 
 *  @param aAccount         账号  需服务器调用微吼注册API 注册该用户账号密码 
 *  @param aPassword        密码
 *  @param aSuccessBlock    成功的回调 
 *  @param aFailureBlock    失败的回调
 * 
 */
 + (void)loginWithAccount:(NSString *)aAccount   password:(NSString *)aPassword  success:(void (^)())aSuccessBlock                failure:(void (^)(NSError *error))aFailureBlock;
 
 
 3：获取当前登陆状态
 /*!
 *  获取当前登录状态
 *
 *  @result 当前是否已登录
 */
+ (BOOL)isLoggedIn;

4:获取当前登陆账号
* 获取当前登录用户账号
*
* @result 前登录用户账号
 */
+ (NSString *)currentAccount;

5：获取当前SDK版本号
VHallApi.h
为了有效、高效定位客户问题，SDK版本号可做为定位原因的基础信息提供给微吼。
/**
 *  获取当前SDK版本号
 *  @return 当前SDK版本号
 */
  +(NSString *) sdkVersion;
  
  6:日志设置
  VHallApi.h
为了有效、高效定位客户问题，SDK版本号可做为定位原因的基础信息提供给微吼。
VHLogType_OFF = 0, //关闭日志 默认设置
VHLogType_ON = 1, //开启日志
VHLogType_ALL = 2, //开启全部日志
+ (void)setLogType:(VHLogType)type;


 