---
title: "整合 iOS 版 Viewer SDK"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/zheng-he-ios-ban-viewer-sdk-zh-TW"
---

若要在您的 iOS 應用程式中加入直播功能，例如觀看直播畫面、發送評論及與主播互動，您可以整合 Viewer SDK。本指南提供全面且逐步的操作說明，涵蓋從初始設定、依賴管理，到進入及離開直播間的所有步驟，確保整合流程順暢。

## 先決條件

* 運行 iOS 12.0 及以上版本的實體裝置或模擬器。如果使用 Swift Package Manager 整合 SDK，則需要運行 iOS 13.0 及以上版本的實體裝置或模擬器。

   > **说明**

   * > 若你使用 Apple Silicon Mac，則需要 Rosetta 模擬器。

   * > 該模擬器僅用於介面除錯，並不保證音訊、視訊及子母畫面（PiP）等功能能正常運作。為避免螢幕殘影或黑邊等問題，建議你使用實體裝置。

* Xcode。建議使用最新版本。

* 若您使用 CocoaPods 整合 SDK，建議使用 1.11.0 或以上版本。如需更多資訊，請參閱[CocoaPods 入門指南](https://guides.cocoapods.org/using/getting-started.html#getting-started)。若您使用 Swift Package Manager 整合 SDK，請使用 swift\-tools\-version 5.9 或以上版本。您可以透過`Package.swift` 或 Xcode UI 來整合 SDK。

* CPU 架構：arm64 或 x86_64。

* 請聯絡 BytePlus Live 技術支援，以取得直播授權檔案和隨選視訊（VOD）授權檔案、申請授權時所用的應用程式名稱，以及申請成功後回傳的 app ID。

## 整合步驟

### Step 1: 新增依賴項

您可以選擇使用 CocoaPods（選項 1）或 Swift Package Manager（選項 2）來整合 SDK。

**選項 1：CocoaPods**

1. 打開專案的 `Podfile` 檔案以新增依賴。

   > **说明**

   > 若您的專案尚未使用 CocoaPods，請在專案根目錄執行 `pod init && pod install` 指令，以產生 `Podfile` 檔案。

   ```Ruby
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   
   # 您的 app target 名稱
   target 'XXXX' do
     # 從 1.33.0 版本開始，您可以使用 ViewerWithoutRTC 作為 podspec 以優化 SDK 套件大小。這將提供一個不包含超低延遲直播功能的 SDK 套件。
     pod 'BPLive', '1.66.1'
     ]
   end  
   ```

2. 打開終端機視窗並執行 `cd` 指令以切換至你的專案目錄。執行 `pod install` 指令以安裝依賴。

3. （可選）使用 TTSDK 的靜態庫版本

   預設情況下，TTSDK 使用動態庫版本。若要使用 TTSDK 的靜態庫版本，新增依賴時請在版本號後加上 `-static-ttsdk`。如需更多資訊，請參閱 `Podfile` 檔案中的前述配置。

   ```Ruby
   pod 'BPLive', '1.66.1-static-ttsdk'
   ```

**選項 2：Swift Package Manager**

你可以透過 `Package.swift` 或 Xcode UI 整合 SDK。

**Repository**：

SDK：[https://github.com/byteplus-sdk/BPLive_SPM](https://github.com/byteplus-sdk/BPLive_SPM)

**選項 A：透過 Package.swift 整合**

將 BPLive_SPM 依賴新增至你的 `Package.swift`，並在需要的 target 中匯入對應的庫。以下為 Viewer SDK 的整合範例：

```Swift
// swift-tools-version: 5.9
import PackageDescription

let package = Package(
    name: "MyApp",
    platforms: [.iOS(.v13)],
    products: [
        .library(name: "MyApp", targets: ["MyApp"]),
    ],
    dependencies: [
        // Replace with your target version
        .package(url: "https://github.com/byteplus-sdk/BPLive_SPM.git", exact: "1.66.4")
    ],
    targets: [
        .target(
            name: "MyApp",
            dependencies: [
                // Base library and common component library
                .product(name: "BPLiveBaseLibrary", package: "BPLive_SPM"),
                .product(name: "BPLiveCommonLibrary", package: "BPLive_SPM"),
                // Viewer SDK.您可以將 BPLiveViewerLibrary 替換為 BPLiveViewerWithoutRTCLibrary，以優化 SDK 套件大小。BPLiveViewerWithoutRTCLibrary 不包含超低延遲直播功能。
                .product(name: "BPLiveViewerLibrary", package: "BPLive_SPM")
            ]
        ),
    ]
)
```

**選項 B：在 Xcode 中整合**

1. 打開 Xcode 並選擇 **File** \> **Add Package Dependencies…** 。

2. 輸入倉庫網址 `https://github.com/byteplus-sdk/BPLive_SPM`。

3. 在版本規則中，選擇標記的目標版本（例如 **Exact Version: 1.66.4**）。

4. 在庫清單中，選擇與 Viewer SDK 相關的庫，並將其關聯到對應的 target：

   * **BPLiveBaseLibrary**：基礎庫（必選）

   * **BPLiveCommonLibrary**：通用組件庫（必選）

   * **BPLiveViewerLibrary**：Viewer 庫

   * **BPLiveViewerWithoutRTCLibrary**：不含超低延遲直播功能的 Viewer 庫

### Step 2: 配置環境

請在 Xcode 的 app target 中完成以下步驟：

1. 開啟`info.plist` 檔案，新增參數 `SSAppID`，並將該參數的值設為您授權申請通過後收到的 app ID。

2. 在`info.plist` 檔案中，透過以下任一方式新增權限：

   * 點擊\*\*+\*\*，新增 **Privacy \- Photo Library Additions Usage Description** 及 **Privacy \- Calendars Usage Description** 鍵值。對每個鍵值，將 **Type** 設為 **String**，**Value** 設為您希望在系統授權對話框中顯示的提示訊息。

   * 以原始碼模式開啟`info.plist` 檔案，並新增以下鍵值與字串。您可以自訂字串的值，作為系統授權對話框中顯示的提示訊息。

      ```Plain
      <!-- Write access to photo library -->
      <key>NSPhotoLibraryAddUsageDescription</key> 
      <string>The app needs your permission to write to your photo library for saving images to the photo library</string>
      <!-- Write access to calendar -->
      <key>NSCalendarsUsageDescription</key>
      <string>Used to remind viewers before live stream starts</string>
      ```

3. （選用）若您需要應用程式在背景執行時繼續播放音訊，或需要使用子母畫面（PiP）功能，請完成以下步驟：

   1. 在**Signing & Capabilities** 標籤下點擊  **+ Capability**，並雙擊新增 **Background Modes**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/147f155c322d4f6cba5c2f26c813f33b~tplv-goo7wpa0wc-image.image)

   2. 於**Background Modes** 區段中，勾選 **Audio, AirPlay, and Picture in Picture** 選項。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eefa3e63dd374db686c0b232547c944b~tplv-goo7wpa0wc-image.image)

4. （選用）若您的專案使用 Bitcode，則需停用 Bitcode。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/991f4357e3bb47579b6256340415e73d~tplv-goo7wpa0wc-image.image)

   1. 點擊**Build Settings** 標籤。

   2. 於**Build Options** 區段，將 **Enable Bitcode** 設為 **No**。

5. 配置全螢幕播放直播、預覽或回放時所支援的螢幕方向。

   1. 點擊**General** 標籤。

   2. 於**Deployment Info** 區段，於 **iPhone Orientation** 及 **iPad Orientation** 中勾選 **Portrait** 和 **Landscape Right**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab42c8820c0f4eee99fe655eb65c2ff6~tplv-goo7wpa0wc-image.image)

   > **说明**

   * > 為了讓觀眾能在全螢幕模式下根據裝置方向自動左右旋轉螢幕，必須滿足以下條件：

      * > 觀眾裝置的直向鎖定已關閉。關於如何關閉直向鎖定，請參閱 [官方 Apple 文件](https://support.apple.com/en-us/118226)。

      * > 在 **Deployment Info** 區段中，需勾選 **Landscape Left** 和 **Landscape Right**。

   * > 為避免觀眾點擊全螢幕按鈕時全螢幕動畫出現顯示問題，請務必勾選 **Landscape Right**。

   * > 若要停用全螢幕模式，可透過以下範例程式碼在播放器中隱藏全螢幕按鈕。停用全螢幕模式後，只能在 **Deployment Info** 區段中勾選 **Portrait**。

   > `[BDLLiveEngine sharedInstance].liveRoomConfiguration.playerConfig.common.enterFullScreenEnable = NO;`

### Step 3: 匯入授權檔案

將直播授權檔案與 VOD 授權檔案加入 Xcode 的 app target。選擇 **Copy items if needed**，然後點擊 **Finish**。

### Step 4: 初始化 BPLive

於 Xcode 的 app target 中，開啟 `AppDelegate.m` 檔案以初始化 BPLive：

```objectivec
#import <BPLive/BPLive.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self initBPLive];
    return YES;
}

- (void)initBPLive {
    BDLiveAuthInfo *authInfo = [[BDLiveAuthInfo alloc] init];
    authInfo.bizType = BDLiveBizTypeViewer; // If you integrate both the Live Streaming SDK and Viewer SDK, replace BDLiveBizTypeViewer with BDLiveBizTypeViewer | BDLiveBizTypeLiveStreaming.
    authInfo.appId = @"APP_ID"; // Replace APP_ID with the app ID returned after the successful license application.請聯繫 BytePlus Live 技術支持以取得 app ID。
    authInfo.appName = @"APP_NAME"; // Replace APP_NAME with the app name used to apply for the license.請聯繫 BytePlus Live 技術支持以取得 app 名稱。
    authInfo.channel = @"CHANNEL_NAME"; // Replace CHANNEL_NAME with the name of the channel through which to download the app.預設值為 App Store。
    
    authInfo.vodLicensePath = [[NSBundle mainBundle] pathForResource:@"VOD_LICENSE_NAME" ofType:@"lic"]; // Replace VOD_LICENSE_NAME with the name of the VOD license file.
    authInfo.liveLicensePath = [[NSBundle mainBundle] pathForResource:@"LIVE_LICENSE_NAME" ofType:@"lic"];// Replace LIVE_LICENSE_NAME with the name of the live streaming license file.
    // Initialize the SDK.必須在連接網路後呼叫此方法。可從完成回呼中取得授權結果。
    [[BDLiveManager sharedInstance] startWithAuthInfo:authInfo complete:^(BOOL allSuccess, NSString * _Nullable warningInfo, NSArray<NSError *> * _Nullable errors) {
        NSLog(@"BDLive 【allSuccess】 %d \n 【warningInfo】: %@ 【errors】:\n\n%@", allSuccess, warningInfo, errors);
    }];
}
```

相關方法：[startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete)

### Step 5: 建立進入直播間所需的 Activity

在 Xcode 的 app target 中，打開定義如何加入和離開直播房間的檔案，並新增以下程式碼。

> **说明**

> 可透過呼叫 [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-TW) 或 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得直播間的活動 ID，並透過呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW) 取得進入直播間所需的授權 token。

```objectivec
#import <BPLive/BPLive.h>

BDLActivity *activity = [[BDLActivity alloc] init];
activity.activityId = @(ACTIVITY_ID); // 將 ACTIVITY_ID 替換為直播間的活動 ID。
activity.token = @"TOKEN"; // 將 TOKEN 替換為進入直播間所需的授權 token。
activity.authMode = BDLActivityAuthModePublic; // 直播間的驗證模式。此處以公開模式為例。觀眾無需登入直播間即可觀看直播、查看評論及執行其他操作。
activity.isPortrait = YES; // Whether the live room is in portrait mode.此處以直向模式為例。
```

### Step 6: 加入和離開直播房間

在 Xcode 的 app target 中，打開定義如何加入和離開直播房間的檔案，然後新增相關方法。

以下範例程式碼展示了加入和離開全功能直播房間的方法。

```objectivec
...
// Join the live room.
[[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity success:^{
    // Join the live room successfully
} failure:^(NSError * _Nonnull error) {
    // Failed to join the live room.
}];
// Leave the live room.
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}
```

## 優化 SDK 套件大小

從 1.33.0 版本開始，你可以透過以下方式在 `Podfile` 檔案中新增依賴來 優化 SDK 套件大小。如需更多資訊，請參閱 [Step 1: 新增依賴項](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-ios-ban-viewer-sdk-zh-TW#b1a1a0ed)。

```Ruby
  # The optimized SDK package excludes the feature of ultra-low latency live streaming.
  pod 'BPLive', '1.66.1-static-ttsdk', :subspecs => [
    'ViewerWithoutRTC', 
  ]
```

## 套件大小

此處的套件大小指的是：

* SDK 整合後壓縮 IPA 檔案大小的增加量。此數值是以新檔案大小減去原始檔案大小計算得出。

* SDK 整合後未壓縮 IPA 檔案大小的增加量。此數值是以新檔案大小減去原始檔案大小計算得出。

壓縮 IPA 檔案大小代表你的 app 下載大小，而未壓縮 IPA 檔案大小則對應於裝置上安裝後的 app 大小。

裝置上的實際未壓縮 IPA 檔案大小會比下表所列的數值更小，因為安裝時僅保留適用於當前裝置的資源。

以下數據基於 app 僅支援 arm64 CPU 架構。

|版本 |類型 |TTSDK 庫 |增量壓縮 IPA 檔案大小 |增量未壓縮 IPA 檔案大小 |依賴 |
|---|---|---|---|---|---|
|1.58.0 \- 1.66.1（依賴範例以 1.66.1 為例） |Viewer SDK |動態庫 |約 47 MB |約 94.8 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1'```<br> |
|||靜態庫 |約 43.7 MB |約 79.1 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1-static-ttsdk'```<br> |
||優化包體大小的 Viewer SDK |動態庫 |約 30.8 MB |約 64.7 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |
|||靜態函式庫 |約 27.5 MB |約 49 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1-static-ttsdk', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |

經過套件大小優化的 Viewer SDK 不包含超低延遲直播功能。如需新增依賴的更多資訊，請參閱 [Step 1: 新增依賴項](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-ios-ban-viewer-sdk-zh-TW#b1a1a0ed)。

## FAQ

[iOS Viewer SDK 常見問題](https://docs.byteplus.com/docs/byteplus-livesaas/ios-viewer-sdk-chang-jian-wen-ti-zh-TW)
