---
title: "Integrating the Viewer SDK for iOS (for versions earlier than 1.39.0)"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-ios"
---

The Viewer SDK enables your mobile app to include features such as watching a live stream, sending comments, and interacting with the host. This topic describes how to integrate the Viewer SDK into your iOS app.

<span id="Prerequisites"></span>
## Prerequisites


* Real devices or simulators running iOS 9.0 and above.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The simulator is only intended for interface debugging and does not guarantee the normal functioning of features such as audio, video, and picture\-in\-picture (PiP). To avoid issues like screen artifacts or black borders, we recommend that you use a physical device.   </div>
   

* Xcode. The latest version is recommended.

* CocoaPods. 1.11.0 or later versions are recommended. For more information, see [Getting Started with CocoaPods](https://guides.cocoapods.org/using/getting-started.html#getting-started).

* CPU architecture: armv7, arm64, or x86_64.

* Contact the sales representative to obtain the TTSDK license files for live streaming and VOD (Video\-on\-Demand), the app name used to apply for the TTSDK license, and the app ID returned after a successful application. If you do not have a sales representative, click [here](https://www.byteplus.com/en/contact) to fill in the form so that the BytePlus sales team can contact you later.


<span id="Integrating the SDK"></span>
## Integration steps

<span id="6fbbbde0"></span>
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
     # Starting from version 1.33.0, you can use ViewerWithoutRTC as podspec to optimize the SDK package size. This action, however, will still include all the available features. 
     pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.35.0/BPLive.podspec.json'
     # If you integrate both the Live Streaming SDK and Viewer SDK
     # Starting from version 1.33.0, you can replace LiveStreaming with LiveStreamingWithoutRTC to optimize the SDK package size. This action will provide you with an SDK package that excludes the feature of screen-sharing live streaming. Additionally, you can replace Viewer with ViewerWithoutRTC to also optimize the SDK package size. This action, however, will still include all the available features.
     pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.35.0/BPLive.podspec.json', :subspecs => [
       'LiveStreaming',
       'Viewer',
     ]
     # Add BPLive dependencies
     pod 'TTSDKFramework', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/TTSDKFramework/1.40.200.5-premium/TTSDKFramework.podspec'
     pod 'RangersAppLog', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/RangersAppLog/6.15.5/RangersAppLog.podspec.json'
     # Add this dependency only when you integrate both the Live Streaming SDK and Viewer SDK 
     pod 'TTVideoEditor', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/iOS/Byteplus/TTVideoEditor/11.8.1.83-D/TTVideoEditor.podspec'
   end  
   ```
   

2. Open a terminal window and run the command `cd` to navigate to your project's directory. Run the command `pod install` to install the dependencies.


<span id="ec95947b"></span>
#### Optimizing the SDK package size

Starting from version 1.33.0, you can optimize the SDK package size by adding dependencies in the `Podfile` file in the following way. For more information, see the preceding configurations in the `Podfile` file.

```Ruby
  # If you only integrate the Viewer SDK
  # The optimized SDK package still includes all the available features.  
  pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.35.0/BPLive.podspec.json', :subspecs => [
    'ViewerWithoutRTC', 
  ]
  # If you integrate both the Live Streaming SDK and Viewer SDK
  pod 'BPLive', :podspec => 'https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/BPLive/1.35.0/BPLive.podspec.json', :subspecs => [
    'LiveStreamingWithoutRTC',  #  The optimized SDK package excludes the feature of screen-sharing live streaming.  
    'ViewerWithoutRTC',         #  The optimized SDK package still includes all the available features.  
  ]
```


<span id="Setting up the environment"></span>
### Step 2: Configure the environment


1. Privacy statement. Add the following information in `Info.plist`:

   ```Plain
   NSPhotoLibraryAddUsageDescription // Permission to access the photo library album, used when viewers save pictures from the live room.
   SSAppID // AppID you get when applying license for your application
   ```
   

2. Set **Background** **Modes** to **Audio, AirPlay, and Picture in Picture** so that the application can continue to play audio and display picture in picture when it goes to the background.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6b63daa3f7ce4161d8afcd5e70174abd) </span>

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_7fd6ae6c785134bccfad7ec87483eb58) </span>


<span id="Initializing TTSDK"></span>
### Step 3: Initialize the TTSDKIdentifier


1. Add the TTSDK license to your project and initialize TTSDK:

   ```objectivec
   #import <TTSDKFramework/TTSDKManager.h>
   
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   
       [self initTTSDK];
       
       return YES;
   }
   
   - (void)initTTSDK { 
       TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"AppID"]; // The app ID returned after the successful TTSDK license application. Contact the sales representative to obtain the AppID 
       configuration.appName = @"AppName"; // The app name used to apply for the TTSDK license. Contact the sales representative to obtain the AppName 
       configuration.channel = @"App Store"; // The channel through which to download the app 
       configuration.bundleID = @"BundleID"; // The bundle identifier of the app 
        
       // Set the VOD license and live streaming license 
       // VOD license 
       configuration.licenseFilePath = [[NSBundle mainBundle] pathForResource:@"vodLicenseName" ofType:@"lic"]; // VOD license name 
       [TTSDKManager startWithConfiguration:configuration]; 
        
       // Live streaming license 
       configuration.licenseFilePath = [[NSBundle mainBundle] pathForResource:@"liveLicenseName" ofType:@"lic"]; // Live streaming license name 
       [TTSDKManager startWithConfiguration:configuration]; 
   }
   ```
   

2. TTSDK uses OpenGL ES to render video. To make sure your application can render the video correctly, call `stopOpenGLESActivity` to ensure that all OpenGL ES commands have finished executing before your application goes to the background, and call `startOpenGLESActivity` when the application returns to the foreground.

   ```objectivec
   
   - (void)applicationWillResignActive:(UIApplication *)application {
       [TTVideoEngine stopOpenGLESActivity]; // Video on Demand engine
       [TVLManager stopOpenGLESActivity];    // Live streaming engine
   }
   
   - (void)applicationDidBecomeActive:(UIApplication *)application {
       [TTVideoEngine startOpenGLESActivity];
       [TVLManager startOpenGLESActivity];
   }
   
   ```
   

3. If your project uses SceneDelegate, you also need to add the following code in SceneDelegate:

   ```objectivec
   - (void)sceneWillResignActive:(UIScene *)scene {
       [TTVideoEngine stopOpenGLESActivity]; // Video on Demand engine
       [TVLManager stopOpenGLESActivity];    // Live streaming engine
   }
   
   - (void)sceneDidBecomeActive:(UIScene *)scene {
       [TTVideoEngine startOpenGLESActivity];
       [TVLManager startOpenGLESActivity];
   }
   ```
   


<span id="Entering the live room"></span>
## Entering the live room

Call [joinLiveRoomWithActivity:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#joinliveroomwithactivity) to enter the live room.

```objectivec
#import <BPLive/BPLive.h>
- (void)joinLiveRoom {    
    BDLActivity *activity = [[BDLActivity alloc] init];
    activity.activityId = @(167808997736****); // The activity ID of the live room.
    activity.token = @"JQ****"; // The authorization token required to enter the live room. 
    activity.isPortrait = YES; // Specifies whether the live room is in portrait mode. In this example, the live room is in portrait mode.
    activity.authMode = BDLActivityAuthModePublic; // The authentication mode of the live room. In this example, the authentication mode is public. Viewers can watch a live stream and view comments without logging in.
    [[BDLLiveEngine sharedInstance] joinLiveRoomWithActivity:activity];
}
```


<span id="Leaving the live room"></span>
## Leaving the live room

Call [leaveLiveRoom](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#leaveliveroom) to make viewers leave the live room, for example, when they do not have sufficient viewing permissions.

```objectivec
#import <BPLive/BPLive.h>
- (void)leaveLiveRoom {
    [[BDLLiveEngine sharedInstance] leaveLiveRoom];
}
```
