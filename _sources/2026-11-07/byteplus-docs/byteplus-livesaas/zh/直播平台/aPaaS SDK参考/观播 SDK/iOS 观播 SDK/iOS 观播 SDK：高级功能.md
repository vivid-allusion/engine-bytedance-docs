---
title: "iOS 观播 SDK：高级功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN"
---

为提升你的直播流应用，本指南提供集成 iOS 观播 SDK 高级功能的操作说明。你将学习如何实现自定义用户登录流程、重写广告和商品卡片等互动元素的默认跳转逻辑，并根据你的应用的具体业务需求和品牌定制观播界面。

<span id="ca684b73"></span>
## 前提条件


* 完成 [集成 iOS 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-zh-CN) 中的前 5 步。

* 按需集成以下组件。

   * 集成基础功能以自定义视频缩放模式。更多信息，请参见 [iOS 观播 SDK：基础功能](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN)。

   * 集成完整直播间，以实现本主题所述的其他高级功能。更多信息，请参见 [完整直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-the-viewer-sdk-for-ios-zh-CN#f2a7c3c8)。


<span id="7b020e01"></span>
## 功能

本主题介绍如何集成以下功能。


* [自定义登录](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#0f3118f8)

* [自定义跳转逻辑](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#971bbcde)

   * [菜单下展示的商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#cbaa61a3)

   * [页头广告](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#19643834)

   * [页中广告](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#dd1a11eb)

   * [浮标广告或商品浮窗](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#d100ba3a)

   * [主播账号](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#27ae5bd9)

   * [菜单下聊天互动评论区中的URL](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#80b34b11)

   * [置顶评论中的URL](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#b68c3584)

* [UI自定义](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#0269f8d1)

   * [视频缩放模式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#a625195e)

   * [关闭完整直播间的图标](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#eb320cbc)

   * [悬浮互动工具](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#ee6cf81c)

   * [商品卡片菜单的高度](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-the-viewer-sdk-for-ios-zh-CN#8ea12ced)


<span id="0f3118f8"></span>
## 自定义登录

若你需要观众先登录你的应用，再观看直播流、参与评论和互动等，可以选择自定义登录方式。观众可使用其在你的应用中的身份信息加入直播间。

你可以选择观众需要登录你的应用的时机。


* 观众先登录你的应用，然后加入直播间。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46a7b800924a41d7a4f88933f07df41f~tplv-goo7wpa0wc-image.image) </span>

   1. 观众登录应用并加入直播间后，你需要调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将 `Mode` 的值设置为 `2`，以获取授权令牌。

   2. 获取令牌后，调用 SDK 的 `joinLiveRoomWithActivity:success:failure:` 方法加入直播间。

   示例代码如下。

   ```objectivec
   - (void)joinLiveRoom {    
       BDLActivity *activity = [[BDLActivity alloc] init];
       activity.activityId = @(167808997736****); // 直播间的活动 ID。
       activity.token = @"ak3T%2FdaGJDL5zSFD7%2F1GPGP****"; // 当 Mode 的值为 2 时的授权 token。
       activity.isPortrait = YES; // 竖屏模式下的直播间。
       activity.authMode = BDLActivityAuthModeCustom; // 自定义模式。
       [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity success:^{
           // 成功加入直播间。
       } failure:^(NSError * _Nonnull error) {
           // 加入直播间失败。
       }];
   }
   ```
   

* 观众先加入直播间，观看直播流、查看评论等。当观众执行如参与评论和互动等操作时，将触发登录流程，认证模式由公开模式切换为自定义模式。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">如果方法 <code>setNickname:complete:</code> 中 <code>nickname</code> 参数的值不为空，则无法触发 <code>BDLLoginProvider</code> 的任何方法。   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edc06578a28c4ab89f8d9c120fd31a38~tplv-goo7wpa0wc-image.image) </span>

   1. 观众首先以公开模式加入直播间。

   2. 你需要实现公开模式下获取授权令牌的方法。然后调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将 `Mode` 的值设置为 `1`，以获取令牌。

   3. 设置 `loginProvider` 到 `BDLLiveEngine`，即自定义模式下登录直播间的代理。

      示例代码如下。

      ```objectivec
      ...
      [[BDLLiveEngine sharedInstance] setLoginProvider:self];
      ...
      ```
      

   4. 调用 SDK 的 `joinLiveRoomWithActivity:success:failure:` 方法加入直播间。

   5. 当观众执行以下需要用户信息的操作时，将触发应用的自定义登录流程：

      * 点击聊天互动菜单下的评论输入框

      * 点赞评论

      * 为主播送礼

      * 点击预约按钮预约直播流

      * 答题

      * 投票

      * 抽奖

      * 非匿名问卷

   6. SDK 会调用 `loginWithActivity:completion:` 方法，让观众通过你的应用登录直播间。你需要实现自定义模式下获取授权令牌的方法。然后在观众完成自定义登录后，调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将 `Mode` 的值设置为 `2`，以获取令牌。获取令牌后，你需要调用 `completion` 方法，将令牌传递给 SDK。

      示例代码如下。

      ```objectivec
      - (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion {
          // 用你获取授权 token 的方法替换 getToken: 方法。
          [self getToken:^(NSString *token) {
              completion(token);
          }];
      }
      ```
      

   7. SDK通过token向BytePlus Live请求观众信息。

   8. 在验证token有效后，BytePlus Live会将观众信息传递给SDK。如果token验证失败或token为空，BytePlus Live会将错误信息传递给SDK。

   9. SDK调用`loginComplete:error:`方法，通知应用自定义登录流程是否成功。

      示例代码如下。

      ```objectivec
      - (void)loginComplete:(BDLActivity *)activity error:(NSError *)error {
          if (!error) {
              NSLog(@"Custom login is successful");
          }
          else {
              NSLog(@"Custom login failed %@", error.localizedDescription);
          }
      }
      ```
      

   10. （可选）如果在观众登录流程中关闭了直播间页面，SDK会触发`cancelLoginWithActivity:`回调，你可以根据需要取消自定义登录流程。

      示例代码如下。

      ```objectivec
      - (void)cancelLoginWithActivity:(BDLActivity *)activity {
      // After the cancelLoginWithActivity: callback is triggered, cancel the custom login process as needed.
          NSLog(@"If the live room page is closed during the login process, you can cancel the login process as needed in the app");
      }
      ```
      


<span id="971bbcde"></span>
## 自定义跳转逻辑

当观众在直播间点击以下项目时，SDK会执行默认跳转行为：


* 菜单下展示的商品卡片

* 商品浮窗

* 页头广告

* 页中广告

* 浮标广告

* 主播账号

* 菜单下聊天互动评论区中的URL

* 置顶评论中的URL


你可以拦截SDK的默认跳转行为，在观众点击这些项目后实现自定义跳转逻辑。这样可以根据具体场景或需求定制页面跳转行为，提升用户体验。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">关于如何在 BytePlus Live 控制台配置商品卡片、页头广告、页中广告、浮标广告、主播账号、聊天互动菜单和置顶评论的更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN">管理商品卡片</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-logo-and-ads-zh-CN">添加广告</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN">将主播账号关联到直播间</a>, 和 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area-zh-CN">管理聊天区域</a>。</div>


你可以在`configLivePullViewController:`中添加相关代码，获取被点击的URL等信息，并自定义跳转逻辑。

```objectivec
- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}
```


<span id="cbaa61a3"></span>
### 菜单下展示的商品卡片

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d5f66445f134fdcbfcce779cb957bea~tplv-goo7wpa0wc-image.image) </span>

当观众点击菜单下的商品卡片时，会触发`cardViewTappedBlock`回调，传递商品卡片URL以及商品详情页是否以浮层方式展示的布尔值。

示例代码如下。

```objectivec
livePullVC.config.customShoppingCardController = ^(BDLLivePullViewController * _Nonnull viewController, BDLShoppingCardController * _Nonnull shoppingCardController) {
    shoppingCardController.customizeShoppingCardView = ^__kindof BDLBaseView * _Nullable(BDLShoppingCardController * _Nonnull controller, BDLShoppingCardView * _Nonnull shoppingCardView) {
        shoppingCardView.cardViewTappedBlock = ^(NSString * _Nullable urlStr, BOOL enableFloating) {
        // 触发 cardViewTappedBlock 回调后，执行菜单下商品卡片的自定义跳转逻辑。
            NSLog(@"%@ %d", urlStr, enableFloating);
        };
        return shoppingCardView;
    };
};
```


<span id="19643834"></span>
### 页头广告

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496a3e71f2244d44910d5c2f125fb275~tplv-goo7wpa0wc-image.image) </span>

观众点击页头广告后，会触发`livePullViewController:didClickHeaderAd:floatingEnable:`回调，将以下信息传递给应用：页头广告的内嵌链接，以及广告页是否以浮层方式展示。

示例代码如下。

```objectivec
- (void)livePullViewController:(BDLLivePullViewController *)livePullVC didClickHeaderAd:(NSString *)url floatingEnable:(BOOL)floatingEnable {
// 触发 livePullViewController:didClickHeaderAd:floatingEnable: 回调后，执行页头广告的自定义跳转逻辑。
    NSLog(@"%@ %d", url, floatingEnable);
}
```


<span id="dd1a11eb"></span>
### 页中广告

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b62ff8e729444d4989849130571a2e89~tplv-goo7wpa0wc-image.image) </span>

观众点击页中广告后，会触发`viewTappedBlock`回调，将以下信息传递给应用：当前`BDLPageAdView`实例、广告相关信息，以及广告页是否以浮层方式展示。

示例代码如下。

```objectivec
livePullVC.config.customizePageAdView = ^__kindof BDLBaseView * _Nullable(BDLLivePullViewController *viewController, BDLPageAdView * _Nonnull view) {
    view.viewTappedBlock = ^(BDLPageAdView * _Nonnull view, BDLAdvertisementModel * _Nonnull ad, BOOL isFloatingEnable) {
    // 触发 viewTappedBlock 回调后，执行页中广告的自定义跳转逻辑。
        NSLog(@"%@ %d", ad.advertisementRedirectUrl, isFloatingEnable);
    };
    return view;
};
```


<span id="d100ba3a"></span>
### 浮标广告或商品浮窗


<Tabs>
<Tab zoneid="d4m8MX1y8K" title="浮标广告">
<TabTitle>浮标广告</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f1e0d8440cc41b1b5bc362e5f99c6c4~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="hlhnMr9tIA" title="商品浮窗">
<TabTitle>商品浮窗</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87da2c3522a945b284b1c7ed4f89491f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


观众点击浮标广告或商品浮窗后，会触发`openUrlBlock`回调，将以下信息传递给应用：悬浮窗控制器、浮标广告或商品浮窗的URL，以及广告页或商品详情页是否以浮层方式展示。

示例代码如下。

```objectivec
livePullVC.config.customFloatingController = ^(BDLLivePullViewController * _Nonnull viewController, BDLFloatingController * _Nonnull floatingController) {
    
    floatingController.openUrlBlock = ^(BDLFloatingController * _Nonnull floatingController, NSURL * _Nonnull url, BOOL isFloatingEnable) {
    // 触发 openUrlBlock 回调后，执行浮标广告或商品浮窗的自定义跳转逻辑。
        NSLog(@"url: %@ isFloatingEnable:%d", url, isFloatingEnable);
    };
};
```


<span id="27ae5bd9"></span>
### 主播账号

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893f6480223a44eb98e1600506a1fdbd~tplv-goo7wpa0wc-image.image) </span>

观众点击主播账号头像或名称后，会触发`viewTappedBlock`回调，将主播账号的内嵌链接传递给应用。

示例代码如下。

```objectivec
livePullVC.config.customizeAccountView = ^__kindof BDLBaseView * _Nullable(BDLLivePullViewController *viewController, BDLBusinessAccountView * _Nonnull view) {
    view.viewTappedBlock = ^(NSString * _Nullable urlStr) {
     // 触发 viewTappedBlock 回调后，执行主播账号的自定义跳转逻辑。
        NSLog(@"%@", urlStr);
    };
    return view;
};
```


<span id="80b34b11"></span>
### 菜单下聊天互动评论区中的URL

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f36cd2c7f759428ca62815b51ee9a6b5~tplv-goo7wpa0wc-image.image) </span>

默认情况下，仅主播评论中的URL可点击。你可以通过以下方法设置观众评论中的URL为可点击。

```objectivec
[[[BDLLiveEngine sharedInstance] liveRoomConfiguration] commentViewConfig].enableAudienceURLTap = YES;
```


当观众点击聊天互动菜单下评论区中的URL（非置顶评论中的URL）后，会触发`urlClickBlock`回调，并向应用传递以下信息：当前`BDLCommentBaseView`实例、评论相关信息以及评论中的URL。

示例代码如下。

```objectivec
void (^customizeCommentView)(BDLCommentView *view) = ^(BDLCommentView *view) {
    view.urlClickBlock = ^(__kindof BDLCommentBaseView * _Nonnull commentView, BDLCommentModel * _Nonnull comment, NSURL * _Nonnull url) {
       // 触发 urlClickBlock 回调后，执行评论区 URL 的自定义跳转逻辑。
            NSLog(@"%@ %@", url, comment);
    };
};

// 在竖屏模式直播间的聊天互动菜单下的评论区调用 urlClickBlock。
livePullVC.config.customizeCommentView = ^(BDLLivePullViewController * _Nonnull viewController, BDLCommentView * _Nonnull view) {
    customizeCommentView(view);
};

// 在横屏模式直播间的聊天互动菜单下的评论区调用 urlClickBlock。
// 与其他 customizeMenuBarView 方法配合使用此方法，以避免覆盖配置。
livePullVC.config.customizeMenuBarView = ^(BDLLivePullViewController * _Nonnull viewController, BDLMenuBarView * _Nonnull view) {
    view.customizeCommentView = ^(BDLMenuBarView * _Nonnull view, BDLCommentView * _Nonnull commentView) {
        customizeCommentView(commentView);
    };
};
```


<span id="b68c3584"></span>
### 置顶评论中的URL

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b09965eb9a2c4f188485ab86c28b4bc6~tplv-goo7wpa0wc-image.image) </span>

观众点击置顶评论后，会弹出显示置顶评论的窗口。观众点击弹窗中的URL后，会触发`urlClickBlock`回调，并将URL传递给应用。

示例代码如下。

```objectivec
livePullVC.config.customizeAlertController = ^__kindof UIViewController * _Nonnull(BDLLivePullViewController * _Nonnull viewController, BDLAlertController * _Nonnull controller) {
    __weak typeof(self) weakSelf = self;
    __weak BDLAlertController * weakController = controller;
    controller.urlClickBlock = ^(NSURL * _Nonnull url) {
        [weakController dismissAlertControllerAnimated:YES completion:^{
        // 触发 urlClickBlock 回调后，执行置顶评论 URL 的自定义跳转逻辑。
            NSLog(@"%@", url);
        }];
    };
    return controller;
};
```


<span id="0269f8d1"></span>
## UI自定义

你可以通过以下方法自定义观看页的UI。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">通过 SDK 进行的 UI 个性化优先于在 BytePlus Live 控制台或通过服务端 API 配置的个性化。例如，如果你通过 SDK 的 <code>thumbUpButtonImage</code> 方法和控制台同时自定义直播间点赞图标，观看页上显示的图标将以 <code>thumbUpButtonImage</code> 方法的自定义为准。</div>


<span id="cc47b661"></span>
### 自定义方法

<span id="41a574d3"></span>
#### 通过使用以`customize`为前缀的属性

你可以在`joinLiveRoomWithActivity:success:failure:`成功回调中调用`getLivePullViewController`方法获取`BDLLivePullViewController`实例。然后，通过`BDLLivePullViewController`的`config`属性自定义`BDLLivePullViewController`。`BDLLivePullViewControllerConfig`提供以`customize`为前缀的block。你可以根据block参数获取对应的视图，并自定义视图属性。


* 对于有返回值的block，你可以自定义提供的视图并返回，也可以返回你自定义视图实现的实例。

* 对于无返回值的block，你只能自定义视图属性。


以`customizeAccountView`属性为例。

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeAccountView)(BDLLivePullViewController *viewController, BDLBusinessAccountView *view);
```


你可以通过`customizeAccountView`属性自定义主播账号功能的UI。例如，若需自定义主播账号头像除圆角、图片和`frame`以外的所有属性，可以通过`customizeAccountView`属性获取`BDLBusinessAccountView`，然后配置`avatarImageView`。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">如果你使用此方法，建议在观众成功加入直播间后、直播间页面展示前配置 UI。</div>


* <div data-tips="true" data-tips-type="tip">要隐藏某个视图，可以向 SDK 返回 <code>nil</code>，或在 BytePlus Live 控制台禁用对应功能。我们不建议通过 <code>hidden</code> 属性隐藏视图，因为该属性可能会被控制台配置覆盖。</div>


* <div data-tips="true" data-tips-type="tip">由于视图内部采用自动布局，除非明确说明，否则不建议自定义视图的位置属性。要自定义视图的位置，建议你实现自己的视图，并用你的实现替换默认实现。</div>


* <div data-tips="true" data-tips-type="tip">如果在 BytePlus Live 控制台中未开启对应功能，则无法通过 SDK 强制使 UI 控件可见。</div>


* <div data-tips="true" data-tips-type="tip">支持自定义多语言文本，除非有特殊说明。不同语言的文本请用 <code>|</code> 字符分隔，SDK 会自动选择合适的语言。格式如下：</div>


   <div data-tips="true" data-tips-type="tip"><code>简体中文|English|日本語|繁體中文|한국어|ภาษาไทย|Tiếng Việt|اللغة العربية|Türkçe|Español|Bahasa Indonesia|Português|Русский язык</code>   </div>
   


<span id="beaa7af4"></span>
#### 通过使用以`Config`为后缀的属性

SDK在`liveRoomConfiguration`中提供以`Config`为后缀的属性。你可以通过以下示例代码获取对应的`Config` API进行自定义。

```objectivec
[[BDLLiveEngine sharedInstance] liveRoomConfiguration].xxxxConfig
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果使用此方法，建议在观众进入直播间前配置 UI。</div>


<span id="2ccd7abe"></span>
### 实现

本主题以电商场景中常用的UI自定义功能为例。

<span id="a625195e"></span>
#### 视频缩放模式

默认情况下，竖屏模式的视频会以保持原视频长宽比（aspect fill）的方式缩放填满播放器。如果视频长宽比与播放器不一致，视频的部分内容可能会被裁剪。你可以自定义视频缩放模式。

以下示例代码使视频完全填满播放器，但视频长宽比可能会发生变化。


<Tabs>
<Tab zoneid="kk4LjK330w" title="自定义前">
<TabTitle>自定义前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/123a2189d7a840fa8e6b2b6302abc4c7~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="Qm43cvXPkX" title="自定义后">
<TabTitle>自定义后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a81142d11fa34c199aff2c0506d707df~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
BDLLiveRoomConfiguration *config = [[BDLLiveEngine sharedInstance] liveRoomConfiguration];
config.playerConfig.portrait.scalingMode = BDLPlayerScalingModeFill;
```


<span id="eb320cbc"></span>
#### 关闭完整直播间的图标

默认情况下，竖屏模式下关闭完整直播间的图标显示为x。你可以自定义图标的显示样式。

以下示例代码将图标自定义为名为`back`的图片。


<Tabs>
<Tab zoneid="hVUhqTavJP" title="自定义前">
<TabTitle>自定义前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0637d35400574edb81334f2f402fa154~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="is56AW8QHU" title="自定义后">
<TabTitle>自定义后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2fd49d18ce0476bbd40b3f670f019cb~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
livePullVC.config.customizeCloseButton = ^__kindof UIButton * _Nullable(BDLLivePullViewController * _Nonnull viewController, UIButton * _Nonnull button) {
    // Customize the corner radius and border.
    button.clipsToBounds = YES;
    button.layer.cornerRadius = 3;
    button.layer.borderWidth = 2;
    button.layer.borderColor = UIColor.grayColor.CGColor;
    // Customize the icon as the image named back.
    [button setImage:[UIImage imageNamed:@"back"] forState:UIControlStateNormal];
    return button;
};
```


<span id="ee6cf81c"></span>
#### 悬浮互动工具

悬浮互动工具包含抽奖、答题、投票、问卷和公告的图标。竖屏模式下的直播间，悬浮互动工具默认显示在直播间左上角。你可以自定义悬浮互动工具的默认位置。

以下示例代码将悬浮互动工具的默认位置下移50 pt。


<Tabs>
<Tab zoneid="MHCElhjdqA" title="自定义前">
<TabTitle>自定义前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2c389a4b49d437d97ef29c2eaa39b29~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="gZGjcB4M2a" title="自定义后">
<TabTitle>自定义后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bcad45935ec4e7e9da9c74dc16a1170~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
// Customize the floating window in the full-featured live room.
livePullVC.config.customFloatingController = ^(BDLLivePullViewController * _Nonnull viewController, BDLFloatingController * _Nonnull floatingController) {
    // Customize the default position of floating interaction tools.该视图支持拖动，因此必须通过设置 view.frame 调整位置，而不是使用自动布局。
    floatingController.customizeInteractiveToolContainerView = ^__kindof UIStackView * _Nullable(BDLFloatingController * _Nonnull floatingController, UIStackView * _Nonnull view) {
        CGRect frame = view.frame;
        // Move the default position of floating interaction tools down by 50 pt.
        frame.origin.y += 50;
        view.frame = frame;
        return view;
    };
};
```


<span id="8ea12ced"></span>
#### 商品卡片菜单的高度

默认情况下，商品卡片菜单的高度为屏幕高度的 73%。你可以自定义菜单的高度。

以下示例代码将菜单的高度设置为屏幕高度的一半。


<Tabs>
<Tab zoneid="qZEkn39c4A" title="自定义前">
<TabTitle>自定义前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4789ad68e6c248f7876e4cfce8059b49~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="kqqmWIOIqG" title="自定义后">
<TabTitle>自定义后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8ff0f6b33c645d385457b7d7f53747c~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
livePullVC.config.customShoppingCardController = ^(BDLLivePullViewController * _Nonnull viewController, BDLShoppingCardController * _Nonnull shoppingCardController) {
    shoppingCardController.customizeShoppingCardView = ^__kindof BDLBaseView * _Nullable(BDLShoppingCardController * _Nonnull controller, BDLShoppingCardView * _Nonnull shoppingCardView) {
        [shoppingCardView mas_updateConstraints:^(MASConstraintMaker *make) {
            make.height.mas_equalTo(CGRectGetHeight(UIScreen.mainScreen.bounds) * 1 / 2);
        }];
        return shoppingCardView;
    };
};
```
