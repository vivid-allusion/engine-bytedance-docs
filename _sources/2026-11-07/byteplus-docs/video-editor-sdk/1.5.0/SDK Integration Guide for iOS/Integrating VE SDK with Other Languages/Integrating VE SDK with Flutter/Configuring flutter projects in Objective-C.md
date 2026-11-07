---
title: "Configuring flutter projects in Objective-C"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-configuring-flutter-projects-in-objective-c"
---

This section describes how to quickly integrate BytePlus Video Editor SDK through configuring your iOS Flutter project using Objective\-C.

<span id="4b9a7f05"></span>
# Prerequisities

Before configuring Flutter projects using Objective\-C, you have to complete the following:


* Add the dependencies using Cocoapods. For details, refer to [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-dependencies-using-cocoapods).

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to the [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list).

* You have Android Studio installed on your system.

* You have Flutter version 3.16 or newer installed on your system.


<span id="e36a9df1"></span>
# Step 1: Adding iOS dependent resources

You can add your iOS dependent resources by following these steps.

<span id="7229363f"></span>
## Step 1.1: Navigate to the iOS project's file location


1. Open your Flutter iOS project in Android Studio.

2. Right\-click **iOS** \> **Open In** \> **Finder**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77bb7b01bbdd4d278520ab8b7f6178c1~tplv-goo7wpa0wc-image.image) </span>


The file opens on your device.

<span id="899f5400"></span>
## Step 1.2: Add the dependent files to the iOS project directory


1. Open the iOS Flutter demo file provided by the BytePlus Video Editor SDK team.

2. Add the following demo project files to the Flutter project's iOS folder: `EOExportUI`, `EOExportUI.podspec`, and `EOLocal Resources.bundle`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42039af8e6174b84920955f315921220~tplv-goo7wpa0wc-image.image) </span>

3. Add the following demo project files to the Flutter project iOS's Runner folder: `EffectOneModule.h` and `EffectOneModule.m`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d1a6d37514e4751ae1d71a0cb4416ab~tplv-goo7wpa0wc-image.image) </span>


<span id="122e615b"></span>
## Step 1.3: Add `podfile` files


1. Open a terminal window and navigate to the iOS directory of your Flutter project.

2. If you have not initialized CocoaPods for your iOS project, run the command:

   ```C#
   pod init     
      
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4224284c8cc46f09442d4e097d2aca0~tplv-goo7wpa0wc-image.image) </span>

   This adds a podfile to your iOS directory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fef2d63846684da6a7302859387f171f~tplv-goo7wpa0wc-image.image) </span>


<span id="730cb71c"></span>
## Step 1.4: Modify `podfile` files


1. Open the `Podfile` folder.

2. Add the resource address and pod configuration by using the following code:

   ```Dart
   source 'https://github.com/CocoaPods/Specs.git'
   source 'https://cdn.cocoapods.org/'
   source 'https://github.com/volcengine/volcengine-specs.git'
   
   install! 'cocoapods', :generate_multiple_pod_projects => true,
                         :deterministic_uuids => false,
   #                      :incremental_installation => true,
                         :preserve_pod_file_structure => true
                         
   $EFFECT_ONE_KEY = "EffectOneKit"
   ```
   

3. Add the dependency library resources by using the following code:

   ```Dart
   pod 'EOExportUI', :path => './'
   pod 'EffectOneKit', '1.0.0', :source => 'https://github.com/volcengine/volcengine-specs' 
   ```
   


The dependencies are added.

**Full sample code**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eeab6ce6e5bd46ceb315b9e77121a1bd~tplv-goo7wpa0wc-image.image) </span>

<span id="53cc9d9b"></span>
## Step 1.5: Execute the `pod install` command


1. Open a terminal window and navigate to the iOS directory of your Flutter project.

2. Execute the command: `pod install`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09873f87e6514b3e8fabdc715435d23e~tplv-goo7wpa0wc-image.image) </span>


The installation process starts.

<span id="84680ebd"></span>
# Step 2: Configuring iOS projects

You can configure your iOS project by following these steps.

<span id="5091e439"></span>
## Step 2.1: Configure `bundleid`


1. Open Xcode.

2. Navigate to the Runner tab of your iOS project.

3. Under the TARGETS section, click **Runner**.

4. Click **Signing & Capabilities**.

5. Modify the **Bundle Identifier** to the following: `com.volcengine.effectone.inhouse`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f1e52ddc6ba4d9fba69fea23049e1e4~tplv-goo7wpa0wc-image.image) </span>


<span id="648b280e"></span>
## Step 2.2: Add the Runner files into the iOS directory


1. Navigate to your iOS project's Runner.

2. Right\-click **Runner** \> **Add Files to "Runner"** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82a20247dcdb4fd68c122a0e4cd7e6be~tplv-goo7wpa0wc-image.image) </span>

3. In the iOS folder, select `EOLocalResources.bundle`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a346a62d8e11470e95fff95a2e3ca941~tplv-goo7wpa0wc-image.image) </span>

4. In the Runner folder, select `EffectOneModule.h` and `EffectOneModule.m`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9cf98fb48b446b4b465b356bd1c23b8~tplv-goo7wpa0wc-image.image) </span>

5. In the Added folders section, select **Create groups**.

6. In the Add to targets section, select **Runner**.

7. Click **Add**.

   The files are added to Runner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/101196e791e14ff08fe43dc0eac12df5~tplv-goo7wpa0wc-image.image) </span>


<span id="e38d37ce"></span>
## Step 2.3 Create communication channels with Flutter


1. In Android Studio, open the iOS project.

2. Add the following code to the `Appdelete.m` file:

   ```Dart
   UIViewController *vc = self.window.rootViewController;
       FlutterMethodChannel *channel = [FlutterMethodChannel methodChannelWithName:@"effectOne.flutter" binaryMessenger:vc];
       [channel setMethodCallHandler:^(FlutterMethodCall * _Nonnull call, FlutterResult  _Nonnull result) {
           if ([call.method isEqualToString:@"recoder"]) {
   
           } else if ([call.method isEqualToString:@"draft"]) {
               
           }
           result(FlutterMethodNotImplemented);
       }];
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85fa1a8cb7b44ce792759a7578dac2b8~tplv-goo7wpa0wc-image.image) </span>


<span id="2eaf0ae0"></span>
## Step 2.4: Implement authentication and call camera and draft box features


1. In Android Studio, open your iOS project.

2. Add the following code to your project:


```objectivec
- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self.effectOneModule makeAuth];
    UIViewController *vc = self.window.rootViewController;
    FlutterMethodChannel *channel = [FlutterMethodChannel methodChannelWithName:@"effectOne.flutter" binaryMessenger:vc];
    [channel setMethodCallHandler:^(FlutterMethodCall * _Nonnull call, FlutterResult  _Nonnull result) {
        if ([call.method isEqualToString:@"recoder"]) {
            [self.effectOneModule showRecorderViewController];
        } else if ([call.method isEqualToString:@"draft"]) {
             [self.effectOneModule showDraftViewController];
        }
        result(FlutterMethodNotImplemented);
    }];
    [GeneratedPluginRegistrant registerWithRegistry:self];
    // Override point for customization after application launch.
    return [super application:application didFinishLaunchingWithOptions:launchOptions];
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e04f8c89e63e4ab78a2780f2bc60137a~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure that the channel name is the same as the channel name in your Flutter project, which in this case is <code>effectOne.flutter</code>.</div>


<div data-tips="true" data-tips-type="tip"><strong>Flutter project:</strong></div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6587684fc26444cfba653b61eae643cc~tplv-goo7wpa0wc-image.image" width="449px" /></div>


<div data-tips="true" data-tips-type="tip"><strong>Android Studio:</strong></div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f153628dca224ef0990301b01c62d06a~tplv-goo7wpa0wc-image.image" width="449px" /></div>


**Full sample code:** 

```objectivec
#import "AppDelegate.h"
#import "GeneratedPluginRegistrant.h"
#import "EffectOneModule.h"


@interface AppDelegate ()
@property (nonatomic, strong) EffectOneModule *effectOneModule;
@end

@implementation AppDelegate

- (EffectOneModule *)effectOneModule {
    if (!_effectOneModule) {
        _effectOneModule = [[EffectOneModule alloc] initWithParentVC:self.window.rootViewController];
    }
    return _effectOneModule;
}
 
- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [self.effectOneModule makeAuth];
    UIViewController *vc = self.window.rootViewController;
    FlutterMethodChannel *channel = [FlutterMethodChannel methodChannelWithName:@"effectOne.flutter" binaryMessenger:vc];
    [channel setMethodCallHandler:^(FlutterMethodCall * _Nonnull call, FlutterResult  _Nonnull result) {
        if ([call.method isEqualToString:@"recoder"]) {
            [self.effectOneModule showRecorderViewController];
        } else if ([call.method isEqualToString:@"draft"]) {
             [self.effectOneModule showDraftViewController];
        }
        result(FlutterMethodNotImplemented);
    }];
    [GeneratedPluginRegistrant registerWithRegistry:self];
    // Override point for customization after application launch.
    return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

@end
```


<span id="0501e2f2"></span>
## Step 2.5: Configuring permissions

To configure access permissions for the camera, microphone, and photo library in your project's `Info.plist` file, follow these steps:

```objectivec
//Whether you allow the app to access your music library 
NSAppleMusicUsageDescription  
mediastring>//Write your own media description
//Whether you allow the app to access your camera
NSCameraUsageDescriptionkey>
Camerastring>//Write your own camera description
//Whether you allow the app to access your microphone
NSMicrophoneUsageDescriptionkey>
micstring>//Write your own description
//Whether you allow the app to access your photo library.
NSPhotoLibraryAddUsageDescriptionkey>    
photo libstring>//write your own description
//Whether you allow the app to access your photo library
NSPhotoLibraryUsageDescriptionkey>
photostring>//write your description
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dd74006911f4bcd8c123ce34dccb1a0~tplv-goo7wpa0wc-image.image) </span>

The configuration process is completed. You can now run your Flutter project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ed0fa6a8d6f443c910779efe829df81~tplv-goo7wpa0wc-image.image) </span>
