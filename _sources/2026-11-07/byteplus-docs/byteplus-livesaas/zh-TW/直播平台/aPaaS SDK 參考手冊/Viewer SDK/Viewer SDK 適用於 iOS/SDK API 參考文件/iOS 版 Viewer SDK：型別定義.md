---
title: "iOS 版 Viewer SDK：型別定義"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ios-ban-viewer-sdk-xing-bie-ding-yi-zh-TW"
---

<span id="cb8274c4"></span>
## BDLActivityAuthMode

直播間的驗證模式。

```objectivec
typedef NS_ENUM(NSInteger, BDLActivityAuthMode) {
    BDLActivityAuthModeUnknown = 0,
    BDLActivityAuthModePublic = 1, 
    BDLActivityAuthModeCustom = 2, 
};
```



* `BDLActivityAuthModeUnknown(0)`：未知模式。

* `BDLActivityAuthModePublic(1)`：公開模式。暱稱由觀眾輸入，或通過 `setNickname:complete:` 方法，經由 `BDLUserInfoConfiguration` 的 `nickname` 參數傳入。

* `BDLActivityAuthModeCustom(2)`：自訂模式。觀眾需登入您的帳號系統後進入直播間。暱稱會從您的系統同步，觀眾無需手動輸入。


<span id="f60b8d87"></span>
# BDLLivePullViewControllerConfig

```objectivec
@interface BDLLivePullViewControllerConfig : NSObject
```


完整功能直播間的配置。

<span id="4fb9817d"></span>
## 屬性

<span id="40e7c9c0"></span>
### showCloseButtonWhenClearingScreen

```objectivec
@property (nonatomic, assign) BOOL showCloseButtonWhenClearingScreen;
```


當螢幕控制項隱藏時，是否顯示關閉按鈕。預設值：`NO`。


* `YES`：顯示按鈕。

* `NO`：不顯示按鈕。
