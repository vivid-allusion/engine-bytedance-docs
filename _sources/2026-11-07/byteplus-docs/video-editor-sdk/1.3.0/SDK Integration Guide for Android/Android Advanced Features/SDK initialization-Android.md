---
title: "SDK initialization-Android"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-sdk-initialization-android"
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

Configure default values for the SDK including model paths, maximum number of albums, SDK image loading, logging, default values for albums, image editing modes, and so on, supporting customization by users within the host app.

Copy the `DefaultImageLoader.kt` file from the Sample Code directly into your own project for use.

```Kotlin

//  Provided in SampleCode, can be directly copied.
// Additional glide dependency is required for default implementation.
// implementation("com.github.bumptech.glide:glide:4.13.2")
EffectOneSdk.imageLoader = DefaultImageLoader() // Image loading implementation
 
EffectOneSdk.logger = DebugLogger() //Log implementation

EffectOneSdk.modelPath = EOResourceManager.getModelRootPath() //Model path

EffectOneSdk.photoEditingMode = PhotoEditingMode.MODE_PICTURE //Photo editing mode

```


<span id="254a7933"></span>
# Step 3: Built\-in authentication configuration

There are two methods for authentication configuration:


* Offline authentication.

* Online authentication.


<span id="a056fd7e"></span>
## Offline authentication


1. Place the offline authentication file in the host project's `/app/src/main/assets/license/` directory

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b75fc8e3c40044fa85669da6d5fc839d~tplv-goo7wpa0wc-image.image) </span>

2. Copy the offline authentication file to the app's private directory:

   ```Kotlin
   //  Copy the offline authentication file to the app's private directory based on the file name
      
   val licenseFileName = "com.volcengine.effectone.licbag"
      
   val licenseFile = File(EOUtils.pathUtil.internalLicense(), licenseFileName)
      
   if (!licenseFile.exists()) {
      
       EOUtils.fileUtil.copyAssetFile("license/${licenseFileName}", licenseFile.absolutePath)
      
   }
      
   ```
   

3. Ensure that the package name matches the authentication file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For internal testing, use the package name: <code>com.volcengine.effectone</code>.   </div>
   

   ```Kotlin
     defaultConfig {
           ...
           applicationId = "com.volcengine.effectone"
           ...
       }
   ```
   

4. Call the `auth()` method with offline authentication mode in `prepareAndInit()`.

   ```Kotlin
   override fun prepareAndInit(callback: (Boolean, String) -> Unit) {
       coroutineScope.launch(Dispatchers.Main) {
           initConfigs()
           initResourceData()
           val authResult = withContext(Dispatchers.IO) {
               auth()
           }
           if (authResult.resCode != EOAuthErrCode.EO_SUCCESS) {
               EOToaster.show(AppSingleton.instance, authResult.resMsg)
               callback(false, "auth failed:${authResult.resMsg}")
           } else {
               callback(true, "auth success")
           }
       }
   }
   ```
   

5. Perform offline authentication and proceed with the next steps based on the authentication result.

   ```Kotlin
   EOQuickInitHelper.prepareAndInit{ isSuccess, msg ->
       authResult = isSuccess
   } 
   ```
   


<span id="f8f9da0e"></span>
# Step 4: Initializing EOResourceManager

Video Editor SDK requires materials to complete effects such as stickers, special effects, and filters. For ease of use, the `EOResourceManager` SDK is provided for material management, facilitating the management and configuration of materials for integrators. For the vast majority of scenarios, integrators can directly use `EOResourceManager` to manage materials.

Before use, integrators need to initialize `EOResourceManager`: language, material storage path, domain (for online materials), and more.

```Kotlin
//  Specify the directory for saving material files and the language used for materials.
val config = EOResourceConfig.Builder()
    .setResourceSavePath(EOUtils.pathUtil.internalResource())
    .setSysLanguage(Locale.getDefault().language)
    .build() 
// Initialize the resource SDK.
EOResourceManager.init(config)
```


<span id="a909c64f"></span>
# Step 5: Built\-in resources import


1. Move the contents of the `EffectResource`folder under the Android resource deliverables `EffectOne-Android/business/src/main/assets/EffectResource/`. The directory structure should be as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa5b97f3ecec4a6d956430f333b6ca6c~tplv-goo7wpa0wc-image.image) </span>

2. Move the contents of the `Resource_icons` folder under the EffectResource folder in the Android resource deliverables to `EffectOne-Android/business/src/main/res/drawable-xxhdpi/`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eec2c1813f214a2a81191c886044bf78~tplv-goo7wpa0wc-image.image) </span>

3. Copy the materials and configuration files from assets to the file system.


```Kotlin
// In the EOQuickInitHelper class, you need to add implementation to read the panel configuration file.：
DefaultLocalResourceLoader.instance.localConfigsLoader = object : LocalConfigsLoader {
    private val configsPathMap : Map<String, String> = mutableMapOf<EOResourcePanelKey, String>().apply {
        put(EOResourcePanelKey.PREVIEW_EDITOR_EFFECT, "Panel_configs/preview_editor_effect.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_FILTER, "Panel_configs/preview_editor_filter.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_FONT, "Panel_configs/preview_editor_font.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_INFO_STICKER, "Panel_configs/preview_editor_info_sticker.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_MUSIC, "Panel_configs/eo_music.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_STICKER, "Panel_configs/preview_editor_sticker.json")
        put(EOResourcePanelKey.PREVIEW_EDITOR_VOICE, "Panel_configs/preview_editor_tone.json")
        put(EOResourcePanelKey.RECORDER_BEAUTY, "Panel_configs/recorder_beauty.json")
        put(EOResourcePanelKey.RECORDER_FILTER, "Panel_configs/recorder_filter.json")
        put(EOResourcePanelKey.RECORDER_MUSIC, "Panel_configs/eo_music.json")
        put(EOResourcePanelKey.RECORDER_STICKER, "Panel_configs/recorder_sticker.json")
        put(EOResourcePanelKey.TRACK_EDITOR_MUSIC, "Panel_configs/eo_music.json")
        put(EOResourcePanelKey.TRACK_EDITOR_SOUND, "Panel_configs/track_editor_sound.json")
        put(EOResourcePanelKey.TRACK_EDITOR_TRANSITION, "Panel_configs/track_editor_transition.json")
    }.map {
        it.key.value to it.value
    }.toMap()
    override fun loadConfigs(panelKey: String, type: String): String? {
        val value = configsPathMap.getValue(panelKey) ?: return null
       // To read the panel configuration file from the assets folder
        return EOUtils.fileUtil.readJsonFromAssets(AppSingleton.instance, "${EOUtils.pathUtil.assetsResourcePath}/${value}")
    }
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to built\-in materials, you can also adopt the CDN or online access method for materials. For more information, refer to<a href="https://docs.byteplus.com/docs/video-editor-sdk/120-android-resources-import-and-configuration">Android resources import and configuration</a></div>


<div data-tips="true" data-tips-type="tip">.</div>


<span id="9a7076d9"></span>
# Step 6: Photo editing mode

By configuring the value of `photoEditingMode` in Video Editor SDK, you can customize the way your app edits image files. By default, it will be set to picture editing mode (`MODE_PICTURE`).


|**Parameter** |**Description** |**Mode definition** |
|---|---|---|
|photoEditingMode |The editing mode of the photo. |```Kotlin```<br>```enum class PhotoEditingMode {```<br>```    MODE_NON_PICTURE, // Non-picture editing, processes image files as 3s videos for editing```<br>```    MODE_PICTURE   //Picture editing, hides video editing functionalities in the preview editing page}```<br> |


Once set to photo editing mode, the captured or imported photo files will be edited and exported as image files. For more information, refer to [Exporting photos](https://docs.byteplus.com/docs/video-editor-sdk/27283#658ce273).

<span id="1af6e81d"></span>
# Step 7: `EffectOneActivity` Management

`EffectOneSdk.activityManager` can be used to manage activities within Video Editor SDK, providing the following capabilities:


* Obtain the corresponding Activity instance by class name.

* Close the specified Activity of Video Editor SDK and set the activity result. The corresponding callback can be obtained in `onActivityResult` when launching the corresponding Activity's page.


```Kotlin
interface IActivityManager {
    fun finishActivities(filter: ((activity: AppCompatActivity)-> Boolean)? = null, resultCode: Int? = null, result: Intent? = null)
    fun  getActivity(clazz: Class<T>): AppCompatActivity? 
} 
```
