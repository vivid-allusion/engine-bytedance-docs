---
title: "Integrating the Viewer SDK for iOS"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios"
---

To incorporate live streaming capabilities into your iOS application, such as watching live feeds, sending comments, and interacting with hosts, you can integrate the Viewer SDK. This guide provides comprehensive, step\-by\-step instructions covering everything from initial setup and dependency management to joining and leaving a live room, ensuring a smooth integration process.

## Prerequisites

* Real devices or simulators running iOS 12.0 and above. If you integrate the SDK using Swift Package Manager, use a real device or simulator running iOS 13.0 or later.

   > **说明**

   * > If you use an Apple Silicon Mac, the Rosetta simulator is required.

   * > The simulator is only intended for interface debugging and does not guarantee the proper functioning of features such as audio, video, and picture\-in\-picture (PiP). To avoid issues like screen artifacts or black borders, we recommend that you use a physical device.

* Xcode. The latest version is recommended.

* If you integrate the SDK with CocoaPods, 1.11.0 or later versions are recommended. For more information, see [Getting Started with CocoaPods](https://guides.cocoapods.org/using/getting-started.html#getting-started). If you integrate the SDK using Swift Package Manager, use swift\-tools\-version 5.9 or later.

* CPU architecture: arm64 or x86_64.

* Contact BytePlus Live technical support to obtain the live streaming license file and Video on Demand (VOD) license file, the app name used to apply for the license, and the app ID returned after a successful application.

## Integration steps

### Step 1: Add dependencies

You can integrate the SDK using either CocoaPods (Option 1) or Swift Package Manager (Option 2).

**Option 1: CocoaPods**

1. Open the `Podfile` file of your project to add dependencies.

   > **说明**

   > If your project does not already use CocoaPods, run the `pod init && pod install` command in the project's root directory to generate a `Podfile` file.

   ```Ruby
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   
   # Your app target name
   target 'XXXX' do
     # Starting from version 1.33.0, you can use ViewerWithoutRTC as podspec to optimize the SDK package size. This provides an SDK package that excludes the ultra-low latency live streaming feature. 
     pod 'BPLive', '1.66.1'
   end  
   ```

2. Open a terminal window and run the command `cd` to navigate to your project's directory. Run the command `pod install` to install the dependencies.

3. (Optional) Using the static library version of TTSDK

   By default, the dynamic library version of TTSDK is used. To use the static library version of TTSDK, append `-static-ttsdk` to the version number when adding dependencies. For more information, see the preceding configurations in the `Podfile` file.

   ```Ruby
   pod 'BPLive', '1.66.1-static-ttsdk'
   ```

**Option 2: Swift Package Manager**

You can integrate the SDK either through `Package.swift` or through the Xcode UI.

**Repository**:

SDK: [https://github.com/byteplus-sdk/BPLive_SPM](https://github.com/byteplus-sdk/BPLive_SPM)

**Option A: Integrate via Package.swift**

Add the BPLive_SPM dependency to your `Package.swift`, and import the corresponding libraries in the target(s) that need them. The following is an integration example for the Viewer SDK:

```Swift
// swift-tools-version: 5.9
import PackageDescription

let package = Package(
    name: "MyApp",
    platforms: [.iOS(.v13)],
    products: [
        .library(name: "MyApp", targets: ["MyApp"]),
    ],
    dependencies: [
        // Replace with your target version
        .package(url: "https://github.com/byteplus-sdk/BPLive_SPM.git", exact: "1.66.4")
    ],
    targets: [
        .target(
            name: "MyApp",
            dependencies: [
                // Base library and common component library
                .product(name: "BPLiveBaseLibrary", package: "BPLive_SPM"),
                .product(name: "BPLiveCommonLibrary", package: "BPLive_SPM"),
                // Viewer SDK. You can replace BPLiveViewerLibrary with BPLiveViewerWithoutRTCLibrary to optimize the SDK package size. BPLiveViewerWithoutRTCLibrary does not include the ultra-low latency live streaming feature.
                .product(name: "BPLiveViewerLibrary", package: "BPLive_SPM")
            ]
        ),
    ]
)
```

**Option B: Integrate in Xcode**

1. Open Xcode and select **File** \> **Add Package Dependencies…** .

2. Enter the repository URL `https://github.com/byteplus-sdk/BPLive_SPM`.

3. In the version rule, select the tagged target version (for example, **Exact Version: 1.66.4**).

4. In the library checklist, select the libraries related to the Viewer SDK and associate them with the corresponding target:

   * **BPLiveBaseLibrary**: Base library (required)

   * **BPLiveCommonLibrary**: Common component library (required)

   * **BPLiveViewerLibrary**: Viewer library

   * **BPLiveViewerWithoutRTCLibrary**: Viewer library without the ultra\-low latency live streaming feature

### Step 2: Configure the environment

In the app target of Xcode, complete the following steps:

1. Open the `info.plist` file, add the parameter `SSAppID`, and set the parameter's value to the app ID you received after your license application was approved.

2. In the `info.plist` file, add permissions in one of the following ways:

   * Click  **+**  to add the **Privacy \- Photo Library Additions Usage Description** and **Privacy \- Calendars Usage Description** keys. For each key, set **Type** to **String** and **Value** to the prompt message that you want to display in the system authorization dialog.

   * Open the `info.plist` file in source code mode and add the following keys and strings. You can customize the value of the string as the prompt message displayed in the system authorization dialog box.

      ```Plain
      <!-- Write access to photo library -->
      <key>NSPhotoLibraryAddUsageDescription</key> 
      <string>The app needs your permission to write to your photo library for saving images to the photo library</string>
      <!-- Write access to calendar -->
      <key>NSCalendarsUsageDescription</key>
      <string>Used to remind viewers before a live stream starts</string>
      ```

3. (Optional) If you need the app to continue playing audio when running in the background or need to use the Picture\-in\-Picture (PiP) feature, complete the following steps:

   1. Click  **+ Capability** under the **Signing & Capabilities** tab, and double\-click to add **Background Modes**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/147f155c322d4f6cba5c2f26c813f33b~tplv-goo7wpa0wc-image.image)

   2. In the **Background Modes** section, select the **Audio, AirPlay, and Picture in Picture** checkbox.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eefa3e63dd374db686c0b232547c944b~tplv-goo7wpa0wc-image.image)

4. (Optional) If your project is using Bitcode, you need to disable Bitcode.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/991f4357e3bb47579b6256340415e73d~tplv-goo7wpa0wc-image.image)

   1. Click the **Build Settings** tab.

   2. In the **Build Options** section, set **Enable Bitcode** to **No**.

5. Configure the screen orientation supported when playing live videos, previews, or playbacks in full\-screen mode.

   1. Click the **General** tab.

   2. In the **Deployment Info** section, select the **Portrait** and **Landscape Right** checkboxes for **iPhone Orientation** and **iPad Orientation**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab42c8820c0f4eee99fe655eb65c2ff6~tplv-goo7wpa0wc-image.image)

   > **说明**

   * > If you want viewers to be able to automatically rotate the screen left and right according to the device orientation in full\-screen mode, the following conditions must be met:

      * > The portrait orientation lock of the viewer's device is turned off. For instructions on how to turn off the portrait orientation lock, see the [official Apple documentation](https://support.apple.com/en-us/118226).

      * > Both **Landscape Left** and **Landscape Right** checkboxes are selected in the **Deployment Info** section.

   * > To prevent display issues with the full\-screen animation when viewers tap the full\-screen button, make sure to select the **Landscape Right** checkbox.

   * > To disable the full\-screen mode, you can hide the full\-screen button in the player with the following sample code. After disabling the full\-screen mode, you can only select the **Portrait** checkbox in the **Deployment Info** section.

   > `[BDLLiveEngine sharedInstance].liveRoomConfiguration.playerConfig.common.enterFullScreenEnable = NO;`

### Step 3: Import licenses

Add the live streaming license file and VOD license file to the app target in Xcode. Select **Copy items if needed**, and click **Finish**.

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
    authInfo.channel = @"CHANNEL_NAME"; // Replace CHANNEL_NAME with the name of the app's distribution channel. The default value is App Store.
    
    authInfo.vodLicensePath = [[NSBundle mainBundle] pathForResource:@"VOD_LICENSE_NAME" ofType:@"lic"]; // Replace VOD_LICENSE_NAME with the name of the VOD license file.
    authInfo.liveLicensePath = [[NSBundle mainBundle] pathForResource:@"LIVE_LICENSE_NAME" ofType:@"lic"];// Replace LIVE_LICENSE_NAME with the name of the live streaming license file.
    // Initialize the SDK. You must call this method after connecting to the network. You can get the license authorization result from the completion callback.    
    [[BDLiveManager sharedInstance] startWithAuthInfo:authInfo complete:^(BOOL allSuccess, NSString * _Nullable warningInfo, NSArray<NSError *> * _Nullable errors) {
        NSLog(@"BDLive 【allSuccess】 %d \n 【warningInfo】: %@ 【errors】:\n\n%@", allSuccess, warningInfo, errors);
    }];
}
```

Related method: [startWithAuthInfo:complete:](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine#BDLiveManager-startwithauthinfo-complete)

### Step 5: Create the Activity object required to join a live room

In the app target of Xcode, open the file that defines how to join and leave a live room and add the following code.

> **说明**

> You can obtain the activity ID of the live room by calling [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2) or [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi), and obtain the authorization token required to join the live room by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi).

```objectivec
#import <BPLive/BPLive.h>

BDLActivity *activity = [[BDLActivity alloc] init];
activity.activityId = @(ACTIVITY_ID); // Replace ACTIVITY_ID with the activity ID of the live room.
activity.token = @"TOKEN"; // Replace TOKEN with the authorization token required to join the live room.
activity.authMode = BDLActivityAuthModePublic; // The authentication mode of the live room. This example uses the public mode. Viewers can watch live streams, view comments, and perform other operations without logging in to the live room.
activity.isPortrait = YES; // Whether the live room is in portrait mode. This example uses portrait mode.
```

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

## Optimizing the SDK package size

Starting from version 1.33.0, you can optimize the SDK package size by adding dependencies in the `Podfile` file in the following way. For more information, see [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed).

```Ruby
  # The optimized SDK package excludes the ultra-low latency live streaming feature.  
  pod 'BPLive', '1.66.1-static-ttsdk', :subspecs => [
    'ViewerWithoutRTC', 
  ]
```

## Package size

Here, the package size refers to:

* The increase in the compressed IPA file size after SDK integration. This is calculated by subtracting the original file size from the new file size.

* The increase in the uncompressed IPA file size after SDK integration. This is calculated by subtracting the original file size from the new file size.

The compressed IPA file size represents the download size of your app, while the uncompressed IPA file size corresponds to the size of the installed app on the device.

The actual uncompressed IPA file size on devices is smaller than the size listed in the following table, as only the resources applicable to the current device are kept during installation.

The following data is based on the app supporting only the arm64 CPU architecture.

|Version |Type |TTSDK library |Incremental compressed IPA file size |Incremental uncompressed IPA file size |Dependency |
|---|---|---|---|---|---|
|1.58.0 \- 1.66.1 (Use 1.66.1 as an example in the dependency) |Viewer SDK |Dynamic library |About 47 MB |About 94.8 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1'```<br> |
|||Static library |About 43.7 MB |About 79.1 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1-static-ttsdk'```<br> |
||Viewer SDK with optimized package size |Dynamic library |About 30.8 MB |About 64.7 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |
|||Static library |About 27.5 MB |About 49 MB |```Ruby```<br>```  pod 'BPLive', '1.66.1-static-ttsdk', :subspecs => [```<br>```    'ViewerWithoutRTC',```<br>```  ]```<br> |

The Viewer SDK with optimized package size excludes the ultra\-low latency live streaming feature. For more information on adding dependencies, see [Step 1: Add dependencies](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-ios#b1a1a0ed).

## FAQ

[Viewer SDK for iOS FAQs](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-ios-faqs)
