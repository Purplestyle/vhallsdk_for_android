# 修订记录

* 修订记录
  | 日期 | 版本号 | 描述 | 修订者 |
  | :--- | :--- | :--- | :--- |
  | 2016-04-21 | v2.1.1 | 初稿 | xy |
  | 2016-05-06 | v2.2.0 | 新增文档演示 | xy |
  | 2016-05-06 | v2.8.0 | VR、陀螺仪 |  |
  |  |  |  |  |

---

# 简介

```
| 2016-05-06 | v2.2.0 | 新增文档演示 | xy |
| 2016-05-06 | v2.2.0 | 新增文档演示 | xy |
```

本文档为了指导开发者更快使用Android系统上的 “自助式网络直播服务SDK”，默认读者已经熟悉IDE的基本使用方法（本文以Android Studio为例），以及具有一定的编程知识基础等

### 1. 新版本重点说明

### 2. 支持的产品特性如下

| 分类 | 特性名称 | 描述 |
| :--- | :--- | :--- |
| 发直播 | 支持编码类型 | 音频编码：AAC，视频编码：H.264 |
|  | 支持推流协议 | RTMP |
|  | 视频分辨率 | 640\*480 |
|  | 屏幕朝向 | 横屏 竖屏 |
|  | 闪光灯 | 开/关 |
|  | 静音 | 开/关 |
|  | 切换摄像头 | 前、后置摄像头 |
|  | 目标码率 | 使用软编，码率固定在300-400之间 |
|  | 目标帧率 | 帧率默认为10帧 最大可修改到30帧 |
| 看直播 | 支持播放协议 | RTMP |
|  | 延时 | RTMP: 2-5秒 |
|  | 支持解码 | H.264 |
| 文档演示 | 支持文档演示 | 文档可与视频同步演示 |
| 观看回放 | 支持协议 | HLS |
| 权限 | 第三方K值认证 | 支持客户自己的权限验证机制来控制看直播看回放 |
| 用户标识\(new\) | 支持用户标识 | 主要用于聊天、问答等用户互动模块 |
| 聊天 | 支持发起观看直播聊天 | 用户标识后可聊天 |
| 问答 | 支持看直播提问 | 用户标识后可提问 |
| 单音频切换 | 观看对音频转换 | 视频转音频，视频+文档转音频 |
| 签名校验 | 应用签名包名 | 保证应用安全防护 |

### 3. SDK 流程图

![](/assets/1502357659.jpg)

# 权限开通申请

### 1. 申请Key

[http://webim.qiao.baidu.com//im/index?siteid=113762&ucid=2052738](http://webim.qiao.baidu.com//im/index?siteid=113762&ucid=2052738)  
或者致电400-888-9970  
申请后客户经理会在线上与您直接联系。

### 2. 绑定应用签名信息

使用SDK前集成前，务必先配置好此签名信息，否则使用时会出现"**身份验证失败**"提示信息，配置信息流程如下

* 进入[http://e.vhall.com/home/vhallapi/authlist](http://e.vhall.com/home/vhallapi/authlist) 
* 选择已开通的应用进行编辑操作

  ![](/assets/create_auth.jpg)

* AppKey,SecretKey,AppSecretKey 自动生成,初始化SDK时需要传入

* Android 集成需要填写 SHA1 和 包名 , 对应集成的App 

### 3. 获取安全码SHA1注意事项

SHA1分为Debug和Release版本 如果绑定签名时使用的是Debug签名,运行时也要使用debug.keystore.

* Debug 版本 一般直接运行时使用的是Debug版 地址 C:\Users\用户名.android\debug.keystore
* Release 版本 一般发版时使用的是Release版 使用打包时的KeyStore

### 4. 获取直播Token

* 通过客户端接口获取到，此接口需调用vhall接口 **verify/access-token** 获取

# SDK集成前必要的准备工作

### 1. 下载SDK与DEMO

Github ：[https://github.com/vhall/vhallsdk\_live\_android/releases](https://github.com/vhall/vhallsdk_live_android/releases)

### 2. 开发环境要求

Pc操作系统：64window系统  
JDK: 1.7以上  
Android studio : 建议使用Android studio 2.0以上  
Android: 4.0以上  
备注： Android设备操作系统需要4.0以上, 需要访问手机硬件,暂不支持模拟器开发

### 3. 需要导入的AAR

vhallsdk.aar

### 4. 添加依赖

```
compile 'com.github.bumptech.glide:glide:3.7.0' // 用于加载PPT
compile('io.socket:socket.io-client:0.8.3') {//用于SDK网络连接
    exclude group: 'org.json', module: 'json'
}
```

### 5. 开发环境要求

```
  <uses-permission android:name="android.permission.CAMERA" />
  <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.RECORD_VIDEO" />
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.WRITE_SETTINGS" />
  <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.FLASHLIGHT" />
  <uses-permission android:name="android.permission.CHANGE_WIFI_MULTICAST_STATE" />
  <uses-feature android:name="android.hardware.camera" />
  <uses-feature android:name="android.hardware.camera.autofocus" />

```

# SDK快速接入
### 1、初始化配置








