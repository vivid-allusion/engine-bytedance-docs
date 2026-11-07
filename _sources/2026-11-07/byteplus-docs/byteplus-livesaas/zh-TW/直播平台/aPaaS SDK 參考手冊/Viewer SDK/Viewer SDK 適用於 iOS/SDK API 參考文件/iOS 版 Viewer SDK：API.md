---
title: "iOS 版 Viewer SDK：API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ios-ban-viewer-sdk-api-zh-TW"
---

<span id="e53a9ad6"></span>
# BDLLiveEngine

提供進入與離開直播間的方法，以及執行其他操作。

```objectivec
#import <BPLive/BPLive.h>
```


<span id="joinLiveRoomWithActivityId"></span>
## joinLiveRoomWithActivity:

進入直播間。

```objectivec
- (BOOL)joinLiveRoomWithActivity:(BDLActivity *)activity;
```


**參數**


|**名稱** |**資料型別** |**說明** |
|---|---|---|
|activity |[BDLActivity](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlactivity) |直播間資訊。 |


**返回值**


* `YES`：方法呼叫成功。

* `NO`：參數無效，即 `activityId` 或 `token` 的值為空。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">此方法已於 1.40.0 版本棄用。你可以改用 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-api-zh-TW#c30e3d0f">joinLiveRoomWithActivity:success:failure:</a> 方法。</div>


<span id="c30e3d0f"></span>
## joinLiveRoomWithActivity:success:failure:

```objectivec
- (BOOL)joinLiveRoomWithActivity:(BDLActivity *)activity
                         success:(void (^)(void))success
                         failure:(void (^)(NSError *error))failure;
```


進入直播間。SDK 會在成功或失敗時觸發相應的回呼。

**參數**


|**名稱** |**資料型別** |**說明** |
|---|---|---|
|activity |BDLActivity\* |直播間資訊。更多資訊請參閱 [BDLActivity](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-api-zh-TW#0b6ae4e5)。 |
|success |void(^)(void) |使用者成功進入直播間時所觸發的回呼。 |
|failure |void(^)(NSError\*error) |使用者進入直播間失敗時所觸發的回呼。<br><br>輸入參數：<br><br>`error`：錯誤資訊。`error.code` 的值來自 `BDLError` 枚舉。<br><br>範例：<br><br>```objectivec```<br>```failure:^(NSError * _Nonnull error) {```<br>```    if ([error.domain isEqualToString:BDLErrorDomain]) {```<br>```        if (error.code == BDLErrorPullDisallowed)```<br>```        }```<br>```        else if ... {```<br>```        }```<br>```    }```<br>```    else {```<br>```    }```<br>```  }];```<br> |


<span id="leaveLiveRoom"></span>
## leaveLiveRoom

離開直播間。

```objectivec
- (void)leaveLiveRoom;
```


<span id="fd0b93df"></span>
## userUniqueId

取得使用者的唯一 ID。此方法會在使用者成功進入直播間後呼叫。你可以將此 ID 提供給技術支援人員以協助排查問題。

```objectivec
(nullable NSString *)userUniqueId;
```


<span id="0b6ae4e5"></span>
# BDLActivity

直播間資訊。

```objectivec
@interface BDLActivity : NSObject
```


<span id="15b679d0"></span>
## 成員屬性

<span id="4d8fa3c5"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


直播間的活動 ID。你可以透過呼叫 [CreateActivityAPIV2](https://docs.byteplus.com/en/byteplus-livesaas/docs/createactivityapiv2) 取得此 ID。

<span id="04d20ca2"></span>
### token

```objectivec
@property (nonatomic, copy) NSString *token;
```


進入直播間所需的授權 token。你可以透過呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/getsdktokenapi) 取得此 token。

<span id="e4d5fd61"></span>
### authMode

```objectivec
@property (nonatomic, assign) BDLActivityAuthMode authMode;
```


直播間的驗證模式。更多資訊請參閱 [BDLActivityAuthMode](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlactivityauthmode)。

<span id="1356f9c5"></span>
### nickName

```objectivec
@property (nonatomic, copy, nullable) NSString *nickName;
```


若 [authMode](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#authmode) 的值為 `BDLActivityAuthModePublic`，即直播間的驗證模式為公開，且參數 `nickName` 有值，則 `nickName` 的參數值將作為觀眾的暱稱。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">此屬性已於 1.40.0 版本棄用。你可以改用 <code>nickname</code> 參數，並在 <code>setNickname:complete:</code> 方法的 <code>BDLUserInfoConfiguration</code> 中設定。</div>


<span id="e49ff0cd"></span>
### isPortrait

```objectivec
@property (nonatomic, assign) BOOL isPortrait;
```


指定直播間是否為直式模式。


* `YES`：直式模式。

* `NO`：橫式模式。


<span id="f3694599"></span>
## 成員函式

<span id="a61dc7e2"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


驗證直播間資訊。

**返回值**


* `YES`：有效。`activityId` 與 `token` 均有值。

* `NO`：若 activityId 或 token 任一無值則無效。
