---
title: "初始化 Android 拉流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-android-zh-CN"
---

本主题介绍如何初始化 Android 拉流 SDK。你只需初始化 SDK 一次。

<span id="e276cc57"></span>
## 前提条件


* 你已按照 [集成 Android 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-CN) 提供的说明将 SDK 集成到你的项目中。

* 你已获取应用 ID 及其他基本信息。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。


<span id="a7180685"></span>
## 初始化 SDK

调用 `Env.start` 初始化 SDK。

启用日志上报功能后，你可以通过日志分析生产问题并定位原因。日志上报功能 **默认未开启**。你可以在初始化 SDK 时启用日志上报，并根据需要设置日志输出级别。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">仅 1.50.200.3 及以上版本支持启用日志上报功能。</div>


```Java
// Log configuration.
LogConfig config = new LogConfig.Builder(mApplicationContext)
        .setEnable(true) // Enable the log reporting feature.
        .setLogLevel(LogConfig.LogLevel.Info) // Set the log output level.默认值为 Debug。
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

// Enable logcat.建议在开发阶段启用 logcat，发布 APK 时关闭 logcat。
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


下表描述了初始化所需的每个参数：


|**参数** |**必填** |**数据类型** |**描述** |**示例** |
|---|---|---|---|---|
|AppID |是 |String |App ID，即你的 SDK 应用的唯一标识符。你可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)页面获取该 ID。更多信息，请参见 [获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。 |`123456` |
|AppName |是 |String |你的 SDK 应用名称。你可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)页面获取该名称。欲了解更多信息，请参见[获取您的 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/managing_sdk_licenses-zh-CN)。 |`video_demo` |
|AppVersion |是 |字符串 |你的 Android 应用的版本号。有效的版本号应包含两个或更多分隔符，例如“1.3.2”。 |`1.3.2` |
|AppChannel |是 |字符串 |用于下载应用的渠道。你也可以使用此参数区分不同环境下的应用构建，例如生产、测试和调试。 |`google_play` |
|LicenseUri |是 |字符串 |许可证文件的本地路径。 |`assets:///license2/license2_test.lic` |


初始化 SDK 时，你可以设置以下日志输出级别：


* `Verbose`：输出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 级别日志。

* `Debug`：输出 DEBUG、INFO、WARNING 和 ERROR 级别日志。

* `Info`：输出 INFO、WARNING 和 ERROR 级别日志。

* `Warning`：输出 WARNING 和 ERROR 级别日志。

* `Error`：输出 ERROR 级别日志。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">初始化 SDK 后，你可以调用<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#setloglevel">setLogLevel</a>来更改日志输出级别。</div>


<span id="a414e6c4"></span>
## 事件上报

为帮助排查生产问题和分析质量数据，事件上报 **默认已开启**。如有特殊数据隐私需求，你可以在配置 SDK 前调用 `Env.openAppLog(false)` 以关闭事件上报。

默认情况下，SDK 使用内置默认上报域名进行事件数据上报。从 1.51.300.2 版本开始，你可以选择使用内置双栈上报域名或自定义 URL 进行事件数据上报。


* 内置双栈上报域名：将 `setApplogDomainIpv6Enabled` 设置为 `true`，使 SDK 通过内置双栈上报域名上报事件数据。该域名支持 IPv4 和 IPv6 网络类型。当你的应用需要在仅 IPv6 网络类型环境下上报事件数据时，请使用内置双栈上报域名。示例代码如下。

   ```Java
   Env.start(new Config.Builder()
          // Other SDK configurations.
          .setApplogDomainIpv6Enabled(true)
          .build());
   ```
   

* 自定义 URL：如需将事件数据上报到指定 URL，请先联系 [技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 获取上报 URL，然后使用 `setApplogDomain` 配置自定义 URL。该 URL 可通过 IPv4 或 IPv6 访问。示例代码如下。

   ```Java
   Env.start(new Config.Builder()
          // Other SDK configurations.
          .setApplogDomain("https://custom-report-url.com")
          .build());
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果你启用内置的双栈上报域名并同时配置自定义 URL，SDK 只会使用自定义 URL 上报事件数据。   </div>
