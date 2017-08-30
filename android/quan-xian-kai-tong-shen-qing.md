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

