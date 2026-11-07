---
title: "iOS 观播 SDK：类型详情"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-viewer-sdk-api-reference-for-ios-zh-CN"
---

<span id="cb8274c4"></span>
## BDLActivityAuthMode

直播间的认证模式。

```objectivec
typedef NS_ENUM(NSInteger, BDLActivityAuthMode) {
    BDLActivityAuthModeUnknown = 0,
    BDLActivityAuthModePublic = 1, 
    BDLActivityAuthModeCustom = 2, 
};
```



* `BDLActivityAuthModeUnknown(0)`：未知模式。

* `BDLActivityAuthModePublic(1)`：公开模式。观众输入昵称，或通过`setNickname:complete:`方法，将昵称作为`nickname`参数传递给`BDLUserInfoConfiguration`。

* `BDLActivityAuthModeCustom(2)`：自定义模式。观众通过登录你的账号系统进入直播间。昵称会从你的系统同步，观众无需手动输入。


<span id="f60b8d87"></span>
# BDLLivePullViewControllerConfig

```objectivec
@interface BDLLivePullViewControllerConfig : NSObject
```


功能完整的直播间配置。

<span id="4fb9817d"></span>
## 属性

<span id="40e7c9c0"></span>
### showCloseButtonWhenClearingScreen

```objectivec
@property (nonatomic, assign) BOOL showCloseButtonWhenClearingScreen;
```


当屏幕控件隐藏时，是否显示关闭按钮。默认值：`NO`。


* `YES`：显示按钮。

* `NO`：不显示按钮。
