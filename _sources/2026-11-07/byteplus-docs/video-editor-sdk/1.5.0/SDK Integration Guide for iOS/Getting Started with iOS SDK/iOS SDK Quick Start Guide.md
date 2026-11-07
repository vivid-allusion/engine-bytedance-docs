---
title: "iOS SDK Quick Start Guide"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-ios-sdk-quick-start-guide"
---

Get started swiftly with our iOS SDK Quick Start Guide, designed to help developers seamlessly integrate and leverage our BytePlus Video Editor (VE) SDK's powerful features for iOS applications.

The following section introduces how to integrate VE SDK using Swift. For other programming languages, refer to


* [Integrating VE SDK using Objective-C](https://docs.byteplus.com/docs/video-editor-sdk/150-integrating-ve-sdk-using-objective-c).

* [Integrating VE SDK using SwiftUI](https://docs.byteplus.com/docs/video-editor-sdk/150-integrating-ve-sdk-using-swiftui).


<span id="0cb65476"></span>
## Prerequisites

Before integrating VE SDK using Swift, you have to complete the following:


* Add the dependencies either using Cocoapds or SPM. For details, refer to:

   * [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-dependencies-using-cocoapods).

   * [Managing dependencies using SPM](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-dependencies-using-spm).

* Retrieve your SDK package from your BytePlus representatives.

   * For more information, refer to [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list).


<span id="586f4fa1"></span>
## Step 1: Setting up your Xcode project

Learn how to set up your Xcode project and prepare the development environment for your Swift projects.

**To set up a Swift project:** 


1. Create an iOS app project named TestEO in Xcode.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The package name should match the one used when applying for the Video Editor SDK.   </div>
   

2. Select Swift as the language.

3. Obtain the relevant SDK packages.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on the SDK packages, refer to <a href="https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list">iOS package deliverables list</a>.   </div>
   

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


<span id="73c255ed"></span>
## Step 2: Importing resources and core code snippets

The SDK can be delivered with special effect props, models, and other files as dependencies. This section specifically focuses on the method of embedding them within the app. For other methods, refer to [iOS resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-resources-import-and-configuration).

**To import resources and core code snippets:** 


1. Import the `EOLocalResources.bundle` file into your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You must select the <strong>Create folder references</strong> option during the import and ensure that the bundle is directly under the main bundle at runtime.   </div>
   

2. Add the `EffectOneModule.swift` file to your project to enable the required functionality. Ensure that you follow the recommended integration practices for a seamless and efficient implementation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8893aace232049ed8a5deda2aa7ed9b3~tplv-goo7wpa0wc-image.image) </span>


<span id="528ee493"></span>
## Step 3: Add the authentication logic


1. Place the authentication logic in the `AppDelegate` or the initial `ViewController` before launching other functionalities.

2. Add the following code to the ViewController file:

   ```Swift
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

   ```Swift
   let authFileName : String = "XXX.licbag"  
   ```
   


<span id="2385a035"></span>
## Step 4: Configuring permissions

In the configuration file `Info.plist` of the project, grant permissions to access the camera, microphone, and album:

```Swift
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

<span id="379428e7"></span>
## Step 5: Launch the editor module


4. Create a Button control.

5. In the click event, run the following code to launch the basic editor module:

   ```objectivec
       @objc private func buttonTapped() {
           effectOneModule.showRecorderViewController();
       } 
   ```
   


<span id="27d079ec"></span>
## Step 6: Launch the draft module


6. Create a Button control.

7. In the click event, run the following code to launch the draft screen.

   ```Swift
       @objc private func buttonTapped1() {
           effectOneModule.showDraftViewController();
       } 
   ```
   


<span id="fa69b0ed"></span>
## Step 7: Launching the duet video function

Create a button control and use the following code in the click event to start the video duet feature:

```Swift
    @objc private func buttonTapped1() {
        effectOneModule.showDuetViewController()
    }
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For any integration related questions, refer to our <a href="https://docs.byteplus.com/docs/video-editor-sdk/150-faq">FAQ</a>.</div>
