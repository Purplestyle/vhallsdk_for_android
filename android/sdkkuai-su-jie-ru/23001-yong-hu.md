
#### 1 创建用户

第三方创建用户接口 [http://e.vhall.com/home/vhallapi/active\#user\_register](http://e.vhall.com/home/vhallapi/active#user_register)  
如果使用聊天和问答功能，需要用户提前调用WebApi进行创建用户标识操作。详细接口说明，请参数请参照API地址，

#### 2 登陆

当用户在vhall平台创建用户成功之后，调用VhallSDK中的login方法，如果用户需要使用如聊天，问答等功能则必须用户标识。如果不用户标识则默认是游客模式 \(Demo里即使是游客也是可以聊天的，用户可以根据自己的场景控制。问答必须创建用户\)

```
   VhallSDK.getInstance().login(username, userpass, new UserInfoDataSource.UserInfoCallback() {
            @Override
            public void onSuccess(UserInfo userInfo) {}
            @Override
            public void onError(int errorCode, String reason) {}
   });
```

#### 3 返回错误码



| 错误码 | 描述 |
| :--- | :--- |
| 10501 | 用户不存在 |
| 10502 | 登陆密码不正确 |






