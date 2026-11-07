---
title: "iOS 版 Viewer SDK：基本功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW"
---

本主題說明如何整合 iOS 版 Viewer SDK 的基本功能，包括如何整合全功能直播間、預設播放器、自訂播放器以及浮動播放器。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">目前，觀眾一次僅能加入一個直播間。</div>


<span id="59273a71"></span>
## 先決條件

請完成 [整合 iOS 版 Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-ios-ban-viewer-sdk-zh-TW) 中的前 5 個步驟。

<span id="98b7076d"></span>
## 功能

本主題說明如何整合以下功能。


* [全功能直播間](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#f2a7c3c8)

* [預設播放器](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#886e9207)

* [自訂播放器](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#8f276f8b)

* [浮動播放器](https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#765f75ba)


<span id="f2a7c3c8"></span>
## 全功能直播間

全功能直播間包含 BytePlus Live 直播間的所有功能模組，較單獨整合各模組更為簡便且方便。除非有特殊需求，建議您整合全功能直播間。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0572b0440b4404dbdb4ef127dc6e574~tplv-goo7wpa0wc-image.image) </span>

如需瞭解全功能直播間支援的功能，請參見 [SaaS 與 aPaaS 的功能比較](https://docs.byteplus.com/docs/byteplus-livesaas/saas-yu-apaas-de-gong-neng-bi-jiao-zh-TW)。

<span id="bb63491d"></span>
### 進入直播間

以下範例程式碼可讓觀眾進入全功能直播間，並在應用程式中顯示全功能直播間頁面。

```objectivec
...
[[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                 success:^{
    // 1. Get the full-featured live room instance.
    BDLLivePullViewController *livePullVC = [[BDLLiveEngine sharedInstance] getLivePullViewController];
    // 2. (Optional) Set the modalPresentationStyle, which is the mode of displaying the live room.本例將直播間以全螢幕模式顯示。
    // If you choose to display the live room using the UINavigationController push mode, or to display the live room using the system's default mode, no additional configuration is needed.
    livePullVC.modalPresentationStyle = UIModalPresentationFullScreen;
    // 3. Set the actionProvider.此處以 "self" 為例，用於響應直播間顯示與隱藏等事件。
    livePullVC.actionProvider = self;
    // 4.（可選）配置直播間。
    [self configLivePullViewController:livePullVC];
    // 5. Display the live room.此處以 present 模式顯示直播間為例。
    // 若需使用 UINavigationController push 模式顯示直播間，請參見以 push 模式顯示直播間。
    [self showLivePullViewController:livePullVC];
} failure:^(NSError * _Nonnull error) {
    // Process error messages.本例將錯誤訊息輸出到控制台以便除錯與排查。
    NSLog(@"%@", error.localizedDescription);
}];

/// Configure the live room, including customizing the UI.你可以將功能代碼複製到此方法中運行。
- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}

/// 6. Methods required for implementing actionProvider.
/// 6.1 顯示直播間的方法。
/// Display the live room.當需要顯示全功能直播間時，SDK 會調用此方法。此處以 present 模式顯示直播間為例。
/// To display the live room using the UINavigationController push mode, see Displaying the live room using push mode.
- (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self presentViewController:livePullVC animated:NO completion:nil];
}

/// 6.2 The method to hide the live room.
/// 隱藏直播間。當需要隱藏全功能直播間時，SDK 會調用此方法。
- (void)hideLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self dismissViewControllerAnimated:YES completion:nil];
}
```


<span id="d649b214"></span>
### 以推送模式顯示直播間

若要使用 `UINavigationController` `push` 模式顯示全功能直播間，可參考以下流程。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">僅 SDK 1.29.1 及以上版本支援<code>push</code>模式。</div>



1. 取得全功能直播間實例後，請配置浮動播放器（即應用內子母畫面（PiP））的顯示邏輯。

   1. 設定是否顯示浮動播放器。

      ```objectivec
      /// 當直播間狀態變化時，會觸發此回調，並將以下資訊傳遞給 App：全功能直播間實例、直播間狀態，以及直播間頁面是否關閉。
      livePullVC.config.shouldShowInAppPipIfAvailable = ^BOOL(BDLLivePullViewController * _Nonnull viewController, BDLActivityStatus status, BOOL isClose) {
          /// 根據直播間狀態及頁面是否關閉來判斷是否顯示浮動播放器。
          switch (status) {
              case BDLActivityStatusLive: // 若直播間狀態為 Live，則執行以下邏輯。
                  return isClose ? YES : NO; // 本例中，當 isClose 值為 YES 時回傳 YES，isClose 值為 NO 時回傳 NO。換句話說，當直播間頁面通過pop 或 dismiss 操作關閉時，會顯示浮動播放器。當以push 或 present 模式顯示商品詳情頁等新頁面時，不會顯示浮動播放器。
              case BDLActivityStatusReplay: // 若直播間狀態為Playback，執行以下邏輯。
                  return isClose ? YES : NO; // 本範例中，當 isClose 的值為 YES 時回傳 YES，當 isClose 的值為 NO 時回傳 NO。換句話說，當直播間頁面透過pop 或 dismiss操作關閉時，會顯示浮動播放器。當使用push 或 present模式顯示商品詳情頁等新頁面時，浮動播放器不會顯示。
              case BDLActivityStatusPreview: // 若直播間狀態為Preview 且預覽正在播放時，執行以下邏輯。
                  return isClose ? YES : NO; // 本範例中，當 isClose 的值為 YES 時回傳 YES，當 isClose 的值為 NO 時回傳 NO。換句話說，當直播間頁面透過pop 或 dismiss操作關閉時，會顯示浮動播放器。當使用push 或 present模式顯示商品詳情頁等新頁面時，浮動播放器不會顯示。
              default:
                  return NO; // The floating player is not displayed.一般情況下，此邏輯不會觸發，但為避免錯誤，必須設定此預設回傳值。
          }
      };
      ```
      

   2. 配置當 `viewDidAppear`（即顯示全功能直播間對應視圖時）時，是否自動關閉正在顯示的浮動播放器。

      可使用以下範例程式碼自動關閉正在顯示的浮動播放器。

      ```objectivec
      livePullVC.config.autoCloseFloatingPlayerWhenAppear = YES;
      ```
      

   若值為 `NO`，則需在適當時機呼叫關閉浮動播放器的方法。

   可使用以下範例程式碼關閉浮動播放器並同時顯示全功能直播間。

   ```objectivec
   [livePullVC hideFloatingPlayerIfAvailable:YES]
   ```
   

2. 顯示全功能直播間。

   範例程式碼如下。

   ```objectivec
   - (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
       if (self.livePullVC.navigationController) { // 當使用 push 或 present 模式顯示商品詳情頁等新頁面時，SDK 會關閉浮動播放器，不顯示全功能直播間，且觀眾點擊浮動播放器的關閉按鈕後不會離開直播間。
           [self.navigationController popToViewController:livePullVC animated:YES]; // 使用 pop 操作移除顯示於全功能直播間之上的其他頁面（ViewController）。
           return;
       }
       [self.navigationController pushViewController:livePullVC animated:YES]; // 使用 push 模式顯示全功能直播間。
   }
   ```
   

3. （可選）若您配置浮動播放器在新頁面被推送或呈現時顯示（即在步驟 1.a 中 isClose 為 NO 時回傳 YES），則還需自訂浮動播放器關閉按鈕的點擊行為。

   範例程式碼如下。

   ```objectivec
       __weak typeof(self) weakSelf = self;
       livePullVC.onFloatingPlayerCloseTapped = ^BOOL(BDLLivePullViewController * _Nonnull viewController, BDLFloatingPlayer * _Nonnull floatingPlayer) {
           if (viewController.navigationController) {
               // 當使用 push 或 present 模式顯示商品詳情頁等新頁面時，SDK 會關閉浮動播放器，不顯示全功能直播間，且觀眾點擊浮動播放器的關閉按鈕後不會離開直播間。
               [viewController hideFloatingPlayerIfAvailable:NO];
               return NO;
           }
           else {
               // 當直播間頁面透過 pop 或 dismiss 操作關閉時，SDK 會在觀眾點擊浮動播放器的關閉按鈕後執行預設點擊行為：關閉浮動播放器並離開直播間。
               return YES;
           }
       };
   ```
   

4. （可選）除全螢幕模式外，全功能直播間僅支援直向顯示。若應用程式頁面支援橫向顯示，請完成以下配置。

   * 顯示全功能直播間時，請確保前一頁僅支援直向顯示。

      範例程式碼如下。

      ```objectivec
      // 請在 ViewController 中新增以下程式碼。
      @interface ViewController : UIViewController
      @property (nonatomic, assign) BOOL visible;
      @end
      
      // 當 viewDidAppear，也就是前一頁對應的視圖顯示時，將 visible 設為 YES，表示目前視圖可見。
      - (void)viewDidAppear:(BOOL)animated {
          [super viewDidAppear:animated];
          self.visible = YES;
      }
      // 當 viewDidDisappear，也就是前一頁對應的視圖消失時，將 visible 設為 NO，表示目前視圖不可見。
      - (void)viewDidDisappear:(BOOL)animated {
          [super viewDidDisappear:animated];
          self.visible = NO;
      }
      
      // 指定目前視圖所支援的頁面方向。
      - (UIInterfaceOrientationMask)supportedInterfaceOrientations {
          if (!self.visible) { // 當目前視圖不可見時，直播間僅支援直向，以避免側滑返回前一頁造成顯示異常。
              return UIInterfaceOrientationMaskPortrait;
          }
          // 當目前視圖可見時，前一頁所支援的頁面方向。本範例中，前一頁支援除 UpsideDown 以外的所有方向。
          return UIInterfaceOrientationMaskAllButUpsideDown;
      }
      ```
      

   * 當直播間頁面以橫向（即全螢幕模式）顯示時，請停用側滑返回，以避免頁面顯示異常。

      ```objectivec
      // 請在 ViewController 中新增以下程式碼。
      // 當裝置方向即將改變時，系統會呼叫此方法。
      - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
          if (size.width > size.height) { // 寬度大於高度，表示頁面方向為橫向。
              self.navigationController.interactivePopGestureRecognizer.enabled = NO; // 禁用側滑返回。
          }
          else {
              self.navigationController.interactivePopGestureRecognizer.enabled = YES; // 啟用側滑返回。
          }
      }
      ```
      

   * 當裝置在直向與橫向間切換時，請確保浮動播放器的方向與應用程式當前頁面方向一致。

      ```objectivec
      // 將以下程式碼加入 NavigationController 或 UIViewController。
      
      #import <BPLive/BPLive.h>
      @interface ViewController : UIViewController
      //NOTE:在取得全功能直播間實例時，為 livePullViewController 設定值。
      @property (nonatomic, weak) BDLLivePullViewController *livePullViewController;
      @end
      
      // 當裝置方向即將改變時，系統會呼叫此方法。
      - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
          [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
      // 取得 App 的目前頁面方向。
          UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
          if (@available(iOS 13, *)) {
              // 若使用 self.view.window，當 ViewController 不可見時會回傳 nil。因此，請改用 self.navigationController.view.window。
              orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
          } else {
              orientation = UIApplication.sharedApplication.statusBarOrientation;
          }
          // 當先顯示全功能直播間再顯示浮動播放器時，請調整 livePullViewController.floatingPlayerOrientation，使浮動播放器的方向與 App 的目前頁面方向一致。
          if (self.livePullViewController.isFloating) {
              self.livePullViewController.floatingPlayerOrientation = orientation;
          }
          // 若直接顯示浮動播放器，請調整 floatingPlayer，使浮動播放器的方向與 App 的目前頁面方向一致。
          if (self.floatingPlayer) {
              [self.floatingPlayer setUIOrientation:orientation];
          }
      }
      ```
      


<span id="b9af31ad"></span>
### 離開直播間

當需要讓觀眾離開直播間時，例如觀眾無權觀看影片，可參考以下範例程式碼實現。

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}
```


<span id="de46cbc8"></span>
### 完整範例程式碼

以下範例程式碼以以 `present` 模式顯示的直向直播間為例，活動 ID（`activityId`）為 `167808997736****`，`token` 為 `JQ****`，驗證模式（`authMode`）為 public。你可以根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a> 以取得直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a> 並將 <code>Mode</code> 的值設為 <code>1</code>，以取得公開模式下的授權令牌。如需將驗證模式更改為自訂，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/ios-ban-viewer-sdk-jin-jie-gong-neng-zh-TW#0f3118f8">自訂登入</a>。</div>



```objectivec
- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        BDLLivePullViewController *livePullVC = [[BDLLiveEngine sharedInstance] getLivePullViewController];
        livePullVC.modalPresentationStyle = UIModalPresentationFullScreen;
        livePullVC.actionProvider = self;
        [self configLivePullViewController:livePullVC];
        [self showLivePullViewController:livePullVC];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}

- (void)configLivePullViewController:(BDLLivePullViewController *)livePullVC {
}

- (void)showLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self presentViewController:livePullVC animated:NO completion:nil];
}

- (void)hideLivePullViewController:(BDLLivePullViewController *)livePullVC {
    [self dismissViewControllerAnimated:YES completion:nil];
}
```


<span id="886e9207"></span>
## 預設播放器

若你有自己的觀看頁面且不需要自訂播放器控制介面，可以選擇只整合預設播放器。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/336044b1c120414bb089a238261d94ff~tplv-goo7wpa0wc-image.image) </span>

<span id="76e1141c"></span>
### 加入直播間

使用以下範例程式碼加入直播間並建立預設播放器。

```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLPlayerView *playerView;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        // Create a player with the control interface, which means it has interactive buttons such as the play button.此處以直向模式初始化播放器作為範例。
        self.playerView =[[BDLPlayerView alloc] initWithPortrait:YES];
        // Set popupSuperView to the current view.SDK 會使用此視圖來顯示彈出選單，例如播放速度與解析度選擇。
        self.playerView.popupSuperView = self.view;
        //  Add the playerView as a subview to the current view.
        [self.view addSubview:self.playerView];
        //  Set the playerView to fill its parent view, namely the current view.
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
     // Process error messages.本範例將錯誤訊息輸出至主控台以便除錯與排查。
        NSLog(@"%@", error.localizedDescription);
    }];
```


<span id="a14bdc9d"></span>
### 離開直播間

當觀眾離開你的觀看頁面時，請使用以下範例程式碼離開直播間並釋放預設播放器的引用。

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="380f8e9b"></span>
### 完整範例程式碼

以下範例程式碼以直式直播間為例，活動 ID（`activityId`）為 `167808997736****`，`token` 為 `JQ****`，驗證模式（`authMode`）為 public。你可以根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a> 以取得直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a> 並將 <code>Mode</code> 的值設為 <code>1</code>，以取得公開模式下的授權令牌。</div>



```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLPlayerView *playerView;
@end

- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        self.playerView =[[BDLPlayerView alloc] initWithPortrait:YES];
        self.playerView.popupSuperView = self.view;
        [self.view addSubview:self.playerView];
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="8f276f8b"></span>
## 自訂播放器

自訂播放器不包含控制介面，亦即沒有播放按鈕等互動按鈕。若你有自己的觀看頁面且對播放器控制介面有自訂需求，可以選擇只整合自訂播放器。整合自訂播放器後，你可以新增自己的自訂控制介面。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12a767eab5b045c79c9cd7137b2adebb~tplv-goo7wpa0wc-image.image) </span>

<span id="a8ad5281"></span>
### 加入直播間

使用以下範例程式碼加入直播間並建立自訂播放器。

```objectivec
@interface ViewController () <BDLBasePlayerViewDelegate>
@property (nonatomic, strong) BDLBasePlayerView *playerView;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        //  Create a custom player.
        self.playerView =[[BDLBasePlayerView alloc] init];
        // Set the current ViewController as the delegate of playerView to receive and process playerView events.
        self.playerView.delegate = self;
        // Add the playerView as a subview to the ViewController view.
        [self.view addSubview:self.playerView];
        // Set the playerView to fill its parent view, namely the ViewController view.
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
    // Process error messages.本範例將錯誤訊息輸出至主控台以便除錯與排查。
        NSLog(@"%@", error.localizedDescription);
    }];
    ...
```


<span id="98960cf6"></span>
### 處理 delegate

你可以處理 delegate，將相關回呼資訊傳遞給你的應用程式，以便在以下情境自訂控制介面：


* 封面圖片、播放內容、播放狀態、影片尺寸或卡頓狀態變化。

* 進入或離開 PiP 模式。

* 首幀載入成功。


在以下範例程式碼中，當影片卡頓狀態變化時會輸出 log 訊息。

```objectivec
// The video starts to stutter.
- (void)basePlayerViewStallStart:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}

// The video stops stuttering.
- (void)basePlayerViewStallEnd:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}
```


<span id="5193c9b6"></span>
### 離開直播間

當觀眾離開你的觀看頁面時，請使用以下範例程式碼離開直播間並釋放自訂播放器的引用。

```objectivec
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}
```


<span id="b59c0c4b"></span>
### 完整範例程式碼

以下範例程式碼以直式直播間為例，活動 ID（`activityId`）為 `167808997736****`，`token` 為 `JQ****`，驗證模式（`authMode`）為 public。你可以根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a> 以取得直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a> 並將 <code>Mode</code> 的值設為 <code>1</code>，以取得公開模式下的授權令牌。</div>



```objectivec
@interface ViewController () <BDLBasePlayerViewDelegate>
@property (nonatomic, strong) BDLBasePlayerView *playerView;
@end

- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        self.playerView =[[BDLBasePlayerView alloc] init];
        self.playerView.delegate = self;
        [self.view addSubview:self.playerView];
        [self.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
            make.edges.equalTo(self.view);
        }];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}

- (void)basePlayerViewStallStart:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}

- (void)basePlayerViewStallEnd:(BDLBasePlayerView *)basePlayerView {
    NSLog(@"%s", __func__);
}
```


<span id="765f75ba"></span>
## 浮動播放器

浮動播放器，也稱為畫中畫（Picture\-in\-Picture，PiP），可在直播間頁面關閉後，透過 `pop` 或 `dismiss` 動作顯示。

整合完整功能直播間後，即可使用浮動播放器。但若需先顯示浮動播放器再顯示完整功能直播間，則必須整合浮動播放器。例如，觀眾先進入你的商品詳情頁觀看商品，然後點擊浮動播放器加入完整功能直播間。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eecf0f7799614561aa635a2eb28ebf66~tplv-goo7wpa0wc-image.image) </span>

<span id="c430d76f"></span>
### 加入直播間

使用以下範例程式碼加入直播間並顯示浮動播放器。

```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLFloatingPlayer *floatingPlayer;
@end

    ...
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
       
        // Create the floating player.此處以直向模式初始化浮動播放器作為範例。
        // 此參數值僅影響取得浮動播放器載入圖片及圖片尺寸的方法，不影響浮動播放器的顯示。浮動播放器的長寬比與影片相同。
        self.floatingPlayer = [[BDLFloatingPlayer alloc] initWithPortrait:YES];
        // 顯示浮動播放器。此處以在浮動播放器右上角顯示關閉圖示作為範例。
        self.floatingPlayer.delegate = self;
        [self.floatingPlayer showWithCloseButton:YES];
    } failure:^(NSError * _Nonnull error) {
     // 處理錯誤訊息。在此範例中，錯誤訊息會列印到主控台以進行除錯和問題排查。
        NSLog(@"%@", error.localizedDescription);
    }];
```


<span id="69016853"></span>
### 離開直播間

使用以下範例程式碼關閉浮動播放器並離開直播間。

```objectivec
// 當觀眾點擊浮動播放器的關閉圖示時，關閉浮動播放器並離開直播間。
- (void)floatingPlayerWillClose:(BDLFloatingPlayer *)floatingPlayer {
    [self leaveLiveRoom]
}

// 關閉浮動播放器、離開直播間，並釋放對浮動播放器的參考，當你需要關閉浮動播放器時。
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.floatingPlayer hide];
    self.floatingPlayer = nil;
}
```


<span id="1252ec6b"></span>
### 自動旋轉浮動播放器方向

使用以下範例程式碼，當裝置方向在直式與橫式間切換時，讓浮動播放器方向與應用程式目前頁面方向保持一致。

```objectivec
// 當裝置方向即將變更時，系統會呼叫此方法。
- (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
    [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
// 取得應用程式目前頁面方向。
    UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
    if (@available(iOS 13, *)) {
        // 如果你使用 self.view.window，當 ViewController 不可見時會回傳 nil。因此，請改用 self.navigationController.view.window。
        orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
    } else {
        orientation = UIApplication.sharedApplication.statusBarOrientation;
    }
    // 保持浮動播放器的方向與應用程式目前頁面方向一致。
    [self.floatingPlayer setUIOrientation:orientation];
}
```


<span id="a5a967d5"></span>
### 返回全功能直播間後繼續播放視頻

為確保觀眾點擊浮動播放器返回全功能直播間時能持續播放，請使用以下範例代碼。

```objectivec
// MARK: - BDLFloatingPlayerDelegate
// This callback is triggered when viewers tap the floating player.
- (void)floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
    // Hide the floating player.
    [self.floatingPlayer hide];
    // 取得浮動播放器中的 basePlayerView。
    BDLBasePlayerView *basePlayerView = [floatingPlayer removeBasePlayerView];
    // Create the full-featured live room and pass the obtained basePlayerView.
    BDLLivePullViewController *vc = [[BDLLiveEngine sharedInstance] getLivePullViewControllerWithBasePlayerView:basePlayerView];
    vc.delegate = self;
    vc.actionProvider = self;
    self.livePullViewController = vc;
    self.floatingPlayer = nil;
    // 根據需要選擇以 push 或 present 模式顯示全功能直播間。
    [self.navigationController pushViewController:self.livePullViewController animated:YES];
}
```


<span id="ef5b1cff"></span>
### 完整範例代碼

以下範例代碼以直向模式的直播間為例，activity ID（`activityId`）為`167808997736****`，`token` 為 `JQ****`，驗證模式（`authMode`）為 public。你可以根據需要修改參數值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW">CreateActivityAPIV2</a> 或 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW">ListActivityAPI</a> 以取得直播間的活動 ID。</div>


* <div data-tips="true" data-tips-type="tip">呼叫 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW">GetSDKTokenAPI</a> 並將 <code>Mode</code> 的值設為 <code>1</code>，以取得公開模式下的授權令牌。</div>



```objectivec
@interface ViewController ()
@property (nonatomic, strong) BDLFloatingPlayer *floatingPlayer;
@end


- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****);
    activity.token = @"JQ****";
    activity.isPortrait = YES;
    activity.authMode = BDLActivityAuthModePublic;
    
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity
                                                     success:^{
        self.floatingPlayer = [[BDLFloatingPlayer alloc] initWithPortrait:YES];
        self.floatingPlayer.delegate = self;
        [self.floatingPlayer showWithCloseButton:YES];
    } failure:^(NSError * _Nonnull error) {
        NSLog(@"%@", error.localizedDescription);
    }];
}

- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
    [self.playerView removeFromSuperview];
    self.playerView = nil;
}

- (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
    [super viewWillTransitionToSize:size withTransitionCoordinator:coordinator];
    
    UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
    if (@available(iOS 13, *)) {
        orientation = self.navigationController.view.window.windowScene.interfaceOrientation;
    } else {
        orientation = UIApplication.sharedApplication.statusBarOrientation;
    }
    [self.floatingPlayer setUIOrientation:orientation];
}

- (void)floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
    [self.floatingPlayer hide];
    BDLBasePlayerView *basePlayerView = [floatingPlayer removeBasePlayerView];
    BDLLivePullViewController *vc = [[BDLLiveEngine sharedInstance] getLivePullViewControllerWithBasePlayerView:basePlayerView];
    vc.delegate = self;
    vc.actionProvider = self;
    self.livePullViewController = vc;
    self.floatingPlayer = nil;
    [self.navigationController pushViewController:self.livePullViewController animated:YES];
}
```
