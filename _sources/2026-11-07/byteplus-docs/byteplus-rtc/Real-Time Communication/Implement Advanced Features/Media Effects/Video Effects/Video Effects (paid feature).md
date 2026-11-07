---
title: "Video Effects (paid feature)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717"
---

To add effects like beautification, filters, and stickers to locally captured videos, utilize the BytePlus Effects SDK. You can quickly access and utilize the rich set of features provided by the BytePlus Effects SDK without the necessity to interface with it as a separate entity since the RTC SDK has been engineered to encapsulate the functionalities of the Effects SDK.

Compared with accessing third\-party beautification through RTC [custom video pre-processing](https://docs.byteplus.com/en/docs/12/docs-79888) function, this strategy is faster, more convenient, and more effective.

This document introduces how to implement real\-time audio and video effects, such as filters, overlays, and augmentations, directly through the RTC SDK's interface.

## Prerequisite

* The RTC SDK version 3.50 or newer versions has been integrated into the project and the RTC video call function has been implemented. To ensure that you can use all new features, it is recommended to use the [latest version of RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707).

* The Effects SDK for the platform has been installed by extracting the [RTC SDK compressed package](https://docs.byteplus.com/en/docs/12/docs-75707).

* You have purchased the [BytePlus Effects](https://www.byteplus.com/en/product/effects). And the product license and material resource package that meet the business functional requirements have been obtained.

> Note: Please ensure that the versions of the obtained license and effect resources are **completely consistent** with that of the integrated Effects SDK to ensure the normal functioning of related functions.

* Operating system requirements:

   * Android 5.0+

   * iOS 11+ (not supported for emulators)

   * macOS 10.11+

   * Windows 7+

### Add Gradle dependencies

### Integrate Effects library and related resource

1. Download and extract the Android [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707) and obtain the smart beautification effect library file `effectAAR-release_V4.x.xLite.aar`.

2. Add the effect library file to the `app/libs` folder in the Android project. Note that if you rename the effect library file, ensure that the effect library name is consistent across the Android project. Here is an example of renaming to `ByteEffect.aar`.

   ![图片](https://tosv.byted.org/obj/social-friends-dev/docc/img/ZYeAdIp92ogeQUxNVAucGS3rn0g/ZBhnbLjdFoIcHuxLeJncusVtny2)

3. Add the smart beautification effect library by using the `implementation` field in the dependencies of the `<yourprojectname>/app/build.gradle` file under the project root directory, and click the Sync button to synchronize.

## To add BytePlus Effects to your Android app

```Groovy
dependencies {
    //...
    implementation(name: 'ByteEffect', ext: 'aar')
    implementation 'com.byteplus:BytePlusRTC:3.xx.xxx'
}
```

1. Create a new assets folder and add a custom beautification folder under it (using Effect as an example), and copy the available effect material resource files to the Effect folder.

   ![图片](https://tosv.byted.org/obj/social-friends-dev/docc/img/ZYeAdIp92ogeQUxNVAucGS3rn0g/YJO2bpN8FoG7YjxVhZ0ceNvfnsH)

> Note:

> 1. LicenseBag.bundle stores effect certificates, and other bundles store various types of material resource files.

> 2. The package name of the effect certificate must be consistent with the package name of the project, otherwise the certificate will not be valid.

### **Initialize**

1. When building\-in materials in an Android, the materials are stored in `Assets`, which cannot be accessed through a path. Therefore, you need to copy those files to the private directory of the app when you start the app for the first time.

   ![图片](https://tosv.byted.org/obj/social-friends-dev/docc/img/ZYeAdIp92ogeQUxNVAucGS3rn0g/XTagbA0Dqo2hYOxbpuvcewoSn4b)

2. The specified resource copy path can be obtained by running the getExternalResourcePath() function in the example below, and the specified path can be customized. Use `copyAssetFolder()` to copy the resources under the `assets` path to the specified resource path, ensuring both the resource path and the copy path are correct.

   ```java
   // Initialize beautification resource files
   // Copy resource files in the installation package to external storage
   public static void initVideoEffectResource() {
       Context context = mAppCxt;
       File licensePath = new File(getExternalResourcePath(), "LicenseBag.bundle");
       licensePath.deleteOnExit();
       copyAssetFolder(context, "Effect/LicenseBag.bundle", licensePath.getAbsolutePath());
       
       File modelPath = new File(getExternalResourcePath(), "ModelResource.bundle");
       if (!modelPath.exists()) {
           copyAssetFolder(context, "Effect/ModelResource.bundle", modelPath.getAbsolutePath());
       }
       File stickerPath = new File(getExternalResourcePath(), "StickerResource.bundle");
       if (!stickerPath.exists()) {
           copyAssetFolder(context, "Effect/StickerResource.bundle", stickerPath.getAbsolutePath());
       }
       File filterPath = new File(getExternalResourcePath(), "FilterResource.bundle");
       if (!filterPath.exists()) {
           copyAssetFolder(context, "Effect/FilterResource.bundle", filterPath.getAbsolutePath());
       }
       File composerPath = new File(getExternalResourcePath(), "ComposeMakeup.bundle");
       if (!composerPath.exists()) {
           copyAssetFolder(context, "Effect/ComposeMakeup.bundle", composerPath.getAbsolutePath());
       }
       File virtualPicturePath = new File(getExternalResourcePath(), "virtual_background.png");
       if (!virtualPicturePath.exists()) {
           copyAssetFile(context, "virtual_background.png", virtualPicturePath.getAbsolutePath());
       }
   }
   
   public static String getExternalResourcePath() {
       return mAppCxt.getExternalFilesDir("assets").getAbsolutePath() + "/Effect/";
   }
   
   public static String getEffectPortraitPath() {
       return getStickerPathByName("matting_bg");
   }
   
   public static String getStickerPathByName(String name) {
       return mAppCxt.getExternalFilesDir("assets").getAbsolutePath() + "/Effect/StickerResource.bundle/stickers/" + name;
   }
   
   public static String getFilterPathByName(String name) {
       return mAppCxt.getExternalFilesDir("assets").getAbsolutePath() + "/Effect/FilterResource.bundle/Filter/" + name;
   }
   
   public static String getBeautyPath() {
       return mAppCxt.getExternalFilesDir("assets").getAbsolutePath() + "/Effect/ComposeMakeup.bundle/ComposeMakeup/beauty_Android_lite";
   }
   
   public static String getStylePathByName(String name) {
       return mAppCxt.getExternalFilesDir("assets").getAbsolutePath() + "/Effect/ComposeMakeup.bundle/ComposeMakeup/style_makeup/" + name;
   }
   ```

3. When `createRTCEngine` is called to create an engine and video capture, you need to initialize the beautification resources and set the paths of the beautification resources and the certificate, and then you can enable the beautification and see these effects in the native preview screen. Note that you need to set the full path of the certificate file, that is, to the specific certificate file level. The model file path can be specified to the `ModelResource.bundle` level.

4. After the integration is completed, call `initCVResource()` to check the return value to see whether the integration is successful.

   ```java
   private void configEffect(){
       //EffectManager is a custom encapsulated class of beautification tool class
       EffectManager.initVideoEffectResource();
       String licPath = EffectManager.getLicensePath();
       String modelPath = EffectManager.getModelPath();
       IVideoEffect effect = mRTCEngine.getVideoEffectInterface();
       int result = effect.initCVResource(licPath, modelPath);
       result = effect.enableVideoEffect();
   }
   ```

5. Disable all beautification effects.

   ```java
   effect.disableVideoEffect();
   ```

### **Beautification**

Beautification effect materials are stored in the `ComposeMakeup.bundle` file. Use `setEffectNodes` to set the material path and updateEffectNode to update the effect intensity, and then the beautification effect can be displayed. For the material keys that can be set by `updateEffectNode`, refer to the [Description of Each Material Key](https://docs.byteplus.com/en/docs/effects/docs-functions-of-material-keys).

> Note: The resource path needs to be specified to the ../ComposeMakeup.bundle/ComposeMakeup/beauty_Android_lite level.

```java
private void configEffect(){
    //...Omit the beautification resource initialization and beautification configuration code
    //Beautification settings
    String composePath = EffectManager.getBeautyPath();
    List<String> nodes = Arrays.asList(composePath);
    result = effect.setEffectNodes(nodes);
    result = effect.updateEffectNode(composePath, "smooth", 0.8f);
 }
```

### **Stickers**

Sticker effect materials are stored in the `StickerResource.bundle` file. Use the `setEffectNodes`API to set the material path, and then the sticker effect can be displayed.

> Note: The sticker path needs to be specified to a specific sticker name level, such as ../StickerResource.bundle/stickers/stickers_zhaocaimao.

```java
private void configEffect(){
    //...Omit the beautification resource initialization and beautification configuration code
    //Sticker
    String stickerPath = EffectManager.getStickerPathByName("stickers_zhaocaimao");
    List<String> nodes = Arrays.asList(stickerPath);
    result = effect.setEffectNodes(nodes);
 }
```

### **Styled makeups**

Styled makeup effect materials are stored in the `ComposeMakeup.bundle` file. Use `setEffectNodes` to set the material path and updateEffectNode to update the effect intensity, and then the styled makeup effect can be displayed. For the material keys that can be set by updateEffectNode, refer to the [Description of Each Material Key](https://docs.byteplus.com/en/docs/effects/docs-functions-of-material-keys).

> Note: The styled makeup path needs to be specified to a specific styled makeup name level, such as `../ComposeMakeup.bundle/ComposeMakeup/style_makeup/aidou.*`.

```java
   private void configEffect(){
       //...Omit the beautification resource initialization and beautification configuration code
       //Styled makeups
       String stylePath = EffectManager.getStylePathByName("nuannan");
       List<String> nodes = Arrays.asList(stylePath);
       result = effect.setEffectNodes(nodes);
       result = effect.updateEffectNode(composePath,"Filter_ALL",0.8f);
       result = effect.updateEffectNode(composePath,"Makeup_ALL",0.8f);
    }
```

### **Filters**

Filter effect materials are stored in the `FilterResource.bundle` file. Use `setColorFilter`to set the material path, and then use `setColorFilterIntensity`to adjust the filter intensity. The default intensity is 1.0, with the value ranging from 0 to 1. When a value is set out of the range, it is invalid.

> Note: The filter path needs to be specified to a specific filter name level, such as ../FilterResource.bundle/Filter/Filter_01_38.

```java
private void configEffect(){
     //...Omit the beautification resource initialization and beautification configuration code
    effect.setColorFilter(filterPath);
    effect.setColorFilterIntensity(0.8f);
 }
```

### **Virtual background**

Use `enableVirtualBackground(backgroundStickerRes, source)` to enable virtual background effects. The parameter `bg_sticker_res` is to set the absolute path of the background sticker material. The parameter `source` is to set the desired background. When you want to set a custom image as the background, you need to specify the `sourceType` as `SourceTypeImage`, and set the absolute path of the custom background image through `sourcePath`.

> Note: The type of sticker effect material for the virtual background must be selected as "matting_bg".

```java
private void configEffect(){
    //...Omit the beautification resource initialization and beautification configuration code
    //Enable virtual background
    VirtualBackgroundSource backgroundSource = new VirtualBackgroundSource();
    backgroundSource.sourceType = VirtualBackgroundSourceType.IMAGE;
    backgroundSource.sourcePath = EffectManager.getExternalResourcePath() + File.separator + "virtual_background.png";
    String portraitPath = EffectManager.getEffectPortraitPath();
    effect.enableVirtualBackground(portraitPath,backgroundSource);
    //Disable virtual background
    effect.disableVirtualBackground();
 }
```

### With the legacy API

The API for smart beautification effects has been migrated from the `RTCVideo` class to the `IVideEffect` class from version 3.50. If you are using an RTC SDK before version 3.50, you need to call the API for smart beautification effects through the `RTCVideo`instance. It is highly recommended to use the latest version of the RTC SDK to experience more rich and comprehensive smart beautification effects. The legacy API will be deleted in version 3.56.

#### API call sequence

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/114717_legacy_en.png)

#### Sample codes

```java
private void configEffect(){
    EffectManager.initVideoEffectResource();
    String licPath = EffectManager.getLicensePath();

    String modelPath = EffectManager.getModelPath();
    // Beautification
    String composePath = EffectManager.getBeautyPath();
    //Filters
    String filterPath = EffectManager.getFilterPathByName("Filter_01_38");
    //Sticker
    String stickerPath = EffectManager.getStickerPathByName("stickers_zhaocaimao");
    //Makeup
    String stylePath = EffectManager.getStylePathByName("nuannan");
    List<String> nodes = Arrays.asList(composePath,stickerPath);
    int result = mRTCVideo.checkVideoEffectLicense(EffectManager.getApplicationContext(),licPath);
    mRTCVideo.setVideoEffectAlgoModelPath(modelPath);
    result = mRTCVideo.enableVideoEffect(true);
    result = mRTCVideo.setVideoEffectNodes(nodes);
    result = mRTCVideo.updateVideoEffectNode(composePath,"smooth",0.8f);
    mRTCVideo.setVideoEffectColorFilter(filterPath);
    mRTCVideo.setVideoEffectColorFilterIntensity(0.8f);
    mRTCVideo.updateVideoEffectNode(stylePath,"Filter_ALL",0.8f);
    mRTCVideo.updateVideoEffectNode(stylePath,"Makeup_ALL",0.8f);
    
    //Enable virtual background
    VirtualBackgroundSource backgroundSource = new VirtualBackgroundSource();
    backgroundSource.sourceType = VirtualBackgroundSourceType.SourceTypeImage;
    backgroundSource.sourcePath = EffectManager.getExternalResourcePath() + File.separator + "virtual_background.png";
    String portraitPath = EffectManager.getEffectPortraitPath();
    mRTCEngine.setBackgroundSticker(portraitPath,backgroundSource);
    //Disable
    mRTCEngine.setBackgroundSticker(null,backgroundSource);
 }
```

## To add BytePlus Effects to your iOS app

### Integrate Effects library and related resource

We provide two ways of integration: direct integration and integration via native pods. You can choose one as needed.

#### **Direct integration**

1. Download and extract the iOS [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707) , and obtain the `effect-sdk.framework` file of the smart beautification effects library.

2. Drag the `effect-sdk.framework` file into the project, and set its `embed` property to `Embed & Sign` mode in `General`.

   ![图片](https://tosv.byted.org/obj/social-friends-dev/docc/img/ZYeAdIp92ogeQUxNVAucGS3rn0g/Qs42bcrLyo7tUPxnkbNc1Utunng)

3. Manually add the obtained material resources to the project.

> Note: The package name of the effect certificate must be consistent with the bundle identifier of the project; otherwise, it will not work.

#### **Integrate via native Cocoapods**

Please make sure you have Cocoapods configured.

1. Download and extract the iOS [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707) , and obtain the `effect-sdk.framework` file of the smart beautification effects library.

2. Create the configuration file for the smart beautification effects SDK. Create the `BytedEffectSDK.podspec` file as follows:

   ```ruby
   Pod::Spec.new do |spec|
     spec.name         = 'BytedEffectSDK'
     spec.version      = '4.x.x' 
     spec.summary      = 'Demo for effect-sdk'
     spec.description  = 'Demo for effect-sdk'
     spec.homepage     = 'https://github.com/byteplus-sdk'
     spec.license      = { :type => 'Copyright', :text => 'Bytedance copyright' }
     spec.author       = { 'bytertc' => 'bytertc@bytedance.com' }
     spec.source       = { :path => './'}
     spec.ios.deployment_target = '11.0'
     spec.requires_arc = true
     spec.libraries = 'stdc++', 'z'
     spec.frameworks   = 'Accelerate','AssetsLibrary','AVFoundation','CoreGraphics','CoreImage','CoreMedia','CoreVideo','Foundation','QuartzCore','UIKit','CoreMotion'
     spec.weak_frameworks = 'Metal','MetalPerformanceShaders', 'Photos', 'CoreML'
     spec.resources = ['Resource/*.{bundle}']
     spec.vendored_frameworks = 'effect-sdk.framework'
   end
   ```

3. Place `BytedEffectSDK.podspec`, `effect-sdk.framework`, and `Resource` files in the same directory level:

   ```ruby
   ├── ApiExample
   │   ├── ApiExample.xcodeproj
   │   ├── ApiExample.xcworkspace
   │   ├── Podfile  
   │   ├── BytedEffectSDK  
   │   ├── ├── BytedEffectSDK.podspec
   │   ├── ├── effect-sdk.framework
   │   ├── ├── Resource
   │   ├── ├── ├── ComposeMakeup.bundle
   │   ├── ├── ├── FilterResource.bundle
   │   ├── ├── ├── LicenseBag.bundle
   │   ├── ├── ├── ModelResource.bundle
   │   ├── ├── ├── StickerResource.bundle
   
   ```

4. Add the BytePlus Effects SDK to the Cocoapods project directory. Append the following code to the `Podfile`file:

   ```ruby
   pod 'BytedEffectSDK', :path => './BytedEffectSDK'
   ```

5. Execute the following command in the directory where the `Podfile`file is located:

   ```shell
   pod install
   ```

### **Initialize**

When `createRTCEngine` is called to create the engine and video capturing is started, you need to initialize the beautification resources and set the paths of the beautification resources and the certificate before you can enable the beautification.

> Note

> You need to set the full path of the certificate file, that is, to the specific certificate file level. The model file path can be specified to the `ModelResource.bundle` level.

After the integration is completed, call `initCVResource:withAlgoModelDir:` to check the return value to see whether the integration is successful.

```swift
func configEffect() {
    let bundlePath = Bundle.main.path(forResource: "LicenseBag", ofType: "bundle")
    let licensePath = bundlePath! + "/xxxx.licbag"
    let modelBundlePath = Bundle.main.path(forResource: "ModelResource", ofType: "bundle")
    guard let effect = self.video.getVideoEffectInterface() else {
       return
    }
    let result = effect.initCVResource(licensePath: licensePath, withAlgoModelDir: modelBundlePath)
    effect.enableVideoEffect()
}
```

Disable all beautification effects.

```swift
effect.disableVideoEffect()
```

### **Beautification**

Beautification effect materials are stored in the `ComposeMakeup.bundle` file. Use `setEffectNodes` to set the material path and `updateEffectNode` to update the effect intensity, and then the beautification effect can be displayed. For the material keys that can be set by `updateEffectNode`, refer to the [Description of Each Material Key](https://docs.byteplus.com/en/docs/effects/docs-functions-of-material-keys).

> Note: The resource path needs to be specified to the ../ComposeMakeup.bundle/ComposeMakeup/beauty_IOS_lite level.

```swift
func configEffect() {
    //...Omit the beautification resource initialization and beautification configuration code
    let beautyPrefix = Bundle.main.path(forResource: "ComposeMakeup", ofType: "bundle")
    let beautyPath = beautyPrefix! + "/ComposeMakeup/beauty_IOS_lite"
    effect.setEffectNodes([beautyStylePath])
    effect.updateEffectNode(node: beautyPath, key: "smooth", value: 0.8)
}
```

### **Stickers**

Sticker effect materials are stored in the `StickerResource.bundle` file. Use the `setEffectNodes`API to set the material path, and then the sticker effect can be displayed.

> Note: The sticker path needs to be specified to a specific sticker name level, such as ../StickerResource.bundle/stickers/stickers_zhaocaimao.

```swift
func configEffect() {
    //...Omit the beautification resource initialization and beautification configuration code
    let portraitPrefix = Bundle.main.path(forResource: "StickerResource", ofType: "bundle")
    let stickerPath = portraitPrefix! + "/stickers/stickers_zhaocaimao"
    effect.setEffectNodes([stickerPath])
}
```

### **Styled makeups**

Styled makeup effects materials are stored in the `ComposeMakeup.bundle` file. Use `setEffectNodes` to set the material path and `updateEffectNode` to update the effect intensity, and then the styled makeup effect can be displayed. For the material keys that can be set by `updateEffectNode`, refer to the [Description of Each Material Key](https://docs.byteplus.com/en/docs/effects/docs-functions-of-material-keys).

> Note: The styled makeup path needs to be specified to a specific styled makeup name level, such as ../ComposeMakeup.bundle/ComposeMakeup/style_makeup/aidou.

```swift
func configEffect() {
    //...Omit the beautification resource initialization and beautification configuration code
    let beautyPrefix = Bundle.main.path(forResource: "ComposeMakeup", ofType: "bundle")
    let beautyStylePath = beautyPrefix! + "/ComposeMakeup/style_makeup/yuanqi"
    effect.setEffectNodes([beautyStylePath])
    effect.updateEffectNode(node: beautyStylePath, key: "Filter_ALL", value: 0.8)
    effect.updateEffectNode(node: beautyStylePath, key: "Makeup_ALL", value: 0.8)
}
```

### **Filters**

Filter effect materials are stored in the `FilterResource.bundle` file. Use `setColorFilter`to set the material path, and then use `setColorFilterIntensity`to adjust the filter intensity. The default intensity is 1.0, with the value ranging from 0 to 1. When a value is set out of the range, it is invalid.

> Note: The filter path needs to be specified to a specific filter name level, such as ../FilterResource.bundle/Filter/Filter_01_38.

```swift
func configEffect() {
    //...Omit the beautification resource initialization and beautification configuration code
    let filterPath = filterPrefix + "/Filter/Filter_26_Po4"
    effect.setColorFilter(filter: filterPath)
    effect.setColorFilterIntensity(intensity: 1)
}
```

### **Virtual background**

Use `enableVirtualBackground:withSource` to enable virtual background effects. The parameter `bg_sticker_path` is to set the absolute path of the background sticker material. The parameter `source`is the desired background. When you want to set a custom image as the background, you need to specify the `sourceType`as `ByteRTCVirtualBackgroundSourceTypeImage`, and use `sourcePath`to set the absolute path of the custom background image.

> Note: The type of sticker effect material for the virtual background must be selected as "matting_bg".

```swift
func configEffect() {
     //...Omit the beautification resource initialization and beautification configuration code
    //Enable virtual background
    let source = ByteRTCVirtualBackgroundSource()
    let sourcePath = Bundle.main.path(forResource: "virtual_background", ofType: "png")
    source.sourceType = .image
    source.sourcePath = sourcePath
    let bgPath = portraitPrefix + "/stickers/matting_bg"
    effect.enableVirtualBackground(bgPath, withSource: source)
    //Disable virtual background
    effect.disableVirtualBackground()
}
```

### With the legacy API

The API for smart beautification effects has been migrated from the `ByteRTCVideo`class to the `ByteRTCVideoEffect`class from version 3.50. If you are using an RTC SDK before version 3.50, you need to call the API for smart beautification effects through the `ByteRTCVideo`instance. It is highly recommended to use the latest version of the RTC SDK to experience more rich and comprehensive smart beautification effects. The legacy API will be deleted in version 3.56.

#### API call sequence

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/114717_legacy_en.png)

#### Sample codes

```swift
func configEffect() {
    let bunldePath = Bundle.main.path(forResource: "LicenseBag", ofType: "bundle")
    let licensePath = bunldePath! + "/xxxxx.licbag"
    
    let modelBundlePath = Bundle.main.path(forResource: "ModelResource", ofType: "bundle")
    let portraitPrefix = Bundle.main.path(forResource: "StickerResource", ofType: "bundle")
    let beautyPrefix = Bundle.main.path(forResource: "ComposeMakeup", ofType: "bundle")
    let filterPrefix = Bundle.main.path(forResource: "FilterResource", ofType: "bundle")
    
    let beautyPath = beautyPrefix! + "/ComposeMakeup/beauty_IOS_lite"
    let beautyStylePath = beautyPrefix! + "/ComposeMakeup/style_makeup/yuanqi"
    let stickerPath = portraitPrefix! + "/stickers/stickers_zhaocaimao"
    let filterPath = filterPrefix! + "/Filter/Filter_26_Po4"

    self.video.checkVideoEffectLicense(licensePath: licensePath)
    self.video.setVideoEffectAlgoModelPath(modelBundlePath: modelBundlePath!)
    self.video.enableVideoEffect(enable: true)
    // Stickers
    self.video.setVideoEffectNodes([beautyStylePath])
    self.video.updateVideoEffectNode(node: beautyStylePath, nodeKey: "Filter_ALL", nodeValue: 0.8)
    self.video.updateVideoEffectNode(node: beautyStylePath, nodeKey: "Makeup_ALL", nodeValue: 0.8)
    // Update the beautification intensity. The default intensity is 0, which has no effect.
    self.video.updateVideoEffectNode(node: beautyPath, nodeKey: "smooth", nodeValue: 0.8)
    let result = self.video.setVideoEffectColorFilter(filterPath: filterPath)
    print("-----------------setVideoEffectColorFilter result---------------: \(result)")
    let result2 = self.video.setVideoEffectColorFilterIntensity(intensity: 0.9)
    print("-----------------setVideoEffectColorFilterIntensity result---------------: \(result2)")
    
    // Enable and configure virtual background
    let source = ByteRTCVirtualBackgroundSource()
    let sourcePath = Bundle.main.path(forResource: "virtual_background", ofType: "png")
    source.sourceType = .image
    source.sourcePath = sourcePath
    let bgPath = portraitPrefix! + "/stickers/matting_bg"
    self.video.setBackgroundSticker(sticker: bgPath, source: source)
    // Disable virtual background
    self.video.setBackgroundSticker(sticker: nil, source: source)
}
```

## To add BytePlus Effects to your Windows/ macOS app

### Integrate the effect library and related resources

1. Unzip the [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75705) to get the effect.dll file.

2. If you have integrated the RTC SDK, copy the effect.dll file to the RTC dynamic library folder of the project directory; if not, copy the entire BytePlusRTC directory to the project directory.

3. Add the resources to the project. They can be placed in any location within the project directory.

### Initialization

After calling createRTCEngine to create the engine and start video capture, you need to initialize the Effects resources and set the paths for the Effects resources and license. By doing so, you will be able to see the effect in the local preview video. Note that you need to specify the full path of your license file. As for the model file, you only need to specify it to the level of ModelResource.bundle. After the integration is completed, you can check the return value by calling initCVResource to determine whether the integration is successful.

```cpp
auto video_effect = video->getVideoEffectInterface();
    auto ret = video_effect->initCVResource(license_path_ptr, model_path_ptr);       
    video_effect->enableVideoEffect();
```

Disable all video effects.

```cpp
auto ret = video_effect->disableVideoEffect();
```

### Beauty effect

Beauty effect resources are stored in the ComposeMakeup.bundle file. You need to set the resource path with setEffectNodes and update the effect intensity with updateEffectNode before displaying the beauty effect. For more information about resource keys that can be set with updateEffectNode, see the [Functions of Resource Keys](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later).

> Note: You need to specify the resource path to `../ComposeMakeup.bundle/ComposeMakeup/beauty_Android_lite`.

```cpp
ret = video_effect->setEffectNodes(reinterpret_cast<const char**>(&effect_node_paths[0]), data.nodeNum);
    std::string node_path = GetFilePath("cvlab_for_pc/" + data.nodePath);
    ret = video_effect->updateEffectNode(node_path.c_str(), data.nodeKey.c_str(), data.nodeValue);
```

### Sticker

Stickers are stored in the StickerResource.bundle file. You need to set the resource path with setEffectNodes before displaying the sticker effect.

> Note: You need to specify the sticker path to a specific sticker name, such as ../StickerResource.bundle/stickers/stickers_zhaocaimao

```cpp
ret = video_effect->setEffectNodes(reinterpret_cast<const char**>(&effect_node_paths[0]), data.nodeNum);
```

### Makeup style

Makeup styles are stored in the ComposeMakeup.bundle file. You need to set the resource path with setEffectNodes and update the effect intensity with updateEffectNode before displaying the makeup effect. For more information about resource keys that can be set with updateEffectNode, see the [Functions of Resource Keys](https://docs.byteplus.com/en/effects/docs/functions-of-resource-keys-v421-and-later).

> Note: You need to specify the makeup style path to a specific makeup style name, such as ../ComposeMakeup.bundle/ComposeMakeup/style_makeup/aidou

```cpp
ret = video_effect->setEffectNodes(reinterpret_cast<const char**>(&effect_node_paths[0]), data.nodeNum);
    std::string node_path = GetFilePath("cvlab_for_pc/" + data.nodePath);
    ret = video_effect->updateEffectNode(node_path.c_str(), "Makeup_ALL", data.nodeValue);
```

### Filter

The filter effects resources are stored in the `FilterResource.bundle` file. To apply a filter, set the resource path using `setColorFilter`. You can then adjust the filter intensity using `setColorFilterIntensity`. The default intensity is 1.0, and the valid range is [0, 1]. If a value outside this range is set, it will have no effect.

> Note:

> You need to specify the filter path to a specific sticker name, such as `../FilterResource.bundle/Filter/Filter_01_38`.

```cpp
std::string res_path = GetFilePath("cvlab_for_pc/" + data.resPath);
    auto ret = 0;
    ret = video_effect->setColorFilter(res_path.c_str());
    ret = video_effect->setColorFilterIntensity(data.intensity);
```

### Virtual background

You need to enable virtual background with enableVirtualBackground(background_sticker_path, source). The parameter bg_sticker_path is the absolute path of the background sticker resource and the parameter source is the desired background. If you want to set a custom image as the background, specify the source_type as kVirtualBackgroundSourceImage, and set the absolute path of the custom background image through sourcePath.

> Note: You must choose the "matting_bg" type when selecting sticker effect resources for virtual background.

```cpp
//Enable virtual background
    std::string bg_sticker_path = GetFilePath("cvlab_for_pc/" + data.bg_model_path);
    std::string source_path = GetFilePath(data.source.source_path);
    const char* source_path_ptr = source_path.c_str();
    bytertc::VirtualBackgroundSource source;
    source.source_color = data.source.source_color;
    source.source_path = source_path_ptr;
    source.source_type = data.source.source_type;
    auto ret = video_effect->enableVirtualBackground(bg_sticker_path_ptr, source);
    //Disable virtual background
    video_effect->disableVirtualBackground();
```

### With the legacy API

Since version 3.50, the Effects interfaces have been migrated from the RTCVideo class to the IVideoEffect class. If you are using an RTC SDK version before 3.50, you need to call the APIs through the RTCVideo instance. It is strongly recommended to use the latest version of the RTC SDK to experience more diverse effects. The old version interfaces will also be deleted in version 3.56.

#### API call sequence

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/114717_pc_legacy_en.png)

#### Sample codes

```cpp
auto ret = video->checkLicense(nullptr, nullptr, license_path_ptr);
    video_effect->setAlgoModelPath(model_path.c_str());
    ret = video->setVideoEffectNodes(reinterpret_cast<const char**>(&effect_node_paths[0]), data.nodeNum);
    ret = video->updateVideoEffectNode(node_path.c_str(), data.nodeKey.c_str(), data.nodeValue);
    ret = video->setVideoEffectColorFilter(res_path.c_str());
    auto ret = video->setVideoEffectColorFilterIntensity(data.intensity);
    //Enable virtual background
    std::string bg_sticker_path = GetFilePath("cvlab_for_pc/" + data.bg_model_path);
    std::string source_path = GetFilePath(data.source.source_path);
    const char* source_path_ptr = source_path.c_str();
    bytertc::VirtualBackgroundSource source;
    source.source_color = data.source.source_color;
    source.source_path = source_path_ptr;
    source.source_type = data.source.source_type;
    ret = video->setBackgroundSticker(bg_sticker_path_ptr, source);
    //Disable virtual background
    ret = video->setBackgroundSticker(nullptr, source);
```

## To add BytePlus Effects to your app with Electron

### Integrating Effects library and other resources

1. Unzip the CV SDK provided by the CV technical support team and obtain the corresponding effects library file for your target platform. Copy the library file to the project directory.

   * Windows: effect.dll，pthreadVC2.dll

   * macOS: libeffect.dylib

2. Update the packaging setting to copy the dynamic libraries to the designated directory. For the electron\-builder, specify the files to be packaged and the target path after packaging in the field of extraResources.

   * Windows: the same directory as the main program

   * macOS: `Frameworks/*`

   ```json
   "build": {
       "win": {
          "extraResources": [
           {
             "from": "./effect.dll",
             "to": "../effect.dll" 
           },
           {
             "from": "./pthreadVC2.dll",
             "to": "../pthreadVC2.dll" 
           }
         ]
       },
       "mac": {
          "extraResources": [
           {
             "from": "./libeffect.dylib",
             "to": "../Frameworks/libeffect.dylib"
           }
         ]
       }
     }
   ```

3. Add resources to the project

   ```json
   cvlab/
     ComposeMakeup.bundle/
       ComposeMakeup/
         beauty_Android_live/
         ...
     FilterResource.bundle/
       Filter/
         Filter_06_03
         ...
     ModelResource.bundle/
       handmodel/
         tt_hand_gesture_v11.1.model
         ...
       ...
     StickerResource.bundle/
       stickers/
         biaobaiqixi
         ...
   ```

### API call sequence

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/114717_electron_en.png)

### Initialize

1. Create and initialize an engine, and call [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startvideocapture) to start video capture.

```typescript
const { RTCEngine } = require('@byteplus/byteplus-electron-sdk');

const rtcEngine = new RTCEngine();
const ret = rtcEngine.createRTCEngine({
  app_id: APP_ID,
  parameters: '',
});
if (ret === 0) {
  rtcEngine.startVideoCapture();
}
```

2. Obtain an online license and save it to a local file. Call your app server to request the license. Do not store the business key or secret in the Electron app. The following example assumes that the app server returns the Base64\-encoded license in the `license` field. For the server\-side implementation, refer to the [Online Authorization Instructions](https://docs.byteplus.com/en/effects/docs/online-license-guide).

```typescript
const axios = require("axios");
const fse = require("fs-extra");
const path = require("path");
const BUSINESS_LICENSE_SERVICE_URL = "https://your-server.example.com/effects/license";

async function obtainEffectsLicense(rtcEngine) {
  const licensePath = path.join(process.cwd(), "effect.lic");
  const response = await axios.post(BUSINESS_LICENSE_SERVICE_URL, {
    authMsg: rtcEngine.getAuthMessage(),
  });
  const licenseBase64 = response.data.license;
  if (!licenseBase64) {
    throw new Error("The license service returned an empty license.");
  }
  await fse.writeFile(licensePath, Buffer.from(licenseBase64, "base64"));
  return licensePath;
}
```

3. Initialize the Effects resource. Check the return value to determine if the integration is successful.

```typescript
const algoModelPath = path.join(
  __dirname,
  "../assets/cvlab/ModelResource.bundle",
);

async function initializeEffects(rtcEngine) {
  const licensePath = await obtainEffectsLicense(rtcEngine);
  const initRet = rtcEngine.initCVResource(licensePath, algoModelPath);
  if (initRet !== 0) {
    throw new Error(`Failed to initialize Effects resources: ${initRet}`);
  }
}
```

### Beauty effect

1. Enable beauty effect

```typescript
let ret = rtcEngine.enableVideoEffect();
```

2. Disable beauty effect

```typescript
let ret = rtcEngine.disableVideoEffect();
```

3. Set the beauty effect resources

```typescript
const beautyResPath = path.join(
  __dirname,
  "../assets/cvlab/ComposeMakeup.bundle/ComposeMakeup",
);
const EffectNodesPath = [
  beautyResPath + "/beauty_Android_live",
  beautyResPath + "/reshape_live",
];
let ret = rtcEngine.setEffectNodes(EffectNodesPath);
```

4. Set the intensity of beauty effect

```typescript
// Whiten
rtcEngine.updateEffectNode(
   beautyResPath + "/beauty_Android_live",
   "whiten",
   0.8,
 );
// Smooth
rtcEngine.updateEffectNode(
   beautyResPath + "/beauty_Android_live",
   "smooth",
   0.8,
 );
 
// Enlarge eyes
rtcEngine.updateEffectNode(
   beautyResPath + "/reshape_live",
   "Internal_Deform_Eye",
   0.6,
 );
 
// Slim
rtcEngine.updateEffectNode(
   beautyResPath + "/reshape_live",
   "Internal_Deform_Overall",
   0.5,
 );
```

### Sticker

```typescript
const stickerResPath = path.join(
 __dirname,
 "../assets/cvlab/StickerResource.bundle/stickers",
);
EffectNodesPath.push(stickerResPath + "/zhaocaimao");
rtcEngine.setEffectNodes(EffectNodesPath);
```

### Filter

```typescript
// Set color filter
const filterResPath = path.join(
 __dirname,
 "../assets/cvlab/FilterResource.bundle/Filter",
);
rtcEngine.setColorFilter(filterResPath + "/Filter_06_03");
// Set filter intensity
rtcEngine.setColorFilterIntensity(0.8);
```

### Virtual background

```typescript
const url = "xxx";
const backgroundStickerPath = beautyResPath + "/matting_bg";
let source = {
 source_type: url ? 1 : 0,
 source_path: url || "",
 source_color: 0xffffffff,
};
// Enable virtual background
rtcEngine.enableVirtualBackground(backgroundStickerPath, source);

// Disable virtual background
rtcEngine.disableVirtualBackground();
```

### Face detection

```typescript
const interval = 200; // ms
const faceModelPath = algoModelPath + "/ttfacemodel/tt_face_v10.0.model";

// Enable face detection
rtcEngine.enableFaceDetection(interval, faceModelPath);

// Disable face detection
rtcEngine.disableFaceDetection();
```

## To add BytePlus Effects to your app with Flutter

### Integrate the effect library and related resources

1. The RTC SDK version 3.51 or newer versions has been integrated into the project, and the RTC video call function has been implemented.

2. Download and extract the [RTC SDK](https://docs.byteplus.com/en/docs/12/docs-75707), obtain the effect library file for the platform, and copy it to the project directory. For detailed integration method, see:

   * Android: Integration of the Android smart beautification effect library and related resources

   * iOS: Integration of the iOS smart beautification effect library and related resources

### API call sequence

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/114717_flutter_en.png)

### **Initialize**

1. Create an engine

2. Create an `RTCVideo`engine instance and enable video capture to view beautification and other effects in the native preview screen after enabling effects.

   ```dart
   RTCVideo rtcVideo = await RTCVideo.createRTCVideo(engineContext)
   rtcVideo.startVideoCapture();
   dart
   ```

3. Initialize `RTCVideoEffect`

4. Set the paths for the effect resources and the certificate, and initialize the effect resources.

   ```dart
   RTCVideoEffect videoEffect = rtcVideo.videoEffectInterface
   String licenseFile = '$FullPath/LicenseBag.bundle/licenseFileName.licbag'
   String modelPath = '$FullPath/ModelResource.bundle'
   int? ret = await videoEffect.initCVResource(licenseFile, modelPath)
   dart
   ```

### **Enable/disable video effects**

```dart
// Enable
int? ret = await videoEffect.enableVideoEffect();

// Disable
int? ret = await videoEffect.disableVideoEffect();
dart
```

### **Beauty effects**

1. Set effect materials

2. Set effect material packages to support overlay settings. Beauty effect materials are stored in the `ComposeMakeup.bundle`file. For more materials, see [Material Package Structure Description](https://docs.byteplus.com/en/docs/12/docs-102039).

   ```dart
   List<String>? effectNodesPath = [
       // Lite beautification
       '$FullPath/ComposeMakeup.bundle/ComposeMakeup/beauty_Android_lite', // iOS 为 beauty_IOS_lite
       // Lite retouch effect
       '$FullPath/ComposeMakeup.bundle/ComposeMakeup/reshape_lite',
       // Body shaping
       '$FullPath/ComposeMakeup.bundle/ComposeMakeup/body/allslim',
       ……
   ]
   int? ret = await videoEffectInterface.setEffectNodes(effectNodesPath);
   dart
   ```

3. Set effect intensity

4. After the material path is set with `setEffectNodes`, the effect intensity defaults to 0. You need to use `updateEffectNode` to update the effect intensity to display the effect. The intensity ranges from 0 to 1. Settings outside this range are invalid. For more materials, refer to [Description of Each Material Key](https://docs.byteplus.com/en/docs/12/docs-102041).

```dart
// Skin whitening
videoEffect.updateEffectNode(
    '$FullPath/ComposeMakeup.bundle/ComposeMakeup/beauty_Android_lite', // For iOS, replace with beauty_IOS_lite
    'whiten',
    0.8,
);
  
//  Face slimming
videoEffect.updateEffectNode(
    '$FullPath/ComposeMakeup.bundle/ComposeMakeup/reshape_lite',
    'Internal_Deform_Overall',
    0.5,
);

// Swan neck
videoEffect.updateEffectNode(
    '$FullPath/ComposeMakeup.bundle/ComposeMakeup/body/allslim',
    'BEF_BEAUTY_BODY_ENHANCE_NECK',
    0.6,
);
dart
```

### **Sticker effects**

Sticker effect materials are stored in the `StickerResource.bundle` file. Use `setEffectNodes` to set the material path, and then the sticker effects can be displayed. As shown below, the sticker path needs to be specified to a specific sticker name level.

```dart
effectNodesPath.add('$FullPath/StickerResource.bundle/stickers/stickers_zhaocaimao');
videoEffect.setEffectNodes(effectNodesPath);
dart
```

### **Filter effects**

1. Set effect materials

2. Filter effect materials are stored in the `FilterResource.bundle` file.

   ```dart
   // Load filters
   String filterResPath = '$FullPath/FilterResource.bundle/Filter/xxxx'
   videoEffect.setColorFilter(filterResPath);
   // Unloading filters
   videoEffect.setColorFilter(null);
   dart
   ```

3. Set effect intensity

4. After the material path is set with `setColorFilter`, you can use `setColorFilterIntensity`to adjust the filter intensity. The default intensity is 1.0, with the value ranging from 0 to 1. When a value is set out of the range, it is invalid.

   ```dart
   videoEffect.setColorFilterIntensity(0.8);
   dart
   ```

### **Virtual background**

Use `enableVirtualBackground` to enable the virtual background effect, use parameter `modelPath`to set the absolute path of the background sticker materials, and use `source`to specify an image or solid color as the background.

```dart
String modelPath = '$FullPath/ModelResource.bundle/mattingmodel';
// Set a custom image as the background
VirtualBackgroundSource source = VirtualBackgroundSource(
  sourceType: VirtualBackgroundSourceType.image,
  // Background color, required when sourceType is color, and allowed to be blank when sourceType is image
  sourceColor: 0xffffffff,
  sourcePath: '$FullPath/xxx.png',
);
// Enable
videoEffect.enableVirtualBackground(modelPath: modelPath, source:source);

// Disable
videoEffect.disableVirtualBackground();
dart
```

### **Face detection**

Use `enableFaceDetection`to register a face detection result callback observer, and add processing logic to the detection result callback.

```dart
// Enable
var observer = RTCFaceDetectionObserver(onFaceDetectResult: (FaceDetectionResult result) {
  // Process face recognition results
});
String faceModelPath = '$FullPath/ModelResource.bundle/ttfacemodel/tt_face_vxx.model';
videoEffect.enableFaceDetection(observer: observer, modelPath: faceModelPath, interval: 500);

// Disable
videoEffect.disableFaceDetection();
dart
```

## Sample project

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/thirdpart/bytebeauty/ByteBeautyActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/ImportantComponents/VolcBeauty/VolcBeautyViewController.swift)

## **FAQ**

### **Q1. What error codes may be returned by the API?**

A: Refer to the [Error Codes Returned by the API](https://docs.byteplus.com/en/docs/effects/docs-error-code-table).

### **Q2. How to determine if Android beautification resources are copied to the specified path?**

A: You can check it through the adb tool during the integration testing phase. If you don't have the adb tool, download and install it.

Commands: adb shell, ls, and cd

```java
//1. Run adb shell
~/ adb shell
//2.Run cd to go to the specified path
cupid:/ $ cd /storage/emulated/0/Android/data/com.ss.rtc.demo.advanced/
//3. View the files in the folder through the Is command, and then enter the folder by running cd
cupid:/storage/emulated/0/Android/data/com.ss.rtc.demo.advanced/files/assets $
ls
Effect
cupid:/storage/emulated/0/Android/data/com.ss.rtc.demo.advanced/files/assets $
cd Effect
cupid:/storage/emulated/0/Android/data/com.ss.rtc.demo.advanced/files/assets/Effect $ ls
ComposeMakeup.bundle   LicenseBag.bundle     StickerResource.bundle
FilterResource.bundle  ModelResource.bundle
```

### **Q3. How to troubleshoot the "\-121" error?**

A: First, check whether the file path is correct, then check if the specified resource name is correct.

### **Q4. If the resource path and the code calling sequence are correct, but the beautification effect does not work, what should I do?**

A: Complete the following self\-check:

* Check whether the package name matches the certificate.

* Check whether the called API returns an error code, and follow up based on the error code.

* Ensure that you do not mix old and new smart beautification effects APIs together.

* Check the beautification SDK logs in the console information for troubleshooting. See Common Error Logs.

### **Q5. Can the test certificate be used in the launched SDK?**

A: No, it must be replaced with an official certificate. Please [purchase the product](https://www.byteplus.com/en/product/effects) to obtain the official certificate.

### **Q6. Do I need to request another beautification certificate if I update the app or release a white\-label app?**

A: The package name and the certificate do not match. You need to apply for another one and replace it.

### **Q7. Why does using png images with the iOS virtual background not work?**

A: Xcode compresses png images. Click on the image and change the Type to Data.

![图片](https://tosv.byted.org/obj/social-friends-dev/docc/img/ZYeAdIp92ogeQUxNVAucGS3rn0g/CIVgbqdzVoWP91xmqC9chIQTnzd)

### **Q8. How does Android ensure the smart beautification effects SDK is not obfuscated?**

A: See [How to Configure Obfuscation?](https://docs.byteplus.com/en/docs/12/docs-78295).

### **Q9. It is troublesome to update the app due to large beautification resources, expiration of the beautification certificate, and changes in beautification categories. How to deal with it?**

A: It is recommended to manage beautification material resources in the cloud for management, and download the resources from the cloud to the local on demand during app usage to reduce package size and facilitate the addition/deletion/upgrade of materials.

### **Q10. Why does the actual beautification effect not match the expected effect?**

A: You may have used effects in the Lite SDK that are only available in the Standard SDK. Please check whether the effects SDK version you are using matches the effects material version.

### **Q11. What is the difference between the Standard and the Lite versions of the smart effects SDK?**

A: The Lite version does not provide 3D rendering capabilities; the Standard version provides 3D rendering capabilities to support 3D capabilities such as styled makeup, Animoji, novel stickers, and AR functions, but with a larger SDK package size. Choose the Lite version if you don't need these features and want to control app size. Consult sales for more information.

> For more frequently asked questions, refer to the [FAQs on Smart Beautification Effects](https://docs.byteplus.com/en/docs/effects/docs-faq-sdks).

### **Common Error Logs**

* The effect materials are missing, or the SDK version does not match the effect material version.

```Plain
[FileUtil.cpp 112] FileUtil: readFile: file /** **/cvlab/ModelResource.bundle/ttfacemodel/tt_face_v10.0.model is not exist -1...
plain
```

* The material file is damaged or the authorization file does not match the material.

```Plain
[FileUtil.cpp 112] FileUtil: readFile: file /** **/cvlab/ModelResource.bundle/ttfacemodel/tt_face_v10.0.model is not exist -1...
plain
```
