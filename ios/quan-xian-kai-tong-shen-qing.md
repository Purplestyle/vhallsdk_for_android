1：申请key 
请点击 [API&SDK 权限申请](http://webim.qiao.baidu.com/im/index?siteid=113762&ucid=2052738)，或4006826882电话立即沟通申请，申请后客户经理会在线上与您直接联系

审核通过后，可以获取开发应用的权限信息： App Key 、App Secret Key  , [立即查看](http://e.vhall.com/home/vhallapi/authinfo)

2:绑定应用签名信息
使用SDK前集成前，务必先配置好此签名信息，否则使用时会出现“身份验证失败”提示信息

进入[http://e.vhall.com/home/vhallapi/authlist](http://e.vhall.com/home/vhallapi/authlist), API/SDK使用权限信息页面

选择已开通的应用进行编辑操作

点击下一步进入应用绑定页面

选择 IOS-SDK切页面后输入安全码 BundleID 项。（Bundle Identifier 在项目 Targets的 General中找到 如下图）

![](/assets/图片 1.png)

-----------------------------------------------------------------------------------------

3:第三方K值认证
 1认证流程
 ![](/assets/图片 5.png)
 2开启设置
 2.1 第三方回调接口设置
 1）全局设置： 针对所有的活动配置生效，如果针对单个活动再做配置，以单个活动配置为最终配置。接口调用设置接 口：webinar/whole-auth-url 全局配置第三方K值验证URL
2) 针对某个活动的配置方式一：通过页面配置 http://e.vhall.com/webinar/auth/123456789 ，数字表示自己帐号下的活动id
3）针对某个活动的配置方式二：通过接口(webinar/create或webinar/update)设置
4）接口参数：use_global_k ，默认为0不开启，1为开启,是否针对此活动开启全局K值配置；当设置为0后，则以单个活动的配置为最终配置。

2.2 Vhall接口URL中请务必带上k参数，如果这个参数为空或者没有这个参数，则视为认证失败


注：需要确保您的回调地址支持 multipart/form-data 方式接收 post 数据。


-----------------------------------------------------------------------------------------
4:k值使用
1）网页嵌入或SDK里的调用方法，请务必带上k参数，如果这个参数为空或者没有这个参数，则视为认证失败
  网页嵌入地址类似：
  http://e.vhall.com/webinar/inituser/123456789?email=test@vhall.com&name=visitor&k=随机字符串
  SDK里的调用方法,需要传递3个参数name,email,pass
  email:可选参数，如果不填写系统会随机生成邮箱地址。 由于email自身的唯一性，我们推荐使用email来作为唯一标识有效用户的字段。对于第三方自有用户数据的系统，也可以使用一些特征ID作为此标识，请以email的格式组织，比如在第三方系统中，用户ID为123456，可在其后添加一个@domain.com,组成123456@domain.com形式的email地址。
  
  
  
  2） Vhall系统收到用户的接口访问请求后，会向第三方认证URL(auth_url)发送HTTP POST请求，同时将email和k值作为POST数据提交 给第三方认证。由第三方系统验证k值的合法性。如果认证通过，第三方认证URL(auth_url)返回字符串pass,否则的返回fail
  3）	Vhall 系统根据第三方认证URL返回值判断认证是否成功。只有收到pass，才能认定为验证成功，否则一律跳转到指定的认证失败 URL，或者提示'非法访问'
  
 4）参数特征
 URL请求很容易被探测截获，这就要求第三方系统生成的K值必须有以下特征：
  唯一性：每次调用接口必须产生不同的K值
  时效性：设定一个时间范围，超时的K值即失效。
  如果包含有第三方系统内部信息，必须加密和混淆过。
5）建议的K值实现
第三方系统可以考虑K值元素包括：用户ID、Vhall直播ID、时间戳（1970-01-01至今的秒数）元素组合后加密后，使用Base64或者hex 匹配成URL可识别编码。K值在第三方系统中持久化或放在Cache中


DB或Cache建议有时效性控制，自动失效或定期清理过期数据




  
  

