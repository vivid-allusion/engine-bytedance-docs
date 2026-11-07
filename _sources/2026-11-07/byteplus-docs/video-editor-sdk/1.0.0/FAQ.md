---
title: "FAQ"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-faq"
---

These are some commonly asked questions about Video Editor SDK.

<span id="4417670f"></span>
# 1. **How long does it take to integrate the new SDK?** 

The new SDK significantly reduces integration costs compared to historical versions. Estimated integration time is 2 weeks for one developer per platform (iOS & Android). Customization may extend this duration.

<span id="ad344f44"></span>
# 2. **What are the minimum supported** **OS versions?** 

We have different specifications for Android and iOS. For more information on the OS versions, refer to the following:


* **Android**: [Development environment](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android#development-environment).

* **iOS**: [Development environment.](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios#development-environment)


<span id="036d957a"></span>
# 3. What programming languages does the SDK support?

We support various programming languages. For example, for iOS we support languages like Swift and for Android we support Koitlin.

For more information on the languages, refer to the following:


* **Android**: [Development environment](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android#development-environment).

* **iOS**: [Development environment.](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios#development-environment)


<span id="67afeb5b"></span>
# 4. **Does the SDK support cross\-platform language/framework access?** 

This function is still in development. UI components of the standard SDK can be packaged and bridged to Flutter or RN, incurring adaptation costs on the customer side based on requirements.

<span id="3add8ac3"></span>
# 5. **What are the supported file** **formats and protocols?** 

These are various file formats and protocols supported in iOS and Android, for more information, refer to the following:


* **Android**: [Supported media formats](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android#supported-media-formats).

* **iOS**: [Supported media formats](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios#supported-media-formats).


<span id="126d6dd2"></span>
# 6. What is the a**pp incremental size after** **integrating with the SDK?** 

For more information on app sizes, refer to the following:


* **Android**:[ SDK package sizes.](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android#sdk-package-sizes)

* **iOS**: [SDK package sizes.](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios#sdk-package-sizes)


<span id="3c63d665"></span>
# 7. **How to customize the** **UI&UX** **of Video Editor?** 

You can customize them through the following:


* Default UI/UX is documented.

* Camera and editing modules' interaction flow is fixed.

* Users can customize UI styles, colors, layout, and icons by modifying the SDK standard configuration file.


For more information on UI customization, refer to the following:


* **Android**: [Customizable UI overview.](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-UI-customization-overview)

* **iOS**: [Customizable UI overview](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-ui-customization-overview)


<span id="e07bc137"></span>
# 8. **Does the SDK support simulator for** **iOS?** 

It compiles on the iOS simulator, but features cannot run directly. For more information on the support simulator, refer to [iOS package deliverables list](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-package-deliverables-list).

<span id="ef274ba0"></span>
# 9. **How to check the file** **path of the generated video file?** 

**Default**: video file in sandbox.

SDK provides a callback interface for the path, and customers decide its use. Sample code defaults to placing the video file in the phone's album.

For more information on how to check the file path, refer to the following:


* **Android**: [Export function APIs](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-export-function-apis).

* **iOS**: [Video export APIs for iOS](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-video-export-apis-for-ios).


<span id="5e44941a"></span>
# 10. H**ow can customers handle the downloadable asset process?** 

Assets are delivered offline by default. Customers handling on\-the\-fly asset downloads should manage corresponding development. BytePlus Video Editor SDK offers guides when needed.

For more information on downloading and importing resources, refer to the following:


* **Android**: [Android resources import and configuration](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-resources-import-and-configuration).

* **iOS**:[ iOS resources import and configuration](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-resource-import-and-configuration).


<span id="972e27b7"></span>
# 11. **How do we turn on and off features within the Video Editor?** 

By default, all features are accessible. You can only configure the sidebar in the Camera and Preview Editor features, you can configure the feature icons to control accessibility (for example, hide icons to disable certain features).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1873dc0ad0894724aabf68067ea3c06f~tplv-goo7wpa0wc-image.image) </span>

<span id="42677e14"></span>
# 12. What should I do if I encounter a `pod install` error?

To resolve the pod install error, follow these steps:


1. Ensure that you have the correct version of Xcode installed.

2. Run the following command in your terminal:

   ```C++
   ### Error
   ``
   RuntimeError - [Xcodeproj] Unknown object version (56).
   /Library/Ruby/Gems/2.6.0/gems/xcodeproj-1.21.0/lib/xcodeproj/project.rb:228:in `initialize_from_file'
   /Library/Ruby/Gems/2.6.0/gems/xcodeproj-1.21.0/lib/xcodeproj/project.rb:113:in `open'
   ```
   


<span id="abe004f8"></span>
# 13. How do I determine if the authentication process is successful?

You can check the callback function to determine whether the authentication is successful. For more information on the authentication process, refer to the following:


* **Android**: [Built-in authentication configuration](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-initializing-the-sdk-Android#step-3-built-in-authentication-configuration)

* **iOS**: [Authentication configuration and feature](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-authentication-configuration-and-feature)


<span id="78387272"></span>
# 14. Does Video Editor SDK support customizing watermark settings?

Yes it does. For more information, refer to


* **Android**: [Export function APIs](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-export-function-apis).

* **iOS**: [Video export APIs for iOS](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-video-export-apis-for-ios).


<span id="bfc630d8"></span>
# 15. How do I configure a thumbnail?

Video Editor SDK supports selecting video thumbnails through video clips or from your album. For more information, refer to


* **Android**: [Cover image APIs](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-cover-image-apis).

* **iOS**: [Video export APIs for iOS](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-video-export-apis-for-ios).


<span id="410911be"></span>
# 16. How do I configure the video export parameters such as resolution and frame rate?

Refer to `EffectOneExportViewHelper->doExportAction` in the demo project. You can configure the frame rate, resolution, and software resolution by using `EOOutputVideoSettings`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We currently do not support configuring code rates.</div>


For more information, refer to


* **Android**: [Android dependency data models](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-dependency-data-models).

* **iOS**: [Set the resolution](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-video-export-apis-for-ios#set-the-resolution) and [Set the FPS](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-video-export-apis-for-ios#set-the-fps).


<span id="12b7223c"></span>
# 17. Are there any video size or time limits during the import process in the Editor feature UI?


* **Duration**: <=1 hour

* **Size**: No limit


For more information on the size configurations, refer to


* **Android**: [Android Editor module configuration and features](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-editor-module-configuration-and-features).

* **iOS**: [Editor module configuration and features](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-editor-module-configuration-and-features).


<span id="f5cc35ac"></span>
# 18. How do I obtain information on imported resources (including videos and images), such as resolution, and size of videos?

Video Editor SDK currently does not support this feature.

<span id="c384a00a"></span>
# 19. How to import resources for the editor screen through a local path if I directly open the editor screen?

<span id="7c32c9d4"></span>
## Android

Use the following code to construct a parameter named `List<MediaItem>` to start the editor screen.

```Kotlin
@Parcelize
data class MediaItem(
    val path: String,              // The resource path.
    val type: MediaType,           // The respurce type, such as video or image.
    val duration: Long,            // The duration is measured in milliseconds. 
    val timeClipStart: Long = -1L, // This parameter is measured in milliseconds.
    val timeClipEnd: Long = -1L,   // This parameter is measured in milliseconds.
    val speed: Float = 1F          // The playback speed. The speed setting doesn't work for images. 
) : Parcelable
```


```Kotlin
EditorMainActivity.startEditorActivityFromAlbum(activity, mediaList.map {
    com.volcengine.easyeditor.api.MediaItem(
        path = it.path,
        type = if (it.isVideo()) MediaType.VIDEO else MediaType.IMAGE,
        duration = if (it.isVideo()) it.duration else 3000
    )
} as ArrayList<com.volcengine.easyeditor.api.MediaItem>)
```


<span id="4b144ee7"></span>
## iOS

Construct a model that aligns with the protocol specified by `EOMediaAssetProtocol` and configure `sceneConfig.resources` using this model you just built. For more information, refer to [Editor module configuration and features](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-ios-editor-module-configuration-and-features).

<span id="432e5dc0"></span>
# 20. How to disable or enable default features associated with beauty effects?


* Currently, default beauty effects features include skin smoothing, skin lightening, sharpening, face slimming, and larger eyes. You can configure these settings in the specific configuration file under the `Panel_configs/recorder_beauty.json` directory.

* If you want to disable some of these features, you can open the `recorder_beauty.json` file and set the `defaultOn` field of the corresponding feature that you don't want to use to `0`.

* If you want to enable a default beauty effects feature, you can change the `defaultOn` field of the corresponding feature to `1`.


<span id="3f69391f"></span>
# 21. How to obtain videos that you have produced after video shooting (Un\-edited videos)?

<span id="470b6cc9"></span>
## Android

When configuring `RecorderInitConfig`, the callback function of the `finishAction` parameter provides all related information of videos that you have filmed using the camera feature.

For more information on retrieving the videos, refer to [Export function APIs](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-export-function-apis).

<span id="52593bbb"></span>
## iOS

In the implementation details of the `delegate` function in the camera module, you can check the `info.mediaAssets` function to retrieve a list of media assets that you have filmed. For more information, refer to Video export APIs for iOS.

<span id="608342d3"></span>
# 22. What permissions do I need to grant on my device for when using Video Editor SDK in Android? Are these permissions required and what are they for?

For Android and iOS, there are specific permissions to be granted. For more information, refer to the following:

**Android**: [Getting started with Android](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-android#runtime-permissions).

**iOS**: [Configuring permissions](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-getting-started-with-ve-ios#step-4-configuring-permissions).

<span id="2a7424a9"></span>
# 23. What languages does Video Editor SDK support?

If you want to support multiple available languages for your application, contact the BytePlus Video Editor team first. This helps to prevent potential UI\-related exceptions caused by multilingual settings.

<span id="8d142e03"></span>
## Android

The VE SDK for Android has built\-in multilingual configurations for Chinese and English. You can customize the default settings to use other available languages.

**To modify built\-in text**:


1. Refer to the UI customization file to retrieve information on the key\-value pair of text for all changeable UI elements.

2. Add the value for the corresponding language under the directory of the host project.

3. Add the value according to the corresponding key in `values-xxx/strings.xml` file.


<span id="eddc7937"></span>
## iOS

The VE SDK for iOS has built\-in multilingual configurations for Chinese and English. You can add new settings under the`EOLocalResources.bundle/BuiltInResource/Strings` directory.

Create a filename for the configuration file to look like this：`EffectOne-{Language}.strings`

<span id="8c14fef5"></span>
# 24. What should I do if I encounter errors stating "cannot find xxx_music.json file" while integrating the Android SDK?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a72532948a6440edafd76bc5c454bf03~tplv-goo7wpa0wc-image.image) </span>

If you encounter errors regarding the absence of the xxx_music.json file during Android SDK integration, follow these steps:


1. Locate the file `EOQuickInitHelper.kt` in the directory business/src/main/java/com/volcengine/effectone/business/EOQuickInitHelper.kt.

2. Within EOQuickInitHelper.kt, find the method named `initResourceData()`.

3. Replace the contents within the red brackets with the following items:

   1. `put(EOResourcePanelKey.PREVIEW_EDITOR_MUSIC, "EOResource/Panel_configs/eo_music.json")`

   2. `put(EOResourcePanelKey.RECORDER_MUSIC, "EOResource/Panel_configs/eo_music.json")`

   3. `put(EOResourcePanelKey.TRACK_EDITOR_MUSIC, "EOResource/Panel_configs/eo_music.json")`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44af2c78a01c41ecbcfa5bbe2722e67a~tplv-goo7wpa0wc-image.image) </span>
