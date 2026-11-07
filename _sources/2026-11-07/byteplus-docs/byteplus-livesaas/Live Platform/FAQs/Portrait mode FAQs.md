---
title: "Portrait mode FAQs"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-portrait-mode-faqs"
---

<span id="20c9a2a7"></span>
## Why do the background color, text color, and host color in the comment area of a live room in portrait mode differ from my color configurations on the BytePlus Live console?

By default, viewer comments have a black background with white text, and host comments have a black background with yellow text in the comment area of a live room in portrait mode. This default configuration is designed to adapt to most scenarios, considering that the background of a live room in portrait mode is the live video, preview, or playback.

To customize these color configurations in the comment area of a live room in portrait mode, turn on the **Color configuration synchronization** switch on the **Producer** \> **Appearance** page of your live room.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a40573d7a8345e6adae0deb3803cb67~tplv-goo7wpa0wc-image.image) </span>

<span id="f6cdad3e"></span>
## Why doesn't a preview or playback fill the entire player for a live room in portrait mode when the video's width is smaller than its height?

If a video's width is smaller than its height, the video will fill the entire player as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b646536ffc4d4668a4b1fdec7c6b8373~tplv-goo7wpa0wc-image.image) </span>

However, if an error occurs during the initialization of TTSDK in your Viewer SDK for iOS integration, such as a failure in VOD license settings, the video cannot fill the entire player as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/551d61dc8b184ada99d0edff4faba32b~tplv-goo7wpa0wc-image.image) </span>

<span id="fc4783d2"></span>
### Solution

In your app target in Xcode, open the `AppDelegate.m` file to initialize TTSDK.

```objectivec
#import <TTSDKFramework/TTSDKManager.h>
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self initTTSDK];
    return YES;
}

- (void)initTTSDK {
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"APP_ID"]; // Replace APP_ID with the app ID returned after the successful license application. Contact the sales representative to obtain the app ID.
    configuration.appName = @"APP_NAME"; // Replace APP_NAME with the app name used to apply for the license. Contact the sales representative to obtain the app name.
    configuration.channel = @"CHANNEL_NAME"; // Replace CHANNEL_NAME with the channel through which to download the app, such as App Store.
    configuration.bundleID = @"BUNDLE_ID"; // Replace BUNDLE_ID with the bundle identifier of the app.
    
    // Set the VOD license and live streaming license.
    // VOD license.
    configuration.licenseFilePath = [[NSBundle mainBundle] pathForResource:@"VOD_LICENSE_NAME" ofType:@"lic"]; // Replace VOD_LICENSE_NAME with the name of the VOD license file.
    [TTSDKManager startWithConfiguration:configuration];
    
    // Live streaming license.
    configuration.licenseFilePath = [[NSBundle mainBundle] pathForResource:@"LIVE_LICENSE_NAME" ofType:@"lic"]; // Replace LIVE_LICENSE_NAME with the name of the live streaming license file.
    [TTSDKManager startWithConfiguration:configuration];
}
```
