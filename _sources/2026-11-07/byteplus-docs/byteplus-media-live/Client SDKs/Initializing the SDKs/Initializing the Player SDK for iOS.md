---
title: "Initializing the Player SDK for iOS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-ios"
---

This topic introduces how to initialize the Player SDK for iOS. You only need to initialize the SDK once.

 &nbsp;

<span id="prerequisites"></span>
## Prerequisites


* You have integrated the SDK into your project by following the instructions provided in [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios).

* You have obtained the app ID and other basic information. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).


 &nbsp;

<span id="initializing-the-sdk"></span>
## Initializing the SDK

Initialize the SDK with the following code.

After you enable the log reporting feature, you can use logs to analyze production issues and identify their causes. The log reporting feature is **disabled by default**. You can enable log reporting when you initialize the SDK and set the log output level as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Only versions 1.50.200.3\-premium and later support enabling the log reporting feature.</div>


```objectivec
#import <TTSDK/TTSDKManager.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Your code.
    [self configTTSDK];
    // Your code.
    return YES;
}

- (void)configTTSDK {
    TTSDKLogConfiguration *logConfig = [[TTSDKLogConfiguration alloc] init];
    // Enable the log reporting feature.
    logConfig.enable = YES; 
    // Set the log output level. The default value is TTSDKLogLevelDebug.
    logConfig.logLevel = TTSDKLogLevelInfo; 
    
    // Create TTSDKConfiguration with your AppID.
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"Your AppID"];
    // Configure your SDK application.
    configuration.appName = @"Your application name";
    configuration.channel = @"Your app channel";
    configuration.bundleID = @"Your bundle ID";
    
    // Configure the path to your license file.
    configuration.licenseFilePath = [NSBundle.mainBundle pathForResource:@"Your license path" ofType:nil];
    
    configuration.logConfiguration = logConfig;
    
    // Pass TTSDKConfiguration to TTSDKManager.
    [TTSDKManager startWithConfiguration:configuration];
}
```


The following table describes each initialization parameter:

&nbsp;


|Parameter |Required |Data Type |Description |Example |
|---|---|---|---|---|
|AppID |Yes |String |App ID, which is the unique identifier of your SDK application. You can get the ID on the [SDK management](https://console.byteplus.com/live/main/sdk) page. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management). |`123456` |
|appName |Yes |String |The name of your SDK application. You can get the name on the [SDK management](https://console.byteplus.com/live/main/sdk) page. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management). |`video_demo` |
|channel |No |String |The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging. |`appstore` |
|bundleID |Yes |String |The package name of your iOS app, which is the `bundleID` of the main target in your Xcode project. |`com.byteplus.video.ios` |
|licenseFilePath |Yes |String |The path to the license file. |`live.lic` |


When you initialize the SDK, you can set the following log output levels:


* `TTSDKLogLevelVerbose`: Outputs VERBOSE, DEBUG, INFO, WARNING, and ERROR level logs.

* `TTSDKLogLevelDebug`: Outputs DEBUG, INFO, WARNING, and ERROR level logs.

* `TTSDKLogLevelInfo`: Outputs INFO, WARNING, and ERROR level logs.

* `TTSDKLogLevelWarn`: Outputs WARNING and ERROR level logs.

* `TTSDKLogLevelError`: Outputs ERROR level logs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">After you initialize the SDK, you can call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api#setloglevel">setLogLevel:</a> to change the log output level.</div>


 &nbsp;

<span id="reporting-events"></span>
## Reporting events

To help troubleshoot production issues and analyze quality data, event reporting is **enabled by default**. If you have special data privacy requirements, you can set `shouldInitAppLog` to `NO` in `TTSDKConfiguration` to disable event reporting.

By default, the SDK reports event data by using the built\-in default reporting domain. Starting from version 1.51.300.2\-premium, you can choose to report event data by using either the built\-in dual\-stack reporting domain or a custom URL.


* Built\-in dual\-stack reporting domain: Set `builtInIPv6ReportURLEnabled` to `YES` to make the SDK report event data through the built\-in dual\-stack reporting domain. This domain supports both IPv4 and IPv6 networks. Use the built\-in dual\-stack reporting domain when your app needs to report event data in an IPv6\-only network environment. The sample code is as follows.

   ```objectivec
   - (void)setupSDKWithAppID {
       // Other SDK configurations.
       configuration.reportConfiguration = [TTSDKReportConfiguration defaultReportConfigurationWithBuiltInIPv6ReportURLEnabled:YES];
   }
   ```
   

* Custom URL: If you need to report event data to a specific URL, first contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to get a reporting URL, and then use `customReportURL` to configure the custom URL. The URL can be accessed over IPv4 or IPv6. The sample code is as follows.

   ```objectivec
   - (void)setupSDKWithAppID {
       // Other SDK configurations.
       configuration.reportConfiguration = [TTSDKReportConfiguration customReportURL:@"https://custom-report-url.com"];
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you enable the built\-in dual\-stack reporting domain and also configure a custom URL, the SDK only uses the custom URL to report event data.   </div>
