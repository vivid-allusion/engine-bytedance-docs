---
title: "iOS Player SDK: License guide"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-license-guide-ios"
---

A license is a usage agreement between you and BytePlus VOD. To use the SDKs provided by BytePlus VOD, you must have a license. This article describes how to purchase, acquire, configure, and monitor licenses.

<span id="26aa83cf"></span>
## Acquire a license

You can acquire a license on the BytePlus VOD console. For details, see [SDK Management](https://docs.byteplus.com/en/byteplus-vod/docs/sdk-management).

<span id="c5bf9d95"></span>
## Configure the license

To configure the license when initializing the SDK, see the following sample code:

```objectivec
#import <TTSDK/TTSDKManager.h>

// Pass in the App ID of your app
NSString *appId = @"your app id"; 

// Copy the license file to your project directory and pass in the license name when initializing the SDK 
NSString *licenseName = @"ttlicense.lic";

TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:appId licenseName:licenseName];

[TTSDKManager startWithConfiguration:configuration];
```


<span id="63b1fcce"></span>
## Monitor the license

After initializing the SDK, you can monitor the status of the license and the additional features. The status code indicates whether the license is available or expired. The following table lists the status codes of the license:


|**Status code** |**Constant definitions in the SDK** |**Description** |
|---|---|---|
|0 |TTLicenseStatusInvalid |The license is invalid for one of the following reasons:<br><br><br>* The license file is invalid or tampered with.<br><br>* No license has been found, or the license address is incorrect. |
||||
||||
|1 |TTLicenseStatusOK |The license authentication has been passed. |
|2 |TTLicenseStatusExpired |The license has expired. |
|401 |TTLicenseStatusParamErrorPackageName |The actual application package name does not match the package name that you fill in when purchasing the license. |
|402 |TTLicenseStatusParamErrorFeatureName |* The license does not cover the additional feature.<br><br>* The name of the additional feature is incorrect. |
||||
||||
|403 |TTLicenseStatusParamErrorModuleName |The SDK enumeration pass error. |


If you need to add some business logic when the license status changes, you can use `NotificationCenter` to listen to the relevant notifications. You can get `notification.userinfo` in the callback of `NotificationObserver`. This info can help you check whether the license authentication has passed.

See the following sample code:

```objectivec
// Below is NotificationName. You need to manually declare it if needed. The SDK has assigned a value to the notification name internally
FOUNDATION_EXTERN NSString * const TTLicenseNotificationLicenseDidAdd; // The license has been added
FOUNDATION_EXTERN NSString * const TTLicenseNotificationLicenseInfoDidUpdate; // The license has been updated

// Below is the key of Notification.userInfo.You need to manually declare it if needed. The SDK has assigned a value to the notification name internally
// userInfo[TTLicenseNotificationLicenseResultKey] contains the license authentication result, which is correspond to the status code in the above table
FOUNDATION_EXTERN NSString * const TTLicenseNotificationLicenseResultKey; 


- (void)addLicenseObserver {
    // 1. Use NotificationCenter to listen to whether the license has been added
    [[NSNotificationCenter defaultCenter] addObserverForName:TTLicenseNotificationLicenseDidAdd object:nil queue:NSOperationQueue.mainQueue usingBlock:^(NSNotification * _Nonnull note) {
        NSNumber *success = [note userInfo][TTLicenseNotificationLicenseResultKey];
        BOOL isSuccess = [success boolValue];
        if (isSuccess) {
            // The license authentication succeeds
            NSLog(@"update license successfully");
        } else {
            // The license authentication fails
            NSLog(@"failed to add license");
        }
    }];
    
    // 2. Use NotificationCenter to listen to whether the license has been updated
    [[NSNotificationCenter defaultCenter] addObserverForName:TTLicenseNotificationLicenseInfoDidUpdate object:nil queue:NSOperationQueue.mainQueue usingBlock:^(NSNotification * _Nonnull note) {
        NSNumber *success = [note userInfo][TTLicenseNotificationLicenseResultKey];
        BOOL isSuccess = [success boolValue];
        if (isSuccess) {
            // The license authentication succeeds
            NSLog(@"update license successfully")；
        } else {
            // The license authentication fails
            NSLog(@"failed to update license");
        }
    }];
}
```


<span id="ef6e3c52"></span>
## Handle license authentication failure

Enable `TTVideoEngineLog`during the integration. See the following sample code:

```objectivec
#if DEBUG
[TTVideoEngine setLogFlag:TTVideoEngineLogFlagAll];
#endif
objectivec
```


If the license authentication fails, the following issues may occur:


* When creating a player instance with `- [TTVideoEngine initWithType:]`, the console prints `fail.license`.

* The SDK internally downgrades the player to the system player. At this time, if you check `engine.isOwnPlayer`, the SDK returns `NO`.

* When you try to call APIs to use some features, errors may occur and the console prints the error log:

   * `Failed, the feature is not included in license` means your license does not cover this feature.

   * `using a standard editon which is not support this feature` means your license is for Standard Edition, but the feature is only supported by the Premium or Enterprise Editions.

   * `Failed, using a standard license which is not including this feature` means your license does not cover this feature.


In most cases, when the license authentication fails, the playback fails. You can listen to the `videoEngineDidFinish` callback and troubleshoot according to the error messages.

```objectivec
#import <TTSDK/TTVideoEngineHeader.h>

// 1. Set TTVideoEngine Delegate
self.videoEngine.delegate = self;

// 2. Listen the callback which occurs when the playback finishes
- (void)videoEngineDidFinish:(TTVideoEngine *)videoEngine error:(nullable NSError *)error {
    if (error) {
        NSLog(@"%@", error);  
    }
}
```


Pay special attention to the validity period of your license. We suggest that you renew the license on the BytePlus VOD console two months before the license expires.
