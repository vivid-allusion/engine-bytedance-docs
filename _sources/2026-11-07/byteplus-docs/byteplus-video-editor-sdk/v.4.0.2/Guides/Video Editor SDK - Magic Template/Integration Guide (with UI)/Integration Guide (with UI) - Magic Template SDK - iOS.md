---
title: "Integration Guide (with UI) - Magic Template SDK - iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-magic-template-sdk-ios-v.4.0.2"
---

This guide demonstrates integrating BytePlus Magic Template SDK into your iOS application. This UI\-inclusive integration method allows you to extensively refer to the UI packages in our CKOne Demo App sample code. Using this method, you will directly copy most of the sample code to your project without having to write the UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The BytePlus Video Editor SDK is also known as <strong>CKOne</strong> or <strong>CK</strong>.</div>


* <div data-tips="true" data-tips-type="tip">The BytePlus Magic Template SDK is also called <strong>cutsame</strong> or <strong>CutSame</strong>.</div>


* <div data-tips="true" data-tips-type="tip">These terms will be used interchangeably in this article.</div>



<span id="99f4a508"></span>
# **Prerequisites**

Before you begin, ensure that that the following requirements are met:


* Xcode is version 9 or later.

* Your development environment is OS X 10.10 or later.

* Your application is intended for devices that are iOS 9.0 or later.


<span id="288756af"></span>
# Integrating Magic Template SDK

Integrate Magic Template SDK into your iOS application by completing the following steps:


1. Configuring Podfile.

2. Copying sample code.

3. Configuring project settings.

4. Modifying the license.

5. Replacing resources.

6. Replacing token and app key.

7. (Optional) Configuring host server.

8. Creating bridging headers.


<span id="0e49977d"></span>
## Step 1: Configuring Podfile

Configure Podfile to manage the dependencies used in your project.

**To configure Podfile:** 


1. If there is no Podfile in your project, run pod init && pod install in the root directory of your project to obtain a Podfile.

2. Add the following configurations to your Podfile:


```Ruby
source 'https://cdn.cocoapods.org/'

platform:ios, '9.0'

# Relative path of CKSDK to Podfile
$CKSDK_RELATIVE_PATH = "./CK"

def cutsame_pods
  pod 'TTVideoEditor', '11.8.1.36-D',:source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'NLEPlatform', '0.5.2', :source => 'https://github.com/volcengine/volcengine-specs.git'
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

# Replace 'CKOne' with your own project target. 
target 'CKOne' do
  # Magic Template SDK
  cutsame_pods
end
```


<span id="3eb242b0"></span>
## Step 2: Copying sample code

Add Magic Template SDK to your project by copying the sample code.

**To copy the sample code:** 

Copy the CK folder from the CKOne sample code package into your project directory.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong><em>Note</em></strong>:</div>


<div data-tips="true" data-tips-type="tip"><em>Ensure that the CK folder is placed at the same directory level as the Podfile, so that it matches the relative path configuration specified in the Podfile.</em></div>


**EXAMPLE**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce402a8325c44c8bbda8a1913228a6bd~tplv-goo7wpa0wc-image.image" width="749px" /></div>


<span id="6ea87195"></span>
## Step 3: Configuring project settings

Configure your project settings to allow Magic Template SDK to run properly.

The following details the resource permission descriptions for `info.plist`:


|**Name** |**Key** |**Data Type** |
|---|---|---|
|Privacy – Camera Usage Description |NSCameraUsageDescription |string |
|Privacy – Microphone Usage Description |NSMicrophoneUsageDescription |string |
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

<span id="41dfdaeb"></span>
## Step 4: Modifying the license

Modify the license to authenticate Magic Template SDK. Each SDK license is bound to the app's Bundle ID and uses `.licbag` as its extension. For example, the license for the demo project is `com.bytedance.solution.ck.licbag`, which corresponds to the demo project's Bundle ID.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fc8c664c25048c6b83c52fd2af4fef1~tplv-goo7wpa0wc-image.image" width="622px" /></div>


**To modify the license:** 


1. Go to `CK/CKO/CKOCutSame/CKOCutSame/Assets`.

2. Remove the default SDK license `com.bytedance.solution.ck.licbag`.

3. Add your SDK license, ensuring that the bundle ID matches the license.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1f7ab917444cf69b7292cadd5b6bc9~tplv-goo7wpa0wc-image.image" width="584px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ef15aeae3cf4eef90f8dd9859b392da~tplv-goo7wpa0wc-image.image" width="580px" /></div>


<span id="a54aabae"></span>
## Step 5: Replacing resources

Replace the resources for the recording page, if any.

**To replace resources:** 


1. Replace the resources with your own resources, if any, in `CK/CKResource/CKResource/Resource/Record`.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d011b22bbfca4177b293358b2d15e710~tplv-goo7wpa0wc-image.image" width="468px" /></div>



2. In Terminal, run pod install.

3. Start .xcworkspace.


<span id="1f27335b"></span>
## Step 6: Replacing token and app key

Modify the token and appkey in Development Pods code.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6f2ea45519e411398d2d713a156d5ce~tplv-goo7wpa0wc-image.image" width="722px" /></div>


<span id="750be51a"></span>
## (Optional) Step 7: Configuring host server

If you have built your own service to pull data for templates or effects, you can configure your own host during initialization.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15487f2682f14ec78c88b0d4fc92f718~tplv-goo7wpa0wc-image.image" width="700px" /></div>


**EXAMPLE**

```objectivec
    // Template pull service configuration
    CSIFTemplateFetcherConfig *templateFetcherConfig = [[CSIFTemplateFetcherConfig alloc] init];
    templateFetcherConfig.host = [CSIFConfigViewController cutsameHost];
    
    // Special effects service configuration
    CSIFEffectFetcherConfig *effectFetcherConfig = [[CSIFEffectFetcherConfig alloc] init];
    effectFetcherConfig.host = templateFetcherConfig.host;
    effectFetcherConfig.modelListPath = @"/api/modellistinfo";
    effectFetcherConfig.effectListPath = @"/api/effectlist";
```


<span id="ded2cad5"></span>
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


<span id="e8cde7a8"></span>
# Starting the UI interface

Once Magic Template SDK has been initialized, you can start the UI interface and begin using its functions. Refer to the sample code below to learn how to call the template list page.

```Swift
override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        CKORouter.toCutSame()
    }
```


<span id="9f81e97f"></span>
# FAQ

<span id="787cb269"></span>
## What should I do if there are no network connections available?

You can do the following to enable network connections:

**For computer devices:** 

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
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63d194567b1848769f71f214096bd130~tplv-goo7wpa0wc-image.image" width="338px" /></div>


<span id="bca13589"></span>
## What should I do if the error "unrecognized selector" pops up while running the SDK?

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48a9f9d8bd624d5abbe57a0cd450806d~tplv-goo7wpa0wc-image.image" width="636px" /></div>


You can add a new project by adding the `window` property in `AppDelegate`.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb2635ae449149fa9104de6eecdcec39~tplv-goo7wpa0wc-image.image" width="631px" /></div>


Or

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce90c35d800444a2af6c92f4e627b517~tplv-goo7wpa0wc-image.image" width="622px" /></div>


<span id="542855fc"></span>
## What should I do if the error "Authentication failed. Please check the certificate settings" appears?

You should do the following:


* Check whether the bundle identifier matches the license provided by technical support.

* Ensure that the license read by the code matches the actual bundle identifier.


<span id="5a74a6c5"></span>
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


<span id="e88857ff"></span>
## What should I do if the Xcode version is inconsistent with the Pod?

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6664b1aab349482cbbe10953b3eb865e~tplv-goo7wpa0wc-image.image" width="698px" /></div>


You can do the following to resolve this issue:


* Install **ruby3.0.0**


```Swift
rvm install 3.0.0
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong><em>Note:</em></strong></div>


<div data-tips="true" data-tips-type="tip"><em>You have to install the Ruby Version Manager first.</em></div>



* Check if **ruby3.0.0** is installed successfully.


```Swift
rvm list
```



* Use **ruby3.0.0**.


```Swift
rvm use 3.0.0 --default
```



* Verify if the version is switched successfully.


```Swift
 rvm list                  
   ruby-2.7.2 [ arm64 ]
   ruby-2.7.3 [ arm64 ]
=* ruby-3.0.0 [ arm64 ]
```



* Reinstall **pod** after switching the version.


```Swift
sudo gem install cocoapods
```


When the installation is completed, the pod will run smoothly.
