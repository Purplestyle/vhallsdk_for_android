在用户调用VhallSDK中的任意方法前，一定要先调用init方法，初始化VhallSDK。

```
   /**
    * VhallSDK初始化
    * @param Context 
    * @param APP_KEY  权限申请时获得
    * @param APP_SECRET_KEY 权限申请时获得
    */
    VhallSDK.init(this , APP_KEY , APP_SECRET_KEY);
```



