---
title: "Integrating VE SDK with UI—iOS (Lite)"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-ios-ve-sdk-lite--v.4.0.2"
---

This guide demonstrates how to integrate BytePlus Video Editor SDK into your iOS (Lite) application. With this UI\-inclusive integration method, you can utilize a variety of UI packages included in our CKOne sample code. This approach also enables you to directly use the majority of the sample code in your iOS project, eliminating the need to write the video editing UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus Video Editor SDK is also referred to as CKOne or CK in the SDK file and sample code.</div>


<span id="e7ec5425"></span>
# **Prerequisites**

Before you begin, ensure that that the following requirements are met:


* Your Xcode must be in version 9 or later.

* Your application is intended for devices that are iOS 9.0 or later.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Debugging using a simulator is not supported yet.</div>


<span id="1192cc21"></span>
# **CKOne sample code**

The CKOne sample code is required for the UI\-inclusive integration method for iOS (Lite). In this section, you will learn more about the sample code directory structure and SDK architecture, which will help you understand how to integrate and use Video Editor SDK in your own application.

To obtain the CKOne sample file, please contact the BytePlus Video Editor SDK team.

<span id="38956e4c"></span>
## CKOne sample code directory structure

The CKOne sample code package consists of two folders:


* **CK**: Contains the Video Editor SDK.

* **CKOne\-iOS**: Contains a demo project with the Video Editor SDK integrated. The demo project serves as a reference and can be removed during SDK integration for your project.


The following part shows the directory structure of CKOne sample code after decompression:

```Plain
├── CK
│   ├── CKEditor [SDK initialization]
│   ├── CKRRecorder [Recording/Duet]
│   ├── CKResource [Collection of algorithm resource, assets, and licenses]
│   ├── CKi18n [Content for global users]
│   ├── DVEFoundationKit [Common basic classes]
│   ├── DVETrackKit[Track area in the editor]
│   └── NLEEditor-iOS [Editor module]
└── CKOne-iOS [Integration example]
    ├── CKOBase [Common classes]
    ├── CKOBusiness [Business]
    ├── CKOEditor [Example of redirecting to the editor]
    ├── CKOLog [Log implementation example]
    ├── CKORecord [Example of redirecting to the recording page]
    └── CKOne [Shell project and storage place of Podfile]
```


<span id="19c34fe8"></span>
## Video Editor SDK architecture

Video Editor SDK is stored in the CK folder in the sample code package and contains the following key components:


|**Name** |**Description** |
|---|---|
|CKEditor |The entry point for SDK initialization. |
|CKResource |Contains resources, which will be packaged and added to the main bundle in your application. |
|CKRRecorder |The recording and duet module. |
|NLEEditor\-iOS |The editor module. |
|DVETrackKit |The track area for the editor. |
|DVEFoundationKit |Contains some common basic classes. |


Here's a simplified diagram that illustrates the basic architecture of Video Editor SDK.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cf74cbc7bd04b1a8b42e617288703b8~tplv-goo7wpa0wc-image.image" width="522px" /></div>


<span id="d39873c2"></span>
### CKResource

CKResource contains various resources, such as stickers, filters, and beauty effects. These resources are not included with Video Editor SDK and need to be purchased separately. If you would like to obtain these resources, you can contact the BytePlus Video Editor SDK team.

The following part describes the resource bundles stored in `CK/CKResource/CKResource/Resource`.

```SQL
├── Editor [Editing of related resources]
│   ├── adjust.bundle [Adjust]
│   ├── bubble.bundle [Bubble]
│   ├── canvas.bundle [Canvas]
│   ├── chroma.bundle [Chroma Key]
│   ├── curve_speed.bundle [Curve Speed]
│   ├── flower.bundle [Flourish]
│   ├── mix.bundle [Mixing Mode]
│   ├── smooth_speed.bundle [Smooth Speed]
│   ├── sticker.bundle [Sticker]
│   ├── sticker_animation.bundle [Sticker Animation]
│   ├── text_align.bundle [Text - Style - Arrange]
│   ├── text_animation.bundle [Text Animation]
│   ├── text_color.bundle [Text - Style - Background Color]
│   ├── text_fonts.bundle [Text - Style - Font]
│   ├── text_style.bundle [Text -Style - Style]
│   ├── text_template.bundle [Text Template]
│   ├── tone.bundle [Tone]
│   ├── transitions.bundle [Transition]
│   ├── ve_effect.bundle [Effect]
│   ├── ve_filter.bundle [Filter]
│   ├── video_animation.bundle [Video Animation]
│   ├── video_mask.bundle [Mask]
│   └── voice.bundle [TTS - Voice Selection]
├── License
│   └── com.bytedance.solution.ck.licbag [License]
├── Local [Unencrypted common resources]
│   ├── default.bundle
│   ├── en.lproj [Multi-language content - English]
│   ├── music.bundle
│   ├── sound.bundle
│   └── zh-Hans.lproj [Multi-language content - Chinese]
└── Record[Resources used by recording]
    ├── ComposeMakeup.bundle [Beauty Effects]
    ├── FilterResource.bundle [Filter]
    ├── StickerResource.bundle [Sticker]
    └── duet.bundle [Duet]
    └── ModelResource.bundle [Algorithm model, which is required for recording and editing. Various folders exist according to available features.]
```


<span id="98d75abb"></span>
# Getting started with Video Editor SDK

Get started with Video Editor SDK by completing the following tasks:


1. (Optional) Running the demo project.

2. Integrating Video Editor SDK.

3. Initializing Video Editor SDK.

4. Starting the UI interface.


<span id="cd37a176"></span>
# Running the demo project

Before you begin integration, you can run the CKOne\-iOS demo project on your own device to learn more about the Video Editor SDK features and its UI.

To run the demo project:


1. Download and decompress CKOne sample code.

2. In Terminal, run the following commands to open the demo project.

   ```Bash
   cd CKOne-iOS/CKOne
   pod update
   open CKOne.xcworkspace
   ```
   

3. In Xcode, go to **TARGETS** \> **CKOne** \> **Signing & Capabilities** \> **Signing**.

4. Replace the certificate with your own developer certificate.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfc3be5ab8d1438a9826b9d7f1bf9b14~tplv-goo7wpa0wc-image.image) </span>

5. Select a real device.

6. Click the play icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e2d3c69727c457fab624f55635e9196~tplv-goo7wpa0wc-image.image" width="1000px" />   </div>
   


The demo project now runs on your device.

<span id="166ae2e9"></span>
# Integrating Video Editor SDK

Integrate Video Editor SDK into your iOS application by completing the following steps:


1. Copying the sample code.

2. (Optional) Deleting SceneDelegate.

3. (Optional) Configuring Podfile.

4. Configuring project settings.

5. Modifying the license.

6. Replacing resources.


<span id="b948e2f2"></span>
## Step 1: Copying the sample code to your project.

Copy the CK folder from the CKOne sample code package into your project directory.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9d86ca72bf544f38206143e505252fb~tplv-goo7wpa0wc-image.image" width="550px" /></div>


<span id="53602372"></span>
## Step 2: (Optional) Deleting SceneDelegate

If your project contains `SceneDelegate`, it needs to be deleted from your project directory.

**To delete SceneDelegate**:


1. Navigate to your project directory.

2. Delete `SceneDelegate.h` and `Scenedelegate.m`.

3. In `AppDelegate`, comment on or delete the callbacks related to `UISceneSession`.

   **EXAMPLE**

   ```objectivec
   #pragma mark - UISceneSession lifecycle
    
   //
   //- (UISceneConfiguration *)application:(UIApplication *)application configurationForConnectingSceneSession:(UISceneSession *)connectingSceneSession options:(UISceneConnectionOptions *)options {
   //    // Called when a new scene session is being created.
   //    // Use this method to select a configuration to create the new scene with.
   //    return [[UISceneConfiguration alloc] initWithName:@"Default Configuration" sessionRole:connectingSceneSession.role];
   //}
   //
   //
   //- (void)application:(UIApplication *)application didDiscardSceneSessions:(NSSet<UISceneSession *> *)sceneSessions {
   //    // Called when the user discards a scene session.
   //    // If any sessions were discarded while the application was not running, this will be called shortly after application:didFinishLaunchingWithOptions.
   //    // Use this method to release any resources that were specific to the discarded scenes, as they will not return.
   //}
   ```
   

4. In`Info.plist`, click the minus icon to delete the Application Scene Manifest.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1374fe1c40af4c4db2635830d4462513~tplv-goo7wpa0wc-image.image" width="550px" /></div>



5. In `AppDelegate.m`, create a new window and set `UINavigationController`.

   **EXAMPLE**

   ```objectivec
   @interface AppDelegate : UIResponder <UIApplicationDelegate>
   @property (nonatomic, strong) UIWindow *window;
   @end
   
   
   // AppDelegate.m
   #import "ViewController.h"
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
       UIWindow *window = [[UIWindow alloc] init];
       UIViewController *mainVC = [[ViewController alloc] init];
       UINavigationController *navigationController = [[UINavigationController alloc] initWithRootViewController:mainVC];
       [navigationController setNavigationBarHidden:YES];
       window.rootViewController = navigationController;
       [window makeKeyAndVisible];
       UIApplication.sharedApplication.delegate.window = window;
       return YES;
   }
   ```
   


<span id="3c837385"></span>
## Step 3: (Optional) Configuring Podfile

If your project doesn't contain a Podfile, you need to include it in your project directory, so as to manage the dependencies used in your project.

**To obtain a Podfile**:


1. Run pod init in the directory containing your project's `.xcodeproj`.

2. To modify your Podfile, add the following configurations:

   ```Ruby
   source 'https://cdn.cocoapods.org/'
   
   platform:ios, '9.0'
   
   # Common pods
   def base_pods
     pod 'TTVideoEditor', '11.8.1.36-D',:source => 'https://github.com/volcengine/volcengine-specs.git'
     pod 'NLEPlatform', '0.5.2', :source => 'https://github.com/volcengine/volcengine-specs.git'
     pod 'DVEInject', '0.0.5', :source => 'https://github.com/volcengine/volcengine-specs.git'
   end
   
   # Editing pods
   def editor_pods
     #During the integration, invoke the relative paths based on project situations.
     pod 'NLEEditor', :subspecs => ['CK'], :path => '../NLEEditor-iOS'
     pod 'DVETrackKit', :subspecs => ['CK'], :path => '../DVETrackKit'
     pod 'DVEFoundationKit', :subspecs => ['CK'], :path => '../DVEFoundationKit'
     pod 'CKEditor', :path => '../CKEditor'
     
     ################################### Third-party pods ###################################
     pod 'SGPagingView', '1.7.1'
     pod 'KVOController','1.2.0'
     pod 'Masonry','1.1.0'
     pod 'ReactiveObjC', '3.1.1'
     pod 'YYWebImage', '1.0.5'
     pod 'YYImage', '1.0.4'
     pod 'YYModel', '1.0.4'
     pod 'MBProgressHUD', '1.2.0'
     pod 'lottie-ios', '2.5.3'
     pod 'SDWebImage', '5.11.1'
     pod 'Toast', '4.0.0'
     pod 'MJExtension'
     pod 'MJRefresh', '3.6.1'
     pod 'PocketSVG', '2.7.0'
     pod 'IGListKit', '4.0.0'
     pod 'IGListDiffKit', '4.0.0'
     pod 'FileMD5Hash'
   end
   
   # Recording pods
   def recorder_pods
       pod 'CKRRecorder', :subspecs => ['Arch'], :path => '../CKRRecorder'
   end
   
   # Replace 'Demo' with your own project target.
   target 'Demo' do
     base_pods
     # Basic editing & recording pods
     editor_pods
     recorder_pods
   end
   ```
   

3. Run pod update.


For more information about Podfile, refer to the Podfile file in`CKOne-iOS/CKOne` in the sample code package.

<span id="9f2dac8f"></span>
## Step 4: Configuring project settings

To allow Video Editor SDK to run properly on your device, you need to configure project settings.

**To configure project settings**:


1. In Xcode, go to **TARGETS** \> **Project Name** \> **Build Settings** \> **Build Options**.

2. Set **Enable Bitcode** to **No**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a4571440f4b4bb587c9c4193a72b19e~tplv-goo7wpa0wc-image.image" width="791px" />   </div>
   

3. Open `Info.plist` as a source code and add your desired permission description.

   **EXAMPLE**

   ```XML
           <key>NSCameraUsageDescription</key>
           <string><!--Fill in resource permission description. For example, "Allow XXX to use your camera?"--></string>
           <key>NSMicrophoneUsageDescription</key>
           <string><!--Fill in resource permission description. For example, "Allow XXX to use your microphone?"--></string>
           <key>NSPhotoLibraryAddUsageDescription</key>
           <string><!--Fill in resource permission description. For example, "Allow XXX to access your photo library?"--></string>
           <key>NSPhotoLibraryUsageDescription</key>
           <string><!--Fill in resource permission description. For example, "Allow XXX to access your photo library?"--></string>
   ```
   

   \*\*OR \*\*

   Open `Info.plist` as a property list and click the **Add** icon to add a resource permission description.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eb734d873fe47ea86da86b8de9764d7~tplv-goo7wpa0wc-image.image" width="791px" />   </div>
   

   The following table details the resource permission descriptions for `info.plist`:

   
   |**Permission Name** |**Key** |**Type** |
   |---|---|---|
   |Privacy – Camera Usage Description |NSCameraUsageDescription |String |
   |Privacy – Microphone Usage Description |NSMicrophoneUsageDescription |String |
   |Privacy – Photo Library Additions Usage Description |NSPhotoLibraryAddUsageDescription |String |
   |Privacy – Photo Library Usage Description |NSPhotoLibraryUsageDescription |String |
   


<span id="1012d6ca"></span>
## **Step 5: Modifying the license**

Each SDK license is bound to the app's Bundle ID and uses `.licbag` as its extension. For example, the license for the demo project is `com.bytedance.solution.ck.licbag`, which corresponds to the demo project's Bundle ID.

To get your SDK license, please contact the BytePlus Video Editor SDK team.

**To modify the license**:


1. Remove the default SDK license `com.bytedance.solution.ck.licbag`stored in `CK/CKResource/CKResource/Resource/License`.

2. Change the name of your SDK license to match your app's Bundle ID.

3. Add your SDK license to your project.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The license file is usually stored in the default location <code>CK/CKResource/CKResource/Resource/License</code>. For better use of the Video Editor SDK, you can also store the file in an accessible filepath, such as the main bundle or the sandbox directory.</div>


<span id="528a3b91"></span>
## Step 6: Replacing resources

In `CK/CKResource/CKResource/Resource`, replace the resources with your own resources. After the resources in CKResource are packaged, they will be added to the main bundle.

<span id="6dd2be13"></span>
# Initializing Video Editor SDK

Once Video Editor SDK has been integrated, you can initialize it to begin using its functions. Initialize Video Editor SDK by completing the following steps:


1. Setting veLicensePath.

2. Configuring parameters.

3. Initializing Video Editor SDK.


<span id="4426e83a"></span>
## Step 1: Setting veLicensePath

If the license file is not located in `CK/CKResource/CKResource/Resource/License`, set `CKEditorEngineConfig.veLicensePath` based on the actual filepath before you begin initialization.

**EXAMPLE**

```objectivec
#import <CKEditor/CKEditor.h>

+ (void)setupEditorEngine {
    CKEditorEngineConfig *c = [CKEditorEngineConfig defaultConfig];
    NSBundle *bundle = [NSBundle mainBundle];
    NSString *licensePath = [bundle pathForResource:@"YourBundleID.licbag" ofType:@""];
    c.veLicensePath = licensePath;
    
     // ...
    [CKEditorEngine.shared startWithConfig:c];
}
```


<span id="b61f8d75"></span>
## Step 2: Configuring parameters

Configure `CKEditorEngineConfig` parameters, such as the SDK credentials. If you require any additional features, contact the BytePlus Video Editor SDK team to obtain the relevant parameters.

The description of `CKEditorEngineConfig` parameters is as follows:


|**Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|isOverSea |Boolean |No |Optional. Indicates whether the SDK is for users outside Mainland China. Valid values include:<br><br><br>* true—for users outside Mainland China.<br><br>* false—for users inside Mainland China.<br><br><br>The default value is false. |
|veLicensePath |String | |License filepath. By default, the code will read the license file in CKResource based on the Bundle ID. If no license can be read there, this parameter is required. |
|veAppKey |String |Yes |License key. |
|veToken |String | |License token. Depending on the purchased features, this parameter is required. |
|volcAccessKey |String |No |Access key for the music beat feature. |
|volcSecretKey |String |No |Secret key for the music beat feature. |
|subtitleAppId |String |No |AppKey for features such as text\-to\-speech (TTS) and text recognition. |
|subtitleToken |String |No |Token for features such as text\-to\-speech (TTS) and text recognition. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the credentials for volcAccessKey, volcSecretKey, subtitleAppId, and subtitleToken are not available, you do not need to assign any values. However, you can only use their features if the credentials have been assigned.</div>


<span id="6d11fc31"></span>
## Step 3: Initializing Video Editor SDK

Initialize your SDK using the following code:

**EXAMPLE**

```objectivec
#import <CKEditor/CKEditor.h>

+ (void)setupEditorEngine {    
     // ...
    [CKEditorEngine.shared startWithConfig:c];
}
```


<span id="2c576999"></span>
### SDK initialization full sample code

Refer to the full sample code below to learn how to initialize Video Editor SDK for iOS.

**EXAMPLE**

```objectivec
#import <CKEditor/CKEditor.h>

+ (void)setupEditorEngine {
    CKEditorEngineConfig *c = [CKEditorEngineConfig defaultConfig];
    // Uncomment the following code to set veLicensePath
//    NSBundle *bundle = [NSBundle mainBundle];
//    NSString *licensePath = [bundle pathForResource:@"com.bytedance.solution.ck.licbag" ofType:@""];
//    c.veLicensePath = licensePath;
    
    c.veAppKey = @"";
    c.veToken = @"";
    
    /// Depending on the features you require, contact the BytePlus Video Editor SDK team to obtain the following parameters.
    // c.subtitleAppId = @"";
    // c.subtitleToken = @"";
    // c.volcAccessKey = @"";
    // c.volcSecretKey = @"";

    [CKEditorEngine.shared startWithConfig:c];
}
```


<span id="cebd9cb7"></span>
# Starting the UI interface

Once Video Editor SDK has been initialized, you can start the UI interface and begin using its functions. This section provides methods for calling the editing, recording, duet, and draft box pages.

<span id="d4b61601"></span>
## **Editing page**

Call the editing page using the following code.

```objectivec
#import <CKEditor/CKEditor.h>

[CKEditorEngine.shared toStandarMultiTrackEditor];
```


After you call the editing feature, an image selection window appears. In the window, you can select an image and directly go to the editing page.

<span id="441fd223"></span>
## **Recording page**

Call the recording page using the following code.

```objectivec
#import <CKEditor/CKEditor.h>

[CKEditorEngine.shared toRecord];
```


After you call the recording feature, you can directly go to the recording page.

<span id="f3c7d143"></span>
## **Duet page**

Call the duet page using the following code.

```objectivec
#import <CKEditor/CKEditor.h>

[CKEditorEngine.shared toDuetRecord];
```


After you call the duet feature, an image selector appears. You can select an image and directly go to the duet recording page.

<span id="0bf2ef64"></span>
## **Draft box page**

Call the draft box page using the following code.

```objectivec
#import <CKEditor/CKEditor.h>

[CKEditorEngine.shared toDraft];
```


After you call the draft box feature, you can directly go to the draft page.

<span id="c89469b0"></span>
# **Troubleshooting**

Refer to the following topics to learn how to integrate trial Video Editor SDK, create logs, and upgrade Video Editor SDK.

<span id="68edee7b"></span>
## Integrating trial Video Editor SDK

To use Video Editor SDK as a trial, follow the integration guide for the official SDK. However, instead of modifying the default license, modify your app's Bundle ID to `com.bytedance.solution.ck` to complete the integration process.

**EXAMPLE**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a55d86429ff4253a7dbad38b11b7ef0~tplv-goo7wpa0wc-image.image" width="813px" /></div>


<span id="03398f14"></span>
## **Logging**

When debugging, you can use NSLog by default or implement your own logging function. To facilitate troubleshooting, it is recommended to implement your own logging function that will write logs to the logging platform used by your application.

**To implement your own logging function**:


1. Create `YourLogImpl` and implement `CKLogProtocol`.

   ```objectivec
   #import <CKEditor/CKEditor.h>
   
   @interface YourLogImpl : NSObject <CKLogProtocol>
   
   @end
   
   @implementation YourLogImpl
   - (void)logMsg:(NSString *)msg tag:(NSString *)tag type:(DVELogType)type {
       // log here
   }
   ```
   

2. Add the related settings before calling the initialization interface.

   ```objectivec
   #import <CKEditor/CKEditor.h>
   #import "YourLogImpl.h"
   
   CKEditorEngine.shared.logImpl = [YourLogImpl new];
   ```
   


For more information about implementing your own logging function, refer to `CKOLog+FileImpl` in `CKOne-iOs/CKOLog/CKOLog/Classes/FileImpl` in the sample code package.

<span id="8da05a77"></span>
## **Upgrading Video Editor SDK**

For the latest updates, upgrade your Video Editor SDK to the newest version.

**To upgrade Video Editor SDK**:


1. Download and decompress the updated code package.

2. Copy the updated CK folder and replace the current CK folder in your project.


The Video Editor SDK has been upgraded.
