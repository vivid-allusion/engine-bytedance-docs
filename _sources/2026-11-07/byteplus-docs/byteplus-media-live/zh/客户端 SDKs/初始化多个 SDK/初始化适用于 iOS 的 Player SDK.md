---
title: "初始化适用于 iOS 的 Player SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-ios-zh-CN"
---

本主题介绍如何初始化适用于 iOS 的 Player SDK。你只需初始化一次 SDK。

## 前提条件

* 你已按照[集成适用于 iOS 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)中的说明，将 SDK 集成到项目中。

* 你已获取应用 ID 和其他基本信息。更多信息，请参见[获取 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。

## 初始化 SDK

使用以下代码初始化 SDK。

启用日志上报功能后，你可以使用日志分析生产问题并确定原因。日志上报功能**默认禁用**。你可以在初始化 SDK 时启用日志上报，并按需设置日志输出级别。

> **说明**

> 仅 1.50.200.3\-premium 及更高版本支持启用日志上报功能。

```objectivec
#import <TTSDK/TTSDKManager.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // 你的代码。
    [self configTTSDK];
    // 你的代码。
    return YES;
}

- (void)configTTSDK {
    TTSDKLogConfiguration *logConfig = [[TTSDKLogConfiguration alloc] init];
    // 启用日志上报功能。
    logConfig.enable = YES; 
    // 设置日志输出级别。默认值为 TTSDKLogLevelDebug。
    logConfig.logLevel = TTSDKLogLevelInfo; 
    
    // 使用你的 AppID 创建 TTSDKConfiguration。
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"你的 AppID"];
    // 配置你的 SDK 应用。
    configuration.appName = @"你的应用名称";
    configuration.channel = @"你的应用渠道";
    configuration.bundleID = @"你的 bundle ID";
    
    // 配置许可证文件路径。
    configuration.licenseFilePath = [NSBundle.mainBundle pathForResource:@"你的许可证路径" ofType:nil];
    
    configuration.logConfiguration = logConfig;
    
    // 将 TTSDKConfiguration 传递给 TTSDKManager。
    [TTSDKManager startWithConfiguration:configuration];
}
```

下表介绍每个初始化参数：

|参数 |是否必填 |数据类型 |描述 |示例 |
|---|---|---|---|---|
|AppID |是 |String |应用 ID，即 SDK 应用的唯一标识符。你可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)页面获取该 ID。更多信息，请参见[获取 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。 |`123456` |
|appName |是 |String |SDK 应用的名称。你可以在 [SDK 管理](https://console.byteplus.com/live/main/sdk)页面获取该名称。更多信息，请参见[获取 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。 |`video_demo` |
|channel |否 |String |下载应用的渠道。你也可以使用此参数区分不同环境的应用构建，例如生产、测试和调试环境。 |`appstore` |
|bundleID |是 |String |iOS 应用的包名，即 Xcode 项目中主 target 的 `bundleID`。 |`com.byteplus.video.ios` |
|licenseFilePath |是 |String |许可证文件路径。 |`live.lic` |

初始化 SDK 时，你可以设置以下日志输出级别：

* `TTSDKLogLevelVerbose`：输出 VERBOSE、DEBUG、INFO、WARNING 和 ERROR 级别日志。

* `TTSDKLogLevelDebug`：输出 DEBUG、INFO、WARNING 和 ERROR 级别日志。

* `TTSDKLogLevelInfo`：输出 INFO、WARNING 和 ERROR 级别日志。

* `TTSDKLogLevelWarn`：输出 WARNING 和 ERROR 级别日志。

* `TTSDKLogLevelError`：输出 ERROR 级别日志。

> **说明**

> 初始化 SDK 后，你可以调用 [setLogLevel:](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setloglevel) 更改日志输出级别。

## 上报事件

为帮助排查生产问题并分析质量数据，事件上报**默认启用**。如果你有特殊的数据隐私要求，可以在 `TTSDKConfiguration` 中将 `shouldInitAppLog` 设置为 `NO`，以禁用事件上报。

默认情况下，SDK 使用内置默认上报域名上报事件数据。从 1.51.300.2\-premium 版本开始，你可以选择使用内置双栈上报域名或自定义 URL 上报事件数据。

* 内置双栈上报域名：将 `builtInIPv6ReportURLEnabled` 设置为 `YES`，使 SDK 通过内置双栈上报域名上报事件数据。该域名同时支持 IPv4 和 IPv6 网络。当你的应用需要在仅 IPv6 网络环境中上报事件数据时，请使用内置双栈上报域名。示例代码如下。

   ```objectivec
   - (void)setupSDKWithAppID {
       // 其他 SDK 配置。
       configuration.reportConfiguration = [TTSDKReportConfiguration defaultReportConfigurationWithBuiltInIPv6ReportURLEnabled:YES];
   }
   ```

* 自定义 URL：如果你需要将事件数据上报到特定 URL，请先联系[技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)获取上报 URL，然后使用 `customReportURL` 配置自定义 URL。该 URL 可通过 IPv4 或 IPv6 访问。示例代码如下。

   ```objectivec
   - (void)setupSDKWithAppID {
       // 其他 SDK 配置。
       configuration.reportConfiguration = [TTSDKReportConfiguration customReportURL:@"https://custom-report-url.com"];
   }
   ```

   > **说明**

   > 如果你启用了内置双栈上报域名，并且还配置了自定义 URL，SDK 仅使用自定义 URL 上报事件数据。
