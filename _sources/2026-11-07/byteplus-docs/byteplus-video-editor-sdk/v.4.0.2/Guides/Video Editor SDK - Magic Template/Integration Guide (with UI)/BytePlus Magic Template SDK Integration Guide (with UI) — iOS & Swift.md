---
title: "BytePlus Magic Template SDK Integration Guide (with UI) — iOS & Swift"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-byteplus-magic-template-sdk-integration-guide-with-ui-ios-swift-v.4.0.2"
---

This guide demonstrates integrating BytePlus Magic Template SDK into your iOS & Swift application. This UI\-inclusive integration method allows you to extensively refer to the UI packages in our CKOne Demo App sample code. Using this method, you will directly copy most of the sample code to your project without having to write the UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The BytePlus Video Editor SDK is also known as <strong>CKOne</strong> or <strong>CK</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The BytePlus Magic Template SDK is also called <strong>cutsame</strong> or <strong>CutSame</strong>.</div>


* <div data-tips="true" data-tips-type="tip">These terms will be used interchangeably in this article.</div>



<span id="da34d761"></span>
# **Prerequisites**

Before you begin, ensure that that the following requirements are met:


* Xcode is version 9 or later.

* Your development environment is OS X 10.10 or later.

* Your application is intended for devices that are iOS 9.0 or later.


<span id="457dd9d6"></span>
# Integrating Magic Template SDK

Integrate Magic Template SDK into your iOS & Swift application by completing the following steps:


1. Configuring Podfile.

2. Downloading and copying the sample code.

3. Configuring project settings.

4. Modifying the license.

5. Replacing resources.

6. Replacing token and app key.

7. (Optional) Configuring host server.

8. Creating bridging headers.


<span id="1333d814"></span>
## Step 1: Configuring Podfile

Configure Podfile to manage the dependencies used in your project.

**To configure Podfile:** 


1. If there is no Podfile in your project, run pod init && pod install in the root directory of your project to obtain a Podfile.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using CocoaPods, skip Step 2 and proceed to Step 3.</div>



2. Add the following configurations to your Podfile:


```objectivec
source 'https://cdn.cocoapods.org/'

platform:ios, '9.0'

# {en} CKSDK relative path to Podfile
$CKSDK_RELATIVE_PATH = "./CK"

def cutsame_pods
  pod 'TTVideoEditor', '11.8.1.43-D',:source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'NLEPlatform', '0.5.4', :source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'DVEInject', '0.0.5', :source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'CKi18n', :path => "#$CKSDK_RELATIVE_PATH/CKi18n"

  pod 'NLEEditor', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/NLEEditor-iOS"
  pod 'DVETrackKit', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/DVETrackKit"
  pod 'DVEFoundationKit', :path => "#$CKSDK_RELATIVE_PATH/DVEFoundationKit"
  pod 'CKEditor', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/CKEditor"
  pod 'CKRRecorder', :subspecs => ['Arch'], :path => "#$CKSDK_RELATIVE_PATH/CKRRecorder"
  pod 'CKResource', :path => "#$CKSDK_RELATIVE_PATH/CKResource"

  pod 'CKOBase', :path => "#$CKSDK_RELATIVE_PATH/CKO/CKOBase"
  pod 'CKOBusiness', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/CKO/CKOBusiness"
  pod 'CKOLog', :subspecs => ['FileImpl', 'Editor'], :path => "#$CKSDK_RELATIVE_PATH/CKO/CKOLog"
  pod 'CKOCutSame', :path => "#$CKSDK_RELATIVE_PATH/CKO/CKOCutSame"

  pod 'CutSameIF', :path => "#$CKSDK_RELATIVE_PATH/CutSameIF"
  pod 'CutSameUIIF', :path => "#$CKSDK_RELATIVE_PATH/CutSameUIIF", :subspecs => ['CK','PTK']
end

// change'CKOne' to your own project target.
target 'your own project target' do
  #Magic Templates
  cutsame_pods
end
```


<span id="4af58b78"></span>
## Step 2: Download and copy the SDK

Add Magic Template SDK to your project by copying the sample code.

**To copy the sample code:** 

Copy the CK folder from the CKOne sample code package into your project directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure that the CK folder is placed at the same directory level as the Podfile, so that it matches the relative path configuration specified in the Podfile.</div>


**EXAMPLE**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bec60bba758401fabd0607a3fa31199~tplv-goo7wpa0wc-image.image" width="749px" /></div>


<span id="d398f6d4"></span>
## Step 3: Configuring project settings

Configure your project settings to allow Magic Template SDK to run properly.

The following details the resource permission descriptions for `info.plist`:


|**Name** |**Key** |**Data Type** |
|---|---|---|
|Privacy – Camera Usage Description |NSCameraUsageDescription |string |
|Privacy – Microphone Usage Description |NSMicrophoneUsageDescription |string |
|Privacy – Photo Library Usage Description |NSPhotoLibraryUsageDescription |string |
|Privacy – Media Library Usage Description |NSMediaLibraryUsageDescription |string |
|Privacy – Photo Library Additions Usage Description |NSPhotoLibraryAdditionsUsageDescription |string |
|Privacy – Photo Library Usage Description |NSPhotoLibraryUsageDescription |string |


**To configure project settings:** 


1. In Xcode, go to **TARGETS** \> **Project Name** \> **Build Settings** \> **Build Options**.

2. Set Enable Bitcode as **No**.

3. Open `Info.plist` as source code and add the following:


```XML
        <key>NSCameraUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to use your camera?"--></string>
        <key>NSMicrophoneUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to use your microphone?"--></string>
        <key>NSPhotoLibraryUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to access your photo library?"--></string>
```


**OR**

Open `Info.plist` as property list and click the **Add** icon to add a resource permission description.

<span id="7b57a369"></span>
## Step 4: Modifying the license

Modify the license to authenticate Magic Template SDK. Each SDK license is bound to the app's Bundle ID and uses `.licbag` as its extension. For example, the license for the demo project is `com.bytedance.solution.ck.licbag`, which corresponds to the demo project's Bundle ID.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ecea7780d2a471f990aaa1f48167411~tplv-goo7wpa0wc-image.image" width="690px" /></div>


**To modify the license:** 


1. Go to `CK/CKO/CKOCutSame/CKOCutSame/Assets`.

2. Remove the default SDK license `com.bytedance.solution.ck.licbag`.

3. Add your SDK license, ensuring that the bundle ID matches the license.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7360bb03868e49fe86fd74fab577b7ca~tplv-goo7wpa0wc-image.image" width="682px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0023d53541d41f792cbeb7a7247eef6~tplv-goo7wpa0wc-image.image" width="676px" /></div>


<span id="3edfc3bb"></span>
## Step 5: Replacing resources

Replace the resources for the recording page, if any.

**To replace resources:** 


1. Replace the resources with your own resources, if any, in `CK/CKResource/CKResource/Resource/Record`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a196240c146a49d78905cc63f4f3caac~tplv-goo7wpa0wc-image.image" width="512px" /></div>



2. In Terminal, run pod install.

3. Start .xcworkspace.


<span id="e36c6eda"></span>
## Step 6: Replacing token and app key

Modify the token and appkey in Development Pods code.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f18014d8f0de40d8a44fade20da6d01e~tplv-goo7wpa0wc-image.image" width="636px" /></div>


<span id="401bd090"></span>
## (Optional) Step 7: Configuring host server

If you have built your own service to pull data for templates or effects, you can configure your own host during initialization.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6edaf31cab354822b5200240fc71c952~tplv-goo7wpa0wc-image.image" width="700px" /></div>


<span id="8872d706"></span>
## Step 8: Creating bridging headers

Create bridging headers to enable Objective\-C files to work in your Swift project.

**To create a bridging header:** 


1. Create a new header file called YourApp\-Swift\-Bridging\-Header.

2. Import the following header files.


```Swift
//
//  Use this file to import your target's public headers that you would like to expose to Swift.
//

#import <CKOBase/CKORouter.h>
```


<span id="f48d6324"></span>
# Starting the UI interface

Once Magic Template SDK has been initialized, you can start the UI interface and begin using its functions. Refer to the sample code below to learn how to call the template list page.

```objectivec
override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        CKORouter.toCutSame()
    }
```


<span id="4904d708"></span>
# FAQ

<span id="c4183c21"></span>
## What should I do if there are no network connections available?


* **For computer devices:** 


Add **Enable HTTP request permission** to `info.plist`.

```JavaScript
        <key>NSAppTransportSecurity</key>
        <dict>
                <key>NSAllowsArbitraryLoads</key>
                <true/>
        </dict>   
```


**For mobile devices:** 


1. Go to **Settings** \> **Cellular Network**.

2. Select **WLAN & Cellular Data**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4a8b13d03574f469c2071a105d7c3b4~tplv-goo7wpa0wc-image.image" width="624px" /></div>


<span id="5b28ca48"></span>
## What should I do if the error "unrecognized selector" pops up while running the SDK?

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c5a6fa09a774144bc79d5536dce8665~tplv-goo7wpa0wc-image.image" width="624px" /></div>


You can add a new project by adding the `window` property in `AppDelegate`.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/842eee9a63624948af2c5c316a7c03dd~tplv-goo7wpa0wc-image.image" width="624px" /></div>


Or

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66ecd449c4be42d2a0ede5b4669477ac~tplv-goo7wpa0wc-image.image" width="624px" /></div>


<span id="15742a16"></span>
## What should I do if the error "Authentication failed. Please check the certificate settings" appears?

You should do the following:


* Check whether the bundle identifier matches the license provided by technical support.

* Ensure that the license read by the code matches the actual bundle identifier.


<span id="0b7a5a09"></span>
## What should I do if the Pod signing issue occurs after Xcode 14 is running?

You can add the following configurations to your Podfile:

```objectivec
post_install do |installer|
  installer.generated_projects.each do |project|
    project.targets.each do |target|
      target.build_configurations.each do |config|
        # {zh} Resolve the code signing issue in Xcode 14.{en} [Xcode 14 build failed with manual code sign and app resource bundles](https://github.com/CocoaPods/CocoaPods/issues/11402)
        config.build_settings['CODE_SIGN_IDENTITY'] = '-'
        config.build_settings['CODE_SIGN_ENTITLEMENTS'] = '-'
        config.build_settings['CODE_SIGNING_REQUIRED'] = 'NO'
        config.build_settings['CODE_SIGNING_ALLOWED'] = 'NO'
      end
    end
  end
end
```
