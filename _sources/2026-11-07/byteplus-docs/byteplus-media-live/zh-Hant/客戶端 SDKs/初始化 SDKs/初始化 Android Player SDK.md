---
title: "初始化 Android Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-android-zh-TW"
---

本主題介紹如何初始化 Android Player SDK。SDK 只需初始化一次。

<span id="e276cc57"></span>
## 先決條件


* 你已依照 [整合 Android Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-TW) 提供的指引將 SDK 整合到你的專案中。

* 你已取得 app ID 及其他基本資料。如需更多資訊，請參見 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。


<span id="a7180685"></span>
## 初始化 SDK

呼叫 `Env.start` 來初始化 SDK。

啟用日誌上報功能後，你可以利用日誌來分析生產問題並找出原因。日誌上報功能 **預設為關閉**。你可以在初始化 SDK 時啟用日誌上報，並根據需要設定日誌輸出層級。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">僅 1.50.200.3 及以上版本支援啟用日誌上報功能。</div>


```Java
// Log configuration.
LogConfig config = new LogConfig.Builder(mApplicationContext)
        .setEnable(true) // Enable the log reporting feature.
        .setLogLevel(LogConfig.LogLevel.Info) // Set the log output level.預設值為 Debug。
        .build();
// Initialize the environment.
Env.start(new Config.Builder()
        .setApplicationContext(sApplicationContext)
        .setAppID("Your App ID")
        .setAppName("Your application name")
        .setAppVersion(BuildConfig.VERSION_NAME) // A valid version number should contain two or more separators, such as "1.3.2".
        .setAppChannel("Your app channel")
        .setLicenseUri("Your license URI")
        .setLicenseCallback(mLicenseCallback) // Set the license callbacks.
        .setBizType(BIZ_TYPE_LIVE) // 初始化 MediaLive SDK。
        .setLogConfig(config)
        .build());

// Enable logcat.建議於開發階段啟用 logcat，並於編譯正式 APK 時關閉 logcat。
// LicenseManager.turnOnLogcat(true);

// License callbacks.
LicenseManager.Callback mLicenseCallback =new LicenseManager.Callback() {
        @Override
        public void onLicenseLoadSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
            licenseID = licenseId; // The license ID, which you can use to get license information.
        }

        @Override
        public void onLicenseLoadError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseLoadRetry(@NonNull String licenseUri) {
           
        }

        @Override
        public void onLicenseUpdateSuccess(@NonNull String licenseUri, @NonNull String licenseId) {
          licenseID = licenseId;
        }

        @Override
        public void onLicenseUpdateError(@NonNull String licenseUri, @NonNull Exception e, boolean retryAble) {
           
        }

        @Override
        public void onLicenseUpdateRetry(@NonNull String licenseUri) {
          
        }
    };
```


下表說明初始化所需的各個參數：


|**參數** |**必填** |**資料型別** |**說明** |**範例** |
|---|---|---|---|---|
|AppID |是 |String |App ID，即你的 SDK 應用的唯一識別碼。你可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)頁面取得該 ID。如需更多資訊，請參見 [取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。 |`123456` |
|AppName |是 |String |你的 SDK 應用名稱。你可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)頁面取得該名稱。欲了解更多資訊，請參閱[取得您的 SDK 授權](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-TW)。 |`video_demo` |
|AppVersion |是 |字串 |您的 Android 應用程式的版本號。有效的版本號應包含兩個或以上的分隔符，例如「1.3.2」。 |`1.3.2` |
|AppChannel |是 |字串 |下載應用程式的渠道。您也可以使用此參數來區分不同環境的應用程式建置，例如正式環境、測試環境及除錯環境。 |`google_play` |
|LicenseUri |是 |字串 |授權檔案的本地路徑。 |`assets:///license2/license2_test.lic` |


初始化 SDK 時，你可以設定以下日誌輸出層級：


* `Verbose`：輸出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 層級的日誌。

* `Debug`：輸出 DEBUG、INFO、WARNING 和 ERROR 層級的日誌。

* `Info`：輸出 INFO、WARNING 和 ERROR 層級的日誌。

* `Warning`：輸出 WARNING 和 ERROR 層級的日誌。

* `Error`：僅輸出 ERROR 層級的日誌。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">初始化 SDK 後，您可以呼叫<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#setloglevel">setLogLevel</a>來變更日誌輸出層級。</div>


<span id="a414e6c4"></span>
## 事件上報

為協助排除生產問題及分析品質資料，事件上報功能 **預設為啟用**。若你有特殊的資料隱私需求，可於配置 SDK 前呼叫 `Env.openAppLog(false)` 以關閉事件上報。

SDK 預設使用內建的預設上報網域來上報事件資料。自 1.51.300.2 版本起，你可以選擇使用內建雙疊上報網域或自訂 URL 來上報事件資料。


* 內建雙疊上報網域：設定 `setApplogDomainIpv6Enabled` 為 `true`，即可讓 SDK 通過內建雙疊上報網域上報事件資料。此網域同時支援 IPv4 和 IPv6 網路。當你的應用需在僅 IPv6 的網路環境中上報事件資料時，請使用內建雙疊上報網域。範例程式碼如下。

   ```Java
   Env.start(new Config.Builder()
          // Other SDK configurations.
          .setApplogDomainIpv6Enabled(true)
          .build());
   ```
   

* 自訂 URL：若需將事件資料上報至指定 URL，請先聯繫 [技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 取得上報 URL，然後使用 `setApplogDomain` 配置自訂 URL。該 URL 可透過 IPv4 或 IPv6 存取。範例程式碼如下。

   ```Java
   Env.start(new Config.Builder()
          // Other SDK configurations.
          .setApplogDomain("https://custom-report-url.com")
          .build());
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若啟用內建的雙堆疊報告網域並同時設定自訂 URL，SDK 僅會使用自訂 URL 來報告事件資料。   </div>
