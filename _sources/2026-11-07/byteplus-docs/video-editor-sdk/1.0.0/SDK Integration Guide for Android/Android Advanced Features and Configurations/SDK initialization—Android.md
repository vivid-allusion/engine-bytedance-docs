---
title: "SDK initialization—Android"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-initializing-the-sdk-Android"
---

You can follow these steps to initialize the SDK.

<span id="afd5ef16"></span>
# Step 1: Bind the application

You can bind the application by calling the following code:

```Kotlin
AppSingleton.bindInstance(this)
```


<span id="17403cd3"></span>
# Step 2: Configuring default values for the SDK

Configure default values for the SDK including model paths, maximum number of albums, SDK image loading, logging, and so on, supporting customization by users within the host app.

Copy the `DefaultImageLoader.kt` file from the Sample Code directly into your own project for use.

```Kotlin
Copy code
// Provided in SampleCode, can be directly copied.
// Additional glide dependency is required for default implementation.
// implementation("com.github.bumptech.glide:glide:4.13.2")
EffectOneSdk.imageLoader = DefaultImageLoader() // Image loading implementation

EffectOneSdk.logger = DebugLogger() // Log implementation

EffectOneSdk.modelPath = EOResourceManager.getModelRootPath() // Model path
```


<span id="254a7933"></span>
# Step 3: Built\-in authentication configuration

There are two methods for authentication configuration:


* Offline authentication.

* Online authentication.


<span id="a056fd7e"></span>
## Offline authentication


1. Place the offline authentication file in the host project's `/app/src/main/assets/license/` directory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff3325663148410d9d18cbf1441c760d~tplv-goo7wpa0wc-image.image) </span>

2. Copy the offline authentication file to the app's private directory:

   ```Kotlin
   // Copy the offline authentication file to the app's private directory based on the file name
   val licenseFileName = "com.volcengine.effectone.licbag"
   val licenseFile = File(EOUtils.pathUtil.internalLicense(), licenseFileName)
   if (!licenseFile.exists()) {
       EOUtils.fileUtil.copyAssetFile("license/${licenseFileName}", licenseFile.absolutePath)
   }
   ```
   

3. Ensure that the package name matches the authentication file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For internal testing, use the package name: "com.volcengine.effectone"   </div>
   

   ```Kotlin
     defaultConfig {
           ...
           applicationId = "com.volcengine.effectone"
           ...
       }
   ```
   

4. Call the `auth()` method with offline authentication mode in `prepareAndInit()`.

   ```Kotlin
   override fun prepareAndInit() {
       // true for online authentication, false for offline authentication; default is false
       val authResult = auth(false)
       if (authResult.resCode != EOAuthErrCode.EO_SUCCESS) {
           EOToaster.show(AppSingleton.instance, authResult.resMsg)
           return
       }
   }
   
   private fun auth(useOnlineAuth: Boolean = false): EOAuthResData {}
   ```
   

5. Perform offline authentication and proceed with the next steps based on the authentication result.

   ```Kotlin
   // Configure offline authentication mode and set the source directory of the offline authentication file.
   val authConfig = EOAuthConfig(
       isOnline = false,
       offlineLicensePath = licenseFile.absolutePath
   )
   // Authentication interface.
   val result:EOAuthResData = EOAuthorization.makeAuthWithConfig(authConfig)
   
   data class EOAuthResData(
       val resCode: EOAuthErrCode,
       val resMsg: String
   )
   ```
   


<span id="f8f9da0e"></span>
## Online authentication

In addition to built\-in authentication, users can also obtain authentication files through their own servers or integrate with online authentication services.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The online authentication function is currently under development. We recommend opting for the offline authentication method instead.</div>


**To do online authentication:** 


1. Call the `auth()` method with online authentication mode in `prepareAndInit()`.

   ```Kotlin
   override fun prepareAndInit() {
       // true for online authentication, false for offline authentication; default is false
       val authResult = auth(true)
       if (authResult.resCode != EOAuthErrCode.EO_SUCCESS) {
           EOToaster.show(AppSingleton.instance, authResult.resMsg)
           return
       }
   }
   
   private fun auth(useOnlineAuth: Boolean = false): EOAuthResData {}
   ```
   

2. Perform online authentication and proceed with the next steps based on the authentication result.

   ```Kotlin
   // Configure for online authentication mode and set up online authentication.
   val VERSION_NAME = "1.0.0"    // Video Editor SDK version number.
   val authConfig = EOAuthConfig(
       isOnline = true,
       isOverSea = false,
       onlineToken = "your_auth_token",    // Replace with the auth_token for the corresponding application on the Para Cloud platform.
       serverConfig = EOAuthRemoteAddressConfig("https://artob-boe.bytedance.net/api/ck/license",
           mapOf(
               "x-para-auth-token" to "your_auth_token",
               "x-para-pkg-name" to AppSingleton.instance.packageName,
               "x-para-platform" to "android",
               "x-para-pkg-version" to VERSION_NAME,
               "x-para-authMsg" to OnlineLicense.GetAuthMsg()
           ))
   )
   val result:EOAuthResData = EOAuthResData(EOAuthErrCode.EO_SUCCESS, "")
   
   data class EOAuthResData(
       val resCode: EOAuthErrCode,
       val resMsg: String
   )
   ```
   


<span id="c73110b6"></span>
# Step 4: Initializing EOResourceManager

Video Editor SDK requires materials to complete effects such as stickers, special effects, and filters. For ease of use, the EOResourceManager SDK is provided for material management, facilitating the management and configuration of materials for integrators. For the vast majority of scenarios, integrators can directly use EOResourceManager to manage materials.

Before use, integrators need to initialize EOResourceManager: language, material storage path, domain (for online materials), and more.

```Kotlin
// Specify the directory for saving material files and the language used for materials.
val config = EOResourceConfig.Builder()
    .setResourceSavePath(EOUtils.pathUtil.internalResource())
    .setDomainConfig(domainConfig) //This line is required for online materials. If you use offline materials, skip this line.
    .setSysLanguage(Locale.getDefault().language)
    .build()
// Initialize the resource SDK.
EOResourceManager.init(config)
```


<span id="a909c64f"></span>
# Step 5: Built\-in resources import


1. Unzip the delivery package `EOResource.zip` under Android, and place the contents under the `EOResource` directory into `EffectOne-Android/business/src/main/assets/EOResource/`. The directory structure should be as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae67586d8ce045388f9a00cd31445e9a~tplv-goo7wpa0wc-image.image) </span>

2. Unzip the delivery package `EOResource` under Android, and place the contents under the icons directory into `EffectOne-Android/business/src/main/res/drawable-xxhdpi/`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eec2c1813f214a2a81191c886044bf78~tplv-goo7wpa0wc-image.image) </span>

3. Copy the materials and configuration files from assets to the file system.

   ```Kotlin
   val configs = mutableMapOf<EOResourcePanelKey, String>().apply {
       put(EOResourcePanelKey.PREVIEW_EDITOR_EFFECT, "EOResource/Panel_configs/preview_editor_effect.json")
       put(EOResourcePanelKey.PREVIEW_EDITOR_FILTER, "EOResource/Panel_configs/preview_editor_filter.json")
       put(EOResourcePanelKey.PREVIEW_EDITOR_FONT, "EOResource/Panel_configs/preview_editor_font.json")
       put(EOResourcePanelKey.PREVIEW_EDITOR_INFO_STICKER, "EOResource/Panel_configs/preview_editor_info_sticker.json")
       put(EOResourcePanelKey.PREVIEW_EDITOR_MUSIC, "EOResource/Panel_configs/eo_music.json")
       put(EOResourcePanelKey.PREVIEW_EDITOR_STICKER, "EOResource/Panel_configs/preview_editor_sticker.json")
       put(EOResourcePanelKey.PREVIEW_EDITOR_VOICE, "EOResource/Panel_configs/preview_editor_tone.json")
       put(EOResourcePanelKey.RECORDER_BEAUTY, "EOResource/Panel_configs/recorder_beauty.json")
       put(EOResourcePanelKey.RECORDER_FILTER, "EOResource/Panel_configs/recorder_filter.json")
       put(EOResourcePanelKey.RECORDER_MUSIC, "EOResource/Panel_configs/eo_music.json")
       put(EOResourcePanelKey.RECORDER_STICKER, "EOResource/Panel_configs/recorder_sticker.json")
       put(EOResourcePanelKey.TRACK_EDITOR_MUSIC, "EOResource/Panel_configs/eo_music.json")
       put(EOResourcePanelKey.TRACK_EDITOR_SOUND, "EOResource/Panel_configs/track_editor_sound.json")
       put(EOResourcePanelKey.TRACK_EDITOR_TRANSITION, "EOResource/Panel_configs/track_editor_transition.json")
   }
   configs.forEach {
       EOResourceManager.setLocalConfigJson(
           it.key,
           EOUtils.fileUtil.readJsonFromAssets(AppSingleton.instance, it.value)
       )
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In addition to built\-in materials, you can also adopt the CDN or online access method for materials. For more information, refer to <a href="https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-resources-import-and-configuration">Android resources import and configuration</a>.   </div>
