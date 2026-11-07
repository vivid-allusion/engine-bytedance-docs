---
title: "Integrating VE SDK using SwiftUI"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-integrating-ve-sdk-using-swiftui"
---

This section describes how to quickly integrate BytePlus Video Editor SDK by using SwiftUI. This integration method is based on CocoaPods.

<span id="ac933ff4"></span>
# Prerequisities

Before integrating VE SDK using Swift, you have to complete the following:


* Add the dependencies either using Cocoapods or SPM. For details, refer to:

   * [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-dependencies-using-cocoapods).

   * [Managing dependencies using SPM](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-dependencies-using-spm).

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to the [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list).


<span id="199efaa9"></span>
# Step 1: Create a new project and copy the code and resources


1. Launch Xcode and create an iOS App project.

   For demonstration purposes, we will use `EffectOne-SwiftUI`as the project name.

2. In Xcode, select `SwiftUI` as the language.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The package name should match the one used when applying for the Video Editor SDK. Use the resources and authorization files obtained from the official source of the SDK.   </div>
   

3. Obtain files related to the SDK by unzipping the SDK package for SwiftUI.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Reach out to the BytePlus Video Editor SDK team for more information on the SDK package.   </div>
   

4. In the `EffectOne-SwiftUI` directory, locate and copy the `EOExportUI` folder, the `EOLocalResources.bundle`, `EOExportUI.podspec`, and `Podfile` files into the root directory of the new project, which is `EffectOne-SwiftUI` in this example.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e76080f3e2b41d0a1f53273c6c8a0d2~tplv-goo7wpa0wc-image.image) </span>

5. Under the `EffectOne-SwiftUI` folder, copy the `EffectOneModule.swift` file into the directory of your project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4c612b955d6476eb5cef164c55d035e~tplv-goo7wpa0wc-image.image) </span>

6. Open the Podfile file and make modifications as shown in the following figure:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25939b9aa967493a97fbfb1eaf788353~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you name your project with a different name, replace <code>EffectOne-SwiftUI</code> with the name of your project.   </div>
   

7. In Terminal, navigate to the directory where the Podfile file of the `EffectOne-OC` project is located.

8. Run the following commands to open the project:

   ```Plain
   pod install --repo-update   
   open EffectOne-SwiftUI.xcworkspace   
   ```
   


<span id="dcad7e41"></span>
# Step 2: Importing resource packages and core code samples.

For BytePlus Video Editor SDK integration, only the built\-in methods within the app need consideration. There's no requirement to integrate dependent files, including special effects and models. For additional methods and information, refer here.

**To import resource packages and core code samples:** 


1. Import the `EOLocalResources.bundle` file into your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You must select the <strong>Create folder references</strong> option during the import and ensure that the bundle is directly under the main bundle at runtime.   </div>
   

2. Add the `EffectOneModule.swift` file to your project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd11e6734b1042c98702d46a80c444e0~tplv-goo7wpa0wc-image.image) </span>


<span id="6802f0b2"></span>
# Step 3: Grant permissions

In the configuration file `Info.plist` of the project, grant permissions to access the camera, microphone, and album:

```Swift
//Whether to allow the app to access your media library. 
NSAppleMusicUsageDescription  
media//Write your own description.
//Whether to allow the app to use your camera.
NSCameraUsageDescription
Camera//Write your own description.
//Whether to allow the app to use your microphone. 
NSMicrophoneUsageDescription
mic//Write your own description.
//Whether to allow the app to save pictures to your mobile phone.
NSPhotoLibraryAddUsageDescription
photo lib//Write your own description.
//Whether to allow the app to access your photo album.
NSPhotoLibraryUsageDescription
photo//Write your own description. 
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c5080189ba14da3831a5893eeec96e0~tplv-goo7wpa0wc-image.image) </span>

<span id="a8b4c172"></span>
# Step 4: Add authentication logic


1. Add the following code to the ContentView file of your project.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The authentication logic is placed in the ContentView and must be used before you launch other functionalities.   </div>
   

   ```Swift
   var body: some View {
           func getKeyWindowRootViewController() -> UIViewController? {
               return UIApplication.shared.windows.first{ $0.isKeyWindow }?.rootViewController
           }
           lazy var pageVC : UIViewController = {
               let pageVC = getKeyWindowRootViewController()!
               return pageVC
           }()
          
           func _creatEffectOneModule() -> EffectOneModule {
               return EffectOneModule(parentVC: pageVC)
           }
           lazy var effectOneModule = _creatEffectOneModule()
           //Start the authentication.
           effectOneModule.makeAuth()
           return VStack {
               Button("Recorder") {
                   effectOneModule.showRecorderViewController()
               }
               .padding(EdgeInsets(top: 0, leading: 0, bottom: 30, trailing: 0))
               Button("Draft") {
                   effectOneModule.showDraftViewController()
               }
           }
           .padding()
       }
   ```
   

2. Your authentication certificate is typically placed in the `EOLocalResources.bundle\License\` directory with a file name like `XXX.licbag`. Open `EffectOneModule.swift` and replace the string in the following code with `"XXX.licbag"`.

   ```Swift
   self.authFileName = @"XXX.licbag"; 
   ```
   


<span id="ee902e39"></span>
# Step 5: Launch the editor module


1. Create a Button control.

2. In the click event, run the following code to launch the basic editor module:

   ```Swift
    Button("Recorder") {
        effectOneModule.showRecorderViewController()
    }
   ```
   


<span id="53049d67"></span>
# Step 6: Launch the draft box


1. Create a Button control.

2. In the click event, run the following code to launch the draft screen.

   ```Swift
       Button("Draft") {  
          effectOneModule.showDraftViewController() 
       }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6331ce506fa4509ab04b6c12fdb1d52~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For any integration related questions, refer to our <a href="https://docs.byteplus.com/docs/video-editor-sdk/150-faq">FAQ</a>.   </div>
