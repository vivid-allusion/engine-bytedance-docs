---
title: "Integrating the Viewer SDK for iOS (for versions 1.39.0 - 1.48.0)"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios-1-39-0-1-48-0"
---

The Viewer SDK enables your mobile app to include features such as watching a live stream, sending comments, and interacting with the host. This topic describes how to integrate the Viewer SDK into your iOS app.

<span id="26ac4150"></span>
## Prerequisites


* Real devices or simulators running iOS 11.0 and above.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you use an Apple Silicon Mac, the Rosetta simulator is required.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The simulator is only intended for interface debugging and does not guarantee the normal functioning of features such as audio, video, and picture\-in\-picture (PiP). To avoid issues like screen artifacts or black borders, we recommend that you use a physical device.   </div>
   

* Xcode. The latest version is recommended.

* CocoaPods. 1.11.0 or later versions are recommended. For more information, see [Getting Started with CocoaPods](https://guides.cocoapods.org/using/getting-started.html#getting-started).

* CPU architecture: arm64 or x86_64.

* Contact BytePlus Live technical support to obtain the live streaming license file and Video on Demand (VOD) license file, the app name used to apply for the license, and the app ID returned after a successful application.


<span id="3930f42e"></span>
## Integration steps

<span id="8132f984"></span>
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
     pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.48.0/BPLive.podspec.json'
     # If you integrate both the Live Streaming SDK and Viewer SDK
     # Starting from version 1.33.0, you can replace LiveStreaming with LiveStreamingWithoutRTC to optimize the SDK package size. This action will provide you with an SDK package that excludes the feature of live streaming by sharing the screen. Additionally, you can replace Viewer with ViewerWithoutRTC to also optimize the SDK package size. This action will provide you with an SDK package that excludes the feature of ultra-low latency live streaming.
     pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.48.0/BPLive.podspec.json', :subspecs => [
       'LiveStreaming',
       'Viewer',
     ]
     # Add BPLive dependencies
     pod 'RangersAppLog', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/RangersAppLog/6.16.2/RangersAppLog.podspec.json'
     pod 'TTNetworkManager', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/TTNetworkManager/4.1.127.42/TTNetworkManager.podspec'
     # Add this dependency only when you integrate both the Live Streaming SDK and Viewer SDK 
     pod 'TTVideoEditor', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/TTVideoEditor/11.8.1.83-D/TTVideoEditor.podspec'
   end  
   ```
   

2. Open a terminal window and run the command `cd` to navigate to your project's directory. Run the command `pod install` to install the dependencies.


<span id="1d00b584"></span>
#### Using the static library version of TTSDK

By default, the dynamic library version of TTSDK is used. To use the static library version of TTSDK, follow these steps:


1. When adding dependencies, append `-static-ttsdk` to the version number. For more information, see the preceding configurations in the `Podfile` file.

   ```Ruby
     # If you only integrate the Viewer SDK
     pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.48.0-static-ttsdk/BPLive.podspec.json'
   
     # If you integrate both the Live Streaming SDK and Viewer SDK  
     pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.48.0-static-ttsdk/BPLive.podspec.json', :subspecs => [
       'LiveStreaming',
       'Viewer',
     ]
   ```
   

2. When initializing TTSDK, replace `#import <TTSDKFramework/TTSDKManager.h>` with `#import <TTSDK/TTSDKManager.h>`. For more information, see [Step 4: Initialize TTSDK](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#f951ba1a).


<span id="8672ca00"></span>
### Step 2: Configure the environment

In the app target of Xcode, complete the following steps:


1. Open the `info.plist` file, add the parameter `SSAppID`, and set the parameter value as the app ID returned after the successful license application.

2. In the `info.plist` file, add permissions in one of the following ways:

   * Click  **+**  to add **Privacy \- Photo Library Additions Usage Description** and **Privacy \- Calendars Usage Description** as **Key**, select **String** as **Type**, and then enter the prompt message displayed in the system authorization dialog box as **Value**.

   * Open the `info.plist` file in source code mode and add the following keys and strings. You can customize the value of the string as the prompt message displayed in the system authorization dialog box.

      ```Plain
      <!-- Write access to photo library -->
      <key>NSPhotoLibraryAddUsageDescription</key> 
      <string>The app needs your permission to write to your photo library for saving images to the photo library</string>
      <!-- Write access to calendar -->
      <key>NSCalendarsUsageDescription</key>
      <string>Used to remind viewers before live stream starts</string>
      ```
      

3. (Optional) If you need the app to continue playing audio when running in the background or need to use the Picture\-in\-Picture (PiP) feature, complete the following steps:

   1. Click  **+ Capability** under the **Signing & Capabilities** tab, and double\-click to add **Background Modes**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/147f155c322d4f6cba5c2f26c813f33b~tplv-goo7wpa0wc-image.image) </span>

   2. In the **Background Modes** section, select the **Audio, AirPlay, and Picture in Picture** checkbox.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eefa3e63dd374db686c0b232547c944b~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) If your project is using Bitcode, you need to disable Bitcode.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/991f4357e3bb47579b6256340415e73d~tplv-goo7wpa0wc-image.image) </span>

   1. Click the **Build Settings** tab.

   2. In the **Build Options** section, set **Enable Bitcode** to **No**.

5. Configure the screen orientation supported when playing live videos, previews, or playbacks in full\-screen mode.

   1. Click the **General** tab.

   2. In the **Deployment Info** section, select the **Portrait** and **Landscape Right** checkboxes for **iPhone Orientation** and **iPad Orientation**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab42c8820c0f4eee99fe655eb65c2ff6~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want viewers to be able to automatically rotate the screen left and right according to the device orientation in full\-screen mode, the following conditions must be met:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The portrait orientation lock of the viewer's device is turned off. For how to turn off the portrait orientation lock, see the <a href="https://support.apple.com/en-us/118226">official Apple documentation</a>.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Both <strong>Landscape Left</strong> and <strong>Landscape Right</strong> checkboxes are selected in the <strong>Deployment Info</strong> section.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To avoid abnormal display of the full\-screen animation after viewers tap the full\-screen button, make sure to select the <strong>Landscape Right</strong> checkbox.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To disable the full\-screen mode, you can hide the full\-screen button in the player with the following sample code. After disabling the full\-screen mode, you can only select the <strong>Portrait</strong> checkbox in the <strong>Deployment Info</strong> section.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>[BDLLiveEngine sharedInstance].liveRoomConfiguration.playerConfig.common.enterFullScreenEnable = NO;</code>   </div>
   


<span id="21eabdfd"></span>
### Step 3: Import licenses

Add the live streaming license file and VOD license file to the app target in Xcode. Select **Copy items if needed**, and click **Finish**.

<span id="b53627a3"></span>
### Step 4: Initialize TTSDK

In the app target of Xcode, open the `AppDelegate.m` file to initialize TTSDK:

```objectivec
// To use the static library version of TTSDK, replace #import <TTSDKFramework/TTSDKManager.h> with #import <TTSDK/TTSDKManager.h>.
#import <TTSDKFramework/TTSDKManager.h> 

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self initTTSDK];
    return YES;
}

- (void)initTTSDK {
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"APP_ID"]; // Replace APP_ID with the app ID returned after the successful license application. Contact BytePlus Live technical support to obtain the app ID.
    configuration.appName = @"APP_NAME"; // Replace APP_NAME with the app name used to apply for the license. Contact BytePlus Live technical support to obtain the app name.
    configuration.channel = @"CHANNEL_NAME"; // Replace CHANNEL_NAME with the name of the channel through which to download the app, such as App Store.
    configuration.bundleID = @"BUNDLE_ID"; // Replace BUNDLE_ID with the bundle identifier of the app.
    
    // Set the VOD license and live streaming license respectively
    // VOD license 
    configuration.licenseFilePath = [[NSBundle mainBundle] pathForResource:@"VOD_LICENSE_NAME" ofType:@"lic"]; // Replace VOD_LICENSE_NAME with the name of VOD license file
    configuration.bizType = TTSDKServiceBizType_All & ~TTSDKServiceBizType_Live;
    [TTSDKManager startWithConfiguration:configuration];
    
    // Live streaming license 
    configuration.licenseFilePath = [[NSBundle mainBundle] pathForResource:@"LIVE_LICENSE_NAME" ofType:@"lic"]; // Replace LIVE_LICENSE_NAME with the name of live streaming license file
    configuration.bizType = TTSDKServiceBizType_Live;
    [TTSDKManager startWithConfiguration:configuration];
}
```


<span id="819e74e3"></span>
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


<span id="f9ae5b08"></span>
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


<span id="b26f458a"></span>
## Optimizing the SDK package size

Starting from version 1.33.0, you can optimize the SDK package size by adding dependencies in the `Podfile` file in the following way. For more information, see [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed).

```Ruby
  # If you only integrate the Viewer SDK
  # The optimized SDK package excludes the feature of ultra-low latency live streaming.  
  pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.48.0/BPLive.podspec.json', :subspecs => [
    'ViewerWithoutRTC', 
  ]
  # If you integrate both the Live Streaming SDK and Viewer SDK
  pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.48.0/BPLive.podspec.json', :subspecs => [
    'LiveStreamingWithoutRTC',  #  The optimized SDK package excludes the feature of live streaming by sharing the screen.  
    'ViewerWithoutRTC',         #  The optimized SDK package excludes the feature of ultra-low latency live streaming.  
  ]
```


<span id="ff4b157e"></span>
## FAQ

[Viewer SDK for iOS FAQs](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-faqs)
