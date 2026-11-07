---
title: "Viewer SDK for iOS: Error codes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-SDK-for-ios-error-codes"
---

<span id="BDLError"></span>
# BDLError

```objectivec
typedef NS_ENUM(
    NSUInteger,
    BDLError
)
```


The error codes.

<span id="enumerated-value"></span>
## Enumerated Value


|Type |Value |Instructions |
|---|---|---|
|BDLErrorUnknown |0 |Unknown error. |
|BDLErrorGetActivityFailed |1 |Failed to get the live room data. |
|BDLErrorPullDisallowed |2 |Pulling streams by using the SDK is not allowed. |
|BDLErrorChangeTokenFailed |3 |Failed to call the `changeToken` API. |
|BDLErrorVodUrlFailed |4 |Failed to get the playback URL based on the video ID. |
|BDLErrorCustomLoginTokenInvalid |5 |The `token` parameter passed in through the `completion` callback of [loginWithActivity:completion:](https://docs.byteplus.com/en/docs/11/viewer-SDK-for-ios-callbacks#BDLLoginProvider-loginwithactivity-completion) is in any of the following conditions:<br><br><br>* `nil`<br><br>* Not of `NSString` type<br><br>* Length is 0 |
|BDLErrorGetRTCTokenFailed |7 |Failed to get the RTC token. |
|BDLErrorJoinRTCRoomFailed |8 |Failed to join the RTC room. |
|BDLErrorProductVersionDisallowed |9 |Not supported by the current feature version. Contact BytePlus Live technical support. |
|BDLErrorFrequencyLimitError |10 |Comments are sent too frequently. |
|BDLErrorCodeUserHasJoinLiveRoom |11 |Failed to set the user nickname by calling the [setNickname:complete:](https://docs.byteplus.com/en/docs/11/viewer-sdk-for-ios-type-definitions#BDLUserInfoConfiguration-setnickname-complete) method. You must call this method before viewers join the live room. |
|BDLErrorCodeForceOffline |12 |The current viewer has been blocked and cannot join the live room. To allow the viewer to join, contact the host to unblock them. |
