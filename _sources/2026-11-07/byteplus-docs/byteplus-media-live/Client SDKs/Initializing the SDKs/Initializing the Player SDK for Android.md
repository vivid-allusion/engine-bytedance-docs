---
title: "Initializing the Player SDK for Android"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-initializing-for-android"
---

This topic introduces how to initialize the Player SDK for Android. You only need to initialize the SDK once.

<span id="e276cc57"></span>
## Prerequisites


* You have integrated the SDK into your project by following the instructions provided in [Integrating the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android).

* You have obtained the app ID and other basic information. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).


<span id="a7180685"></span>
## Initializing the SDK

Call `Env.start` to initialize the SDK.

After you enable the log reporting feature, you can use logs to analyze production issues and identify their causes. The log reporting feature is **disabled by default**. You can enable log reporting when you initialize the SDK and set the log output level as needed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only versions 1.50.200.3 and later support enabling the log reporting feature.</div>


```Java
// Log configuration.
LogConfig config = new LogConfig.Builder(mApplicationContext)
        .setEnable(true) // Enable the log reporting feature.
        .setLogLevel(LogConfig.LogLevel.Info) // Set the log output level. The default value is Debug.
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
        .setBizType(BIZ_TYPE_LIVE) // Initialize the MediaLive SDK.
        .setLogConfig(config)
        .build());

// Enable logcat. It is recommended to enable logcat during development and disable logcat when compiling the release APK.
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


The following table describes each parameter required for initialization:


|**Parameter** |**Required** |**Data Type** |**Description** |**Example** |
|---|---|---|---|---|
|AppID |Yes |String |App ID, which is the unique identifier of your SDK application. You can get the ID on the [SDK management](https://console.byteplus.com/live/main/sdk) page. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management). |`123456` |
|AppName |Yes |String |The name of your SDK application. You can get the name on the [SDK management](https://console.byteplus.com/live/main/sdk) page. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management). |`video_demo` |
|AppVersion |Yes |String |The version number of your Android app. A valid version number should contain two or more separators, such as "1.3.2". |`1.3.2` |
|AppChannel |Yes |String |The channel through which to download the app. You can also use this parameter to distinguish between app builds for different environments, such as production, testing, and debugging. |`google_play` |
|LicenseUri |Yes |String |The local path to the license file. |`assets:///license2/license2_test.lic` |


When you initialize the SDK, you can set the following log output levels:


* `Verbose`: Outputs VERBOSE, DEBUG, INFO, WARNING, and ERROR level logs.

* `Debug`: Outputs DEBUG, INFO, WARNING, and ERROR level logs.

* `Info`: Outputs INFO, WARNING, and ERROR level logs.

* `Warning`: Outputs WARNING and ERROR level logs.

* `Error`: Outputs ERROR level logs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you initialize the SDK, you can call <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference#setloglevel">setLogLevel</a> to change the log output level.</div>


<span id="a414e6c4"></span>
## Reporting events

To help troubleshoot production issues and analyze quality data, event reporting is **enabled by default**. If you have special data privacy requirements, you can call `Env.openAppLog(false)` before configuring the SDK to disable event reporting.

By default, the SDK reports event data by using the built\-in default reporting domain. Starting from version 1.51.300.2, you can choose to report event data by using either the built\-in dual\-stack reporting domain or a custom URL.


* Built\-in dual\-stack reporting domain: Set `setApplogDomainIpv6Enabled` to `true` to make the SDK report event data through the built\-in dual\-stack reporting domain. This domain supports both IPv4 and IPv6 networks. Use the built\-in dual\-stack reporting domain when your app needs to report event data in an IPv6\-only network environment. The sample code is as follows.

   ```Java
   Env.start(new Config.Builder()
          // Other SDK configurations.
          .setApplogDomainIpv6Enabled(true)
          .build());
   ```
   

* Custom URL: If you need to report event data to a specific URL, first contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to get a reporting URL, and then use `setApplogDomain` to configure the custom URL. The URL can be accessed over IPv4 or IPv6. The sample code is as follows.

   ```Java
   Env.start(new Config.Builder()
          // Other SDK configurations.
          .setApplogDomain("https://custom-report-url.com")
          .build());
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you enable the built\-in dual\-stack reporting domain and also configure a custom URL, the SDK only uses the custom URL to report event data.   </div>
