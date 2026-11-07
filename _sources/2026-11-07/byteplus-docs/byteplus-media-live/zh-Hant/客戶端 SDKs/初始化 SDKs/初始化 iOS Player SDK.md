---
title: "初始化 iOS Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-ios-zh-TW"
---

本主題介紹如何初始化 iOS Player SDK。您只需初始化 SDK 一次。

## 前提條件

* 您已按照[整合 iOS Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) 中提供的說明，將 SDK 整合至專案。

* 您已取得應用程式 ID 和其他基本資訊。如需詳細資訊，請參閱[取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。

## 初始化 SDK

使用以下程式碼初始化 SDK。

啟用日誌上報功能後，您可以使用日誌分析生產環境問題並找出原因。日誌上報功能**預設為停用**。您可以在初始化 SDK 時啟用日誌上報，並視需要設定日誌輸出等級。

> **說明**

> 只有 1.50.200.3\-premium 及更高版本支援啟用日誌上報功能。

```objectivec
#import <TTSDK/TTSDKManager.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // 您的程式碼。
    [self configTTSDK];
    // 您的程式碼。
    return YES;
}

- (void)configTTSDK {
    TTSDKLogConfiguration *logConfig = [[TTSDKLogConfiguration alloc] init];
    // 啟用日誌上報功能。
    logConfig.enable = YES; 
    // 設定日誌輸出等級。預設值為 TTSDKLogLevelDebug。
    logConfig.logLevel = TTSDKLogLevelInfo; 
    
    // 使用您的 AppID 建立 TTSDKConfiguration。
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"您的 AppID"];
    // 設定您的 SDK 應用程式。
    configuration.appName = @"您的應用程式名稱";
    configuration.channel = @"您的應用程式通道";
    configuration.bundleID = @"您的 bundle ID";
    
    // 設定授權檔案的路徑。
    configuration.licenseFilePath = [NSBundle.mainBundle pathForResource:@"您的授權路徑" ofType:nil];
    
    configuration.logConfiguration = logConfig;
    
    // 將 TTSDKConfiguration 傳遞至 TTSDKManager。
    [TTSDKManager startWithConfiguration:configuration];
}
```

下表說明每個初始化參數：

|參數 |是否必要 |資料類型 |說明 |範例 |
|---|---|---|---|---|
|AppID |是 |字串 |應用程式 ID，是您的 SDK 應用程式的唯一識別碼。您可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)頁面取得此 ID。如需詳細資訊，請參閱[取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。 |`123456` |
|appName |是 |字串 |您的 SDK 應用程式名稱。您可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)頁面取得此名稱。如需詳細資訊，請參閱[取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。 |`video_demo` |
|channel |否 |字串 |下載應用程式的通道。您也可以使用此參數來區分不同環境的應用程式建置版本，例如生產、測試和偵錯。 |`appstore` |
|bundleID |是 |字串 |您 iOS 應用程式的套件名稱，即 Xcode 專案中主要目標的 `bundleID`。 |`com.byteplus.video.ios` |
|licenseFilePath |是 |字串 |授權檔案的路徑。 |`live.lic` |

初始化 SDK 時，您可以設定以下日誌輸出等級：

* `TTSDKLogLevelVerbose`：輸出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 等級的日誌。

* `TTSDKLogLevelDebug`：輸出 DEBUG、INFO、WARNING 和 ERROR 等級的日誌。

* `TTSDKLogLevelInfo`：輸出 INFO、WARNING 和 ERROR 等級的日誌。

* `TTSDKLogLevelWarn`：輸出 WARNING 和 ERROR 等級的日誌。

* `TTSDKLogLevelError`：輸出 ERROR 等級的日誌。

> **說明**

> 初始化 SDK 後，您可以呼叫 [setLogLevel:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setloglevel) 來變更日誌輸出等級。

## 上報事件

為了協助排解生產環境問題並分析品質資料，事件上報**預設為啟用**。如果您有特殊的資料隱私需求，可以在 `TTSDKConfiguration` 中將 `shouldInitAppLog` 設定為 `NO`，以停用事件上報。

預設情況下，SDK 會使用內建的預設上報網域上報事件資料。從 1.51.300.2\-premium 版本開始，您可以選擇使用內建雙堆疊上報網域或自訂 URL 上報事件資料。

* 內建雙堆疊上報網域：將 `builtInIPv6ReportURLEnabled` 設定為 `YES`，讓 SDK 透過內建雙堆疊上報網域上報事件資料。此網域同時支援 IPv4 和 IPv6 網路。當您的應用程式需要在僅 IPv6 網路環境中上報事件資料時，請使用內建雙堆疊上報網域。範例程式碼如下。

   ```objectivec
   - (void)setupSDKWithAppID {
       // 其他 SDK 設定。
       configuration.reportConfiguration = [TTSDKReportConfiguration defaultReportConfigurationWithBuiltInIPv6ReportURLEnabled:YES];
   }
   ```

* 自訂 URL：如果您需要將事件資料上報到特定 URL，請先聯絡[技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)取得上報 URL，然後使用 `customReportURL` 設定自訂 URL。可透過 IPv4 或 IPv6 存取該 URL。範例程式碼如下。

   ```objectivec
   - (void)setupSDKWithAppID {
       // 其他 SDK 設定。
       configuration.reportConfiguration = [TTSDKReportConfiguration customReportURL:@"https://custom-report-url.com"];
   }
   ```

   > **說明**

   > 如果您啟用內建雙堆疊上報網域，同時也設定自訂 URL，SDK 只會使用自訂 URL 上報事件資料。
