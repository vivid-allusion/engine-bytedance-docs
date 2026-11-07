---
title: "Integrating the Viewer SDK for iOS (for versions 1.56.0 - 1.59.0)"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-1-56-0-1-59-0"
---

The Viewer SDK enables your mobile app to include features such as watching a live stream, sending comments, and interacting with the host. This topic describes how to integrate the Viewer SDK into your iOS app.

<span id="3116ad93"></span>
## Prerequisites


* Real devices or simulators running iOS 11.0 and above.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use an Apple Silicon Mac, the Rosetta simulator is required.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The simulator is only intended for interface debugging and does not guarantee the normal functioning of features such as audio, video, and picture\-in\-picture (PiP). To avoid issues like screen artifacts or black borders, we recommend that you use a physical device.   </div>
   

* Xcode. The latest version is recommended.

* CocoaPods. 1.11.0 or later versions are recommended. For more information, see [Getting Started with CocoaPods](https://guides.cocoapods.org/using/getting-started.html#getting-started).

* CPU architecture: arm64 or x86_64.

* Contact BytePlus Live technical support to obtain the live streaming license file and Video on Demand (VOD) license file, the app name used to apply for the license, and the app ID returned after a successful application.


<span id="14ae9f8a"></span>
## Integration steps

<span id="b1a1a0ed"></span>
### Step 1: Add dependencies


1. Open the `Podfile` file of your project to add dependencies.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If CocoaPods is not used in your project before, run the command <code>pod init && pod install</code> in the project's root directory and then you can obtain the <code>Podfile</code> file.   </div>
   

   ```Ruby
   source 'https://github.com/cocoapods/Specs.git'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   
   # Your app target name
   target 'XXXX' do
     # If you only integrate the Viewer SDK
     # Starting from version 1.33.0, you can use ViewerWithoutRTC as podspec to optimize the SDK package size. This action will provide you with an SDK package that excludes the feature of ultra-low latency live streaming. 
     pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0/BPLive.podspec.json'
     # If you integrate both the Live Streaming SDK and Viewer SDK
     # Starting from version 1.33.0, you can replace LiveStreaming with LiveStreamingWithoutRTC to optimize the SDK package size. This action will provide you with an SDK package that excludes the feature of live streaming by sharing the screen. Additionally, you can replace Viewer with ViewerWithoutRTC to also optimize the SDK package size. This action will provide you with an SDK package that excludes the feature of ultra-low latency live streaming.
     pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0/BPLive.podspec.json', :subspecs => [
       'LiveStreaming',
       'Viewer',
     ]
   end  
   ```
   

2. Open a terminal window and run the command `cd` to navigate to your project's directory. Run the command `pod install` to install the dependencies.


<span id="444cc713"></span>
#### Using the static library version of TTSDK

By default, the dynamic library version of TTSDK is used. To use the static library version of TTSDK, append `-static-ttsdk` to the version number when adding dependencies. For more information, see the preceding configurations in the `Podfile` file.

```Ruby
  # If you only integrate the Viewer SDK
  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json'


1. Open the `info.plist` file, add the parameter `SSAppID`, and set the parameter value as the app ID returned after the successful license application.
2. In the `info.plist` file, add permissions in one of the following ways:
   * Click **+** to add **Privacy - Photo Library Additions Usage Description** and **Privacy - Calendars Usage Description** as **Key**, select **String** as **Type**, and then enter the prompt message displayed in the system authorization dialog box as **Value**.
   * Open the `info.plist` file in source code mode and add the following keys and strings. You can customize the value of the string as the prompt message displayed in the system authorization dialog box.
      ```Plain Text
      <!-- Write access to photo library -->
      <key>NSPhotoLibraryAddUsageDescription</key> 
      <string>The app needs your permission to write to your photo library for saving images to the photo library</string>
      <!-- Write access to calendar -->
      <key>NSCalendarsUsageDescription</key>
      <string>Used to remind viewers before live stream starts</string>
      ```

3. (Optional) If you need the app to continue playing audio when running in the background or need to use the Picture-in-Picture (PiP) feature, complete the following steps:
   1. Click **+ Capability** under the **Signing & Capabilities** tab, and double-click to add **Background Modes**.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/147f155c322d4f6cba5c2f26c813f33b~tplv-goo7wpa0wc-image.image =468x)
   2. In the **Background Modes** section, select the **Audio, AirPlay, and Picture in Picture** checkbox.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eefa3e63dd374db686c0b232547c944b~tplv-goo7wpa0wc-image.image =566x)
4. (Optional) If your project is using Bitcode, you need to disable Bitcode.
   ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/991f4357e3bb47579b6256340415e73d~tplv-goo7wpa0wc-image.image =2706x)
   1. Click the **Build Settings** tab.
   2. In the **Build Options** section, set **Enable Bitcode** to **No**.
5. Configure the screen orientation supported when playing live videos, previews, or playbacks in full-screen mode.
   1. Click the **General** tab.
   2. In the **Deployment Info** section, select the **Portrait** and **Landscape Right** checkboxes for **iPhone Orientation** and **iPad Orientation**.
      ![Image](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab42c8820c0f4eee99fe655eb65c2ff6~tplv-goo7wpa0wc-image.image =2092x)
   :::tip
   * If you want viewers to be able to automatically rotate the screen left and right according to the device orientation in full-screen mode, the following conditions must be met:
      * The portrait orientation lock of the viewer's device is turned off. For how to turn off the portrait orientation lock, see the [official Apple documentation](https://support.apple.com/en-us/118226).
      * Both **Landscape Left** and **Landscape Right** checkboxes are selected in the **Deployment Info** section.
   * To avoid abnormal display of the full-screen animation after viewers tap the full-screen button, make sure to select the **Landscape Right** checkbox.
   * To disable the full-screen mode, you can hide the full-screen button in the player with the following sample code.  After disabling the full-screen mode, you can only select the **Portrait** checkbox in the **Deployment Info** section.
      `[BDLLiveEngine sharedInstance].liveRoomConfiguration.playerConfig.common.enterFullScreenEnable = NO;`
   :::

<span id="23f96af9"></span>
### Step 3: Import licenses
Add the live streaming license file and VOD license file to the app target in Xcode. Select **Copy items if needed**, and click **Finish**.
<span id="f951ba1a"></span>
### Step 4: Initialize BPLive
In the app target of Xcode, open the `AppDelegate.m` file to initialize BPLive:
```objectivec
#import <BPLive/BPLive.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self initBPLive];
    return YES;
}

- (void)initBPLive {
    BDLiveAuthInfo *authInfo = [[BDLiveAuthInfo alloc] init];
    authInfo.bizType = BDLiveBizTypeViewer; // If you integrate both the Live Streaming SDK and Viewer SDK, replace BDLiveBizTypeViewer with BDLiveBizTypeViewer | BDLiveBizTypeLiveStreaming.
    authInfo.appId = @"APP_ID"; // Replace APP_ID with the app ID returned after the successful license application. Contact BytePlus Live technical support to get the app ID.
    authInfo.appName = @"APP_NAME"; // Replace APP_NAME with the app name used to apply for the license. Contact BytePlus Live technical support to get the app name.
    authInfo.channel = @"CHANNEL_NAME"; // Replace CHANNEL_NAME with the name of the channel through which to download the app. The default value is App Store.
    
    authInfo.vodLicensePath = [[NSBundle mainBundle] pathForResource:@"VOD_LICENSE_NAME" ofType:@"lic"]; // Replace VOD_LICENSE_NAME with the name of the VOD license file.
    authInfo.liveLicensePath = [[NSBundle mainBundle] pathForResource:@"LIVE_LICENSE_NAME" ofType:@"lic"];// Replace LIVE_LICENSE_NAME with the name of the live streaming license file.
    // Initialize the SDK. You must call this method after connecting to the network. You can get the license authorization result through the complete callback.    
    [[BDLiveManager sharedInstance] startWithAuthInfo:authInfo complete:^(BOOL allSuccess, NSString * _Nullable warningInfo, NSArray<NSError *> * _Nullable errors) {
        NSLog(@"BDLive 【allSuccess】 %d \n 【warningInfo】: %@ 【errors】:\n\n%@", allSuccess, warningInfo, errors);
    }];
}
```


Related method: [startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete)

<span id="8dba1063"></span>
### Step 5: Create the Activity required to join a live room

In the app target of Xcode, open the file that defines how to join and leave a live room and add the following code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can obtain the activity ID of the live room by calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2">CreateActivityAPIV2</a> or <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi">ListActivityAPI</a>, and obtain the authorization token required to join the live room by calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a>.</div>


```objectivec
#import <BPLive/BPLive.h>

BDLActivity *activity = [[BDLActivity alloc] init];
activity.activityId = @(ACTIVITY_ID); // Replace ACTIVITY_ID with the activity ID of the live room.
activity.token = @"TOKEN"; // Replace TOKEN with the authorization token required to join the live room.
activity.authMode = BDLActivityAuthModePublic; // The authentication mode of the live room. Here take the public mode as an example. Viewers can watch live streams, view comments, and perform other operations without logging in to the live room.
activity.isPortrait = YES; // Whether the live room is in portrait mode. Here take the portrait mode as an example.
```


<span id="ac793c6c"></span>
### Step 6: Join and leave the live room

In the app target of Xcode, open the file that defines how to join and leave the live room, and then add the relevant methods.

The following sample code shows the methods to join and leave the full\-featured live room.

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


<span id="762f64ce"></span>
## Optimizing the SDK package size

Starting from version 1.33.0, you can optimize the SDK package size by adding dependencies in the `Podfile` file in the following way. For more information, see [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed).

```Ruby
  # If you only integrate the Viewer SDK
  # The optimized SDK package excludes the feature of ultra-low latency live streaming.  
  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json', :subspecs => [
    'ViewerWithoutRTC', 
  ]
  # If you integrate both the Live Streaming SDK and Viewer SDK
  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json', :subspecs => [
    'LiveStreamingWithoutRTC',  #  The optimized SDK package excludes the feature of live streaming by sharing the screen.  
    'ViewerWithoutRTC',         #  The optimized SDK package excludes the feature of ultra-low latency live streaming.  
  ]
```


<span id="a8d75cca"></span>
## Package size

Here, the package size refers to:


* The incremental compressed IPA file size after integrating the SDK, calculated as the compressed IPA file size after SDK integration minus the size before SDK integration.

* The incremental uncompressed IPA file size after integrating the SDK, calculated as the uncompressed IPA file size after SDK integration minus the size before SDK integration.


The compressed IPA file size represents the download size of your app, while the uncompressed IPA file size corresponds to the size of the installed app on the device.

The actual uncompressed IPA file size on devices is smaller than the size listed in the following table, as only the resources applicable to the current device are kept during installation.

The following data is based on the app supporting only the arm64 CPU architecture.


|Version |Type |TTSDK library |Incremental compressed IPA file size |Incremental uncompressed IPA file size |Dependency |
|---|---|---|---|---|---|
|1.58.0 \- 1.59.0 |Viewer SDK |Dynamic library |About 47 MB |About 94.8 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0/BPLive.podspec.json'```<br> |
|||Static library |About 43.7 MB |About 79.1 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json'```<br> |
||Viewer SDK with optimized package size |Dynamic library |About 30.8 MB |About 64.7 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0/BPLive.podspec.json', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |
|||Static library |About 27.5 MB |About 49 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |
||Live Streaming SDK + Viewer SDK |Dynamic library |About 66 MB |About 139 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0/BPLive.podspec.json', :subspecs => [```<br>```    'LiveStreaming',```<br>```    'Viewer',```<br>```  ]```<br> |
|||Static library |About 61.5 MB |About 117 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json', :subspecs => [```<br>```    'LiveStreaming',```<br>```    'Viewer',```<br>```  ]```<br> |
||Live Streaming SDK with optimized package size + Viewer SDK with optimized package size |Dynamic library |About 53.2 MB |About 116 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0/BPLive.podspec.json', :subspecs => [```<br>```    'LiveStreamingWithoutRTC',```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |
|||Static library |About 48.8 MB |About 94.3 MB |```Ruby```<br>```  pod 'BPLive', :podspec => 'https://tos-sgcomm.byteisource.com/obj/live-activity/SDK/iOS/BPLive/1.59.0-static-ttsdk/BPLive.podspec.json', :subspecs => [```<br>```    'LiveStreamingWithoutRTC',```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |


The Live Streaming SDK with optimized package size excludes the screen sharing feature, while the Viewer SDK with optimized package size excludes the ultra\-low latency live streaming feature. For more information on adding dependencies, see [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed).

<span id="8eb179cc"></span>
## FAQ

[Viewer SDK for iOS FAQs](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-faqs)
