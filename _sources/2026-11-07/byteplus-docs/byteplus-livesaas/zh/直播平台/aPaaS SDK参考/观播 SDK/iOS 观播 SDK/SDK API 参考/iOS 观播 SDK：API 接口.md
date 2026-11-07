---
title: "iOS 观播 SDK：API 接口"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-viewer-sdk-type-for-ios-zh-CN"
---

<span id="e53a9ad6"></span>
# BDLLiveEngine

提供进入和离开直播间的方法，以及执行其他操作。

```objectivec
#import <BPLive/BPLive.h>
```


<span id="joinLiveRoomWithActivityId"></span>
## joinLiveRoomWithActivity:

进入直播间。

```objectivec
- (BOOL)joinLiveRoomWithActivity:(BDLActivity *)activity;
```


**参数**


|**名称** |**数据类型** |**接口行为** |
|---|---|---|
|activity |[BDLActivity](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#bdlactivity) |直播间信息。 |


**返回值**


* `YES`：方法调用成功。

* `NO`：参数无效，即`activityId`或`token`的值为空。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">该方法在 1.40.0 版本中已废弃。你可以改用<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-type-for-ios-zh-CN#c30e3d0f">joinLiveRoomWithActivity:success:failure:</a>方法。</div>


<span id="c30e3d0f"></span>
## joinLiveRoomWithActivity:success:failure:

```objectivec
- (BOOL)joinLiveRoomWithActivity:(BDLActivity *)activity
                         success:(void (^)(void))success
                         failure:(void (^)(NSError *error))failure;
```


进入直播间。SDK 会在成功或失败时触发相应的回调。

**参数**


|**名称** |**数据类型** |**接口行为** |
|---|---|---|
|activity |BDLActivity\* |直播间信息。更多信息请参见[BDLActivity](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-type-for-ios-zh-CN#0b6ae4e5)。 |
|success |void(^)(void) |用户成功进入直播间时调用的回调。 |
|failure |void(^)(NSError\*error) |用户进入直播间失败时调用的回调。<br><br>输入参数：<br><br>`error`：错误信息。`error.code`的值为`BDLError`枚举中的值。<br><br>示例：<br><br>```objectivec```<br>```failure:^(NSError * _Nonnull error) {```<br>```    if ([error.domain isEqualToString:BDLErrorDomain]) {```<br>```        if (error.code == BDLErrorPullDisallowed)```<br>```        }```<br>```        else if ... {```<br>```        }```<br>```    }```<br>```    else {```<br>```    }```<br>```  }];```<br> |


<span id="leaveLiveRoom"></span>
## leaveLiveRoom

离开直播间。

```objectivec
- (void)leaveLiveRoom;
```


<span id="fd0b93df"></span>
## userUniqueId

获取用户的唯一 ID。该方法在用户成功进入直播间后调用。你可以将该 ID 提供给技术支持以便排查问题。

```objectivec
(nullable NSString *)userUniqueId;
```


<span id="0b6ae4e5"></span>
# BDLActivity

直播间信息。

```objectivec
@interface BDLActivity : NSObject
```


<span id="15b679d0"></span>
## 成员属性

<span id="4d8fa3c5"></span>
### activityId

```objectivec
@property (nonatomic, strong) NSNumber *activityId;
```


直播间的活动 ID。你可以通过调用[CreateActivityAPIV2](https://docs.byteplus.com/en/byteplus-livesaas/docs/createactivityapiv2)获取该 ID。

<span id="04d20ca2"></span>
### token

```objectivec
@property (nonatomic, copy) NSString *token;
```


进入直播间所需的授权 token。你可以通过调用[GetSDKTokenAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/getsdktokenapi)获取该 token。

<span id="e4d5fd61"></span>
### authMode

```objectivec
@property (nonatomic, assign) BDLActivityAuthMode authMode;
```


直播间的认证模式。更多信息请参见[BDLActivityAuthMode](https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-ios-type-definitions#bdlactivityauthmode)。

<span id="1356f9c5"></span>
### nickName

```objectivec
@property (nonatomic, copy, nullable) NSString *nickName;
```


若[authMode](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#authmode)的值为`BDLActivityAuthModePublic`，即直播间的认证模式为公开，且参数`nickName`有值，则`nickName`的参数值将作为观众的昵称。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">该属性在 1.40.0 版本中已废弃。你可以在<code>BDLUserInfoConfiguration</code>的<code>setNickname:complete:</code>方法中使用<code>nickname</code>参数。</div>


<span id="e49ff0cd"></span>
### isPortrait

```objectivec
@property (nonatomic, assign) BOOL isPortrait;
```


指定直播间是否为竖屏模式。


* `YES`：为竖屏模式。

* `NO`：为横屏模式。


<span id="f3694599"></span>
## 成员函数

<span id="a61dc7e2"></span>
### isValid

```objectivec
- (BOOL)isValid;
```


校验直播间信息。

**返回值**


* `YES`：有效。`activityId`和`token`均有值。

* `NO`：若activityId或token没有值则无效。
