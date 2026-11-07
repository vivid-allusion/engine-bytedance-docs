---
title: "Android Editor module configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-android-editor-module-configuration-and-features"
---

Learn how to initialize the editor module in this topic.

<span id="79f43cdf"></span>
# Initializing the editor module

The initialization of the editor module includes the configuration of the camera page, the configuration of general panel and the configuration of beauty effect panel. This section introduces how to initialize the camera module.

The process of entering the editing page from the photo album is basically the same as entering the editing page from shooting, but the parameters are different. The following is an example of selecting pictures/videos from the album and entering the editing page to demonstrate the overall process of starting the editing page:

**To Initialize the editor module**:

```Kotlin
class HostActivity: AppCompatActivity {
    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ...
         
        // Configure common panels for editing and shooting
        // Filter panel
        EffectOneConfigList.configure(FilterUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        // Face effect panel
        EffectOneConfigList.configure(EOBaseStickerUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        // Music/Sound Effects panel
        EffectOneConfigList.configure(EOBaseMusicUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        
        // Configure editing function panels
        // Info sticker panel
        EffectOneConfigList.configure(InfoStickerUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        // Text panel
        EffectOneConfigList.configure(TextStickerUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        // Animation effects panel
        EffectOneConfigList.configure(EffectPanelUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        // Recording - Sound Color panel
        EffectOneConfigList.configure(AudioFilterUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        // Transition panel
        EffectOneConfigList.configure(TransitionUIConfig()) {
            it.resourceLoader = DefaultLocalResourceLoader.instance
        }
        ...
        // Start editing page
        startEditorBtn.setOnClickListener {
            EditorMainActivity.startEditorActivityFromAlbum(activity = activity, 
                list = arrayListOf().apply {
                    add(
                        MediaItem(
                            path = "local media file path",
                            type = MediaType.VIDEO_OR_IMAGE,
                            duration = "media file duration"
                        )
                    )
                    add(
                        MediaItem(
                            path = "local media file path",
                            type = MediaType.VIDEO_OR_IMAGE,
                            duration = "media file duration"
                        )
                    )
                }
            )
        }
    }
    ...
}
```


<span id="02805922"></span>
# EditorMenuUIConfig

Preview the sidebar configuration on the editor page as needed.


|**Parameter** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|menuList |List |```Kotlin```<br>```listOf(```<br>```    EditorItemType.ITEM_PRO,```<br>```    EditorItemType.ITEM_TEXT_STICKER,```<br>```    EditorItemType.ITEM_INFO_STICKER,```<br>```    EditorItemType.ITEM_FILTER,```<br>```    EditorItemType.ITEM_EFFECT,```<br>```    EditorItemType.ITEM_FACE_EFFECT,```<br>```    EditorItemType.ITEM_AUDIO_FILTER,```<br>```)```<br> |Configure item displayed on the side bar.<br><br>The parameter can be configured with the following data types:<br><br><br>* RecorderItemType.ITEM_FLIP: Flips the camera.<br><br>* RecorderItemType.ITEM_FLASH：Flashlight.<br><br>* RecorderItemType.ITEM_COUNTDOWN：The timer.<br><br>* ecorderItemType.ITEM_FILTER：Filter.<br><br>* RecorderItemType.ITEM_BEAUTY：Beauty effect.<br><br>* RecorderItemType.ITEM_SPEED：Speed changer. |
|unfoldCount |Int |5 |Set the number of unfolding items on the side bar. If the number of items on the side bar exceeds this limit, it will cause some items to be folded . |
|foldEnabled |Boolean |true |Set whether to turn on the sidebar folding function.<br><br>By default, the sidebar folding function is enabled. |


<span id="2be3cf4d"></span>
# Configuration on the general panel

The camera and editing modules have several shared panels, including the filter panel, the special effects panel, and the music panel. By default, these resources are managed in an offline manner. If you need to use other resource management methods, you can implement the function by yourself. For more information on the implementation of `DefaultLocalResourceLoader`, refer to [Android resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/27310).

**Sample code**

```Kotlin
// The filter panel.  
EffectOneConfigList.configure(FilterUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
//The special effect panel.
EffectOneConfigList.configure(EOBaseStickerUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
//The music or music effect panel.
EffectOneConfigList.configure(EOBaseMusicUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
    it.showInEditor = true // the main switch for the music UI in the preview editing
    it.showInRecorder = true // the main switch for music UI during shooting
}
        
```


<span id="af2bfdfc"></span>
# Configuration on the editor panel

In the editor module, resources are managed in a offline manner. If you need to manage resources in other ways, you can rewrite the `ResourceLoader` function yourself. For more details about `DefaultLocalResourceLoader`, refer to [Android resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/27310).

```Kotlin
//   The information sticker panel.
EffectOneConfigList.configure(InfoStickerUIConfig()) {
    it.resourceLoader = DefaultLocalResourceLoader.instance
} 
// The text panel. 
EffectOneConfigList.configure(TextStickerUIConfig()) {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
// The animation special effects panel.
EffectOneConfigList.configure(EffectPanelUIConfig()) {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
// The audio recorder and audio tone panel. 
EffectOneConfigList.configure(AudioFilterUIConfig()) {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
// The transition panel. 
EffectOneConfigList.configure(TransitionUIConfig()) {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
```


<span id="46a73036"></span>
# Configuring additional editor panel parameters

Video Editor SDK supports configuring the maximum number of certain resources within the same editing instance to avoid performance issues caused by excessive resource additions. The default values provided by Video Editor SDK are suitable for most mid\-range devices. Integrators can adjust these values based on their specific business requirements, particularly for lower\-end devices.

**Resource Types and Parameters**


|**Resource Type** |**Parameter** |**Default Value** |**Description** |
|---|---|---|---|
|Image/Text/Info Sticker |EditorResourceCountConfig.maxStickerCount |30 |Maximum number of stickers (text + images + info stickers) |
|Sound effects |EditorResourceCountConfig.maxSoundEffectCount |30 |Maximum number of sound effects in the track editor. |


**Sample code**

```Kotlin
EffectOneConfigList.configure(EditorResourceCountConfig()) {
    it.maxStickerCount = 30
    it.maxSoundEffectCount = 30
} 
```


<span id="b1c3216c"></span>
# Launching the editor page

**To launch the editor page**:


1. Ensure that you have obtained the required permissions by calling the following:

   ```Kotlin
   val albumPermissions = mutableListOf<String>().apply {
       if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {
           add(Manifest.permission.READ_MEDIA_IMAGES)
           add(Manifest.permission.READ_MEDIA_VIDEO)
           add(Manifest.permission.READ_MEDIA_AUDIO)
       } else {
           add(Manifest.permission.READ_EXTERNAL_STORAGE)
           add(Manifest.permission.WRITE_EXTERNAL_STORAGE)
       }
   }
   EOUtils.permission.checkPermissions(activity, albumPermissions) {
       //call back after permission all granted
   }
   ```
   

   If the hosted activity is derived from FragmentActivity, you can directly apply for these permissions using the tools encapsulated in Video Editor SDK.

   If the hosted activity is not derived from FragmentActivity, you need to develop authentication functions on your own. For more information, refer to [Request runtime permissions](https://developer.android.com/training/permissions/requesting). After you have obtained relevant permissions, start the album page.

2. Start the editor page by using the following ways:

   1. **Method 1**: After you select resources on the album page, you can be redirected to the editor page by using the following code:

      ```Kotlin
      /**
       * After you select resources on the album page, you can be redirected to the editor page by using the following code:
       * @param activity The is current page.
       * @param list [MediaItem] The type of the resource list.
       * @param options The add-on custom parameters which can be used to facilitate transition or share animation elements. 
        */
      EditorMainActivity.startEditorActivityFromAlbum(
          activity: Activity,
          list: ArrayList<MediaItem>,
          options: Bundle? = null,
      )  
      ```
      

   2. **Method 2**: After you take a photo or a video in the camera module, you can be redirected to the editor page by using the following code:

      ```Kotlin
      /**
       *  After you take a photo or a video in the camera module, you can be redirected to the editor page by using the following code
       * @param activity The is current page.
       * @param list [MediaItem] The type of the resource list.
       * @param options The add-on custom parameters which can be used to facilitate transition or share animation elements. 
       * @param musicItem [EOBaseMusicItem] The type of music item which can be used to include background information of the added music items. 
       */
      EditorMainActivity.startEditorActivityFromRecord(
          activity: Activity,
          list: ArrayList<MediaItem>,
          options: Bundle? = null,
          musicItem: EOBaseMusicItem? = null,
      )
      ```
