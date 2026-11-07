---
title: "Integrating VE SDK with UI—iOS & Swift"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-integration-guide-with-ui-ios-swift-ve-sdk-v.4.0.2"
---

This guide demonstrates how to integrate BytePlus Video Editor SDK into your iOS application using Swift. This UI\-inclusive integration method allows you to extensively refer to the UI packages in our CKOne sample code. Using this method, you will directly copy most of the sample code to your project without having to write the video editing UI logic by yourself.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus Video Editor SDK is also known as CKOne or CK within the SDK file and sample code.</div>


<span id="06639308"></span>
# CKOne sample code

The CKOne sample code includes the Video Editor SDK and an integrated demo project. Download the CKOne sample code below:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fab2043fb6c74ff9890fd1cbc364bb61~tplv-goo7wpa0wc-image.image" name="CKDemo-Swift-0103.zip">CKDemo-Swift-0103.zip</Attachment>


&nbsp;

<span id="564277cb"></span>
# Getting started with Video Editor SDK

Get started with Video Editor SDK by completing the following tasks:


1. Integrating Video Editor SDK.

2. Initializing Video Editor SDK.

3. Starting the UI interface.


<span id="13315e42"></span>
# Integrating Video Editor SDK

Integrate Video Editor SDK into your iOS application by completing the following steps:


1. Configuring Podfile.

2. Copying CKSDK.

3. Configuring project settings.

4. Creating bridging headers.


<span id="6519a7cb"></span>
## Step 1: Configuring Podfile

Configure your Podfile to manage the dependencies used in your project. Video Editor SDK currently does not support the importing of dynamic frameworks. If your project's Podfile contains `use_frameworks!`, it should be deleted. Adding on, for CocoaPods 1.5.0 onwards, `use_frameworks!` is no longer required for Swift pods, and `use_modular_headers!` can be used to generate module maps. For more information on CocoaPods, refer [here](https://blog.cocoapods.org/CocoaPods-1.5.0/).

You can add the following configurations to your Podfile:

```Ruby
# {en} Disable use_frameworks!
use_modular_headers!

# {en} CKSDK relative path to Podfile
$CKSDK_RELATIVE_PATH = "./CKSDK"

# {en} General pods
def base_pods
  pod 'TTVideoEditor', '11.8.1.29-D',:source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'NLEPlatform', '0.5.2', :source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'DVEInject', '0.0.5', :source => 'https://github.com/volcengine/volcengine-specs.git'
  # supports
  pod 'CKi18n', :path => "#$CKSDK_RELATIVE_PATH/CKi18n", :modular_headers => false
  pod 'CKResource', :path => "#$CKSDK_RELATIVE_PATH/CKResource", :modular_headers => false
end

# {en} Editing
def editor_pods
  base_pods
  # When integrating, adjust the relative path according to the actual situation of the project
  pod 'NLEEditor', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/NLEEditor-iOS", :modular_headers => false
  pod 'DVETrackKit', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/DVETrackKit", :modular_headers => false
  pod 'DVEFoundationKit', :path => "#$CKSDK_RELATIVE_PATH/DVEFoundationKit", :modular_headers => false
  pod 'CKEditor', :subspecs => ['CKStandard'], :path => "#$CKSDK_RELATIVE_PATH/CKEditor", :modular_headers => false
  
  ################################### Third party ###################################
  pod 'SGPagingView', '1.7.1'
  pod 'lottie-ios', '2.5.3'
  pod 'FileMD5Hash'
  pod 'SDWebImage'
end

# {en} Recording
def recorder_pods
    base_pods
    pod 'CKRRecorder', :subspecs => ['Arch'], :path => "#$CKSDK_RELATIVE_PATH/CKRRecorder", :modular_headers => false
end

target 'CKDemo-Swift' do
  # Editing & Recording
  editor_pods

  recorder_pods
end

# {en} optional: Modify some compilation parameters to optimize the development experience
post_install do |installer|
  installer.generated_projects.each do |project|
      project.targets.each do |target|
        target.build_configurations.each do |config|
          #  {en} Resolving Xcode14 compilation issues
          config.build_settings['CODE_SIGN_IDENTITY'] = '-'
          config.build_settings['CODE_SIGN_ENTITLEMENTS'] = '-'
          config.build_settings['CODE_SIGNING_REQUIRED'] = 'NO'
          config.build_settings['CODE_SIGNING_ALLOWED'] = 'NO'
        end
      end
      project.build_configurations.each do |config|
        config.build_settings['CLANG_WARN_DOCUMENTATION_COMMENTS'] = 'NO'
        # Hide warnings partiallay
        config.build_settings['WARNING_CFLAGS'] = '-Wno-strict-prototypes -Wno-swift-name-attribute -Wno-comment -Wno-shorten-64-to-32 -Wno-unused-function -Wno-unused-variable -Wno-nullability -Wno-nullability-completeness -Wno-documentation -Wno-documentation-html -Wno-incomplete-umbrella'
        # Hide all warnings
        if project.targets.first.name.start_with?("NLEPlatform")
          config.build_settings['GCC_WARN_INHIBIT_ALL_WARNINGS'] = "YES"
        end
        # Reduce Xcode lag caused by warnings
        if project.targets.first.name.start_with?("NLEEditor") || project.targets.first.name.start_with?("DVETrackKit")
          config.build_settings['WARNING_CFLAGS'] = '-Wno-strict-prototypes -Wno-swift-name-attribute -Wno-comment -Wno-shorten-64-to-32 -Wno-unused-function -Wno-unused-variable -Wno-nullability -Wno-nullability-completeness -Wno-documentation -Wno-documentation-html -Wno-ambiguous-macro'
        end
      end
  end
end
```


<span id="07fd2d4d"></span>
### Importing dynamic libraries

If your project involves pods that must be imported as dynamic frameworks, you can configure Podfile using the following method.

**EXAMPLE**

```Ruby
dynamic_frameworks = ['Alamofire','SnapKit']

pre_install do |installer|
 # Pod::Installer::Xcode::TargetValidator.send(:define_method, :verify_no_static_framework_transitive_dependencies) {}
  installer.pod_targets.each do |target|
    if dynamic_frameworks.include?(target.name)
      def target.build_type
        Pod::BuildType.dynamic_framework
      end
    end
  end
end
```


<span id="58f422a1"></span>
## Step 2: Copying CKSDK

The CKSDK folder in the sample code package contains the Video Editor SDK. Copy CKSDK from CKDemo\-Swift into your project directory. Ensure that CKSDK is placed at the same directory level as Podfile, in order to match the path configuration specified in Podfile.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d09353c0058427b995880731ae64aad~tplv-goo7wpa0wc-image.image" width="670px" /></div>


<span id="4d67f7c1"></span>
## Step 3: Configuring project settings

Configure your project settings to allow Video Editor SDK to run properly.

The following table details the resource permission descriptions for `info.plist`:


|**Name** |**Key** |**Type** |
|---|---|---|
|Privacy – Camera Usage Description |NSCameraUsageDescription |string |
|Privacy – Microphone Usage Description |NSMicrophoneUsageDescription |string |
|Privacy – Photo Library Additions Usage Description |NSPhotoLibraryAddUsageDescription |string |
|Privacy – Photo Library Usage Description |NSPhotoLibraryUsageDescription |string |


**To configure project settings:** 


1. In Xcode, go to **TARGETS** \> **Project Name** \> **Build Settings** \> **Build Options**.

2. Set Enable Bitcode as **No**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f665f360b9a34e76b7ac297bcd09d25b~tplv-goo7wpa0wc-image.image" width="864px" /></div>



3. Open `Info.plist` as source code and add the following:


```XML
        <key>NSCameraUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to use your camera?"--></string>
        <key>NSMicrophoneUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to use your microphone?"--></string>
        <key>NSPhotoLibraryAddUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to access your photo library?"--></string>
        <key>NSPhotoLibraryUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to access your photo library?"--></string>
        <key>NSAppleMusicUsageDescription</key>
        <string><!--Fill in resource permission description. For example, "Allow XXX to access your media library?"--></string>
```


**OR**

Open `Info.plist` as property list and click the **Add** icon to add a resource permission description.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be03767b275f4194b9eeb1c66d260787~tplv-goo7wpa0wc-image.image" width="864px" /></div>


<span id="e197f32f"></span>
## Step 4: Creating bridging headers

Create bridging headers to enable Objective\-C files to work in your Swift project.

**To create a bridging header:** 


1. Create a new header file called YourApp\-Swift\-Bridging\-Header.

2. Import the following header files.


```objectivec
// YourApp-Swift-Bridging-Header

#import <CKEditor/CKEditor.h>
#import <DVEFoundationKit/UIViewController+Private.h>
#import <CKEditor/CKRResourceLoader.h>

// recorder
#import <CKRRecorder/CKRRecorderViewController.h>

// duet
#import <CKRRecorder/CKRResourcePicker.h>
#import <CKRRecorder/CKRDuetViewController.h>

// edit
#import <CKRRecorder/CKRResourcePicker.h>
#import <NLEEditor/DVEUIFactory.h>

// draft
#import <CKEditor/CKEDraftBoxController.h>

// result callback
#import <NLEEditor/DVEVCContextExternalInjectProtocol.h>
```


<span id="d1393889"></span>
## Step 5: Replacing resources and licenses

Replace the resources and licenses for Video Editor SDK.

**To replace resources and licenses:** 


1. Replace the resources with your own resources, if any, in the following directories:

   * `CKSDK/CKResource/CKResource/Resource/Editor`

   * `CKSDK/CKResource/CKResource/Resource/Record`

2. Replace the licenses in `CKSDK/CKResource/CKResource/Resource/License` with your own licenses.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d0ab3a7bc8440f88bc1f243086a910c~tplv-goo7wpa0wc-image.image" width="624px" /></div>



3. In Terminal, run pod install.


<span id="dcd00b48"></span>
# Initializing Video Editor SDK

Once Video Editor SDK has been integrated, you can initialize it to begin using its functions. Configure the initialization parameters, such as the SDK credentials, to initialize the SDK.

**EXAMPLE**

```objectivec
    func initCKSDK() {
        let config = CKEditorEngineConfig.default()
        config.veLicensePath = Bundle.main.path(forResource: "com.bytedance.solution.ck.licbag", ofType: "") ?? ""
        config.veAppKey = "iWwiXvXhlN"
        config.veToken = "cJ75jX6c9m8eObgQif7okMgb3U2398MrE1DCr1LH1neWx3x4BkL5hIqlRwbrC1Hf6aVQRcvSWrFuXbf8ROmHIHTz1X5daYyh6Gmb+J/cI1deUayXIgmE2KUIlYyjMgDHL0gbyUNl6+XJhspB1nZP6tHyDfBhSISdQ5Aq6/1zqilrPYJSjo547IkdVg2xfuhDACrbgs1iu9LqI7pHDc+JEOSTYuHA3Fe5aVyVkwBRqBNf1EgrsgMtZ1W1U2GAZpLMQke7DUvB7WDaAb+GdZSAcovLM8WjGzZiIV4Cj6YTFYBtNH3WfM15954YRcS1rOeYhPmZN7/N6yYmBBz3OZKx/sD8OyFk5cY6Q9PdaqDF14qPhUIy0rqX79tqxNwyOLnKYWR+e/8nrG2N8NDef9BZ7dDSREVkgiDl8ELmDgKYzraUxyy5MOV1hbITl6nieiuI/oeVu0z3snytsDt4yMyOdsaT3acngkJJhHX3tz2dh+R5v2diJW6+VsybE6166eJm5swVLAxqdn1wcQuPX64hKHXuc6SssjwddRKqMgKrCzHrGdW5IJKQC25lOdY4ENMnSV8HwRUaaEZQJPBIyC605H6VQCDwUTHGL4VKu5enIA/itdoYJY8lJ9YQ7ZSWFZO21gTaAPhEj1JuuToYg6wh9xIPgFhKbpLknJzweKKxyzgtM3Ndf6Z4czyFrCKhJgZm+yEkl5/CplXWJ/MZT2tH9yIjnZlySfUHZFwJtB78MNdrxd3p+ux/me2CK70uvSBAB7pXautnEEpQdkQ3TDSJEgMvMN1QGZ09LaDPOINWjH2xl2aNCFMkB7Q5p1AqJFu69tZjzwRorFvLETwJNpBXZSP9M660/86y5MRPhvbFgWIrZwhM6/sf66/3MoRyz5cmwQ9fiYNheTCPLs+TVAkvKulQFZnSF2PgcuEBgqFCR03pcS2wn6C/QjMbIIa8B26aImgPzBzi9WqEjZjoVrb1OxkkSsJZFpvLWXr1YQslRut4sR9zldy1BijVN2AJdKnP2D1Zu9za/HodeX7dskbe2tiTX4xbfNCFPbAvubtI9UlOMsTOTdmnG7GRPykSsEO1fPmIEx0YeSlf6M1whjRzPQhhhqs3cnn8QbhDcpRj/Big3+PWeNf7c+vPjPBSYbXIYS2cNE5grP56/1Pv+VqftNMQP5dHIQJ7A1iXPabP0VPsgrlpH5KnBe/bX4jDLgP4FUWG4jl/YroGO0ETSwUWboldc6ia45pgcOCibQ9Gx/PmGdP2JzYx6QyImo3TwbDrhWhCMqYtKgwpPo+UD9lh4Q=="
        
        /// {en} Optional: According to the required functions, contact BytePlus Tech Support to provide
        config.subtitleAppId = ""
        config.subtitleToken = ""
        config.volcAccessKey = ""
        config.volcSecretKey = ""

        CKEditorEngine.shared().start(with: config)
    }
```


<span id="1439cc4f"></span>
# Starting the UI interface

Once Video Editor SDK has been initialized, you can start the UI interface and begin using its functions. This section provides code samples for calling the recording, duet, editing, and draft box pages, and for obtaining the exported video URL.

<span id="8ee8aa2b"></span>
## Recording page

Call the recording page using the following code.

```objectivec
    @IBAction func goRecord(_ sender: Any) {
        let vc = CKRRecorderViewController()
        vc.injectedContainer = CustomServiceContainer()
        let nav = UINavigationController.init(rootViewController: vc)
        nav.modalPresentationStyle = .fullScreen
        present(nav, animated: true)
    }
```


<span id="54adaf1f"></span>
## Duet page

Call the duet page using the following code.

```objectivec
    @IBAction func goDuet(_ sender: Any) {
        CKRResourcePicker().pickResources { [weak self] resources, error, cancel in
            let vc = CKRDuetViewController()
            let model = resources.first
            guard let url = model?.url() else { return }
            vc.duetURL = url
            vc.injectedContainer = CustomServiceContainer()
            let nav = UINavigationController.init(rootViewController: vc)
            nav.modalPresentationStyle = .fullScreen
            nav.modalPresentationStyle = .fullScreen
            self?.present(nav, animated: true)
        }
    }
```


<span id="db1f0189"></span>
## Editing page

Call the editing page using the following code.

```objectivec
    @IBAction func goEdit(_ sender: Any) {
        CKRResourcePicker().pickResources { [weak self] resources, error, cancel in
            if resources.count <= 0 { return }
            let vc = DVEUIFactory.createDVEViewController(withResources: resources, injectService: CustomServiceContainer())
            self?.navigationController?.pushViewController(vc, animated: true)
        }
    }
```


<span id="2c52b553"></span>
## Draft box page

Call the draft box page using the following code.

```objectivec
    @IBAction func goDraft(_ sender: Any) {
        let vc = CKEDraftBoxController()
        vc.serviceInjectContainer = CustomServiceContainer()
        self.present(vc, animated: true)
    }
```


<span id="e4bab3a5"></span>
## Getting the exported video URL

Add a callback class to get the exported video in`editorDidExportedVideo`.

```objectivec
import UIKit

@objc class CustomServiceContainer: NSObject, DVEVCContextExternalInjectProtocol {
    lazy var resourceLoader: DVEResourceLoaderProtocol = {
        return CKRResourceLoader()
    }()
    lazy var eventDelagate: DVEEditorEventProtocol = {
        return CustomEditorEventDelegate()
    }()
    
    func provideResourceLoader() -> DVEResourceLoaderProtocol {
        resourceLoader
    }
    
    func provideEditorEvent() -> DVEEditorEventProtocol {
        eventDelagate
    }
}

class CustomEditorEventDelegate: NSObject, DVEEditorEventProtocol {
    func editorDidExportedVideo(_ viewController: UIViewController, result success: Bool, videoURL url: URL?, draftID: String) {
        if success, let url = url {
            // Process the video.
            UISaveVideoAtPathToSavedPhotosAlbum(url.path, nil, nil, nil)
        }
        //  Close the SDK. 
        viewController.dve_close(animated: true)
    }
}
```
