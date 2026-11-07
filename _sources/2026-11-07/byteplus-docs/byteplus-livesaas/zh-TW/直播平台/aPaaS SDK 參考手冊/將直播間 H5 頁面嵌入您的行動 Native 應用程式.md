---
title: "將直播間 H5 頁面嵌入您的行動 Native 應用程式"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW"
---

您可以將 BytePlus Live 直播間的 H5 頁面嵌入您的行動 Native 應用程式，以啟用常見功能，例如子母畫面（PiP）和自動播放。本主題以 iOS 和 Android 應用程式範例為例，介紹如何實現這些功能。

<span id="259416b3"></span>
## 先決條件

您可以透過以下任一方式取得直播間的 H5 頁面：


* Web Viewer SDK：整合 2.0.16 版本或以上的 Web Viewer SDK 時，建立直播或隨選視訊（VOD）播放器實例。整合 Web Viewer SDK 的觀看頁面即為直播間 H5 頁面，僅顯示一個播放器。如需更多關於如何整合 Web Viewer SDK 的資訊，請參閱 [整合 Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-web-viewer-sdk-zh-TW)。

* SaaS：此處以 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)為例，介紹如何取得 SaaS 直播間 H5 頁面。

   1. 在直播間列表中，點擊進入某個直播間。

   2. 點擊觀看頁面地址，即可開啟 SaaS 直播間 H5 頁面。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cb3dbd6a900415191cc07edc9f8a9e3~tplv-goo7wpa0wc-image.image) </span>


<span id="04b7fe45"></span>
## 執行範例的環境要求


<Tabs>
<Tab zoneid="V3OuylN7EI" title="iOS">
<TabTitle>iOS</TabTitle>

* 運行 iOS 11.0 或以上版本的實體設備或模擬器。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">要在你的 demo 或專案中實現系統 PiP 功能，請確保 iOS 作業系統版本為 14.0 或以上。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">模擬器僅供介面除錯使用，不保證音訊、視訊及子母畫面（PiP）等功能可正常運作。為避免螢幕殘影或黑邊等問題，建議使用實體裝置。   </div>
   

* Xcode 16 或以上版本。

* CocoaPods 16 或以上版本。


</Tab>
<Tab zoneid="AzTNVwcNHC" title="Android">
<TabTitle>Android</TabTitle>

* Android Studio 3.0 或以上版本。

* 運行 Android 5.0（API level 21）或以上版本的實體設備。

* JDK 1.7.0 或以上版本。


</Tab>
</Tabs>


<span id="f34e455d"></span>
## 專案介紹

BytePlus Live 提供一個開源範例專案 `BDLWebDemo`，展示如何將直播間 H5 頁面嵌入您的行動 Native 應用程式。範例專案已針對 H5 頁面進行良好適配，優化觀看體驗，並提供 PiP、自動播放等擴展功能。

您可根據需求修改範例中的程式碼，以實現自訂業務邏輯。

範例專案實現了以下功能：


<Tabs>
<Tab zoneid="x9wOGWUJ1x" title="iOS">
<TabTitle>iOS</TabTitle>

* PiP，包括系統 PiP 與應用內 PiP

* 自動播放

* 配置全螢幕圖示點擊行為

* 自訂跳轉邏輯


</Tab>
<Tab zoneid="s2dFpPiLCP" title="Android">
<TabTitle>Android</TabTitle>

* PiP，包括系統 PiP 與應用內 PiP

* 自動播放

* 配置全螢幕圖示點擊行為

* 系統 PiP 關閉時的背景播放

* 自訂播放備用圖片

* 自訂跳轉邏輯


</Tab>
</Tabs>


<span id="596b1370"></span>
## 執行範例


<Tabs>
<Tab zoneid="QHgNVzG73M" title="iOS">
<TabTitle>iOS</TabTitle>

完成以下步驟以運行 iOS 應用的示例：


1. 聯繫 BytePlus Live 技術支持取得 `BDLWebDemo` 套件並解壓縮。

2. 打開終端視窗，執行 `cd` 命令切換至 `BDLWebDemo/iOS/Example` 目錄，並執行 `pod install` 命令安裝第三方庫。

   ```Shell
   cd ./BDLWebDemo/iOS/Example
   pod install
   ```
   

3. 在 Finder 中找到 **BDLWebDemo.xcworkspace** 檔案，雙擊打開 Xcode 專案。

4. 在 **BDLWebDemo** \> **Signing & Capabilities** \> **All** \> **Signing (Debug)**  區段，勾選 **Automatically manage signing** 核取方塊，然後修改 **Team** 和 **Bundle Identifier** 以符合你的應用資訊。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79f580df703c425fb677b1253acd837b~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果你是在模擬器上運行示範，則可以跳過此步驟。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">在 Xcode 中勾選 <strong>自動管理簽名</strong>核取方塊可以簡化程式碼簽名流程，節省時間並減少潛在錯誤。因此，我們建議你勾選此核取方塊。如果你未勾選此核取方塊，則必須修改 <strong>Provisioning Profile</strong> 和 <strong>Bundle Identifier</strong>，以符合你的應用程式資訊。   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">在示範中，<strong>音訊、AirPlay 和子母畫面</strong>核取方塊於 <strong>背景模式</strong>區段預設已勾選，因此在運行示範時無需手動勾選。但當你在專案中實作示範的系統子母畫面功能時，需手動勾選該核取方塊。詳細步驟請參見 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#850b1dac">快速實現範例功能</a>。   </div>
   

5. 在鍵盤上按下 `⌘+R` 以啟動示範應用程式。

6. 開啟應用程式以查看以下介面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea8d077e522439fac34699d331e1aff~tplv-goo7wpa0wc-image.image) </span>

   你可以執行以下操作：

   * 點選 **Enter live room** 以加入 BytePlus Live 的官方示範直播間。你也可以將預填地址替換為直播間 H5 頁面的地址，以加入特定直播間。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#259416b3)。

   * 點選右上角的掃描圖示，並掃描 QR 碼以加入特定直播間。

      * 要透過掃描 QR 碼進入 SaaS 直播間 H5 頁面，請依照以下步驟操作：

         1. 登入 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)。

         2. 在直播間列表中，點擊進入一個直播間。

         3. 將滑鼠指標移至 **View on mobile**，並掃描相應的 QR 碼。

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0507eea490454bf9989785bd6586d652~tplv-goo7wpa0wc-image.image) </span>

      * 要透過掃描 QR 碼進入整合 Web Viewer SDK 的直播間 H5 頁面，請確保該頁面具有相應的 QR 碼。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#259416b3)。

   * 點選 **Demo Config** 以進入 設定頁面。你可以根據需求完成以下配置，以實現不同的示範效果。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4d0bf188c44ebaa5c6fc1d90e190a6~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">上述所選項目為預設配置。      </div>
      


</Tab>
<Tab zoneid="AlICSjeF5x" title="Android">
<TabTitle>Android</TabTitle>

完成以下步驟以執行 Android 應用的示範：


1. 聯絡 BytePlus Live 技術支援以取得 `BDLWebDemo` 套件並解壓縮。

2. 使用 Android Studio 開啟 `BDLWebDemo` 專案檔案。

3. 連接 Android 裝置後，在 Android Studio 中點擊 **Run** 圖示以執行專案。

4. 專案成功執行後，依提示在你的 Android 裝置上安裝名為 `BDLWebDemo` 的應用程式。

5. 開啟應用程式以查看以下介面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911f35c1e7bc484ab9af6314b94a6330~tplv-goo7wpa0wc-image.image) </span>

   你可以執行以下操作：

   * 點選 **GO TO LIVEROOM** 以加入 BytePlus Live 的官方示範直播間。你也可以將預填地址替換為直播間 H5 頁面的地址，以加入特定直播間。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#259416b3)。

   * 點選右上角的掃描圖示，並掃描 QR 碼以加入特定直播間。

      * 要透過掃描 QR 碼進入 SaaS 直播間 H5 頁面，請依照以下步驟操作：

         1. 登入 [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement)。

         2. 在直播間列表中，點擊進入一個直播間。

         3. 將滑鼠指標移至 **View on mobile**，並掃描相應的 QR 碼。

            <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f556d9da28514d8b8896d8d3dde73196~tplv-goo7wpa0wc-image.image) </span>

      * 要透過掃描 QR 碼進入整合 Web Viewer SDK 的直播間 H5 頁面，請確保該頁面具有相應的 QR 碼。如需取得直播間 H5 頁面的更多資訊，請參閱 [先決條件](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#259416b3)。

   * 點選 **DEMO CONFIGURATION** 以進入 設定頁面。你可以根據需求完成以下配置，以實現不同的示範效果。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fda0c24b7dd0476b92b908e9ab67fe4b~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">上述所選項目為預設配置。      </div>
      


</Tab>
</Tabs>


<span id="dc6ebb18"></span>
## 功能實現

<span id="850b1dac"></span>
### 快速實現範例功能

若無自訂需求，您可直接複製範例程式碼，快速在專案中實現範例功能。


<Tabs>
<Tab zoneid="g85cMmJRa3" title="iOS">
<TabTitle>iOS</TabTitle>

完成以下步驟：


1. 將 `BDLWebDemo/iOS/BDLWeb` 目錄中的所有程式碼複製到你的專案中。

   ```objectivec
   BDLWebDemo
   └── iOS
       ├── BDLWeb // 網頁功能封裝程式碼。你可以將此目錄下的所有程式碼複製到你的專案中，以快速實現示範功能。
       │   ├── BDLWeb
       │   │   ├── Category // 系統類能力擴展。
       │   │   │   ├── UIDevice+BDL.h
       │   │   │   ├── UIDevice+BDL.m
       │   │   │   ├── UIImage+BDLAdditions.h
       │   │   │   ├── UIImage+BDLAdditions.m
       │   │   │   ├── UIWindow+BDLAdditions.h
       │   │   │   └── UIWindow+BDLAdditions.m
       │   │   ├── Config // 自訂配置。
       │   │   │   ├── BDLSettings.h
       │   │   │   └── BDLSettings.m
       │   │   ├── FloatingPlayer // 應用內子母畫面邏輯。
       │   │   │   ├── BDLFloatingPlayer.h
       │   │   │   ├── BDLFloatingPlayer.m
       │   │   │   ├── BDLFloatingWindow.h
       │   │   │   └── BDLFloatingWindow.m
       │   │   ├── PiP // 系統子母畫面邏輯。
       │   │   │   ├── BDLPiPHelper.h
       │   │   │   ├── BDLPiPHelper.m
       │   │   │   ├── BDLPiPVideoWriter.h
       │   │   │   └── BDLPiPVideoWriter.m
       │   │   ├── Utils // 工具函式。
       │   │   │   ├── BDLDefines.h
       │   │   │   ├── BDLResponder.h
       │   │   │   ├── BDLResponder.m
       │   │   │   ├── BDLUtils.h
       │   │   │   └── BDLUtils.m
       │   │   └── WebView // 直播間容器。
       │   │       ├── BDLWebMessageModel.h
       │   │       ├── BDLWebMessageModel.m
       │   │       ├── BDLWebView.h
       │   │       ├── BDLWebView.m
       │   │       ├── BDLWebViewController.h
       │   │       └── BDLWebViewController.m
       │   └── BDLWeb.podspec
       └── Example // 示範 UI 程式碼，包括配置頁、QR Code 掃描頁，以及輸入觀看頁面地址的引導頁。
           └── BDLWebDemo
               ├── AppDelegate.h
               ├── AppDelegate.m
               ├── BDLCommonWebViewController.h // 通用 WebView，可開啟如商品詳情頁等網址，亦可替換為你應用中的 WebView 或商品頁。
               ├── BDLCommonWebViewController.m
               ├── BDLCustomConfig.h
               ├── BDLCustomConfig.m
               ├── BDLScanViewController.h // 示範中的 QR Code 掃描頁。
               ├── BDLScanViewController.m
               ├── BDLSelectionCell.h
               ├── BDLSelectionCell.m
               ├── BDLSelectionView.h
               ├── BDLSelectionView.m
               ├── BDLSelectionViewController.h  // 示範中的配置頁。
               ├── BDLSelectionViewController.m
               ├── NavigationController.h // 示範中的導覽列。
               ├── NavigationController.m
               ├── ViewController.h // 示範中的輸入觀看頁面地址引導頁。
               └── ViewController.m
           └── Podfile
   ```
   

2. 參考 `BDLWebDemo/iOS/Example/Podfile` 檔案中的配置，並在你的專案 `Podfile` 檔案中新增對 `BDLWeb` 的依賴。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若你的專案先前未使用 CocoaPods，請在專案根目錄執行 <code>pod init && pod install</code>，以取得 <code>Podfile</code> 檔案。   </div>
   

   ```Ruby
   # 你的應用程式目標名稱
   target 'BDLWebDemo' do
   ...
     # 將 ../BDLWeb 替換為你專案中 BDLWeb 資料夾的路徑。
     pod 'BDLWeb', :path => '../BDLWeb'
   
   end
   ```
   

3. 開啟終端視窗，執行 `cd` 指令以切換到你的專案根目錄。執行 `pod install` 指令以安裝依賴項。

4. 參考位於 `BDLWebDemo/iOS/Example` 目錄下的 `ViewController.m` 程式碼，導入 `BDLWebDemo/iOS/BDLWeb/BDLWeb/ Config` 目錄下的 `BDLSettings.h` 標頭檔，以及 `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` 目錄下的 `BDLWebViewController.h` 標頭檔，以整合 BDLWeb。

5. 參考位於 `BDLWebDemo/iOS/Example` 目錄下 `ViewController.m` 檔案中的以下程式碼，以建立並管理直播間。

   ```objectivec
   
   // MARK: - These are the key codes for integration.
   
   - (void)onJoinButtonClicked:(UIButton *)sender {
       // Since the Enter live room button may be tapped again while in-app PiP is displayed, it is necessary to check if the webViewController already exists.
       if (!self.webViewController) {
           self.webViewController = [[BDLWebViewController alloc] init];
           self.webViewController.modalPresentationStyle = UIModalPresentationFullScreen;
           self.webViewController.delegate = self;
       }
       // Check if the entered viewing page address is the same as the current live room's viewing page address.若不同，則重新載入新輸入的觀看頁面地址。
       if (![self.textField.text isEqualToString:self.currentURL]) {
           [self.webViewController loadURLStr:self.textField.text];
           self.currentURL = self.textField.text;
       }
       [self.navigationController pushViewController:self.webViewController animated:YES];
   }
   
   - (void)viewWillAppear:(BOOL)animated {
       [super viewWillAppear:animated];
       // If in-app PiP is not enabled, set webViewController to nil to destroy webViewController, avoiding memory leaks and continuous live room audio playback.
       if (!BDLSettings.sharedInstance.enableInAppPiP) {
           self.webViewController = nil;
           self.currentURL = nil;
       }
   }
   
   - (void)viewWillTransitionToSize:(CGSize)size withTransitionCoordinator:(id<UIViewControllerTransitionCoordinator>)coordinator {
       [coordinator animateAlongsideTransition:nil completion:^(id<UIViewControllerTransitionCoordinatorContext>  _Nonnull context) {
       }];
       UIInterfaceOrientation orientation = UIInterfaceOrientationUnknown;
       if (@available(iOS 13, *)) {
           orientation = self.view.window.windowScene.interfaceOrientation;
       } else {
           orientation = UIApplication.sharedApplication.statusBarOrientation;
       }
       // Set the floatingPlayerOrientation of webViewController to the current orientation to ensure that the orientation of the in-app PiP window is consistent with the current screen orientation.
       self.webViewController.floatingPlayerOrientation = orientation;
   }
   
   // MARK: - BDLWebViewControllerDelegate
   // Callback triggered when the in-app PiP window is tapped.
   - (void)webViewController:(BDLWebViewController *)controller floatingPlayerDidSingleTap:(BDLFloatingPlayer *)floatingPlayer {
       // Tapping the PiP window on the demo home page displays the live room page in push mode.
       if (![self.navigationController.viewControllers containsObject:controller]) {
           [self.navigationController pushViewController:controller animated:YES];
           return;
       }
       // Tapping the PiP window on the product details page pops the ViewController above the live room page until the live room page is displayed.
       [self.navigationController popToViewController:controller animated:YES];
   }
   
   - (void)webViewController:(BDLWebViewController *)controller floatingPlayerDidClickClose:(BDLFloatingPlayer *)floatingPlayer {
   }
   // Callback triggered when the URL is tapped.此回呼僅在 URL 內容顯示於新頁面時觸發。
   - (void)webViewController:(BDLWebViewController *)controller onURLRequestClicked:(NSURLRequest *)urlRequest {
       NSLog(@"debug %s request %@ url %@", __func__, urlRequest, urlRequest.URL);
       // Here, a general WebView is used as an example.請將其替換為應用程式中的 WebView 或產品頁面，以顯示 URL 內容。
       BDLCommonWebViewController *vc = [[BDLCommonWebViewController alloc] init];
       [vc.webView loadRequest:urlRequest];
       [self.navigationController pushViewController:vc animated:YES];
   }
   
   - (void)webViewControllerWillLeaveLiveRoom:(BDLWebViewController *)controller {
       // When viewers leave the live room, set webViewController to nil to avoid memory leaks.
       self.webViewController = nil;
       self.currentURL = nil;
   }
   ```
   

6. 為確保系統 PiP 功能正常運作，請完成以下步驟：

   1. 在 Xcode 中，於你的專案 app target 下，點擊 **Signing & Capabilities** 標籤下的  **+ Capability**，並雙擊新增 **Background Modes**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2c3f9d97d084533ae3828c115bfe907~tplv-goo7wpa0wc-image.image) </span>

   2. 在 **Background Modes** 區段中，勾選 **Audio, AirPlay, and Picture in Picture** 核取方塊。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c7c65846b8b4bb998593395246a197d~tplv-goo7wpa0wc-image.image) </span>

7. 如需修改範例程式碼中的預設配置，可在 `BDLSettings` 中呼叫以下方法。

   * 系統 PiP

      設定 `BDLSettings.sharedInstance.enableSystemPiP` 的值，以啟用或停用系統 PiP。預設值為 `YES`。

      * `YES`：啟用。當觀眾將 App 送至背景，且其裝置的 **設定 \> 一般 \> 畫中畫** 下的 **自動啟動畫中畫** 開關已啟用時，仍可在 PiP 模式下繼續觀看直播或點播影片。

      * `NO`：停用。

   * 應用內 PiP

      設定 `BDLSettings.sharedInstance.enableInAppPiP` 的值，以啟用或停用應用內 PiP。預設值為 `YES`。

      * `YES`：啟用。當觀眾在 App 內切換至其他頁面時，仍可在 PiP 模式下繼續觀看直播或點播影片。

      * `NO`：停用。

   * 自動播放

      設定 `BDLSettings.sharedInstance.enableAutoPlay` 的值，以設定觀眾進入直播間時，直播或點播影片是否自動播放。預設值為 `YES`。

      * `YES`：自動播放。

      * `NO`：不自動播放。

   * 設定全螢幕圖示點擊行為

      設定 `BDLSettings.sharedInstance.fullscreenBtnType` 的值，以設定全螢幕圖示點擊行為，具體來說，當觀眾進入全螢幕模式時，螢幕是否會旋轉。預設值為 `BDLSettingsFullscreenBtnTypeRotate`，會根據影片的長寬比決定螢幕是否旋轉。

      有效值如下。

      ```objectivec
      typedef NS_ENUM(NSUInteger, BDLSettingsFullscreenBtnType) {
          /**
           * 螢幕不會旋轉，螢幕方向維持為直向。
           */
          BDLSettingsFullscreenBtnTypeDoNotRotate,
          /**
           * 螢幕會根據影片的長寬比自動旋轉。對於橫向影片（寬度大於高度），當觀眾進入全螢幕模式時，螢幕會旋轉為橫向。對於直向影片（寬度小於高度），當觀眾進入全螢幕模式時，螢幕方向維持為直向。
           */
          BDLSettingsFullscreenBtnTypeRotate,
          /**
           * 螢幕會被強制旋轉為橫向。
           */
          BDLSettingsFullscreenBtnTypeForceRotate,
      };
      ```
      


</Tab>
<Tab zoneid="vieT0OGsxh" title="Android">
<TabTitle>Android</TabTitle>

完成以下步驟：


1. 在 `app/src/main/java/com/bdlive/bdlwebdemo` 目錄下，將 `sdk` 目錄中的所有程式碼複製到你的專案中。

   ```Python
   com.bdlive.bdlwebdemo
   ├── demo        # Demo UI 程式碼，包括設定頁、QR code 掃描頁，以及輸入觀看頁面地址的引導頁。
   ├── sdk         # Web 功能封裝程式碼。你可以將本目錄下的所有程式碼複製到你的專案中，快速實現 demo 功能。
       ├── api         # 公開 API。
           ├── BDLWebViewActivity.java  # WebView 容器頁面。
           ├── WebConfig.java  # WebView 設定類別。
       ├── data        # 用於儲存網頁互動資料。
       ├── pip         # PiP 邏輯。
       ├── util        # 工具類別。
       ├── webview     # WebView 封裝邏輯。
           ├── BDLNativeBridge.java     # 用於處理 App 與 Web 之間通訊的橋接。
           ├── BDLWebView.java          # 自訂 WebView。
           ├── BDLWebViewController.java # WebView 管理器。
   ```
   

2. 在 `app/src/main` 目錄下的 `AndroidManifest.xml` 檔案中完成以下配置：

   * 新增權限。

      ```XML
      <!-- 網路狀態權限 -->
      <uses-permission android:name="android.permission.INTERNET" />
      <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
      
      <!-- 系統視窗權限 -->
      <uses-permission android:name="android.permission.REORDER_TASKS" />
      <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
      <uses-permission android:name="android.permission.SYSTEM_OVERLAY_WINDOW" />
      ```
      

   * 宣告 `Activity`，以確保 `BDLWebViewActivity` 的行為符合預期並提供一致的使用者體驗。

      ```XML
      <activity
          android:name="com.bdlive.bdlwebdemo.sdk.api.BDLWebViewActivity"
          android:configChanges="keyboardHidden|orientation|screenSize"
          android:exported="false"
          android:launchMode="singleTask"
          android:screenOrientation="portrait"
          android:theme="@style/TVUAppThemeFullscreen"
          android:windowSoftInputMode="adjustResize|adjustNothing|stateAlwaysHidden"
          tools:ignore="LockedOrientationActivity" />
      ```
      

3. 在 `app/src/main/res` 目錄下，將 `layout` 目錄中的佈局檔案、`values/strings.xml`、`style.xml` 及 Java 程式碼中引用的其他資源檔案，複製到專案中對應的目錄，以避免編譯及執行時出現資源未找到錯誤。若有遺漏，Android Studio 等 IDE 會以紅色標示缺失的資源檔案。請依指示將資源檔案複製到你的專案對應目錄。

4. 在 `BDLWebViewActivity` 中呼叫 `start` 方法以進入直播間頁面。

   ```Java
   BDLWebViewActivity.start(activity, webUrl);
   ```
   

5. 若要修改範例程式碼中的預設配置，可在`WebConfig`中呼叫以下方法。

   * PiP

      使用`setPIPConfig`方法可啟用系統 PiP、啟用應用內 PiP 或停用 PiP。預設值為`VALUE_PIP_SYSTEM`，即啟用系統 PiP。

      * 啟用系統 PiP：當觀眾將應用程式移至背景或在應用程式內瀏覽其他頁面時，仍可在 PiP 模式下繼續觀看直播或點播影片。Android 用戶需在裝置上啟用浮動視窗權限才能使用系統 PiP。為提升使用者體驗，建議啟用系統 PiP。

      * 啟用應用內 PiP：當觀眾在當前應用程式中開啟其他頁面時，仍可在 PiP 模式下繼續觀看直播或點播影片。

      * 停用 PiP：觀眾無法以 PiP 模式觀看直播或點播影片。

      有效值如下。

      ```Java
      // Disable PiP.
      public static final int VALUE_PIP_DISABLE = 0;
      // Enable in-app PiP.
      public static final int VALUE_PIP_APPLICATION = 1;
      // Enable system PiP.
      public static final int VALUE_PIP_SYSTEM = 2;
      ```
      

   * 自動播放

      使用`setAutoPlayConfig`方法可設定觀眾進入直播間時，直播或點播影片是否自動播放。預設值為`true`。

      * `true`：自動播放。

      * `false`：不自動播放。

   * 背景播放

      使用`setBackPlayConfig`方法可設定當系統 PiP 停用時，觀眾將當前應用程式切換至背景後，直播或點播影片是否繼續在背景播放。預設值為`true`。

      * `true`：背景繼續播放。

      * `false`：背景停止播放。

   * 更換播放備用圖片

      播放備用圖片指的是播放器載入影片第一幀時顯示的圖片。預設備用圖片如下所示。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf95747ba41c46459d670681a0180238~tplv-goo7wpa0wc-image.image) </span>

      使用`setDefaultBitmapConfig`方法可設定是否以自訂圖片取代預設備用圖片。預設值為`true`。在範例中，備用圖片已被替換為透明圖片。如需自訂備用圖片，請參見[基本自訂設定](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#7f8f09c3)。

      * `true`：替換。

      * `false`：不替換。

   * 配置全螢幕圖示點擊行為

      使用`setFullscreenActionConfig`方法可設定全螢幕圖示的點擊行為，即觀眾進入全螢幕模式時，螢幕是否會旋轉。預設值為 `VALUE_FULLSCREEN_ACTION_AUTO`，即根據影片長寬比決定螢幕是否旋轉。

      有效值如下。

      ```Java
      // 螢幕會根據影片的長寬比自動旋轉。對於橫向影片（寬度大於高度），當觀眾進入全螢幕模式時，螢幕會旋轉為橫向。對於直向影片（寬度小於高度），當觀眾進入全螢幕模式時，螢幕方向維持為直向。
      public static final int VALUE_FULLSCREEN_ACTION_AUTO = 0;
      // 螢幕會被強制旋轉為橫向。
      public static final int VALUE_FULLSCREEN_ACTION_ROTATE_SCREEN = 1;
      // 螢幕不會旋轉，螢幕方向維持為直向。
      public static final int VALUE_FULLSCREEN_ACTION_KEEP_SCREEN_ORIENTATION = 2;
      ```
      


</Tab>
</Tabs>


<span id="7f8f09c3"></span>
### 基本自訂設定

完成[快速實現範例功能](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#850b1dac)後，若需對範例中的功能進行基本自訂設定，可參考以下內容。


<Tabs>
<Tab zoneid="kEZCkRfCPC" title="iOS">
<TabTitle>iOS</TabTitle>

* 修改應用內 PiP 視窗的寬度與高度

   在`BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView/BDLWebViewController.m`檔案中的`getFloatingFrame`方法內，修改`size.height`（高度）與`size.width`（寬度）的值。單位：點。

   ```objectivec
   - (CGRect)getFloatingFrame {
       CGSize size = self.webView.videoSize;
       // Portrait video, width is less than height.
       if (self.webView.isPortraitVideo) {
           CGFloat height = size.height;
           size.height = 180;
           size.width = size.width / height * 180;
       }
       else {
       // Landscape video, width is greater than height.
           CGFloat width = size.width;
           size.width = 180;
           size.height = size.height / width * 180;
       }
       CGSize screenSize = [BDLUtils landscapeScreenSize];
       if (self.isPortrait) {
           screenSize = [BDLUtils portraitScreenSize];
       }
       return CGRectMake(screenSize.width - size.width - 20,
                         screenSize.height - size.height - 20,
                         size.width,
                         size.height);
   }
   ```
   

* 新增控制 UI 或自訂應用內 PiP 視窗的控制 UI 顯示樣式

   在`BDLWebDemo/iOS/BDLWeb/BDLWeb/FloatingPlayer/BDLFloatingPlayer.m`檔案中的`showWithFrame:closeButton:`方法內，新增控制 UI 或自訂應用內 PiP 視窗的控制 UI 顯示樣式。

   以下範例程式碼修改了應用內 PiP 視窗的關閉圖示顯示樣式。

   ```objectivec
   - (BOOL)showWithFrame:(CGRect)frame closeButton:(BOOL)haveCloseButton {
       if ([self.floatingWindow isFloating]) {
           return NO;
       }
       
       self.haveCloseButton = haveCloseButton;
       self.floatingFrame = frame;
           
       @bdl_weakify(self);
       self.floatingWindow.allowClose = self.haveCloseButton;
       // Replace with a custom close icon image.
       UIImage *closeImage = [BDLUtils imageNamed:@"close"]; 
       [self.floatingWindow showWithView:self.containerView
                              closeImage:closeImage
                          closeImageSize:CGSizeMake(30, 30)
                               initFrame:[self getInitFrame]
                              finalFrame:self.floatingFrame
                                duration:0.3
                              willAppear:^(UIView * _Nonnull floatingView) {
           @bdl_strongify(self);
           if ([self.delegate respondsToSelector:@selector(floatingPlayerWillAppear:)]) {
               [self.delegate floatingPlayerWillAppear:self];
           }
       } didDisappear:^(UIView * _Nonnull floatingView) {
           @bdl_strongify(self);
           if ([self.delegate respondsToSelector:@selector(floatingPlayerDidDisappear:)]) {
               [self.delegate floatingPlayerDidDisappear:self];
           }
       } willClose:^(UIView * _Nonnull floatingView) {
           @bdl_strongify(self);
           if ([self.delegate respondsToSelector:@selector(floatingPlayerWillClose:)]) {
               [self.delegate floatingPlayerWillClose:self];
           }
       }];
       return YES;
   }
   ```
   

* 自訂跳轉邏輯

   在示範中，當觀眾點擊選單下的商品卡片、浮動商品卡片、頂部廣告、頁內廣告、浮動廣告、主播帳號、聊天互動選單下的留言區網址，或置頂留言中的網址時，將使用基本的 WKWebView 開啟帶有`http`或`https`協定標頭的地址。如需自訂跳轉邏輯，並根據特定場景或需求調整頁面跳轉行為，可將`webViewController:onURLRequestClicked:`方法（位於`BDLWebDemo/iOS/Example/ViewController.m`檔案）中的邏輯替換為自訂的跳轉邏輯。

   ```objectivec
   - (void)webViewController:(BDLWebViewController *)controller onURLRequestClicked:(NSURLRequest *)urlRequest {
       NSLog(@"debug %s request %@ url %@", __func__, urlRequest, urlRequest.URL);
       BDLCommonWebViewController *vc = [[BDLCommonWebViewController alloc] init];
       [vc.webView loadRequest:urlRequest];
       [self.navigationController pushViewController:vc animated:YES];
   }
   ```
   


</Tab>
<Tab zoneid="er87rLFMfI" title="Android">
<TabTitle>Android</TabTitle>

* 修改 PiP 視窗的寬度與高度

   在`sdk/pip`目錄下`FloatView`類別的`updateTargetParams`方法中，修改`mTargetWidth`（寬度）與`mTargetHeight`（高度）的值。單位：px。

   ```Java
   public void updateTargetParams() {
   
       // requestWidthHeightRatio is the aspect ratio of the video.
       if (requestWidthHeightRatio > 0) {
           if (requestWidthHeightRatio > 1) {
               // Landscape video, width is greater than height.
               mTargetWidth = SizeUtils.dp2px(180);
               mTargetHeight = mTargetWidth / requestWidthHeightRatio;
           } else {
               // Portrait video, width is less than height.
               mTargetWidth = SizeUtils.dp2px(102);
               mTargetHeight = mTargetWidth / requestWidthHeightRatio;
           }
       } else {
           mTargetWidth = SizeUtils.dp2px(180);
           mTargetHeight = SizeUtils.dp2px(102);
       }
       
       //...
   }
   ```
   

* 在 PiP 視窗中新增控制 UI 或自訂控制 UI 的顯示樣式

   在`sdk/pip`目錄下`FloatView`類別的`addChildView`方法中，新增控制 UI 或自訂 PiP 視窗控制 UI 的顯示樣式，例如自訂關閉圖示的顯示樣式。

   以下範例程式碼會在 PiP 視窗中新增自訂的 TextView。

   ```TypeScript
   // Add a custom TextView.
   TextView textView = new TextView(mContext);
   textView.setText("Custom Text");
   mChildCard.addView(textView,new LayoutParams(SizeUtils.dp2px(30),SizeUtils.dp2px(20)));
   ```
   

* 自訂浮動視窗權限請求對話框

   使用`setPIPConfig`方法啟用系統 PiP 後，觀眾還需開啟裝置的浮動視窗權限才能使用系統 PiP。如需自訂直播間中顯示的浮動視窗權限請求對話框，可在`sdk/api`目錄下`BDLWebViewActivity`類別的`showSystemPIPPermissionDialog`方法中，將`ConfirmDialog`對話框替換為自訂對話框。

   ```Java
   public void showSystemPIPPermissionDialog(boolean isExit) {
       ConfirmDialog.Builder builder = new ConfirmDialog.Builder(this);
       builder.setTitle(getString(R.string.open_float_window_play_tips))
               .setConfirmText(getString(R.string.go_open))
               .setCancelText(getString(R.string.cancel))
               .setConfirmListener(v -> {
                   FloatUtil.requestPermission(this);
               })
               .setCancelListener(v -> {
                   hasShowRequestPIPPermissionDialog = true;
                   if (isExit) {
                       doManualFinish();
                   }
               }).build().show();
   }
   ```
   

* 自訂播放備用圖片

   播放備用圖片是指播放器載入影片首幀時顯示的圖片。

   使用`setDefaultBitmapConfig`方法替換備用圖片後，預設備用圖片為透明圖片。如需將透明圖片替換為自訂備用圖片，可在`sdk/webview`目錄下`BDLWebViewController`類別的`getDefaultVideoPoster`方法中，將回傳的 Bitmap 替換為自訂備用圖片。

   ```Java
   public Bitmap getDefaultVideoPoster() {
       if (WebConfig.getDefaultBitmapConfig(appContext)) {
           // Create a transparent image.
           return Bitmap.createBitmap(1, 1, Bitmap.Config.ARGB_8888);
       }
       return super.getDefaultVideoPoster();
   }
   ```
   

* 自訂跳轉邏輯

   在示範中，當觀眾點擊選單下的商品卡片、浮動商品卡片、頂部廣告、頁內廣告、浮動廣告、主播帳號或留言中的網址時，將使用系統瀏覽器開啟帶有`http`或`https`協定標頭的地址。如需自訂跳轉邏輯，並根據特定場景或需求調整頁面跳轉行為，可將`sdk/webview`目錄下`BDLWebViewController`類別的`shouldOverrideUrlLoading`方法中的邏輯替換為自訂的跳轉邏輯。

   ```Java
   @Override
   public boolean shouldOverrideUrlLoading(WebView view, WebResourceRequest request) {
       Uri requestUri = request.getUrl();
       Log.d(TAG, "shouldOverrideUrlLoading: " + requestUri);
       String scheme = requestUri.getScheme();
       if ("http".equals(scheme) || "https".equals(scheme)) {
           attemptViewUri(appContext, requestUri);
           return true;
       }
       return super.shouldOverrideUrlLoading(view, request);
   }
   ```
   


</Tab>
</Tabs>


<span id="413edda7"></span>
### 深度自訂開發

若[基本自訂設定](https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhi-bo-jian-h5-ye-mian-qian-ru-nin-de-xing-d-zh-TW#7f8f09c3)無法滿足您的需求，您需了解範例功能的具體邏輯，並進行深度自訂開發。

本節介紹範例中核心能力的具體實現，協助您理解其背後的邏輯。


<Tabs>
<Tab zoneid="ybhJkhyyjJ" title="iOS">
<TabTitle>iOS</TabTitle>

<span id="ead8512e"></span>
#### 系統 PiP

在`BDLWebDemo/iOS/BDLWeb/BDLWeb/PiP`目錄中查找關鍵程式碼。`BDLPiPVideoWriter`實現黑畫面影片的生成邏輯，`BDLPiPHelper`負責管理`AVPlayerController`並將 AVPlayerController 加入當前直播間容器（`BDLWebViewController`）。

主要方法如下：


* 在`BDLPiPHelper`中，

   * `setEnablePiPMode`設定是否啟用系統PiP。

   * `updateVideoSize:`更新影片尺寸。切換播放影片時，實際的影片尺寸可能會發生變化。此時，`BDLWebViewController` 會呼叫此方法以更新黑框影片的尺寸。

   * `preparePlayer` 會建立一個 `AV Player Controller`，並將 `AVPlayerController` 加入當前的 直播間容器。

   * `updatePlayerVCParentViewController` 會更新 `AVPlayerController` 的父視圖，以便觀眾從系統 PiP 切回應用時，切換動畫能正常顯示。

   * `playLocalVideoIfNeeded` 會建立並播放本地黑框影片。

   * `playerViewControllerWillStartPictureInPicture:` 會通知 `BDLWebViewController` PiP 即將啟動，並將 WebView 加入 `WindowScene` 以進行系統 PiP。

* 在 `BDLPiPVideoWriter` 中，

   * `videoWithSize:color:completion:` 會嘗試取得對應尺寸的黑框影片。若不存在對應尺寸的黑框影片，則呼叫 `writeVideoWithSize:color:atPath:completion:` 方法來建立黑框影片，並回傳黑框影片路徑。

   * `writeVideoWithSize:color:atPath:completion:` 會根據影片尺寸、顏色及路徑建立黑框影片，並回傳黑框影片路徑。


系統 PiP 視窗的顯示與關閉實現流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0MDVweCIgaGVpZ2h0PSIxMDQ1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSA0MDUgMTA0NSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gNzIgNjIgTCA3MiAxMzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiAxNDAuODggTCA2OC41IDEzMy44OCBMIDcyIDEzNS42MyBMIDc1LjUgMTMzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+Q3JlYXRlIGFuZCBpbml0aWFsaXplwqBCRExQaVBIZWxwZXI8L3NwYW4+PHNwYW4+PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3MiAyMDIgTCA3MiAyNzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MiAyODAuODggTCA2OC41IDI3My44OCBMIDcyIDI3NS42MyBMIDc1LjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTQyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q3JlYXRlIGEgYmxhY2sgZnJhbWUgdmlkZW88L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIgMzQyIEwgNzIgNDE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIgNDIwLjg4IEwgNjguNSA0MTMuODggTCA3MiA0MTUuNjMgTCA3NS41IDQxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9IjI4MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzEycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXkgdGhlIGJsYWNrIGZyYW1lIHZpZGVvPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcyIDQ4MiBMIDcyIDU1NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDU2MC44OCBMIDY4LjUgNTUzLjg4IEwgNzIgNTU1LjYzIEwgNzUuNSA1NTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDcyIDYyMiBMIDcyIDY5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDcwMC44OCBMIDY4LjUgNjkzLjg4IEwgNzIgNjk1LjYzIEwgNzUuNSA2OTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI1NjIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5MnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5FbWJlZCB0aGUgV2ViVmlldyBpbnRvIHRoZSBQaVAgd2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDcyIDc2MiBMIDcyIDgzNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDcyIDg0MC44OCBMIDY4LjUgODMzLjg4IEwgNzIgODM1LjYzIEwgNzUuNSA4MzMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSI3MDIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDczMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAgc3dpdGNoZXMgdG8gdGhlIGZvcmVncm91bmQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIgOTAyIEwgNzIgOTc1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIgOTgwLjg4IEwgNjguNSA5NzMuODggTCA3MiA5NzUuNjMgTCA3NS41IDk3My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjIiIHk9Ijg0MiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODcycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vdGlmeSBCRExXZWJWaWV3Q29udHJvbGxlciB0byBleGl0IFBpUCBtb2RlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI5ODIiIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwMTJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRoZSBXZWJWaWV3IGJhY2sgdG8gQkRMRmxvYXRpbmdQbGF5ZXIgb3IgQkRMV2ViVmlld0NvbnRyb2xsZXLCoDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNTIgNDUyIEwgMjUyIDEwMTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTIgNDUyIEwgMTQ4LjM3IDQ1MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDE0My4xMiA0NTIgTCAxNTAuMTIgNDQ4LjUgTCAxNDguMzcgNDUyIEwgMTUwLjEyIDQ1NS41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjYyIiB5PSI3NTIiIHdpZHRoPSIxNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc2MnB4OyBtYXJnaW4tbGVmdDogMjYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPklmIHRoZSBhcHAgc3dpdGNoZXMgdG8gdGhlIGJhY2tncm91bmQgYWdhaW48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIiIHk9IjQyMiIgd2lkdGg9IjE0MCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDUycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcCBzd2l0Y2hlcyB0byB0aGUgYmFja2dyb3VuZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxNDIgMTAxMiBMIDI1MiAxMDEyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjwvZz48L3N2Zz4=" />

顯示系統 PiP 視窗：


1. 當 WebView 開始播放影片時，`BDLWebViewController` 會建立並初始化 `BDLPiPHelper`。

2. `BDLPiPHelper` 會建立黑框影片，並利用 `AVPlayerController` 以極慢速在螢幕上播放黑框影片，同時將 `AVPlayer` 的視圖透明度設為全透明。這可確保觀眾在觀看影片時不會看到黑框影片。

3. 當應用切換至背景時，`AVPlayerController` 會自動建立一個 `WindowScene` 以進行系統 PiP。

4. `BDLPiPHelper` 會將 WebView 加入系統 PiP 的 `WindowScene`，將 WebView 嵌入 PiP 視窗，從而顯示系統 PiP 視窗。


關閉系統 PiP 視窗：


1. 當應用切回前景時，`BDLPiPHelper` 會重新播放黑框影片，以確保下次應用切換至背景時 PiP 視窗能正常顯示。

2. `BDLPiPHelper` 會通知 `BDLWebViewController` 退出 PiP 模式，並將 WebView 加回 `BDLFloatingPlayer`，將系統 PiP 視窗轉換為應用內 PiP 視窗，或將 WebView 加回 `BDLWebViewController`，返回直播間頁面。


<span id="4115a661"></span>
#### 應用內 PiP

直播間（`BDLWebViewController`）包含 `BDLFloatingPlayer`，而 `BDLFloatingPlayer` 則包含 `BDLFloatingWindow`。

主要方法如下：


* 在 `BDLFloatingPlayer` 中，

   * `updateWebView`：當觀眾退出系統 PiP 模式時，將 `BDLWebView` 加入 `BDLFloatingWindow`。

   * `getNewFloatingWindow`：根據傳入的旋轉方向建立一個 `BDLFloatingWindow` 實例。

   * `setUIOrientation:` 設定 `BDLFloating Player` 的 UI 方向。此方法會呼叫 `getNewFloatingWindow:`，以新的方向重新建立一個 `BDLFloatingWindow` 實例。

   * `showWithFrame:closeButton:` 會顯示 應用內 PiP 視窗。

   * `close` 會關閉 應用內 PiP 視窗。

* 在 `BDLFloatingWindow` 中，

   * `floatingWnd` 會建立 `UIWindow` 的延遲加載方法。

   * `showWithView:closeImage:closeImageSize:initFrame:finalFrame:duration:willAppear:didDisappear:willClose:` 會顯示 應用內 PiP 視窗。

   * `close` 會通知 `BDLWebViewController` 應用內 PiP 模式即將退出，並關閉應用內 PiP 視窗。

   * `onPanGesture:` 實現 應用內 PiP 視窗的拖曳功能。


應用內 PiP 視窗的顯示與關閉實現流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxOTZweCIgaGVpZ2h0PSIxMjM1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxOTYgMTIzNSI+PGRlZnMvPjxnPjxwYXRoIGQ9Ik0gOTggNjIgTCA5OCAxMzUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5OCAxNDAuODggTCA5NC41IDEzMy44OCBMIDk4IDEzNS42MyBMIDEwMS41IDEzMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+T3BlbiBhbm90aGVyIHBhZ2UgaW4gdGhlIGN1cnJlbnQgYXBwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk4IDIwMiBMIDk4IDI3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDI4MC44OCBMIDk0LjUgMjczLjg4IEwgOTggMjc1LjYzIEwgMTAxLjUgMjczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzgiIHk9IjE0MiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTcycHg7IG1hcmdpbi1sZWZ0OiAzOXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DcmVhdGUgQkRMRmxvYXRpbmdQbGF5ZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggMzQyIEwgOTggNDE1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gOTggNDIwLjg4IEwgOTQuNSA0MTMuODggTCA5OCA0MTUuNjMgTCAxMDEuNSA0MTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOCIgeT0iMjgyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMTJweDsgbWFyZ2luLWxlZnQ6IDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNyZWF0ZTxiciAvPkJETEZsb2F0aW5nV2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk4IDQ4MiBMIDk4IDU1NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDU2MC44OCBMIDk0LjUgNTUzLjg4IEwgOTggNTU1LjYzIEwgMTAxLjUgNTUzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzgiIHk9IjQyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNDUycHg7IG1hcmdpbi1sZWZ0OiAzOXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj7CoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPkNyZWF0ZTwvc3Bhbj48ZGl2PjxkaXY+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPsKgVUlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggNjIyIEwgOTggNjYyIEwgOTcuNyA2NjIgTCA5Ny43IDY5NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk3LjcgNzAwLjg4IEwgOTQuMiA2OTMuODggTCA5Ny43IDY5NS42MyBMIDEwMS4yIDY5My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSI1NjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU5MnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+QWRkIHRoZSBVSVdpbmRvdyB0byB0aGUgY3VycmVudCBhcHAncyBrZXlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTcuNyA4MTIgTCA5Ny43IDg0NyBMIDk4IDg0NyBMIDk4IDg3NS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDg4MC44OCBMIDk0LjUgODczLjg4IEwgOTggODc1LjYzIEwgMTAxLjUgODczLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMi4zOCIgeT0iNzAyIiB3aWR0aD0iMTkwLjYyIiBoZWlnaHQ9IjExMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTg5cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzU3cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPldoZW4gdmlld2VycyB0YXAgdGhlIFBpUCB3aW5kb3cncyB2aWRlbyBjb250ZW50IG9yIGNsb3NlIGljb24sIG9yIHdoZW4gYSB3ZWJwYWdlIG5vdGlmaWVzIHRoYXQgdGhlIFBpUCB3aW5kb3cgbmVlZHMgdG8gYmUgY2xvc2VkLCB0aGV5IHJldHVybiB0byB0aGUgbGl2ZSByb29tIHBhZ2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggOTQyIEwgOTggMTAxNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDk4IDEwMjAuODggTCA5NC41IDEwMTMuODggTCA5OCAxMDE1LjYzIEwgMTAxLjUgMTAxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjM4IiB5PSI4ODIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkxMnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmVtb3ZlIHRoZSBVSVdpbmRvdyBmcm9tIHRoZSBrZXlXaW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gOTggMTA4MiBMIDk4IDExNjUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5OCAxMTcwLjg4IEwgOTQuNSAxMTYzLjg4IEwgOTggMTE2NS42MyBMIDEwMS41IDExNjMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzOCIgeT0iMTAyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1MnB4OyBtYXJnaW4tbGVmdDogMzlweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGVzdHJveSBCRExGbG9hdGluZ1dpbmRvdzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzgiIHk9IjExNzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyMDJweDsgbWFyZ2luLWxlZnQ6IDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRlc3Ryb3kgQkRMRmxvYXRpbmdQbGF5ZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />

顯示應用內 PiP 視窗：


1. 當觀眾在當前應用中打開其他頁面（包括返回 demo 首頁）時，`BDLWebViewController` 會建立 `BDLFloatingPlayer`，隨後再建立 `BDLFloatingWindow`。

2. `BDLFloatingWindow` 會建立一個 `UIWindow`，並將 `UIWindow` 加入到當前應用的 `keyWindow`，從而顯示應用內 PiP 視窗。


關閉應用內 PiP 視窗：


1. 當觀眾點擊 PiP 視窗的影片內容或關閉圖示，或當網頁通知需要關閉 PiP 視窗時，會返回直播間頁面。

2. `BDLFloatingWindow` 會從 `keyWindow` 中移除 `UIWindow`。

3. 銷毀 `BDLFloatingWindow`。

4. 銷毀 `BDLFloatingPlayer` 以關閉應用內 PiP 視窗。


在 `BDLWebDemo/iOS/BDLWeb/BDLWeb/FloatingPlayer` 目錄下查找關鍵程式碼。

<span id="b855b04a"></span>
#### 自動播放

請參考 `BDLWebView.m` 檔案，位於 `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` 目錄下。關鍵程式碼如下。

```objectivec
if (BDLSettings.sharedInstance.enableAutoPlay) {
    // If autoplay is enabled, live and VOD videos will play without user action.
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeNone;
}
else {
    // If autoplay is disabled, live and VOD videos require user action to play.
    config.mediaTypesRequiringUserActionForPlayback = WKAudiovisualMediaTypeAll;
}
```


<span id="c0adba21"></span>
#### 全螢幕圖示點擊行為

當觀眾點擊全螢幕圖示進入全螢幕模式時，會呼叫 `webView:didEnterFullScreen:` 方法。

```objectivec
- (void)webView:(nonnull BDLWebView *)webView didEnterFullScreen:(nonnull BDLWebMessageModel *)model {
    BDLSettings *settings = BDLSettings.sharedInstance;
    // If the current screen orientation is portrait and the fullscreen icon tap behavior is set to force rotation to landscape mode, or if the screen rotates based on the video's aspect ratio and the video width is greater than its height.
    if (self.isPortrait
        && (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeForceRotate
            || (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeRotate
                && !self.webView.isPortraitVideo))) {
        // Rotate to landscape mode.
        [UIDevice BDL_switchNewOrientation:UIInterfaceOrientationLandscapeRight];
    }
    [self updateViewFullscreen:YES];
}
```


當觀眾點擊全螢幕圖示退出全螢幕模式時，會呼叫 `webView:didExitFullScreen:` 方法。

```objectivec
- (void)webView:(nonnull BDLWebView *)webView didExitFullScreen:(nonnull BDLWebMessageModel *)model {
     // If the current screen orientation is landscape, rotate to portrait mode.
    if (!self.isPortrait) {
        [UIDevice BDL_switchNewOrientation:UIInterfaceOrientationPortrait];
    }
    [self updateViewFullscreen:NO];
}
```


也可以使用 `supportedInterfaceOrientations` 方法來定義支援的螢幕方向。

```objectivec
- (UIInterfaceOrientationMask)supportedInterfaceOrientations {
    // If the player is not created, the screen orientation only supports portrait.
    if (!self.webView.isPlayerCreated) {
        return UIInterfaceOrientationMaskPortrait;
    }
    BDLSettings *settings = BDLSettings.sharedInstance;
    // If the fullscreen icon tap behavior is set to force rotation to landscape mode, or if the screen rotates based on the video's aspect ratio and the video width is greater than its height, all screen orientations except upside-down are supported.
    if (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeForceRotate
        || (settings.fullscreenBtnType == BDLSettingsFullscreenBtnTypeRotate
            && !self.webView.isPortraitVideo)) {
        return UIInterfaceOrientationMaskAllButUpsideDown;
    }
    //  Otherwise, the screen orientation only supports portrait.
    return UIInterfaceOrientationMaskPortrait;
}
```


更多資訊請參考 `BDLWebViewController.m` 檔案，位於 `BDLWebDemo/iOS/BDLWeb/BDLWeb/WebView` 目錄下。


</Tab>
<Tab zoneid="A3Eb7Bqs6K" title="Android">
<TabTitle>Android</TabTitle>

<span id="bd77eeb4"></span>
#### PiP

主要方法如下：


* 在 `sdk/pip` 目錄下，`PiPManager` 類（負責管理 PiP 視窗的顯示邏輯）包含 `showPiPWebView` 和 `hidePiPWebView` 方法，用於顯示和隱藏 PiP 視窗。此外，PiPManager 類還包含 `handleContentClick` 和 `handleExitClick` 方法，分別處理 PiP 視訊內容和關閉圖示的點擊行為。

* 在 `sdk/pip` 目錄下，`FloatView` 類（負責處理 PiP 視窗與 `WindowManager` 的互動，以及 PiP 視窗的位置和樣式）包含 `initWindow` 和 `addToWindow` 方法。這些方法用於初始化 `WindowManager` 的 `window` 參數，並將小視窗加入 `WindowManager` 的 `window` 階層，從而實現 PiP 效果。

* 在 `sdk/api` 目錄下，`BDLWebViewActivity` 類包含 `onPause`、`onResume` 和 `initWebView` 方法。這些方法分別用於處理直播間頁面（`BDLWebViewActivity`）進入背景、從背景回到前景，以及初始化 WebView 的操作。


**顯示 PiP 視窗**

顯示 PiP 視窗的實現流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxNDM1cHgiIGhlaWdodD0iMTAyNXB4IiB2aWV3Qm94PSItMC41IC0wLjUgMTQzNSAxMDI1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAyODIgMTI3IEwgNDM1LjYzIDEyNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ0MC44OCAxMjcgTCA0MzMuODggMTMwLjUgTCA0MzUuNjMgMTI3IEwgNDMzLjg4IDEyMy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIyIiB5PSI5MiIgd2lkdGg9IjE2MCIgaGVpZ2h0PSI3MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTI3cHg7IG1hcmdpbi1sZWZ0OiAxMjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGlubGluZWNvZGU+QkRMV2ViVmlld0FjdGl2aXR5wqA8L2lubGluZWNvZGU+aXMgYWJvdXQgdG8gZ28gdG8gdGhlIGJhY2tncm91bmQ8ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NTcgMjUyIEwgNTU3IDMyNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU1NyAzMzAuODggTCA1NTMuNSAzMjMuODggTCA1NTcgMzI1LjYzIEwgNTYwLjUgMzIzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA2NjIgMTI3IEwgNzM1LjYzIDEyNyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc0MC44OCAxMjcgTCA3MzMuODggMTMwLjUgTCA3MzUuNjMgMTI3IEwgNzMzLjg4IDEyMy41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA1NTcgMiBMIDY2MiAxMjcgTCA1NTcgMjUyIEwgNDUyIDEyNyBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIwOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiciAvPkRldGVybWluZSB3aGV0aGVyIHRoZSBQaVAgd2luZG93IGNhbiBiZSBkaXNwbGF5ZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijc1MiIgeT0iOTciIHdpZHRoPSIxNDAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEyN3B4OyBtYXJnaW4tbGVmdDogNzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRvIG5vdCBkaXNwbGF5IFBpUCB3aW5kb3c8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjY3NyIgeT0iNzciIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDg3cHg7IG1hcmdpbi1sZWZ0OiA2OTdweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5DYW5ub3QgYmUgZGlzcGxheWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1NzIiIHk9IjI4MiIgd2lkdGg9IjExMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjkycHg7IG1hcmdpbi1sZWZ0OiA1NzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2FuIGJlIGRpc3BsYXllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NjQuNSAzOTIgTCA1NjQuNSA0MjcgTCA1NjQuNiA0MjcgTCA1NjQuNiA0NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NjQuNiA0NjAuODggTCA1NjEuMSA0NTMuODggTCA1NjQuNiA0NTUuNjMgTCA1NjguMSA0NTMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0NTkuNSIgeT0iMzMyIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjJweDsgbWFyZ2luLWxlZnQ6IDQ2MXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DYWxsIHRoZcKgPHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+UElQTWFuYWdlci5zaG93UGlQV2ViVmlldygpIG1ldGhvZDwvc3Bhbj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA1NjQuNiA2MjIgTCA1NjQuNiA2NDIgTCA1NjQuNSA2NDIgTCA1NjQuNSA2NTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NjQuNSA2NjAuODggTCA1NjEgNjUzLjg4IEwgNTY0LjUgNjU1LjYzIEwgNTY4IDY1My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQzNC42NSIgeT0iNDYyIiB3aWR0aD0iMjU5LjY5IiBoZWlnaHQ9IjE2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjU4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNTQycHg7IG1hcmdpbi1sZWZ0OiA0MzZweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PjEuQ3JlYXRlIEZsb2F0Vmlld8KgwqA8L2Rpdj48ZGl2PkZsb2F0VmlldyBmbG9hdFZpZXcgPSBmbG9hdFZpZXdXZWFrUmVmZXJlbmNlLmdldCgpOzwvZGl2PjxkaXY+PGJyIC8+PC9kaXY+PGRpdj4yLiBBZGQgV2ViVmlldyB0byBGbG9hdFZpZXc8L2Rpdj48ZGl2PmZsb2F0Vmlldy5hZGRDaGlsZFZpZXcoYmRsV2ViVmlldyk7PC9kaXY+PGRpdj48YnIgLz48L2Rpdj48ZGl2PjMuIENhbGwgdGhlIGFkZFRvV2luZG93IG1ldGhvZCB0byBhZGQgRmxvYXRWaWV3IHRvIHRoZSB3aW5kb3cgaGllcmFyY2h5PC9kaXY+PGRpdj48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5mbG9hdFZpZXcuYWRkVG9XaW5kb3c8L3NwYW4+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+KCk7PC9zcGFuPjwvZGl2PjxkaXY+PC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDQ2NyA3NzcgTCAzOTMuMzcgNzc3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzg4LjEyIDc3NyBMIDM5NS4xMiA3NzMuNSBMIDM5My4zNyA3NzcgTCAzOTUuMTIgNzgwLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2MiA3NzcgTCA3MzUuNjMgNzc3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzQwLjg4IDc3NyBMIDczMy44OCA3ODAuNSBMIDczNS42MyA3NzcgTCA3MzMuODggNzczLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDU2NC41IDY2MiBMIDY2MiA3NzcgTCA1NjQuNSA4OTIgTCA0NjcgNzc3IFoiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTkzcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzc3cHg7IG1hcmdpbi1sZWZ0OiA0NjhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RGV0ZXJtaW5lIHdoZXRoZXIgc3lzdGVtIFBpUCBpcyBlbmFibGVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDExMTIgNzg0LjUgTCAxMjA1LjYzIDc4NC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTIxMC44OCA3ODQuNSBMIDEyMDMuODggNzg4IEwgMTIwNS42MyA3ODQuNSBMIDEyMDMuODggNzgxIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNzQyIiB5PSI3NDciIHdpZHRoPSIzNzAiIGhlaWdodD0iNzUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc4NXB4OyBtYXJnaW4tbGVmdDogNzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlNldCB0aGUgdmFsdWUgb2bCoDxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPm1QYXJhbXMudHlwZSB0byBXaW5kb3dNYW5hZ2VyLkxheW91dFBhcmFtcy5UWVBFX0FQUExJQ0FUSU9OX1BBTkVMPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTIxMiIgeT0iNzU3IiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjU1IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3ODVweDsgbWFyZ2luLWxlZnQ6IDEyMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5SZWdpc3RlcsKgPGlubGluZWNvZGU+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+QWN0aXZpdHlMaWZlY3ljbGVDYWxsYmFjazwvc3Bhbj48L2lubGluZWNvZGU+PC9kaXY+PGRpdj48aW5saW5lY29kZT50byBoaWRlIG9yIHJlc3RvcmUgdGhlIFBpUCB3aW5kb3c8L2lubGluZWNvZGU+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NjIiIHk9IjczNyIgd2lkdGg9IjcwIiBoZWlnaHQ9IjI1IiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc1MHB4OyBtYXJnaW4tbGVmdDogNjYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkluLUFwcCBQaVAgZW5hYmxlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDAyIiB5PSI3NDIiIHdpZHRoPSI1MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NTJweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TeXN0ZW0gUGlQIGVuYWJsZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iNzIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwN3B4OyBtYXJnaW4tbGVmdDogMjkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbGwgdGhlwqA8c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5vblBhdXNlwqA8L3NwYW4+bWV0aG9kPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyIiB5PSI3NDciIHdpZHRoPSIzODAiIGhlaWdodD0iNjUiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDc4MHB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TZXQgdGhlIHZhbHVlIG9mwqA8c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5tUGFyYW1zLnR5cGUgdG88L3NwYW4+PGRpdj7CoFdpbmRvd01hbmFnZXIuTGF5b3V0UGFyYW1zLlRZUEVfQVBQTElDQVRJT05fT1ZFUkxBWTwvZGl2PjxkaXY+KFRoZSB2YWx1ZXMgb2YgbVBhcmFtcy50eXBlIHZhcnkgYmFzZWQgb24gZGlmZmVyZW50IEFuZHJvaWQgdmVyc2lvbnMuIEhlcmUsIHRha2UgQW5kcm9pZCA4LjAgYW5kIGFib3ZlIGFzIGFuIGV4YW1wbGUpPC9kaXY+PGRpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQzOC4yNSIgeT0iOTUyIiB3aWR0aD0iMjUyLjUiIGhlaWdodD0iNzAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDI1MXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDk4N3B4OyBtYXJnaW4tbGVmdDogNDM5cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbGwgdGhlIHN5c3RlbSBBUEkgdG8gYWRkIEZsb2F0VmlldyB0byB0aGUgc3lzdGVtIHdpbmRvdyBoaWVyYXJjaHk8YnIgLz48c3BhbiBzdHlsZT0iYmFja2dyb3VuZC1jb2xvcjppbml0aWFsIj5XaW5kb3dNYW5hZ2VyLmFkZFZpZXcoZmxvYXR2aWV3LCBtUGFyYW1zKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTkyIDk5MiBMIDE5MS42MiA4MTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxOTIgOTg4IEwgNDMxLjg4IDk4OC4yNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQzNy4xMyA5ODguMjUgTCA0MzAuMTMgOTkxLjc0IEwgNDMxLjg4IDk4OC4yNCBMIDQzMC4xNCA5ODQuNzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDEzMjIgOTgyIEwgMTMyMiA4MTIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMzIyIDk4MiBMIDY5Ny4xMiA5ODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2OTEuODcgOTgyIEwgNjk4Ljg3IDk3OC41IEwgNjk3LjEyIDk4MiBMIDY5OC44NyA5ODUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjwvZz48L3N2Zz4=" />


1. 當直播間頁面（`BDLWebViewActivity`）即將進入背景時，系統會呼叫 `onPause` 方法。

2. 使用 `webViewController.canShowPIP()` 和 `WebConfig.getPIPConfig()` 方法判斷是否可以顯示 PiP 視窗。

   ```Java
   @Override
   protected void onPause() {
       super.onPause();
       if (webViewController == null) {
           return;
       }
       // 離開全螢幕模式。
       webViewController.hideCustomView();
       // 取得應用程式目前的 PiP 設定。
       int pipConfig = WebConfig.getPIPConfig(this);
       Intent intent = getIntent();
       intent.putExtra(INTENT_URL, url);
       // 判斷 PiP 視窗是否可以顯示。
       if (!disablePIP && webViewController.canShowPIP()) {
           switch (pipConfig) {
               case WebConfig.VALUE_PIP_DISABLE:
                   // PiP 已停用，因此不執行任何操作。
                   break;
               case WebConfig.VALUE_PIP_APPLICATION: // 啟用應用內 PiP。
               case WebConfig.VALUE_PIP_SYSTEM: // 啟用系統 PiP。
                   // 顯示 PiP 視窗。
                   PiPManager.showPiPWebView(this, intent, webViewController);
                   break;
           }
       }
   }
   ```
   

3. 判斷 PiP 視窗 可以顯示後，呼叫 `PIPManager.showPiPWebView()` 方法，並在 `PIPManager.showPiPWebView()` 方法中實現以下邏輯：

   1. 建立 `FloatView`。

   2. 將 WebView 加入 `FloatView`。

   3. 呼叫 `addToWindow` 方法，將 `FloatView` 加入視窗階層。

   ```Java
   public static boolean showPiPWebView(Activity activity, Intent intent, BDLWebViewController controller) {
       if (WebConfig.getPIPConfig(activity) == WebConfig.VALUE_PIP_SYSTEM && !FloatUtil.checkPermission(activity)) {
           return false;
       }
       webViewController = controller;
       appContext = activity.getApplicationContext();
       bindActivity = new WeakReference<>(activity);
       backIntentReference = new WeakReference<>(intent);
       BDLWebView bdlWebView = webViewController.getBdlWebView();
       ViewUtil.removeViewParent(bdlWebView);
       floatViewWeakReference = new WeakReference<>(new FloatView(activity.getApplicationContext()));
       // Create FloatView.
       FloatView floatView = floatViewWeakReference.get();
       // Add WebView to FloatView.
       floatView.addChildView(bdlWebView);
       // Call the addToWindow method to add FloatView to the window hierarchy.
       floatView.addToWindow(webViewController.getVideoAspectRatio(), activity);
       floatView.setContentClickListener(v -> {
           handleContentClick();
       });
       floatView.setExitClickListener(v -> {
           handleExitClick();
       });
       webViewController.notifyJoinPIP();
       return true;
   }
   ```
   

4. 呼叫 `initWindow` 和 `addToWindow` 方法，分別為系統 PiP 和應用內 PiP 設定 `mParams.type`，並將 `FloatView` 加入系統 `window` 階層。

   若啟用應用內 PiP，則註冊 `ActivityLifecycleCallback`，以便在直播間頁面進入背景或回到前景時隱藏或還原 PiP 視窗。

   ```Java
   private void initWindow() {
       mWindowManager = getWindowManager(mContext);
       mParams = new WindowManager.LayoutParams();
        // Determine whether in-app PiP is enabled.
       if (WebConfig.getPIPConfig(mContext) == WebConfig.VALUE_PIP_APPLICATION) {
           mParams.type = WindowManager.LayoutParams.TYPE_APPLICATION_PANEL; 
       } else {
           // Set different mParams.type values for system PiP based on different Android versions.
           if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            // Android 8.0 and above.
               mParams.type = WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY; 
           } else if (Build.VERSION.SDK_INT > Build.VERSION_CODES.N) {
            // Android 7.0 and above.
               mParams.type = WindowManager.LayoutParams.TYPE_PHONE;
           } else {
           // Other versions.
               mParams.type = WindowManager.LayoutParams.TYPE_TOAST;
           }
       }
   
       mParams.flags = WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE;
   
       // Set the initial position of the PiP window.
       mParams.gravity = Gravity.TOP | Gravity.START;
   }
   
   
   public boolean addToWindow(float requestWidthHeightRatio, Activity activity) {
       this.requestWidthHeightRatio = requestWidthHeightRatio;
       adjustSize();
       if (mWindowManager != null) {
           if (!isAttachedToWindow()) {
               if (WebConfig.getPIPConfig(mContext) == WebConfig.VALUE_PIP_APPLICATION && activity != null) {
                   application = activity.getApplication();
                   mParams.token = activity.getWindow().getDecorView().getWindowToken();
                   // If in-app PiP is enabled, register ActivityLifecycleCallback to hide or restore the PiP window when the live room page goes to the background or foreground.
                   application.registerActivityLifecycleCallbacks(callback);
               } else {
               // Call the system API to add FloatView to the system window hierarchy.
                   mWindowManager.addView(this, mParams);
               }
               mHasAddWindow = true;
               return true;
           } else {
               return false;
           }
       } else {
           return false;
       }
   }
   ```
   


**點擊 PiP 視窗**

PiP 視窗的影片內容或關閉圖示點擊實現流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0NzBweCIgaGVpZ2h0PSI2MDVweCIgdmlld0JveD0iLTAuNSAtMC41IDQ3MCA2MDUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDE3NyAzMiBMIDM0MC42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM0NS44OCAzMiBMIDMzOC44OCAzNS41IEwgMzQwLjYzIDMyIEwgMzM4Ljg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDExNi43MSAxMiBMIDExNi43MSAyMDUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMTYuNzEgMjEwLjg4IEwgMTEzLjIxIDIwMy44OCBMIDExNi43MSAyMDUuNjMgTCAxMjAuMjEgMjAzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNTciIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA1OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjwvZGl2PjxzcGFuIHN0eWxlPSJiYWNrZ3JvdW5kLWNvbG9yOmluaXRpYWwiPkRpc3BsYXlpbmcgRmxvYXRWaWV3PC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzQ3IiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogMzQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+UmVkaXJlY3Qgdmlld2VycyB0b8KgPC9kaXY+PGRpdj48aW5saW5lY29kZT5CRExXZWJWaWV3QWN0aXZpdHk8L2lubGluZWNvZGU+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxNjciIHk9IjIiIHdpZHRoPSIyMDAiIGhlaWdodD0iMTAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDdweDsgbWFyZ2luLWxlZnQ6IDE2OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PlRhcCB0aGUgdmlkZW8gY29udGVudMKgPC9kaXY+PGRpdj5vZiB0aGUgUGlQIHdpbmRvdzwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMTcgNDUyIEwgMTE3IDUyNS42MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExNyA1MzAuODggTCAxMTMuNSA1MjMuODggTCAxMTcgNTI1LjYzIEwgMTIwLjUgNTIzLjg4IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyMzIgMzMyIEwgMzA1LjYzIDMzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMxMC44OCAzMzIgTCAzMDMuODggMzM1LjUgTCAzMDUuNjMgMzMyIEwgMzAzLjg4IDMyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxMTcgMjEyIEwgMjMyIDMzMiBMIDExNyA0NTIgTCAyIDMzMiBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5DaGVjayB3aGV0aGVyIHRoZSBib3VuZCBBY3Rpdml0eSAoQkRMV2ViVmlld0FjdGl2aXR5KSBpcyBzdGlsbCBhbGl2ZTxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMDciIHk9IjEyMiIgd2lkdGg9IjE4MCIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTM3cHg7IG1hcmdpbi1sZWZ0OiAxMDhweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGFwIHRoZSBjbG9zZSBpY29uIG9mIHRoZSBQaVAgd2luZG93PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NyIgeT0iNTMyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjcwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NjdweDsgbWFyZ2luLWxlZnQ6IDQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+SGlkZSBGbG9hdFZpZXcgYW5kIHBhdXNlIFdlYlZpZXcgcGxheWJhY2s8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMxNyIgeT0iMzAyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzJweDsgbWFyZ2luLWxlZnQ6IDMxOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PkhpZGUgRmxvYXRWaWV3IGFuZCBkZXN0cm95IHRoZSBXZWJWaWV3PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNDciIHk9IjMwMiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMxMnB4OyBtYXJnaW4tbGVmdDogMjQ4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRlc3Ryb3llZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTI3IiB5PSI0ODIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0OTJweDsgbWFyZ2luLWxlZnQ6IDEyOHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BbGl2ZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

當 `FloatView` 顯示時，觀眾點擊 PiP 視窗的影片內容，將跳轉至直播間頁面（`BDLWebViewActivity`）。當觀眾點擊 PiP 視窗的關閉圖示時，系統會檢查綁定的 Activity（`BDLWebViewActivity`）是否仍然存活。


* `BDLWebViewActivity` 仍然存活：隱藏 `FloatView` 並暫停 WebView 播放。

* `BDLWebViewActivity` 已被銷毀：隱藏 `FloatView` 並銷毀 WebView。


範例程式碼如下。

```Java
// Handle the tap behavior of the PiP window's video content.
private static void handleContentClick() {
    // If the PiP window is not currently displayed, do nothing.
    if (!isInPIP()) {
        return;
    }
    if (backIntentReference == null || backIntentReference.get() == null) {
        return;
    }
    FloatUtil.setTopApp(appContext);
    Intent intent = backIntentReference.get();
    intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
    appContext.startActivity(intent);
}
// Handle the tap behavior of the PiP window's close icon.
private static void handleExitClick() {
    if (isBindActivityAlive()) {
        // If the bound Activity (BDLWebViewActivity) is still alive, hide FloatView and pause WebView playback.
        hidePiPWebView();
        if (webViewController != null) {
            webViewController.pauseWebView();
        }
    } else {
        // If the bound Activity (BDLWebViewActivity) has been destroyed, hide FloatView and destroy the WebView.
        hideAndDestroyPiPWebView();
    }
}
```


**直播間頁面重新顯示後繼續播放影片**

透過重用 PiP WebView，當直播間頁面再次顯示時，可在 PiP 視窗中繼續播放直播或點播影片。

實現流程如下。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3NzVweCIgaGVpZ2h0PSI1ODhweCIgdmlld0JveD0iLTAuNSAtMC41IDc3NSA1ODgiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEzMiAxMDUgTCAyOTUuNjMgMTA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzAwLjg4IDEwNSBMIDI5My44OCAxMDguNSBMIDI5NS42MyAxMDUgTCAyOTMuODggMTAxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxMiIgeT0iNzUiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj5XaGVuIHRoZSBsaXZlIHJvb20gcGFnZSBuZWVkcyB0byBiZSByZWRpc3BsYXllZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTUyIiB5PSI3NSIgd2lkdGg9IjEzMCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTI4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODVweDsgbWFyZ2luLWxlZnQ6IDE1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PkNhbGwgdGhlwqA8aW5saW5lY29kZT5vblJlc3VtZTwvaW5saW5lY29kZT7CoG1ldGhvZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzODcgMjA3LjUgTCAzODcgMjYzLjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzg3IDI2OC44OCBMIDM4My41IDI2MS44OCBMIDM4NyAyNjMuNjMgTCAzOTAuNSAyNjEuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MiAxMDUgTCA1NDUuNjMgMTA1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTUwLjg4IDEwNSBMIDU0My44OCAxMDguNSBMIDU0NS42MyAxMDUgTCA1NDMuODggMTAxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDM4NyAyLjUgTCA0NzIgMTA1IEwgMzg3IDIwNy41IEwgMzAyIDEwNSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE2OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwNXB4OyBtYXJnaW4tbGVmdDogMzAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldGVybWluZSB3aGV0aGVyIHRoZSA8YnIgLz5saXZlIHJvb20gcGFnZSBuZWVkcyB0byBwb3B1bGF0ZSB0aGUgV2ViVmlldzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTUyIiB5PSI3NSIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTA1cHg7IG1hcmdpbi1sZWZ0OiA1NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+RG8gbm90IHBvcHVsYXRlIHRoZSBXZWJWaWV3PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0ODIiIHk9Ijc1IiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODVweDsgbWFyZ2luLWxlZnQ6IDQ4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5ObyBuZWVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0MDIiIHk9IjIxNSIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyNXB4OyBtYXJnaW4tbGVmdDogNDAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5lZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDc3IDM3NSBMIDU1MC42MyAzNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1NTUuODggMzc1IEwgNTQ4Ljg4IDM3OC41IEwgNTUwLjYzIDM3NSBMIDU0OC44OCAzNzEuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjk3IDM3NSBMIDIyMy4zNyAzNzUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyMTguMTIgMzc1IEwgMjI1LjEyIDM3MS41IEwgMjIzLjM3IDM3NSBMIDIyNS4xMiAzNzguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzg3IDI3NSBMIDQ3NyAzNzUgTCAzODcgNDc1IEwgMjk3IDM3NSBaIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDE3OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM3NXB4OyBtYXJnaW4tbGVmdDogMjk4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldGVybWluZSB3aGV0aGVyIHRoZSBQSVBNYW5hZ2VyJ3Mgd2ViVmlld0NvbnRyb2xsZXIgY2FuIGJlIHJldXNlZDxkaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0OTIiIHk9IjMzNSIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDM0NXB4OyBtYXJnaW4tbGVmdDogNDkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNhbm5vdCBiZSByZXVzZWQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjIzMiIgeT0iMzQ1IiB3aWR0aD0iNTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzU1cHg7IG1hcmdpbi1sZWZ0OiAyMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Q2FuIGJlIHJldXNlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTYyIiB5PSIzMTUiIHdpZHRoPSIyMTAiIGhlaWdodD0iMTAwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNjVweDsgbWFyZ2luLWxlZnQ6IDU2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjEuIE5vdGlmeSBQSVBNYW5hZ2VyIHRvIGhpZGUgdGhlIEZsb2F0VmlldyBhbmQgZGVzdHJveSB0aGUgYm91bmQgV2ViVmlldzwvZGl2PjxkaXY+PHNwYW4gc3R5bGU9ImJhY2tncm91bmQtY29sb3I6aW5pdGlhbCI+Mi7CoDwvc3Bhbj48L2Rpdj5DcmVhdGUgYSBuZXcgV2Vidmlld0NvbnRyb2xsZXI8YnIgLz48ZGl2PjxpbmxpbmVjb2RlPjMuIExvYWQgdGhlIHZpZXdpbmcgcGFnZSBhZGRyZXNzPC9pbmxpbmVjb2RlPjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMiIgeT0iMzIwIiB3aWR0aD0iMjEwIiBoZWlnaHQ9IjExMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMjA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzc1cHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxkaXY+MS7CoDwvZGl2PlJldXNlIHRoZSB3ZWJWaWV3Q29udHJvbGxlciBvZiBQSVBNYW5hZ2VywqA8ZGl2PjIuwqA8L2Rpdj5Ob3RpZnkgUElQTWFuYWdlciB0byBoaWRlIHRoZSBGbG9hdFZpZXc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI5MiIgeT0iNTI1IiB3aWR0aD0iMTkwIiBoZWlnaHQ9IjYwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NTVweDsgbWFyZ2luLWxlZnQ6IDI5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BZGQgdGhlIFdlYlZpZXcgaW4gd2ViVmlld0NvbnRyb2xsZXIgdG8gdGhlIHdlYlZpZXdDb250YWluZXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTEyIDU1NSBMIDEwNyA0MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzIgNTU1IEwgNjcyIDQxNSIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExMiA1NTUgTCAyODUuNjMgNTU1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjkwLjg4IDU1NSBMIDI4My44OCA1NTguNSBMIDI4NS42MyA1NTUgTCAyODMuODggNTUxLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY3MiA1NTUgTCA0ODguMzcgNTU1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDgzLjEyIDU1NSBMIDQ5MC4xMiA1NTEuNSBMIDQ4OC4zNyA1NTUgTCA0OTAuMTIgNTU4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48L2c+PC9zdmc+" />


1. 當需要重新顯示直播間頁面（`BDLWebViewActivity`），例如觀眾點擊 PiP 視窗的影片內容時，系統會呼叫 `onResume` 方法。

2. 判斷直播間頁面是否需要填充 WebView。

   * 需要填充：`webViewController` 為 null，或 `webViewController` 的父容器不是 `webViewContainer`。此時呼叫 `initWebView` 方法初始化 WebView。

   * 無需填充：`webViewController` 不為 null，且 `webViewController` 的父容器為 `webViewContainer`。

3. 呼叫 `initWebView` 方法初始化 WebView 時，判斷 `PIPManager` 的 `webViewController` 是否可重用。

   * 可重用：當 `PIPManager` 中存在可用影片，且 PiP 視窗的觀看頁面地址與直播間頁面（`BDLWebViewActivity`）相同時，重用 `PIPManager` 的 `webViewController`，並通知 `PIPManager` 隱藏 `FloatView`，從而在直播間頁面在 PiP 視窗中繼續播放直播或點播影片。

   * 不可重用：當 `PIPManager` 中不存在可用影片，或 PiP 視窗的觀看頁面地址與直播間頁面（`BDLWebViewActivity`）不同時，執行以下邏輯：

      1. 通知 `PIPManager` 隱藏 `FloatView` 並銷毀綁定的 WebView。

      2. 新增 `WebviewController`。

      3. 載入觀看頁面地址。

4. 將 `webViewController` 中的 WebView 加入 `webViewContainer`，確保 WebView 顯示於直播間頁面。


範例程式碼如下。

```Java
protected void onResume() {
    super.onResume();
    // When webViewController is null or the parent container of webViewController is not webViewContainer, call the initWebView method to initialize the WebView.
    if (webViewController == null || webViewController.getBdlWebView().getParent() != webViewContainer) {
        initWebView();
    }
}

private void initWebView() {
    BDLWebViewController pipWebController = PiPManager.getWebViewController();
    String pipUrl = null;
    if (pipWebController != null) {
        pipUrl = pipWebController.getUrl();
    }

    if (pipWebController != null
            && Objects.equals(url, pipUrl)) {
        // If a usable video exists in PIPManager, and the viewing page address of the PiP window is the same as that of the live room page, directly reuse the webViewController of PIPManager and notify PIPManager to hide the FloatView.
        webViewController = pipWebController;
        PiPManager.hidePiPWebView();
        webViewController.notifyLeavePIP();
    } else {
        // Notify PIPManager to hide the FloatView and destroy the bound WebView.
        PiPManager.hideAndDestroyPiPWebView();
        // Create a new WebviewController.
        webViewController = new BDLWebViewController(this, url);
        // Load the viewing page address.
        webViewController.getBdlWebView().loadUrl(url);
    }

    webViewController.setJsEventConsumer(jsEventConsumer);
    // Add the WebView in webViewController to the webViewContainer.
    webViewContainer.addView(webViewController.getBdlWebView(), new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
}
```


<span id="92df55d2"></span>
#### 自動播放

請參考 `BDLWebViewController` 類，位於 `sdk/webview` 目錄下。關鍵程式碼如下。

```Java
if (WebConfig.getAutoPlayConfig(appContext)) {
    // 取消影片播放需用戶手勢的限制後，直播或 VOD 影片可自動播放，無需觀眾手勢。
    webSetting.setMediaPlaybackRequiresUserGesture(false);
}
```


<span id="ce7c3d49"></span>
#### 背景播放

若觀眾將當前應用切換至背景時，無需啟用系統 PiP，也能在背景繼續播放直播或點播影片，請參考 `dispatchWindowVisibilityChanged` 方法，位於 `BDLWebView` 類的 `sdk/webview` 目錄下。關鍵程式碼如下。

```Java
public void dispatchWindowVisibilityChanged(int visibility) {
  // 為了讓直播或 VOD 影片在應用切換至背景時繼續播放，強制將可見狀態設為 View.VISIBLE（視窗可見）。
  if (keepMediaPlayWhenPause) {
    visibility = View.VISIBLE;
  }
  // 呼叫父類別的 dispatchWindowVisibilityChanged 方法，傳入處理後的可見狀態。
  super.dispatchWindowVisibilityChanged(visibility);
}
```


<span id="079d5ab7"></span>
#### 全螢幕圖示點擊行為

觀眾點擊全螢幕圖示後，網頁可透過 Android WebView 提供的 `onShowCustomView` 與 `onHideCustomView` 方法進入及退出全螢幕模式。請參考 `onShowCustomView` 與 `onHideCustomView` 方法，位於 `BDLWebViewController` 類的 `sdk/webview` 目錄下，以進入及退出全螢幕模式。

```Java
@Override
public void onShowCustomView(View view, CustomViewCallback callback) {
    super.onShowCustomView(view, callback);
    // Enter fullscreen mode.
    showCustomView(view, callback);
}

@Override
public void onHideCustomView() {
    super.onHideCustomView();
    // Exit fullscreen mode.
    hideCustomView();
}
```


配置全螢幕圖示點擊行為，即設定觀眾點擊全螢幕圖示進入全螢幕模式後螢幕是否旋轉。關鍵程式碼如下。

```Java
boolean needRotateScreen = false;
// Based on the configuration of the fullscreen icon tap behavior, determine whether the screen needs to rotate after viewers enter fullscreen mode.
int fullscreenActionConfig = WebConfig.getFullscreenActionConfig(appContext);
switch (fullscreenActionConfig) {
    case WebConfig.VALUE_FULLSCREEN_ACTION_AUTO:
        // Determine whether the screen needs to rotate based on the aspect ratio of the video.
        float videoAspectRatio = getVideoAspectRatio();
        if (videoAspectRatio > 1) {
            // Landscape video (width greater than height) rotates to landscape mode after viewers enter fullscreen mode.
            needRotateScreen = true;
        }
        break;
    case WebConfig.VALUE_FULLSCREEN_ACTION_KEEP_SCREEN_ORIENTATION:
        // Do not rotate the screen.
        break;
    case WebConfig.VALUE_FULLSCREEN_ACTION_ROTATE_SCREEN:
    default:
        // Rotate to landscape mode.
        needRotateScreen = true;
}

FrameLayout decorView = (FrameLayout) viewAttachActivity.getWindow().getDecorView();
FrameLayout contentLayout = viewAttachActivity.findViewById(R.id.main);
if (contentLayout == null) {
    return;
}
ViewUtil.removeViewParent(view);
if (needRotateScreen) {
    // If the screen needs to rotate to landscape mode, add the view to decorView.
    decorView.addView(view, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
} else {
    // If the screen does not need to rotate to landscape mode, add the view to contentLayout.
    contentLayout.addView(view, new FrameLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
}
// If the screen needs to rotate to landscape mode, set the screen orientation to landscape.
if (needRotateScreen) {
    viewAttachActivity.setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE);
}
```



</Tab>
</Tabs>


<span id="773a72d8"></span>
## 常見問題

<span id="226c57e2"></span>
### Web 與您的行動 Native 應用程式如何互相溝通？

BytePlus Live Web 與您的行動 Native 應用程式（以下簡稱 Native）具備一套溝通機制。Web 與 Native 會互相傳送訊息，以實現本主題介紹的功能。若需在您的網頁（包含以 iframe 嵌入 WebView 的自有網頁）與 Native 之間溝通以實現相關功能，您需了解 Web 與 Native 的溝通機制，並自行在您的網頁上實現 Web 事件的接收與傳送。

<span id="4149446a"></span>
#### `JsBridge` 互動流程

`JSBridge` 是 Native 與 Web 之間的橋樑，作為雙向溝通的媒介。

BytePlus Live 會將全域變數 `window.ByteLiveJsBridge` 注入至 `window`，包含以下 API：


* `nativeCallBack`：Native 呼叫 `window.ByteLiveJsBridge.nativeCallBack`，向 Web 傳送訊息。

* `invokeNative`：Web 呼叫此 API，向 Native 傳送訊息。


**Native 所監聽的 Web 事件**

```TypeScript
const data = {
  eventKey:11000, // The event triggered when the player is created.
  info: {
     isPortrait: true, // Portrait mode.
     isLive: true, // In Live status.
};

// Send a message to the Native.
function sendMessage(){
    if(isIos){
    // Use window.webkit.messageHandlers.invokeNative.postMessage to send messages on iOS platform.
        window.webkit.messageHandlers.invokeNative.postMessage(data);
    }else{
    // Use window.ByteLiveJsBridge.invokeNative to send messages on other platforms.
        window.ByteLiveJsBridge.invokeNative(data);
    }
}
```



|事件 |鍵值 |描述 |
|---|---|---|
|INIT_FINISH |10001 |當 `JsBridge` 載入完成時觸發的事件。 |
|CREATE_PLAYER |11000 |當播放器建立時觸發的事件。<br><br>此事件觸發後，Native 可透過 `isLive` 參數獲取直播間是否處於直播狀態，並透過 `isPortrait` 參數獲取直播間是否為直向模式。<br><br><br>* `isLive` 參數的有效值：<br><br>   * `true`：直播狀態。<br><br>   * `false`：非直播狀態。<br><br>* `isPortrait` 參數的有效值：<br><br>   * `true`：直向模式。<br><br>   * `false`：橫向模式。 |
|DESTROY_PLAYER |11001 |當播放器銷毀時觸發的事件。 |
|OPEN_FULLSCREEN |11002 |當觀眾進入全螢幕模式時觸發的事件。 |
|EXIT_FULLSCREEN |11003 |當觀眾退出全螢幕模式時觸發的事件。 |
|LIVE_ROOM_STATE_CHANGE |11004 |當直播間狀態變更時觸發的事件。<br><br>此事件觸發後，Native 可透過 `status` 參數獲取直播間狀態。<br><br>`status` 參數的有效值：<br><br><br>* `1`：直播中。<br><br>* `2`：預覽中。<br><br>* `3`：回放中。<br><br>* `4`：已結束。 |
|PLAYER_STATE_CHANGE |11005 |當播放器狀態變更時觸發的事件。<br><br>此事件觸發後，Native 可透過 `created` 及 `paused` 參數獲取播放器狀態。<br><br><br>* `created` 參數的有效值：<br><br>   * `true`：已建立。<br><br>   * `false`：已銷毀。<br><br>* `paused` 參數的有效值：<br><br>   * `true`：已暫停或已結束。<br><br>   * `false`：播放中。 |
|MEDIA_LOAD_FINISH |11006 |當影片資源載入完成時觸發的事件。<br><br>此事件觸發後，Native 可透過 `videoWidth` 及 `videoHeight` 參數獲取影片實際尺寸，並依據影片比例設定 PiP 視窗的寬高。 |
|CLOSE_MINI_WINDOW |11008 |當觀眾退出 PiP 模式時觸發的事件。當播放器回報錯誤時會觸發此事件。同時，Web 會關閉 PiP 視窗並返回直播間頁面。 |
|OPEN_WAKE_LOCK |11009 |螢幕常亮啟用事件。當觀眾進入直播間時會觸發此事件。 |
|EXIT_WAKE_LOCK |110010 |螢幕常亮關閉事件。當觀眾離開直播間時會觸發此事件。 |


**Native 發送給 Web 的事件**

```TypeScript
// 進入 PiP 模式的事件。
window.ByteLiveJsBridge.nativeCallBack({
  eventKey: 21000   
})
```



|事件 |鍵值 |描述 |
|---|---|---|
|ENTER_MINI_WINDOW |21000 |進入 PiP 模式的事件。 |
|EXIT_MINI_WINDOW |21001 |退出 PiP 模式的事件。 |
|STOP_PLAY |21002 |暫停播放的事件。 |
|START_PLAY |21003 |恢復播放並退出 PiP 模式的事件。 |
|PLAY |21004 |播放直播或點播影片的事件。 |


<span id="0f3adec3"></span>
#### 實現 PiP 與全螢幕功能的通訊流程

以 PiP 與全螢幕功能為例，本節介紹 Web 與 Native 之間的通訊流程。


* PiP

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4274838fc5a4f21bc87c923587184e6~tplv-goo7wpa0wc-image.image) </span>

   1. 觀眾進入觀看頁面後，Native 會偵測到 Web 的 `INIT_FINISH` 事件，表示 `JSBridge` 已完成載入。

   2. 當偵測到 Web 的 `CREATE_PLAYER` 事件時，Native 確認播放器已建立，並得知直播間是否處於 Live 狀態及是否為直式模式。

   3. 當觀眾離開觀看頁面時，Native 需實現進入 PiP 模式，並向 Web 發送 `ENTER_MINI_WINDOW` 事件。

   4. 偵測到 Native 的 `ENTER_MINI_WINDOW` 事件後，Web 會在 PiP 視窗內以全螢幕模式顯示播放器。

   5. Native 需在以下情況下實現退出 PiP 模式，並向 Web 發送 `EXIT_MINI_WINDOW` 事件。偵測到 Native 的 `EXIT_MINI_WINDOW` 事件後，Web 會退出播放器的全螢幕模式並返回觀看頁面。

      * 觀眾可透過點擊 PiP 視窗或其他方式返回觀看頁面。

      * 當直播間狀態變更或觀眾切換直播源時，Native 會偵測到 Web 的 `DESTROY_PLAYER` 事件，表示播放器已被銷毀。

   6. （可選）Native 可根據需求向 Web 發送事件，以播放或暫停直播或 VOD 視頻：

      * 當 WebView 中播放被暫停時，向 Web 發送 `PLAY` 事件。偵測到此事件後，Web 可恢復播放直播或 VOD 視頻。

      * 在 WebView 播放期間，向 Web 發送 `STOP_PLAY` 事件。偵測到此事件後，Web 可暫停直播或 VOD 視頻。

* 全螢幕

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/698764704c154ab6a2b1609e2c4207d1~tplv-goo7wpa0wc-image.image) </span>

   1. 當觀眾進入全螢幕模式時，Native 會偵測到 Web 的 `OPEN_FULLSCREEN` 事件，表示觀眾已進入全螢幕模式，並判斷是否需旋轉為橫式模式。

   2. 當觀眾退出全螢幕模式時，Native 會偵測到 Web 的 `EXIT_FULLSCREEN` 事件，表示觀眾已退出全螢幕模式，並判斷是否需恢復為直式模式。
