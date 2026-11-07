---
title: "Getting started with iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios_1_1_0"
---

<span id="NU1benUbph"></span>
# Integration overview

Learn about the prerequisite of BytePlus Video Editor SDK before you integrate it into your iOS project.

<span id="qnMWoIkOUU"></span>
## Development environment

These are the development environment requirements that must be met:


* **Device**: iPhone 6s or later

* **Swift**: no version requirement (All components are implemented in Objective\-C.)

* **Xcode**: 14.0 or later

* **iOS**: 9.0 or later

* **Languages**: Objective\-C and Swift

* **CocoaPods**: 1.11.3 or later


<span id="JUGeu9DT0L"></span>
## Obtaining a license

To obtain a test or official license of the BytePlus Video Editor SDK, contact your BytePlus Video Editor SDK team.

<span id="bUbWeaIA2v"></span>
## Available languages

Chinese and English are supported. More languages can be added as needed.

<span id="J8q0cK1uRx"></span>
## Supported media formats

These are the supported media formats within BytePlus Video Editor SDK:


|**Type** ||**Video** |**Image** |**Audio** |
|---|---|---|---|---|
|Input |* File Types<br><br>* Container Formats |* .mp4<br><br>* .mov |* .jpg<br><br>* .png<br><br>* .gif |* .mp3<br><br>* .aac<br><br>* .wav |
||Format |* H.264<br><br>* H.265 |N/A |N/A |
|Output |* File Types<br><br>* Container Formats |.mp4 |N/A |N/A |


<span id="ad8a7fca"></span>
## SDK deliverables list

For more information on the SDK packages, refer to [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-package-deliverables-list_1_1_0).

<span id="e62ZFPNDTt"></span>
## SDK package sizes

The following table details the various BytePlus Video Editor SDK package sizes:


|**Categories** |**Built into the App** | **.zip Package Size** |**Description** |
|---|---|---|---|
|BytePlus Video Editor SDK |Yes |22.3MB |Arm64 architecture |
|Display resources that UI components depend on |Yes |0.4 MB |Icons, text, and configuration files |
|Editing resources that UI components depend on |No |Large in size. We recommend that you put them online. |Stickers, filters, fonts, special effects, licenses, and algorithmic models |


<span id="kae0LyfI8X"></span>
# Running the sample code

Get hands\-on with the BytePlus Video Editor SDK by downloading our sample project and running it in an iOS environment. Dive into the SDK's functionality and explore seamless integration possibilities.

You can proceed to run the sample code in your iOS project by following the steps below.


1. Install Ruby on your Mac and run the following command in Terminal to install CocoaPods:

   ```Plain
   sudo gem install cocoapods
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on methods to install CocoaPods, refer <a href="https://cocoapods.org/">here</a>.   </div>
   

2. Download the sample code. Reach out to the BytePlus Video Editor SDK team if you have not downloaded the sample code.

3. Open the `EffectOne-iOS` folder of the sample code.

   Replace `path/to/EffectOne-iOS` with the actual path to your project.

   ```Plain
   cd {path}/to/EffectOne-iOS
   ```
   

4. Open the command line and run `pod install --repo-update` and `open EffectOne-iOS.xcworkspace` commands.

   ```Plain
   pod install --repo-update
   open EffectOne-iOS.xcworkspace
   ```
   

   If the following error occurs when installing pod, run the `gem update xcodeproj` command to resolve this.

   ```C++
   ### Error
   ```
   

   RuntimeError \- [Xcodeproj] Unknown object version (56).

   /Library/Ruby/Gems/2.6.0/gems/xcodeproj\-1.21.0/lib/xcodeproj/project.rb:228:in `initialize_from_file' /Library/Ruby/Gems/2.6.0/gems/xcodeproj-1.21.0/lib/xcodeproj/project.rb:113:in`open'

   ```Plain Text
   
   ```
   

5. In Xcode, click **TARGETS** \> **EffectOne** \> **Signing & Capabilities** \> **Signing**.

6. Enter your own developer certificate in the **Signing Certificate Apple Development** field.

7. You can proceed to run the demo project.


<span id="a708fe3e"></span>
# Integrating VE SDK using Swift

The following section introduces how to integrate VE SDK using Swift. For other programming languages, refer to


* [Integrating VE SDK using Objective-C](https://docs.byteplus.com/docs/video-editor-sdk/docs-integrating-ve-sdk-using-objective-c_1_1_0).

* [Integrating VE SDK using SwiftUI](https://docs.byteplus.com/docs/video-editor-sdk/docs-integrating-ve-sdk-using-swiftui_1_1_0).


<span id="49078891"></span>
## Prerequisites

Before integrating VE SDK using Swift, you have to complete the following:


* Add the dependencies either using Cocoapds or SPM. For details, refer to:

   * [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/docs-managing-dependencies-using-cocoapoads_1_1_0).

   * [Managing dependencies using SPM](https://docs.byteplus.com/docs/video-editor-sdk/docs-managing-dependencies-using-spm_1_1_0).

* Retrieve your SDK package from your BytePlus representatives.

   * For more information, refer to [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-package-deliverables-list_1_1_0).


<span id="596a0dda"></span>
## Step 1: Setting up your Xcode project

Learn how to set up your Xcode project and prepare the development environment for your Swift projects.

**To set up a Swift project:** 


1. Create an iOS app project named TestEO in Xcode.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The package name should match the one used when applying for the Video Editor SDK.   </div>
   

2. Select Swift as the language.

3. Obtain the relevant SDK packages.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on the SDK packages, refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-package-deliverables-list_1_1_0">iOS package deliverables list</a>.   </div>
   

4. Copy the following specified files and folders from the `EffectOne-iOS` directory and `EOLocalResources.bundle` to the `TestEO` project directory:

   * `EOExportUI` folder

   * `EOExportUI.podspec`

   * `Podfile`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70b8e2bf3a024947a36e9f014b408327~tplv-goo7wpa0wc-image.image) </span>

5. Open the Podfile file and replace `EffectOne-iOS` with your project name, as shown in the following example.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc5ec8e96148483ea44ad7d2be485700~tplv-goo7wpa0wc-image.image) </span>

6. Navigate to the directory where the Podfile of the TestEO project is located in the command line.

7. Run the following commands in the command line to access the TestEO project:

   ```Plain
   pod install --repo-update
   open TestEO.xcworkspace
   ```
   

   These commands will update the CocoaPods repository and open the TestEO project in Xcode.


<span id="6637aa9f"></span>
## Step 2: Importing resources and core code snippets

The SDK can be delivered with special effect props, models, and other files as dependencies. This section specifically focuses on the method of embedding them within the app. For other methods, refer to [iOS resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-resource-import-and-configuration_1_1_0).

**To import resources and core code snippets:** 


1. Import the `EOLocalResources.bundle` file into your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You must select the <strong>Create folder references</strong> option during the import and ensure that the bundle is directly under the main bundle at runtime.   </div>
   

2. Add the `EffectOneModule.swift` file to your project to enable the required functionality. Ensure that you follow the recommended integration practices for a seamless and efficient implementation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8893aace232049ed8a5deda2aa7ed9b3~tplv-goo7wpa0wc-image.image) </span>


<span id="e46dec03"></span>
## Step 3: Add the authentication logic


1. Place the authentication logic in the `AppDelegate` or the initial `ViewController` before launching other functionalities.

2. Add the following code to the ViewController file:

   ```Java
       private lazy var effectOneModule = _creatEffectOneModule()
       private func _creatEffectOneModule() -> EffectOneModule {
           return EffectOneModule(parentVC: self)
       }
      
       override func viewDidLoad() {
           super.viewDidLoad()
           // Start authentication
           effectOneModule.makeAuth()
       }
   ```
   

3. Your authentication certificate is typically placed in `EOLocalResources.bundle\License\` with a file name like `XXX.licbag`. Open `EffectOneModule.swift` and check the string `XXX.licbag` in the following code. If it is not the same, please replace it with `XXX.licbag`:

   ```Java
   let authFileName : String = "XXX.licbag"
   ```
   


<span id="761c9678"></span>
## Step 4: Configuring permissions

In the configuration file `Info.plist` of the project, grant permissions to access the camera, microphone, and album:

```Java
//Whether to allow the app to access your media library
<key>NSAppleMusicUsageDescription</key> 
<string>media</string>//Write your own description.
//Whether to allow the app to use your camera. 
<key>NSCameraUsageDescription</key>
<string>Camera</string>//Write your own description.
//Whether to allow the app to use your microphone. 
<key>NSMicrophoneUsageDescription</key>
<string>mic</string>//Write your own description.
//Whether to allow the app to save pictures to your phone. 
<key>NSPhotoLibraryAddUsageDescription</key>
<string>photo lib</string>//Write your own description.
//Whether to allow the app to access your photo album. 
<key>NSPhotoLibraryUsageDescription</key>
<string>photo</string>//Write your own description.
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa85390f0ce842369d438a3c435b6606~tplv-goo7wpa0wc-image.image) </span>

<span id="1a2ba7a3"></span>
## Step 5: Launch the editor module


1. Create a Button control.

2. In the click event, run the following code to launch the basic editor module:

   ```Java
       @objc private func buttonTapped() {
           effectOneModule.showRecorderViewController();
       }
   ```
   


<span id="9a70c467"></span>
## Step 6: Launch the draft module


1. Create a Button control.

2. In the click event, run the following code to launch the draft screen.

   ```Java
       @objc private func buttonTapped1() {
           effectOneModule.showDraftViewController();
       }
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For any integration related questions, refer to our <a href="https://docs.byteplus.com/docs/video-editor-sdk/docs-faq_1_1_0">FAQ</a>.</div>
