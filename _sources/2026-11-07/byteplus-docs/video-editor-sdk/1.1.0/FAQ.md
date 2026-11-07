---
title: "FAQ"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-faq_1_1_0"
---

<span id="afc50ae8"></span>
# 1. How to check if the authorization is successful?


* **Android**: When using `EOQuickInitHelper` to integrate, check the returned value of the `result` parameter. For more information, refer to the **Offline authentication** section in [SDK initialization—Android](https://docs.byteplus.com/docs/video-editor-sdk/docs-initializing-the-sdk-Android_1_1_0).

* **iOS**: \*\*\*\* Refer to the sample code documented in the **Offline authentication** section [Authentication configuration and feature](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-authentication-configuration-and-feature_1_1_0).


<span id="77a95567"></span>
# 2.How to get the file path of the exported video?


* **Android**: You can specify the export path when calling the **exportVideo** API. For more information, see [Export function APIs](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-export-function-apis_1_1_0).

* **iOS**: Refer to the **Export a video** section in [Video export APIs for iOS](https://docs.byteplus.com/docs/video-editor-sdk/docs-video-export-apis-for-ios_1_1_0).


<span id="0eedc0e4"></span>
# 3. Does Video Editor SDK support customizing watermark settings?

Yes it does. For more information, refer to the following:


* **Android**: [Export function APIs](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-export-function-apis_1_1_0).

* **iOS**: [Video export APIs for iOS](https://docs.byteplus.com/docs/video-editor-sdk/docs-video-export-apis-for-ios_1_1_0).


<span id="726be64e"></span>
# 4.How do I configure a thumbnail?

Video Editor SDK supports selecting video thumbnails through video clips or from your album. For more information, refer to the following:


* **Android**: [Export function APIs](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-export-function-apis_1_1_0).

* **iOS**: [Video export APIs for iOS](https://docs.byteplus.com/docs/video-editor-sdk/docs-video-export-apis-for-ios_1_1_0).


<span id="b862bbc1"></span>
# 5.How to customize the video export duration？

Video Editor SDK currently does not support this feature.

<span id="12ad3856"></span>
# 6. How do I configure the video export parameters such as resolution and frame rate?


* **Android**: Refer to `EffectOneExportViewHelper->doExportAction` in the demo project. You can configure the frame rate, resolution, and software resolution by using `EOOutputVideoSettings`. For more information, see [Export function APIs](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-export-function-apis_1_1_0).

* **iOS**: Refer to the code samples documented in the **Set the resolution** and \*\*Set the FPS \*\*sections in [Video export APIs for iOS](https://docs.byteplus.com/docs/video-editor-sdk/docs-video-export-apis-for-ios_1_1_0).


<span id="0c96e586"></span>
# 7.Are there any video size or time limits during the import process in the Editor feature UI?


* **Duration**: <=1 hour.

* **Size**: No limit.


For more information on the size configurations, refer to the following:


* **Android**: [Android Editor module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-editor-module-configuration-and-features_1_1_0)

* **iOS**: [Editor module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-editor-module-configuration-and-features_1_1_0)


<span id="2504e5cc"></span>
# 8. Does the export video format support customization?

Video Editor SDK currently does not support this feature.

<span id="7846085d"></span>
# 9.How do I obtain information on imported resources (including videos and images), such as resolution, and size of videos?

Video Editor SDK currently does not support this feature.

<span id="30ebb5be"></span>
# 10.How to import resources for the editor screen through a local path if I directly open the editor screen?


* **Android**: Construct **List**as a parameter to start the editing page. After selecting materials from the album page, jump to the logical part of the editing page. Refer to the code samples in [Android Editor module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-editor-module-configuration-and-features_1_1_0).

* **iOS**: Refer to the code samples in [Editor module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-editor-module-configuration-and-features_1_1_0).


<span id="64ad4285"></span>
# 11.How to disable or enable default features associated with beauty effects?


* Currently, default beauty effects features include skin smoothing, skin lightening, sharpening, face slimming, and larger eyes. You can configure these settings in the specific configuration file under the `Panel_configs/recorder_beauty.json` directory.

* If you want to disable some of these features, you can open the `recorder_beauty.json` file and set the `defaultOn` field of the corresponding feature that you don't want to use to `0`.

* If you want to enable a default beauty effects feature, you can change the `defaultOn` field of the corresponding feature to `1`.


<span id="33b86fe8"></span>
# 12.How to obtain videos that you have produced after video shooting (Un\-edited videos)?


* **Android**: When configuring `RecorderInitConfig`, the callback function of the `finishAction` parameter provides all related information of videos that you have filmed using the camera feature. For more information, refer to [Android Camera module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-camera-module-configuration-and-features_1_1_0).

* **iOS**: Refer to the **Callback function** section in [Camera module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-camera-module-configuration-and-features_1_1_0).


<span id="a4c516f4"></span>
# 13.What permissions do I need to grant on my device when using Video Editor SDK? Are these permissions required and what are they for?


* **Android**:

   * camera

   * microphone

   * Storage

   * Get mobile phone information

* **iOS**: Refer to the **Configuring permissions** section in [iOS SDK Quick Start Guide](https://docs.byteplus.com/docs/video-editor-sdk/docs-getting-started-with-ve-ios_1_1_0).


<span id="deb42bad"></span>
# 14.What programming languages does the SDK support?


* **Android**: \*\*\*\* Java/Kotlin/Jetpack Compose

* **iOS**: \*\*\*\* OC/Swift


<span id="5e35c4ba"></span>
# **15.Does the SDK support cross\-platform language/framework access, such as Flutter or RN?** 

Supported.

<span id="c2f7994d"></span>
# 16.What languages does Video Editor SDK support?

If you want to support multiple available languages for your application, contact the BytePlus Video Editor team first. This helps to prevent potential UI\-related exceptions caused by multilingual settings.


* **Android**: The SDK comes with Chinese and English configurations. For other languages, customize the configurations as follows.

   * Materials

      Supports Chinese and English languages. When initializing the resource, call the **setSysLanguage(Locale.getDefault().language)**  interface to configure the material text language. English is used by default for non\-Chinese systems.

   * UI

      Refer to the key of the text corresponding to each UI page provided in the UI skin replacement document. In hosted project value, add the language in the format of `values-xxx` and add the corresponding key for the added value in the `values-xxx/strings.xml` file.

* **iOS**: The SDK comes with Chinese and English configurations. You can add new language configurations in the `EOLocalResources.bundle/BuiltInResource/Strings` directory.

   Follow the file naming rule: `EffectOne-{Language}.strings`


<span id="3d137af6"></span>
# 17.**How do I integrate Android without the source code?** 

When upgrading the environment to Gradle 8.2 sdk34 JDK 17, simply modify the corresponding environment variables.

**References:** 


* Refer to the Gradle official compatibility document: [Gradle Compatibility Documentation](https://gradle.github.net.cn/userguide/compatibility.html#compatibility).

* Refer to the Android official AGP compatibility document: [Android AGP Compatibility Documentation](https://developer.android.com/build/releases/past-releases/agp-8-0-0-release-notes?hl=zh-cn).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86f63a7e857f4cf4ad6f75a86a9566bd~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1762469d42d14c20b3b609e06a4a35ed~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5033ae4115384aee9d8bcd9031736403~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ff9084ea42f42e19107a4b853911e56~tplv-goo7wpa0wc-image.image) </span>


<span id="5f89b00a"></span>
# 18. **How do I navigate back to the homepage from the export page?** 

There are different ways to navigate back to the homepage, depending on whether it is Android or iOS.

<span id="7df71d05"></span>
## iOS


1. Open `EOExportViewController`.

2. To call the method within a block, use the following code:

   ```objectivec
   -(void)dismissToRootViewController  {
       UIViewController *vc = self;
       while (vc.presentingViewController) {
         vc = vc.presentingViewController;
       }
       [vc dismissViewControllerAnimated:YES completion:nil];
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beb1bb7ea8f744579ae029a002c21b36~tplv-goo7wpa0wc-image.image) </span>


<span id="1412114a"></span>
## Android


* Configure the listener parameter as follows when exporting the video.

   ```TypeScript
   eoExportManager.exportVideo(outputPath, outputSetting, exportListener = ActivityResultExportListener())
   ```
   

   ```TypeScript
   class ActivityResultExportListener(eoRootUIViewModel: EffectOneExportRootUIViewModel) :
       EOExportListener(eoRootUIViewModel) {
       companion object {
           const val RESULT_EXPORT_PATH = 10004
           const val KEY_OUTPUT_PATH = "KEY_OUTPUT_PATH"
       }
   
       override fun onDone(outputPath: String) {
           LogKit.d(TAG, "onCompileDone() outputPath  $outputPath")
           EffectOneSdk.activityManager.finishActivities(null, RESULT_EXPORT_PATH, Intent().apply {
               putExtra(KEY_OUTPUT_PATH, outputPath)
           })
       }
   }
   ```
   

* On the startup page, accept callbacks through `onActivityResult`.

   ```TypeScript
   override fun onActivityResult(requestCode: Int, resultCode: Int, data: Intent?) {
       super.onActivityResult(requestCode, resultCode, data)
       if (resultCode == ActivityResultExportListener.RESULT_EXPORT_PATH) {
           LogKit.d("EffectOneMainActivity",
               "requestCode:$requestCode, " +
                       "result:$resultCode, " +
                       "data:${data?.getStringExtra(ActivityResultExportListener.KEY_OUTPUT_PATH)}")
       }
   }
   ```
   


<span id="036d957a"></span>
# 19. How do I integrate the SDK Log？


* **Android**: Refer to the following code to integrate the SDK log.

   ```Kotlin
   EffectOneSdk.logger = DebugLogger() //Register the default logger printing method. This can be replaced with the your own Logger.
   
   // Inherit AbsLogger
   abstract class AbsLogger : LogKitProtocol {
   
       private var prio = LogPriority.DEBUG
   
       private val blockTagSet: Set<String> = emptySet()
   
       protected abstract fun log(priority: LogPriority, tag: String?, message: String, t: Throwable?)
   
       override fun changeLogPriority(priority: LogPriority) {
           prio = priority
       }
   
       override fun v(tag: String?, message: String) {
           prepareLog(LogPriority.VERBOSE, tag, t = null, message)
       }
   
       override fun d(tag: String?, message: String) {
           prepareLog(LogPriority.DEBUG, tag, t = null, message)
       }
   
       override fun i(tag: String?, message: String) {
           prepareLog(LogPriority.INFO, tag, t = null, message)
       }
   
       override fun w(tag: String?, message: String) {
           prepareLog(LogPriority.WARN, tag, t = null, message)
       }
   
       override fun e(tag: String?, message: String?, t: Throwable?) {
           prepareLog(LogPriority.ERROR, tag, t = t, message)
       }
   
       override fun json(priority: LogPriority, tag: String?, msg: String) {
           prepareLog(priority, tag, t = null, msg)
       }
   
       /** Return whether a message at `priority` or `tag` should be logged. */
       protected open fun isLoggable(tag: String?, priority: LogPriority): Boolean {
           if (priority < prio) return false
           return !(!TextUtils.isEmpty(tag) && blockTagSet.contains(tag))
       }
   
       private fun prepareLog(priority: LogPriority, tag: String?, t: Throwable?, msg: String?) {
           // Consume tag even when message is not loggable so that next message is correctly tagged.
           if (!isLoggable(tag, priority)) {
               return
           }
   
           var message = msg
           if (message.isNullOrEmpty()) {
               if (t == null) {
                   return
               }
               message = getStackTraceString(t)
           } else {
               if (t != null) {
                   message += "\n" + getStackTraceString(t)
               }
           }
   
           log(priority, tag, message, t)
       }
   
       private fun getStackTraceString(t: Throwable): String {
           // Don't replace this with Log.getStackTraceString() - it hides
           // UnknownHostException, which is not what we want.
           val sw = StringWriter(256)
           val pw = PrintWriter(sw, false)
           t.printStackTrace(pw)
           pw.flush()
           return sw.toString()
       }
   }
   ```
   

* **iOS**: Refer to the following code to integrate the SDK log.

   ```Swift
   /// 1. A class named `CustomLogger` is defined which implements the `EOSDKLogProtocol`.
   class CustomLogger: NSObject, EOSDKLogProtocol {
       func logMsg(_ msg: String, tag: String, type: EOSDKLogType, filename: UnsafePointer<CChar>, funcName: UnsafePointer<CChar>, line: Int32) {
           /// 3. Print or write to a file as needed. Only log entries above the EOSDKLogTypeInfo level are written to the file.
           print("test logger \(msg)");
       }
   }
   
   /// 2. `EOSDKLogManager` injects an instance of the `CustomLogger`. 
   EOSDKLogManager.shared().injectLogger(CustomLogger())
   ```
   


<span id="67afeb5b"></span>
# 20. How do I remove the Beauty and Effects Sticker UI buttons?

The BytePlus Video Editor SDK does not include beauty and effects sticker features by default. However, the demo includes these features for demonstration purposes. Customers who do not wish to use these features should follow the provided guide to hide them.

This ensures that only the desired functionalities are displayed and used in the final product.

When you are integrating BytePlus Video Editor SDK, you can remove the buttons corresponding to those features from the UI by following the guide.


|**Camera**<br><br>**Beauty** |**Camera**<br><br>**Effects Sticker** |**Preview Editor**<br><br>**Effects Sticker** |
|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acd04ade80d548b79f6363e69aba5011~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20607a99ce924e0cb872dc530dc124e5~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39e20a3e6c5b4259b892dd3158c13f4f~tplv-goo7wpa0wc-image.image) </span> |


<span id="dcf269a7"></span>
## Android

You can remove the UI button of Beauty & Effects Sticker by modifying the **`initConfigs`** method of **`EOQuickInitHelper`**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure that you have used <strong><code>EOQuickInitHelper</code></strong> to complete access to EffectOneSDK Android, and then you can enter the shooting page and editing page normally.</div>



1. Hide the face sticker button at the lower left of the shooting screen by adding `it.enableEffectStickerBtn = false` in `RecorderInitConfig`.

   ```Kotlin
   private fun initConfigs() {
       //Overall configuration of the shooting module
       EffectOneConfigList.configure(RecorderInitConfig()) {
           it.finishAction = { activity, list, musicItem ->
               val options = ActivityOptionsCompat.makeCustomAnimation(activity, 0, 0)
               EditorMainActivity.startEditorActivityFromRecord(activity, list.map { resourceItem ->
                   com.volcengine.easyeditor.api.MediaItem(
                       path = resourceItem.path,
                       type = if (resourceItem.type == RecordMediaType.VIDEO) MediaType.VIDEO else MediaType.IMAGE,
                       duration = resourceItem.duration,
                       speed = resourceItem.speed
                   )
               } as ArrayList<com.volcengine.easyeditor.api.MediaItem>, options.toBundle(), musicItem)
           }
           it.albumConfig = AlbumConfig(
               allEnable = true,
               imageEnable = true,
               videoEnable = true,
               maxSelectCount = EffectOneSdk.albumMaxSelectedCount,
               //maxDuration Unit:ms
               maxDuration = 60 * 60 * 1000L,
               finishClazz = StartEditorFinishImpl::class.java
           )
           it.enableEffectStickerBtn = false //Added to hide special effect stickers
       }
       ...
   }
   ```
   

2. Hide the beauty button in the sidebar of the shooting screen by adding `RecorderMenuUIConfig` in the `initConfigs` method.

   ```Kotlin
   private fun initConfigs() {
       ...
       EffectOneConfigList.configure(RecorderMenuUIConfig()) {
           it.menuList = listOf(
               RecorderItemType.ITEM_FLIP,
               RecorderItemType.ITEM_FLASH,
               RecorderItemType.ITEM_COUNTDOWN,
               RecorderItemType.ITEM_FILTER,
               RecorderItemType.ITEM_SPEED
           )
           it.unfoldCount = 4
       }
   }
   ```
   

3. Hide the face sticker button in the sidebar of the editor screen by adding `EditorMenuUIConfig` in the `initConfigs` method.

   ```Kotlin
   private fun initConfigs() {
       ...
       EffectOneConfigList.configure(EditorMenuUIConfig()) {
           it.menuList = listOf(
               EditorItemType.ITEM_PRO,
               EditorItemType.ITEM_TEXT_STICKER,
               EditorItemType.ITEM_INFO_STICKER,
               EditorItemType.ITEM_FILTER,
               EditorItemType.ITEM_EFFECT,
               EditorItemType.ITEM_AUDIO_FILTER
           )
           it.unfoldCount = 5
       }
   }
   ```
   

4. Hide the sidebar on the camera screen by adding `it.foldenable = false` in `RecorderMenuUIConfig` to disable the collapse feature.

   ```Kotlin
   private fun initConfigs() {
       ...
       EffectOneConfigList.configure(RecorderMenuUIConfig()) {
           it.menuList = listOf(
               RecorderItemType.ITEM_FLIP,
               RecorderItemType.ITEM_FLASH,
               RecorderItemType.ITEM_COUNTDOWN,
               RecorderItemType.ITEM_FILTER,
               RecorderItemType.ITEM_SPEED
           )
           it.unfoldCount = 4
           it.foldEnabled = false 
       }
   }
   ```
   

5. Hide the sidebar on the editor screen by adding `it.foldenabled = false` in `EditorMenuUIConfig` to disable the collapse feature.

   ```Kotlin
   private fun initConfigs() {
       ...
       EffectOneConfigList.configure(EditorMenuUIConfig()) {
           it.menuList = listOf(
               EditorItemType.ITEM_PRO,
               EditorItemType.ITEM_TEXT_STICKER,
               EditorItemType.ITEM_INFO_STICKER,
               EditorItemType.ITEM_FILTER,
               EditorItemType.ITEM_EFFECT,
               EditorItemType.ITEM_AUDIO_FILTER
           )
           it.unfoldCount = 5
           it.foldEnabled = false
       }
   }
   ```
   

6. Disable the default beauty configuration to customize your project's beauty effects by using the following:

   ```Kotlin
   EffectOneConfigList.configure(BeautyUIConfig()) {
       it.resourceLoader = DefaultLocalResourceLoader.instance
       //it.defaultBeautyAction = {
       //    EOResourceManager.syncLoadConfigByPanelKey(EOResourcePanelKey.RECORDER_BEAUTY.value, true).tabs
       //}
   }
   
   
   private fun initResourceData() {
       // Copy the offline authentication file to the app's private directory based on the file name. 
       if (!licenseFile.exists()) {
           EOUtils.fileUtil.copyAssetFile("${EOUtils.pathUtil.assetsLicensePath}/${licenseFileName}", licenseFile.absolutePath)
       }
       // Load the default beauty resources 
       //CoroutineScope(Dispatchers.IO).launch {
       //    EOResourceManager.loadDefaultBeautyResources()
       //}
   }
   ```
   


<span id="b42cb987"></span>
## iOS

Ensure that you have completed the Video Editor SDK integration. For more information, refer to [iOS SDK Quick Start Guide](https://docs.byteplus.com/docs/video-editor-sdk/docs-getting-started-with-ve-ios_1_1_0). After integration, you can access the camera and editor screens.

<span id="5805fc75"></span>
### Camera screen

To hide the beauty and face effect button, use the following code:

```Swift
// Construct the default configuration of the camera component
let config = EORecorderConfig { initializer in
    // Configure recorder UI
    initializer.configRecorderViewController { vcInitializer in
        // Hide sticker button
        vcInitializer.stickerButtonHidden = true
        // Configure side bar to hide beauty button, remove EORecordBarItemBeautyKey
        vcInitializer.sideBarConfig.itemKeys = [
            EORecordSideBarItemKey.barItemRotateCameraKey,
            EORecordSideBarItemKey.barItemFlashKey,
            EORecordSideBarItemKey.barItemTimerKey,
            EORecordSideBarItemKey.barItemFiltersKey,
            //EORecordSideBarItemKey.barItemBeautyKey,
            EORecordSideBarItemKey.barItemSpeedKey
        ]
        vcInitializer.sideBarConfig.unfoldCount = 4
        //  If need to disable the sidebar folding function, open the code commented below
        // vcInitializer.sideBarConfig.foldEnabled = false
    }
}
```


For more information on the other camera UI related configurations, refer to [Camera module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-camera-module-configuration-and-features_1_1_0).

<span id="bb26089e"></span>
### Editor screen

To hide the effects button, use the following configurations,

```Swift
//  Construct editing component default configuration
let config = EOEditorConfig { initializer in
    // Configure editor UI
    initializer.configVideoEditorViewController { vcInitializer in
        //  Configure side bar to hide face sticker button, just remove EOEditorBarItemKeyFaceSticker
        vcInitializer.sideBarConfig.itemKeys = [
            EOEditorBarItemKey.clip,
            EOEditorBarItemKey.text,
            EOEditorBarItemKey.sticker,
            EOEditorBarItemKey.filter,
            EOEditorBarItemKey.effect,
            //EOEditorBarItemKey.faceSticker,
            EOEditorBarItemKey.voice
        ]
        vcInitializer.sideBarConfig.unfoldCount = 5
        // If you need to disable the sidebar folding function, open the code commented below
        // vcInitializer.sideBarConfig.foldEnabled = false
    }
}
```


For more information on the other editor UI related configurations, refer to [Editor module configuration and features](https://docs.byteplus.com/docs/video-editor-sdk/docs-ios-editor-module-configuration-and-features_1_1_0).

<span id="3c8f119b"></span>
# 21.How do you resolve the OkHttp version compatibility issue in Android?

The Video Editor SDK has no version requirements for OkHttp. You can set your own version number according to your needs.

<span id="da602a38"></span>
# 22. Why is it recommended to run`flutter clean`before switching to another platform?

Running `flutter clean` helps remove the build artifacts from the previous platform, ensuring a fresh environment. This prevents potential conflicts or issues when switching to a different platform, such as moving from debugging on Android to iOS.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/875a19e6693e42f48441e80ca528a037~tplv-goo7wpa0wc-image.image) </span>

<span id="6954ce44"></span>
# 23. Android\-related Flutter questions

<span id="5cd4f6a9"></span>
## a. What should we do when "Invalid authentication" is displayed after startup?

Follow the steps to below to troubleshoot:


1. Check if the authentication file and applicationId are the same.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d59dc9707fb4a2eb692141914d24d2f~tplv-goo7wpa0wc-image.image) </span>

2. Check if the name of the authentication file is correct in the configuration file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a843848fde3a41a98b847726e34ae71b~tplv-goo7wpa0wc-image.image) </span>


<span id="07b32723"></span>
### 2. What should I do if there are no effects while using the tools?

Follow the steps below to troubleshoot:


1. Check the authentication file as described in the preceding step.

2. Check whether the imported editing materials and shooting materials match the authentication and applicationId.

3. If there are no problems with the above, provide the console print log to the BytePlus Video Editor SDK team.


<span id="37604848"></span>
### 3. How can I resolve conflicts by setting the app's Target and Compile SDK versions to 30?

Add the following configurations to your application's default configuration to solve the conflict issue when your application's Target and Compile SDK versions are set to 30:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b683389e8a0641b6a124fb49ff748372~tplv-goo7wpa0wc-image.image) </span>

<span id="ba2f1b2b"></span>
### 4. How do I replace the materials within my project?

Add the materials in the following directory.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaa740baaa774cc889cc214443d79ba7~tplv-goo7wpa0wc-image.image) </span>

<span id="db666cf5"></span>
# 24. Why can iOS only support compilation in the simulator, but not execution?

The iOS SDK is built on a multi\-layer architecture that includes critical components such as rendering, authentication, and algorithms. The rendering component, in particular, cannot operate within the simulator environment. Therefore, while we ensure successful compilation, we cannot guarantee identical functionality compared to running on a physical device. If you encounter any UI debugging issues on the simulator, contact the BytePlus Video Editor team for assistance.
