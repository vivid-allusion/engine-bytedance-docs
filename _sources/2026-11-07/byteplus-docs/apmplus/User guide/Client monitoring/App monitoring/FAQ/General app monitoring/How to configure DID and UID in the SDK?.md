---
title: "How to configure DID and UID in the SDK?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_configure_DID_and_UID_in_the_SDK"
---


|**System** |**Location** |**DID configuration in the SDK** |**Configure UID in SDK** |
|---|---|---|---|
|iOS |The `application didFinishLaunchingWithOptions:` method in AppDelegate.m |```JSON```<br>```+ (void)setDeviceID:(NSString *_Nullable)deviceID;```<br> |```JSON```<br>```+ (void)setUserID:(NSString *_Nullable)userID;```<br> |
|Android |The `onCreate` method of Application |```JSON```<br>```@Override```<br>```public String getDid(){```<br>``` returnnull;```<br>```}```<br> |```JSON```<br>```@Override```<br>```public String getUserId(){```<br>``` returnnull;```<br>```}```<br> |
