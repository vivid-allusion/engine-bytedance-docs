---
title: "Integrating VE SDK with UI—iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-ios-ve-sdk"
---

This guide demonstrates how to integrate BytePlus Video Editor SDK into your iOS application. This UI\-inclusive integration method allows you to extensively refer to the UI packages in our CKOne sample code. Using this method, you will directly copy most of the sample code to your project without having to write the video editing UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus Video Editor SDK is also known as CKOne or CK within the SDK file and sample code.</div>


<span id="fea40e56"></span>
# **Prerequisites**

Before you begin, ensure that that the following requirements are met:


* Xcode is version 9 or later.

* Your application is intended for devices that are iOS 9.0 or later, as well as iPhone 6s or later.


<span id="ed745593"></span>
# **CKOne sample code**

The CKOne sample code is required for the UI\-inclusive integration method for iOS. In this section, you will learn more about the sample code directory structure and SDK architecture, which will help you understand how to integrate and use Video Editor SDK in your own application.

To obtain the CKOne sample file, contact the BytePlus Video Editor SDK team.

<span id="92fb19ab"></span>
## CKOne sample code directory structure

The CKOne sample code package consists of two folders:


* **CK**—contains Video Editor SDK.

* **CKDemo\-Swift**—contains a demo project with Video Editor SDK integrated. The demo project serves as a reference and can be removed during SDK integration for your project.


The directory structure for the CKOne sample code is as follows:

```Plain
.
├── CK
│   ├── CKBaseKit-iOS
│   ├── CKCommon-iOS
│   ├── CKEditor
│   ├── CKRRecorder
│   ├── CKi18n
│   ├── DVEAlbum-iOS
│   ├── DVEFoundationKit
│   ├── DVETrackKit
│   └── NLEEditor-iOS
└── CKDemo-Swift
    ├── CKDemo-Swift
    ├── CKDemo-Swift.xcodeproj
    ├── CKDemo-Swift.xcworkspace
    ├── Podfile
    ├── Podfile.lock
    └── Pods
```


<span id="144004ab"></span>
## Video Editor SDK architecture

Video Editor SDK is stored in the CK folder in the sample code package and contains the following key components:


|**Module Name** |**Description** |
|---|---|
|CKBaseKit\-iOS |Contains basic capacities of Video Editor SDK and UI packages. |
|CKCommon\-iOS |Contains resources directory and sample service. |
|CKEditor |Contains configuration files for SDK initialization. |
|CKRRecorder |Recording and duet module. |
|DVEAlbum\-iOS |Stores pictures. |
|DVEFoundationKit |Stores common basic classes related to video editing. |
|DVETrackKit |Track area for the editor. |
|NLEEditor\-iOS |Editor module. |


<span id="358249b9"></span>
# Getting started with CKOne SDK

Get started with Video Editor SDK by completing the following tasks:


1. Downloading Video Editor SDK.

2. (Optional) Running the demo project.

3. Integrating Video Editor SDK.

4. Initializing Video Editor SDK.

5. Starting the UI interface.


<span id="948fb607"></span>
# Downloading CKOne SDK

To download BytePlus Video Editor SDK, contact the BytePlus Video Editor SDK team.

<span id="5277a3b1"></span>
# Running the demo project

Before you begin integration, you can run the CKOne\-iOS demo project on a your own device to learn more about the Video Editor SDK features and its UI.

**To run the demo project:** 


1. Download CKOne sample code and decompress the package.

2. Navigate to the project directory and add the following configurations:

   ```Bash
   cd xxx/CKDemo-Swift
   ```
   

3. In Terminal, run the following commands.

   ```Bash
   cd xxx/CKDemo-Swift
   pod install
   open CKDemo-Swift.xcworkspace
   ```
   

4. In Xcode, click **TARGETS** \> **CKOne** \> **Signing & Capabilities** \> **Signing**.

5. Enter your own developer certificate in the **Signing Certificate Apple Development** field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/181c9631213b44a7a07e6eef133fb15d~tplv-goo7wpa0wc-image.image) </span>

6. Select a device.

7. Click the play icon.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ce62e63bdeb47d1811ae78bc7673fb1~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

   The demo project now runs on your iOS device.


<span id="2c0aca93"></span>
# Integrating CKOne SDK

Integrate Video Editor SDK into your iOS application by completing the following steps:


1. Copying sample code.

2. Configuring project settings.

3. Modifying the license.

4. Replacing resources.


<span id="85e4d2ab"></span>
## Step 1: Copying sample code

Add Video Editor SDK to your project by copying the sample code.

**To copy the sample code:** 

Copy the `CK` folder from the CKOne sample code package into your project directory.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6303a8cbe3f6470aad1405175f2c89d2~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="5279b8dc"></span>
## Step 2: Configuring project settings

Configure your project settings to allow Video Editor SDK to run properly.

The following table details the resource permission descriptions for `info.plist`:


|**Name** |**Key** |**Type** |
|---|---|---|
|Privacy – Camera Usage Description |NSCameraUsageDescription |string |
|Privacy – Microphone Usage Description |NSMicrophoneUsageDescription |string |
|Privacy – Photo Library Additions Usage Description |NSPhotoLibraryAddUsageDescription |string |
|Privacy – Photo Library Usage Description |NSPhotoLibraryUsageDescription |string |


**To configure project settings:** 


1. In Xcode, click **TARGETS** \> **Project Name** \> **Build Settings** \> **Build Options**.

2. Set Enable Bitcode as **No**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bce9aab19f3840038a7c08f42685c01c~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   

3. Open `Info.plist` as source code and add the following code:

   ```JavaScript
   <key>NSCameraUsageDescription</key>
   <string>Use Camera</string>
   <key>NSMicrophoneUsageDescription</key>
   <string>Use Microphone</string>
   <key>NSPhotoLibraryAddUsageDescription</key>
   <string>Use Photo Libary</string>
   <key>NSPhotoLibraryUsageDescription</key>
   <string>Use Photo Library</string>
   ```
   

   **OR**

   Open `Info.plist` as property list and click the **Add** icon to add a resource permission description.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4eaec367774c4153ab0b10cb4400a740~tplv-goo7wpa0wc-image.image" width="864px" />   </div>
   


<span id="2509bd0c"></span>
## Step 3: Modifying the license

Modify the license to authenticate Video Editor SDK. Each SDK license is bound to the app's Bundle ID and uses `.licbag` as its extension. For example, the license for the demo project is `com.bytedance.solution.ck.licbag`, which corresponds to the demo project's Bundle ID.

To get your SDK license, you can contact the BytePlus Video Editor SDK team.

**Modify the license by following the steps below:** 


1. Remove the default SDK license `com.bytedance.solution.ck.licbag`stored in `CK/CKCommon-iOS/Resource/License/Editor&Recorder`.

2. Change the name of your SDK license to match your app's Bundle ID.

3. Add your SDK license to your project.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The license file can be stored in the default location <code>CK/CKCommon-iOS/Resource/License/Editor&Recorder</code>. Otherwise, the license file must be stored in an accessible filepath, such as in the main bundle or the sandbox directory, for initialization later.</div>


<span id="f48c366d"></span>
## Step 4: Replacing resources

Replace the resources in `CK/CKCommon-iOS/Resource` with your own resources. After the resources in this directory are packaged, they will be added to the main bundle.

<span id="77ffd5b5"></span>
# Initializing CKOne SDK

Once Video Editor SDK has been integrated, you can initialize it to begin using its functions. Initialize Video Editor SDK by completing the following steps:


1. Setting veLicensePath.

2. Configuring parameters.


<span id="554458a7"></span>
## Step 1: Setting veLicensePath

If the license file is not located in `CK/CKCommon-iOS/Resource/License/Editor&Recorder`, set `CKEditorEngineConfig.veLicensePath` based on the actual filepath before you begin initialization.

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


<span id="eeba5929"></span>
## Step 2: Configuring parameters

Configure `CKEditorEngineConfig` parameters, such as the SDK credentials. If you require any additional features, contact the BytePlus Video Editor SDK team to obtain the relevant parameters.

The following table contains a detailed description of each parameter required for`CKEditorEngineConfig`:


|**Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|isOverSea |String |No |An optional field indicating whether the SDK is intended for users outside Mainland China. The default value is NO. |
|veLicensePath |String |No |The file path for the license. If a license cannot be read from CKResource, this parameter becomes necessary. |
|veAppKey |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |The license key. |
|veToken |String |Depends on the type of BytePlus Video Editor SDK you use.<br><br><br>* Standard: Yes.<br><br>* Lite: No. |The license token. |
|volcAccessKey |String |No |The access key for the music beat feature. |
|volcSecretKey |String |No |The secret key for the music beat feature. |
|subtitleAppId |String |No |The AppKey used for features like text\-to\-speech (TTS) and text recognition. |
|subtitleToken |String |No |The token used for features like text\-to\-speech (TTS) and text recognition. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the credentials for volcAccessKey, volcSecretKey, subtitleAppId, and subtitleToken are not available, you do not need to assign any values. However, you can only use their features if the credentials have been assigned.</div>


<span id="492e48b2"></span>
# FAQ

This section helps you to learn more about how to resolve problems you have encountered in your iOS applications.

<span id="6d4ad1a3"></span>
## How do I implement my own logging function?

When debugging, you can use NSLog by default or implement your own logging function. To facilitate troubleshooting, it is recommended to implement your own logging function that will write logs to the logging platform used by your app.

**To implement your own logging function**:


1. Create `YourLogImpl` and implement `CKLogProtocol`.

   ```objectivec
   #import <CKBaseKit/CKBLogProtocol.h>
   
   @interface YourLogImpl : NSObject <CKBLogProtocol>
   
   @end
   
   @implementation YourLogImpl
   /// print log
   /// @param msg log content
   /// @param type log type
   /// @param tag log tag
   /// @param filename filename
   /// @param funcName function name
   /// @param line line number
   - (void)logMsg:(NSString *)msg
              tag:(NSString *)tag
             type:(CKBLogType)type
         filename:(const char *)filename
         funcName:(const char *)funcName
             line:(int)line;
   @end
   ```
   

2. Add related settings before calling the initialization interface.

   ```objectivec
   #import <CKBaseKit/CKBLogManager.h>
   #import "YourLogImpl.h"
   
   [CKBLogManager.shared injectLogger:[CKOLog new]];
   ```
   


<span id="f7cdac07"></span>
## My SDK license does not work. What should I do?

License authentication is fundamental to BytePlus Video Eidtor SDK. To fix the problem:


* Check whether your license file path is correct.

   By default, the license file is located in `CK/CKCommon-iOS/CKResource/Resource/License/Editor&Recorder` directory. To update SDK license file, copy the updated license file and replace the current license file in the directory.

* Check whether your license file is valid. The most frequently occurring errors are listed below:

   * The license file path is invalid. For example, the file path is set to null.

      **EXAMPLE**

      ```SQL
      [CKEditorEngine.m，-[CKEditorEngine handleLicCallback:message:]，225] code: -1001, message: please execute the VERegLicense at least once: -[VEEditorSession createSceneWithVideoData:withConfig:], localization msg: license not regist
      ```
      

   * The license file path doesn't correspond with your Bundle ID.

      **EXAMPLE**

      ```SQL
      [CKEditorEngine.m，-[CKEditorEngine handleLicCallback:message:]，225] code: -3504, message: license check failed with func:(null) funcId:8C94A19B, code: -3504, reason:app id do not match, localization msg: Bundle ID does not match
      ```
      


<span id="167120cc"></span>
## How do I replace resources?

You can replace resources in `CKCommon-iOS/Resource` directory. The following figure shows the resource bundles stored in `CK/CKCommon-iOS/Resource`.

```SQL
.
├── Editor 
│   ├── Default
│   │   ├── adjust.bundle       [Adjust]
│   │   ├── bubble.bundle       [Bubble]
│   │   ├── canvas.bundle       [Canvas]
│   │   ├── chroma.bundle       [Chroma Key]
│   │   ├── curve_speed.bundle  [Curve Speed]
│   │   ├── flower.bundle       [Flourish]
│   │   ├── mix.bundle          [Mixing Mode]
│   │   ├── smooth_speed.bundle [Smooth Speed]
│   │   ├── sticker.bundle      [Sticker]
│   │   ├── sticker_animation.bundle [Sticker Animation]
│   │   ├── text_align.bundle        [Text - Style - Arrange]
│   │   ├── text_animation.bundle    [Text Animation]
│   │   ├── text_color.bundle        [Text - Style - Background Color]
│   │   ├── text_fonts.bundle        [Text - Style - Font]
│   │   ├── text_style.bundle        [Text -Style - Style]
│   │   ├── text_template.bundle     [Text Template]
│   │   ├── tone.bundle              [Tone]
│   │   ├── transitions.bundle       [Transition]
│   │   ├── ve_effect.bundle         [Effect]
│   │   ├── ve_filter.bundle         [Filter]
│   │   ├── ve_people_effect.bundle  [Task Effect]
│   │   ├── video_animation.bundle   [Video Animation]
│   │   ├── video_mask.bundle        [Mask]
│   │   └── voice.bundle             [TTS - Voice Selection]
│   └── Local
│       ├── default.bundle
│       ├── music.bundle
│       └── sound.bundle
├── License
│   ├── Editor&Recorder
│   │   └── com.bytedance.solution.ck.licbag  [License]
├── Recorder
│   ├── Default
│   │   ├── ComposeMakeup.bundle   [Beauty Effects]
│   │   ├── FilterResource.bundle  [Filter]
│   │   └── StickerResource.bundle [Sticker]
│   └── Local
│       └── duet.bundle            [Duet]
└── VEModel
    └── ModelResource.bundle       [Algorithm model, which is required for recording and editing. Various folders exist according to available features.]
```


<span id="466b02ce"></span>
## **How do I update Video Editor SDK?** 

For the latest updates, upgrade Video Editor SDK to the newest version.

**To upgrade Video Editor SDK:** 


1. Download and decompress the updated code package.

2. Copy the updated CK folder and replace the current CK folder in your project.


The Video Editor SDK has been upgraded.
