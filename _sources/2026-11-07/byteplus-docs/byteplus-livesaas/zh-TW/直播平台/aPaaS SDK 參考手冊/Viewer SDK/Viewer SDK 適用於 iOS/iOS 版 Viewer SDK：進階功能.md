---
title: "iOS 版 Viewer SDK：進階功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW"
---

為了提升你的直播應用程式，本指南提供整合 iOS 版 Viewer SDK 進階功能的操作說明。你將學會如何實作自訂用戶登入流程、覆寫互動元件（如廣告與商品卡片）的預設跳轉邏輯，並根據你的應用程式的業務需求與品牌風格，調整觀看介面。

<span id="ca684b73"></span>
## 先決條件


* 請先完成 [整合 iOS 版 Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-ios-ban-viewer-sdk-zh-TW) 的前 5 個步驟。

* 根據需求整合以下元件。

   * 整合基礎功能以自訂影片縮放模式。如需詳細資訊，請參閱 [iOS 版 Viewer SDK：基本功能](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW)。

   * 整合全功能直播間，以實現本主題所述的其他進階功能。如需詳細資訊，請參閱 [全功能直播間](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#f2a7c3c8)。


<span id="7b020e01"></span>
## 功能

本主題說明如何整合以下功能。


* [自訂登入](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#0f3118f8)

* [自訂跳轉邏輯](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#971bbcde)

   * [菜單下方顯示的商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#cbaa61a3)

   * [頁首廣告](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#19643834)

   * [頁內廣告](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#dd1a11eb)

   * [浮動廣告或浮動商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#d100ba3a)

   * [主播帳號](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#27ae5bd9)

   * [菜單下方聊天室互動區的留言區 URL](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#80b34b11)

   * [置頂評論中的 URL](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#b68c3584)

* [UI 客製化](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#0269f8d1)

   * [影片縮放模式](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#a625195e)

   * [關閉全功能直播間的圖示](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#eb320cbc)

   * [浮動互動工具](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#ee6cf81c)

   * [商品卡片菜單的高度](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#8ea12ced)


<span id="0f3118f8"></span>
## 自訂登入

若你希望觀眾先登入你的應用程式，再觀看直播、參與留言互動等，可以選擇自訂登入方式。觀眾可使用他們在你的應用程式中的身份資訊加入直播間。

你可以自訂觀眾需要登入應用程式的時機。


* 觀眾先登入你的應用程式，再加入直播間。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46a7b800924a41d7a4f88933f07df41f~tplv-goo7wpa0wc-image.image) </span>

   1. 觀眾登入應用程式並加入直播間後，你需要呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)，並將 `Mode` 的值設為 `2`，以取得授權憑證（token）。

   2. 取得 token 後，呼叫 SDK 的 `joinLiveRoomWithActivity:success:failure:` 方法以加入直播間。

   範例程式碼如下。

   ```objectivec
   - (void)joinLiveRoom {    
       BDLActivity *activity = [[BDLActivity alloc] init];
       activity.activityId = @(167808997736****); // 直播間的活動 ID。
       activity.token = @"ak3T%2FdaGJDL5zSFD7%2F1GPGP****"; // 當 Mode 的值為 2 時的授權憑證。
       activity.isPortrait = YES; // 直式直播間。
       activity.authMode = BDLActivityAuthModeCustom; // 自訂模式。
       [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity success:^{
           // 成功加入直播間。
       } failure:^(NSError * _Nonnull error) {
           // 加入直播間失敗。
       }];
   }
   ```
   

* 觀眾先加入直播間，觀看直播、瀏覽留言等。當觀眾執行如參與留言互動等操作時，會觸發登入流程，並將驗證模式由公開模式切換為自訂模式。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">若方法 <code>setNickname:complete:</code> 中 <code>nickname</code> 參數值不為空，則無法觸發 <code>BDLLoginProvider</code> 的任何方法。   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edc06578a28c4ab89f8d9c120fd31a38~tplv-goo7wpa0wc-image.image) </span>

   1. 觀眾先以公開模式加入直播間。

   2. 你需要實作在公開模式下取得授權 token 的方法。然後，呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)，並將 `Mode` 的值設為 `1`，以取得 token。

   3. 設定 `loginProvider` 至 `BDLLiveEngine`，即自訂模式下登入直播間的代理。

      範例程式碼如下。

      ```objectivec
      ...
      [[BDLLiveEngine sharedInstance] setLoginProvider:self];
      ...
      ```
      

   4. 呼叫 SDK 的 `joinLiveRoomWithActivity:success:failure:` 方法以加入直播間。

   5. 當觀眾執行以下需要用戶資訊的操作時，會觸發應用程式的自訂登入流程：

      * 點擊聊天互動選單下的留言文字框

      * 對留言按讚

      * 贈送禮物給主播

      * 點擊預約按鈕預約直播

      * 答題互動

      * 投票

      * 抽獎

      * 非匿名問卷

   6. SDK 會呼叫 `loginWithActivity:completion:` 方法，讓觀眾透過你的應用程式登入直播間。你需要實作自訂模式下取得授權 token 的方法。然後，在觀眾完成自訂登入後，呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)，並將 `Mode` 的值設為 `2`，以取得 token。取得 token 後，你需要呼叫 `completion` 方法，將 token 傳遞給 SDK。

      範例程式碼如下。

      ```objectivec
      - (void)loginWithActivity:(BDLActivity *)activity completion:(void (^)(NSString * _Nullable token))completion {
          // 將 getToken: 方法替換為你用於獲取授權憑證的方法。
          [self getToken:^(NSString *token) {
              completion(token);
          }];
      }
      ```
      

   7. SDK 會使用 token 向 BytePlus Live 請求觀眾資訊。

   8. 在驗證 token 有效後，BytePlus Live 會將觀眾資訊傳遞給 SDK。若 token 驗證失敗或 token 為空，BytePlus Live 會將錯誤訊息傳遞給 SDK。

   9. SDK 會呼叫 `loginComplete:error:` 方法，通知應用程式自訂登入流程是否成功。

      範例程式碼如下。

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
      

   10. （選用）若觀眾登入流程期間關閉直播間頁面，SDK 會觸發 `cancelLoginWithActivity:` 回呼，您可視需求取消自訂登入流程。

      範例程式碼如下。

      ```objectivec
      - (void)cancelLoginWithActivity:(BDLActivity *)activity {
      // After the cancelLoginWithActivity: callback is triggered, cancel the custom login process as needed.
          NSLog(@"If the live room page is closed during the login process, you can cancel the login process as needed in the app");
      }
      ```
      


<span id="971bbcde"></span>
## 自訂跳轉邏輯

當觀眾在直播間點擊下列項目時，SDK 會執行預設跳轉行為：


* 菜單下方顯示的商品卡片

* 浮動商品卡片

* 頁首廣告

* 頁內廣告

* 浮動廣告

* 主播帳號

* 菜單下方聊天室互動區的留言區 URL

* 置頂留言中的 URL


您可以攔截 SDK 的預設跳轉行為，在觀眾點擊這些項目後實現自訂跳轉邏輯。這可根據特定場景或需求調整頁面跳轉行為，提升用戶體驗。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需瞭解如何在 BytePlus Live 控制台配置商品卡片、標頭廣告、頁內廣告、浮動廣告、主播帳號、聊天室互動選單及置頂留言，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-chan-pin-ka-pian-zh-TW">管理商品卡片</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/xin-zeng-guang-gao-zh-TW">新增廣告</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhu-ban-ren-zhang-hu-guan-lian-zhi-zhi-bo-ji-zh-TW">將主辦人帳戶關聯至直播間</a>, 和 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-liao-tian-qu-yu-zh-TW">管理聊天區域</a>。</div>


您可以在 `configLivePullViewController:` 中新增相關程式碼，以取得點擊的 URL 等資訊並自訂跳轉邏輯。

```objectivec
- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}
```


<span id="cbaa61a3"></span>
### 菜單下方顯示的商品卡片

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d5f66445f134fdcbfcce779cb957bea~tplv-goo7wpa0wc-image.image) </span>

當觀眾點擊菜單下方的商品卡片時，會觸發 `cardViewTappedBlock` 回呼，傳遞商品卡片的 URL 及是否需在浮動層顯示商品詳情頁的布林值。

範例程式碼如下。

```objectivec
livePullVC.config.customShoppingCardController = ^(BDLLivePullViewController * _Nonnull viewController, BDLShoppingCardController * _Nonnull shoppingCardController) {
    shoppingCardController.customizeShoppingCardView = ^__kindof BDLBaseView * _Nullable(BDLShoppingCardController * _Nonnull controller, BDLShoppingCardView * _Nonnull shoppingCardView) {
        shoppingCardView.cardViewTappedBlock = ^(NSString * _Nullable urlStr, BOOL enableFloating) {
        // 觸發 cardViewTappedBlock 回呼後，執行商品卡片選單下的自訂跳轉邏輯。
            NSLog(@"%@ %d", urlStr, enableFloating);
        };
        return shoppingCardView;
    };
};
```


<span id="19643834"></span>
### 頁首廣告

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/496a3e71f2244d44910d5c2f125fb275~tplv-goo7wpa0wc-image.image) </span>

當觀眾點擊頁首廣告後，會觸發 `livePullViewController:didClickHeaderAd:floatingEnable:` 回呼，將以下資訊傳遞給應用程式：頁首廣告的嵌入連結，以及廣告頁是否在浮動層顯示。

範例程式碼如下。

```objectivec
- (void)livePullViewController:(BDLLivePullViewController *)livePullVC didClickHeaderAd:(NSString *)url floatingEnable:(BOOL)floatingEnable {
// 觸發 livePullViewController:didClickHeaderAd:floatingEnable: 回呼後，執行標頭廣告的自訂跳轉邏輯。
    NSLog(@"%@ %d", url, floatingEnable);
}
```


<span id="dd1a11eb"></span>
### 頁內廣告

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b62ff8e729444d4989849130571a2e89~tplv-goo7wpa0wc-image.image) </span>

當觀眾點擊頁內廣告後，會觸發 `viewTappedBlock` 回呼，將以下資訊傳遞給應用程式：目前的 `BDLPageAdView` 實例、廣告相關資訊，以及廣告頁是否在浮動層顯示。

範例程式碼如下。

```objectivec
livePullVC.config.customizePageAdView = ^__kindof BDLBaseView * _Nullable(BDLLivePullViewController *viewController, BDLPageAdView * _Nonnull view) {
    view.viewTappedBlock = ^(BDLPageAdView * _Nonnull view, BDLAdvertisementModel * _Nonnull ad, BOOL isFloatingEnable) {
    // 觸發 viewTappedBlock 回呼後，執行頁內廣告的自訂跳轉邏輯。
        NSLog(@"%@ %d", ad.advertisementRedirectUrl, isFloatingEnable);
    };
    return view;
};
```


<span id="d100ba3a"></span>
### 浮動廣告或浮動商品卡片


<Tabs>
<Tab zoneid="PslFdLaUqx" title="浮動廣告">
<TabTitle>浮動廣告</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f1e0d8440cc41b1b5bc362e5f99c6c4~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="IlQfdErVvQ" title="浮動商品卡片">
<TabTitle>浮動商品卡片</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87da2c3522a945b284b1c7ed4f89491f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


當觀眾點擊浮動廣告或浮動商品卡片後，會觸發 `openUrlBlock` 回呼，將以下資訊傳遞給應用程式：浮動視窗控制器、浮動廣告或浮動商品卡片的 URL，以及廣告頁或商品詳情頁是否在浮動層顯示。

範例程式碼如下。

```objectivec
livePullVC.config.customFloatingController = ^(BDLLivePullViewController * _Nonnull viewController, BDLFloatingController * _Nonnull floatingController) {
    
    floatingController.openUrlBlock = ^(BDLFloatingController * _Nonnull floatingController, NSURL * _Nonnull url, BOOL isFloatingEnable) {
    // 觸發 openUrlBlock 回呼後，執行浮動廣告或浮動商品卡片的自訂跳轉邏輯。
        NSLog(@"url: %@ isFloatingEnable:%d", url, isFloatingEnable);
    };
};
```


<span id="27ae5bd9"></span>
### 主播帳號

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893f6480223a44eb98e1600506a1fdbd~tplv-goo7wpa0wc-image.image) </span>

當觀眾點擊主播帳號的頭像或名稱時，會觸發 `viewTappedBlock` 回呼，將主播帳號的嵌入連結傳遞給應用程式。

範例程式碼如下。

```objectivec
livePullVC.config.customizeAccountView = ^__kindof BDLBaseView * _Nullable(BDLLivePullViewController *viewController, BDLBusinessAccountView * _Nonnull view) {
    view.viewTappedBlock = ^(NSString * _Nullable urlStr) {
     // 觸發 viewTappedBlock 回呼後，執行主播帳號的自訂跳轉邏輯。
        NSLog(@"%@", urlStr);
    };
    return view;
};
```


<span id="80b34b11"></span>
### 菜單下方聊天室互動區的留言區 URL

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f36cd2c7f759428ca62815b51ee9a6b5~tplv-goo7wpa0wc-image.image) </span>

預設情況下，僅主播留言中的 URL 可點擊。您可以使用以下方法，設定觀眾留言中的 URL 可點擊。

```objectivec
[[[BDLLiveEngine sharedInstance] liveRoomConfiguration] commentViewConfig].enableAudienceURLTap = YES;
```


當觀眾點擊聊天互動菜單下方評論區的 URL（非置頂評論中的 URL）後，會觸發 `urlClickBlock` 回調，並將以下資訊傳遞給應用程式：當前 `BDLCommentBaseView` 實例、評論相關資訊，以及評論中的 URL。

範例程式碼如下。

```objectivec
void (^customizeCommentView)(BDLCommentView *view) = ^(BDLCommentView *view) {
    view.urlClickBlock = ^(__kindof BDLCommentBaseView * _Nonnull commentView, BDLCommentModel * _Nonnull comment, NSURL * _Nonnull url) {
       // 觸發 urlClickBlock 回呼後，執行留言區 URL 的自訂跳轉邏輯。
            NSLog(@"%@ %@", url, comment);
    };
};

// 在直式直播間聊天室互動選單下的留言區呼叫 urlClickBlock。
livePullVC.config.customizeCommentView = ^(BDLLivePullViewController * _Nonnull viewController, BDLCommentView * _Nonnull view) {
    customizeCommentView(view);
};

// 在橫式直播間聊天室互動選單下的留言區呼叫 urlClickBlock。
// 請與其他 customizeMenuBarView 方法搭配使用，以避免覆蓋配置。
livePullVC.config.customizeMenuBarView = ^(BDLLivePullViewController * _Nonnull viewController, BDLMenuBarView * _Nonnull view) {
    view.customizeCommentView = ^(BDLMenuBarView * _Nonnull view, BDLCommentView * _Nonnull commentView) {
        customizeCommentView(commentView);
    };
};
```


<span id="b68c3584"></span>
### 置頂評論中的 URL

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b09965eb9a2c4f188485ab86c28b4bc6~tplv-goo7wpa0wc-image.image) </span>

觀眾點擊置頂評論後，會彈出顯示置頂評論的視窗。觀眾點擊彈窗中的 URL 後，會觸發 `urlClickBlock` 回調，並將 URL 傳遞給應用程式。

範例程式碼如下。

```objectivec
livePullVC.config.customizeAlertController = ^__kindof UIViewController * _Nonnull(BDLLivePullViewController * _Nonnull viewController, BDLAlertController * _Nonnull controller) {
    __weak typeof(self) weakSelf = self;
    __weak BDLAlertController * weakController = controller;
    controller.urlClickBlock = ^(NSURL * _Nonnull url) {
        [weakController dismissAlertControllerAnimated:YES completion:^{
        // 觸發 urlClickBlock 回呼後，執行置頂留言 URL 的自訂跳轉邏輯。
            NSLog(@"%@", url);
        }];
    };
    return controller;
};
```


<span id="0269f8d1"></span>
## UI 客製化

你可以透過以下方法，在觀看頁面上進行 UI 客製化。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">透過 SDK 進行的 UI 自訂優先於在 BytePlus Live 控制台或伺服器端 API 配置的自訂。例如，若你同時透過 SDK 的 <code>thumbUpButtonImage</code> 方法及控制台自訂直播間按讚圖示，則觀看頁面上顯示的圖示將以 <code>thumbUpButtonImage</code> 方法自訂為準。</div>


<span id="cc47b661"></span>
### 客製化方法

<span id="41a574d3"></span>
#### 透過使用前綴為 `customize` 的屬性

你可以在 `joinLiveRoomWithActivity:success:failure:` 成功回調中，呼叫 `getLivePullViewController` 方法取得 `BDLLivePullViewController` 實例。然後，使用 `BDLLivePullViewController` 的 `config` 屬性來客製化 `BDLLivePullViewController`。`BDLLivePullViewControllerConfig` 提供前綴為 `customize` 的區塊。你可以根據區塊參數取得對應的視圖並客製化視圖屬性。


* 對於有回傳值的區塊，你可以客製化提供的視圖並回傳，或回傳你自訂視圖實現的實例。

* 對於無回傳值的區塊，你只能客製化視圖屬性。


以 `customizeAccountView` 屬性為例。

```objectivec
@property (nonatomic, copy, nullable) __kindof BDLBaseView * _Nullable (^customizeAccountView)(BDLLivePullViewController *viewController, BDLBusinessAccountView *view);
```


你可以利用 `customizeAccountView` 屬性來客製化主播帳號功能的 UI。例如，若要客製化主播帳號頭像除圓角、圖片及 `frame` 以外的所有屬性，可以使用 `customizeAccountView` 屬性取得 `BDLBusinessAccountView`，然後配置 `avatarImageView`。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">若你使用此方法，建議在觀眾成功加入直播間後、直播間頁面顯示前配置 UI。</div>


* <div data-tips="true" data-tips-type="tip">若要隱藏某個視圖，請回傳 <code>nil</code> 給 SDK，或在 BytePlus Live 控制台停用對應功能。我們不建議使用 <code>hidden</code> 屬性隱藏視圖，因為此設定可能會被控制台配置覆蓋。</div>


* <div data-tips="true" data-tips-type="tip">由於視圖內部採用自動排版，除非特別說明，否則不建議自訂視圖的位置屬性。若要自訂視圖的位置，建議您實作自己的視圖，然後以您的實作取代預設實作。</div>


* <div data-tips="true" data-tips-type="tip">如果對應功能在 BytePlus Live 控制台中被停用，您無法使用 SDK 強制讓 UI 控制項顯示。</div>


* <div data-tips="true" data-tips-type="tip">除非特別說明，否則支援自訂多語言文本。請使用<code>|</code>字元分隔不同語言的文本，SDK 會自動選擇合適的語言。格式如下：</div>


   <div data-tips="true" data-tips-type="tip"><code>简体中文|English|日本語|繁體中文|한국어|ภาษาไทย|Tiếng Việt|اللغة العربية|Türkçe|Español|Bahasa Indonesia|Português|Русский язык</code>   </div>
   


<span id="beaa7af4"></span>
#### 透過使用後綴為 `Config` 的屬性

SDK 在 `liveRoomConfiguration` 中提供後綴為 `Config` 的屬性。你可以使用以下範例程式碼取得對應的 `Config` API 進行客製化。

```objectivec
[[BDLLiveEngine sharedInstance] liveRoomConfiguration].xxxxConfig
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您採用此方法，建議您在觀眾進入直播間前先完成 UI 配置。</div>


<span id="2ccd7abe"></span>
### 實作

本主題以電商場景中常見的 UI 客製化功能為例。

<span id="a625195e"></span>
#### 影片縮放模式

預設情況下，直式影片會以保持原始比例（填滿比例）的方式縮放至填滿播放器。若影片的長寬比與播放器不同，影片部分內容可能會被裁切。你可以客製化影片縮放模式。

以下範例程式碼會讓影片完全填滿播放器，但影片的長寬比可能會改變。


<Tabs>
<Tab zoneid="K1SWhztE0g" title="自訂前">
<TabTitle>自訂前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/123a2189d7a840fa8e6b2b6302abc4c7~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="Qk9lEZxpiJ" title="自訂後">
<TabTitle>自訂後</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a81142d11fa34c199aff2c0506d707df~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
BDLLiveRoomConfiguration *config = [[BDLLiveEngine sharedInstance] liveRoomConfiguration];
config.playerConfig.portrait.scalingMode = BDLPlayerScalingModeFill;
```


<span id="eb320cbc"></span>
#### 關閉全功能直播間的圖示

預設情況下，直式全功能直播間的關閉圖示顯示為 x。你可以客製化圖示的顯示樣式。

以下範例程式碼將圖示客製化為名為 `back` 的圖片。


<Tabs>
<Tab zoneid="A7srEUydxx" title="自訂前">
<TabTitle>自訂前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0637d35400574edb81334f2f402fa154~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="NtsQJ0NHgl" title="自訂後">
<TabTitle>自訂後</TabTitle>

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
#### 浮動互動工具

浮動互動工具包含抽獎、答題、投票、問卷及公告的圖示。直式直播間預設會將浮動互動工具顯示於直播間左上角。你可以客製化浮動互動工具的預設位置。

以下範例程式碼將浮動互動工具的預設位置下移 50 pt。


<Tabs>
<Tab zoneid="NoUt47sh4p" title="自訂前">
<TabTitle>自訂前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2c389a4b49d437d97ef29c2eaa39b29~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="aIcqW6UbP3" title="自訂後">
<TabTitle>自訂後</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bcad45935ec4e7e9da9c74dc16a1170~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```objectivec
// Customize the floating window in the full-featured live room.
livePullVC.config.customFloatingController = ^(BDLLivePullViewController * _Nonnull viewController, BDLFloatingController * _Nonnull floatingController) {
    // Customize the default position of floating interaction tools.該視圖支援拖曳，因此必須透過設定 view.frame 來調整位置，而非使用自動佈局。
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
#### 商品卡片菜單的高度

預設情況下，商品卡片選單的高度為螢幕高度的 73%。你可以自訂選單的高度。

以下範例程式碼將選單高度設為螢幕高度的一半。


<Tabs>
<Tab zoneid="TTYp3dLnOX" title="自訂前">
<TabTitle>自訂前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4789ad68e6c248f7876e4cfce8059b49~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="rnyoymwaau" title="自訂後">
<TabTitle>自訂後</TabTitle>

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
