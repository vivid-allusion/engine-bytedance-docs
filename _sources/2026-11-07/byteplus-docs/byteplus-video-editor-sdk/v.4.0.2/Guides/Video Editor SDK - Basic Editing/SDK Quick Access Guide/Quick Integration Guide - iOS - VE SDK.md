---
title: "Quick Integration Guide - iOS - VE SDK"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-quick-integration-guide-ios-ve-sdk-v.4.0.2"
---

<span id="7111c961"></span>
# System requirements

iOS 9.0 or later

<span id="ac770367"></span>
# Step 1: Integrate the SDK into a project.

<span id="8bf8f06a"></span>
### Method 1: Integrate the SDK by using CocoPods


1. If the project has been using CocoaPods, go to Step 3.

2. In the root directory of the project, run **pod init && pod install** to get the **Podfile** file.

3. Open the **Podfile** file and add a line as follows:


```Bash
  pod 'CKEditor', :path => '../CKEditor', :subspecs => ['Arch']
  pod 'NLEEditor', :path => '../NLEEditor-iOS', :subspecs => ['CK']
  pod 'DVETrackKit', :path => '../DVETrackKit', :subspecs => ['CK']
  pod 'DVEFoundationKit', :subspecs => ['CK'], :path => '../DVEFoundationKit'
  pod 'NLEPlatform', '0.3.9', :source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'TTVideoEditor', '11.3.0.8-D',:source => 'https://github.com/volcengine/volcengine-specs.git'
  pod 'DVEInject', '0.0.5', :source => 'https://github.com/volcengine/volcengine-specs.git'
  
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
```


Copy the four libraries in the demo to the upper\-level directory of podfile.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/7d35251-_1.png) </span>

4. Run **pod install**, and then open the  **.xcworkspace** project. You can see VESDK in the **Pods/TTVideoEditor** directory.

5. Add the assets package (usually in the **resource** folder) to the project.

<span id="1fd49e32"></span>
### Method 2: Import dependency libraries of the SDK

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/d1dfd3bed321413b989c0d14f7bd1a0f~tplv-em5hxbkur4-noop.image) </span>

<span id="1cc7e067"></span>
# Step 2: Grant the app the required permissions.

```objectivec
Privacy - Microphone Usage Description. Enter the reason for using the microphone (Value).
Privacy - Camera Usage Description. Enter the reason for using the camera (Value).
Privacy - Media Library Usage Description. Enter the reason for using the media library (Value).
Privacy - Photo Library Additions Usage Description. Enter the reason for using the photo library (Value).
Privacy - Photo Library Usage Description. Enter the reason for using the photo library (Value).
```


<span id="a812743a"></span>
### Note:

If an error is returned during running after the integration, check the library files under **General** against the following list. If any files are missing, add them manually.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/40662fd341cc4825a1ef8610698f2bd2~tplv-em5hxbkur4-noop.image) </span>

<span id="c421b382"></span>
### Initialize the VE SDK


* Initializes the VE SDK. You must initialize the VE SDK before you can use it.

* **VESDK.init:** 


```objectivec
1. Import the header file.
#import <TTVideoEditor/IESMMParamModule.h>
#import <TTVideoEditor/VEPreloadModule.h>
#import <TTVideoEditor/VEConfigCenter.h>
#import <TTVideoEditor/HTSVideoData+CacheDirPath.h>
2. Configure for initialization.
if (@available(iOS 14.2, *)) {
    [[VEConfigCenter sharedInstance] configVESDKABValue:@1 key:@"veabtest_VTEncodeMode" type:VEABKeyDataType_Int];
  }
//  Enable the composer and OpenGL ES 3.0.
  [IESMMParamModule sharedInstance].composerMode = 1;
  [IESMMParamModule sharedInstance].composerOrder = 0;
  [IESMMParamModule sharedInstance].infoStickerCanUseAmazing = YES;
  [IESMMParamModule sharedInstance].editorCanUseAmazing = YES;
  IESMMParamModule.sharedInstance.useNewAudioEditor = YES;
  IESMMParamModule.sharedInstance.useNewAudioAPI = YES;
  IESMMParamModule.sharedInstance.recordCanUseAmazing = YES;
  [VEPreloadModule prepareVEContext];
   

  [IESMMParamModule sharedInstance].capturePreviewUpTo1080P = YES;
  
  Set the cache path.
  /**
 * @brief Set the path and absolute path for the draft folder. Make sure that you call it before you initialize the camera or HTSPlayer.
 */
+ (void)setCacheDirPath:(NSString *)cacheDirPath;
[HTSVideoData setCacheDirPath:@"your path"]
```



* **Authentication:** 

* Call the authentication method only after you call **VESDK.init**


```objectivec
1. Import the header file.
#import <TTVideoEditor/VETobLicense.h>
2. Register for authentication.
NSString *path = [@"ve_test_20210222_20210822_com.IESVideoEditor.demo.inhouse_v1.0.1_s0308.licbag" pathInBundle:@"licBundle"];

VELicenseRegister(path);
```



* Demo:


```objectivec
1. Import the header file.
#import <TTVideoEditor/VETobLicense.h>
2. Register for authentication.
NSString *path = [@"ve_test_20210222_20210822_com.IESVideoEditor.demo.inhouse_v1.0.1_s0308.licbag" pathInBundle:@"licBundle"];

VELicenseRegister(path);
```



* Callback method:


```objectivec
// The authentication callback for getting the error log.
void licenseCheckerCallback(NSString *message) {
  NSLog(@"licenseCheckerCallback：%@", message);
}
```



* Project logs:


```objectivec
1. Import the header file.
#import <TTVideoEditor/IESMMLogger.h>
2. Set a delegate.
[[IESMMLogger sharedInstance] setLoggerDelegate:self];
3. Implement the delegation method.
- (void)IESEditorlogToLocal:(NSString *)logString andLevel:(IESMMlogLevel)level {
  NSLog(@"%@",logString);// You can write the files as needed.
}
```



* **Set a local directory for saving algorithm models (for the recognition of faces, gestures, objects, and more)** 

   * Set the model directory before using the SDK because some effects such as beauty effects and body shaping can be implemented only under model support.

   * Call **VESDK.init** and **VEAuth.init** before you use **VERecorder** or create **VEEditor**. Otherwise, the call is invalid.


```objectivec
1. Import the header file.
#import <TTVideoEditor/IESMMParamModule.h>
2. Set ResourceFinder and pass the function pointer.
[IESMMParamModule setResourceFinder:resource_finder];
3. Implement the function.
char *resource_finder(__unused void *handle, __unused const char *dir, const char *name){
  // The path of the model folder.
  NSString *path = [@"" pathInBundle:@"TestModel"];
  path = [path stringByAppendingString:[NSString stringWithUTF8String:name]];
  NSURL *url    = [NSURL fileURLWithPath:path];
  path       = url.absoluteString;
  char *result_path = malloc(strlen(path.UTF8String) + 1);
  strcpy(result_path, path.UTF8String ?: "");
  result_path[strlen(path.UTF8String)] = '\0';
  return result_path;
}
```
