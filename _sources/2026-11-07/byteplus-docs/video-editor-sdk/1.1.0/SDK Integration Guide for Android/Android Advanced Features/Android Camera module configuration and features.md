---
title: "Android Camera module configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-camera-module-configuration-and-features_1_1_0"
---

Learn the configuration and features of the camera module in this topic.

<span id="54bd2245"></span>
# Initializing the camera module

The initialization of the camera module includes the overall initialization of the camera page, the configuration of general panel and the configuration of beauty effect panel. This section introduces how to initialize the camera module.

**To Initialize the camera module**:

```Kotlin
// Do record init in your activity before launching the record
class HostActivity : AppCompatActivity {
    ...
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ...
        // Initialize the recording module
        EffectOneConfigList.configure(RecorderInitConfig()) {
            it.finishAction = { activity, list, musicItem ->
                // Start the editing page and pass the recording results
                EditorMainActivity.startEditorActivityFromRecord(
                    activity,
                    list.map { resourceItem ->
                        com.volcengine.easyeditor.api.MediaItem(
                            path = resourceItem.path,
                            type = if (resourceItem.type == RecordMediaType.VIDEO) MediaType.VIDEO else MediaType.IMAGE,
                            duration = resourceItem.duration,
                            speed = resourceItem.speed
                        )
                    } as ArrayList<com.volcengine.easyeditor.api.MediaItem>, null, musicItem)
            }
            it.albumConfig = AlbumConfig(
                allEnable = true,
                imageEnable = true,
                videoEnable = true,
                maxSelectCount = EffectOneSdk.albumMaxSelectedCount,
                maxDuration = 60 * 60 * 1000L,   // maxDuration Unit:ms
                finishClazz = StartEditorFinishImpl::class.java
            )
        }
        ...
        // Launch the recording page
        startRecordBtn.setOnClickListener {
            val recordPermissions = mutableListOf<String>().apply {
                add(Manifest.permission.CAMERA)
                add(Manifest.permission.RECORD_AUDIO)
            }
            EOUtils.permission.checkPermissions(activity, recordPermissions, {
                EORecordActivity.startRecord(activity)
            }, {
                RecordUtils.showRecordPermissionTips(activity, it)
            })
        } 
    }
    ...

}
}
class StartEditorFinishImpl : IAlbumFinish {
    override suspend fun finishAction(activity: Activity, mediaList: List<IMaterialItem>, albumConfig: AlbumConfig) {
        EditorMainActivity.startEditorActivityFromAlbum(activity, mediaList.map {
            com.volcengine.easyeditor.api.MediaItem(
                path = it.path,
                type = if (it.isVideo()) MediaType.VIDEO else MediaType.IMAGE,
                duration = if (it.isVideo()) it.duration else 3000
            )
        } as ArrayList<com.volcengine.easyeditor.api.MediaItem>)
    }
}
```


<span id="94492421"></span>
# RecorderInitConfig

Set the configuration parameters for initializing the camera module.

<span id="a6eeeab5"></span>
## albumConfig

This parameter configures your album UI.

<span id="f8ae15f7"></span>
### Class definition

```Kotlin
data class AlbumConfig(
    val hintText: String = "",
    val singleSelect: Boolean = false,
    val confirmDirectly: Boolean = false,
    val canRepeat: Boolean = true,
    val showGif: Boolean = true,
    val allEnable: Boolean = false,
    val imageEnable: Boolean = true,
    val videoEnable: Boolean = true,
    val maxSelectCount: Int = 35,
    val minSelectCount: Int = 1,
    val minDuration: Long = 0L,
    val maxDuration: Long = Long.MAX_VALUE,
    val enableDocker: Boolean = true,
    var confirmTextResId: Int = 0,
    val finishClazz: Class<out IAlbumFinish> = DefaultFinishImpl::class.java
) : Parcelable
```


<span id="a5c132b4"></span>
### Sample code

```Shell
AlbumConfig(
    allEnable = true,
    imageEnable = true,
    videoEnable = true,
    maxSelectCount = EffectOneSdk.albumMaxSelectedCount,
    //maxDuration Unit:ms
    maxDuration = 60 * 60 * 1000L,
    finishClazz = StartEditorFinishImpl::class.java
)
```


<span id="a5f1350f"></span>
## finishClazz

This parameter defines the redirect page for users after they select their desired albums.

<span id="f87030d0"></span>
### Class definition

```Kotlin
interface IAlbumFinish {
   suspend fun finishAction(activity: Activity, mediaList: List<IMaterialItem>, albumConfig: AlbumConfig)
}
```


<span id="43998024"></span>
### Sample code

```Kotlin
class StartEditorFinishImpl : IAlbumFinish {
    override suspend fun finishAction(activity: Activity, 
    mediaList: List<IMaterialItem>, 
    albumConfig: AlbumConfig) {
        EditorMainActivity.startEditorActivityFromAlbum(activity, mediaList.map {
            com.volcengine.easyeditor.api.MediaItem(
                path = it.path,
                type = if (it.isVideo()) MediaType.VIDEO else MediaType.IMAGE,
                duration = if (it.isVideo()) it.duration else 3000
            )
        } as ArrayList)
    }
}
```


<span id="df1ddf8c"></span>
## finishAction

This parameter defines the response sent back by the callback function when users complete their photo\-shooting or video\-shooting operations.

<span id="475f71b0"></span>
### Class definition

```Kotlin
((Activity, List, EOBaseMusicItem?) -> Unit)
```


<span id="b9c33f78"></span>
### Sample code

```Kotlin
{ activity, list, musicItem ->
    val options = ActivityOptionsCompat.makeCustomAnimation(activity, 0, 0)
    EditorMainActivity.startEditorActivityFromRecord(activity, list.map { resourceItem ->
        com.volcengine.easyeditor.api.MediaItem(
            path = resourceItem.path,
            type = if (resourceItem.type == RecordMediaType.VIDEO) MediaType.VIDEO else MediaType.IMAGE,
            duration = resourceItem.duration,
            speed = resourceItem.speed
        )
    } as ArrayList, options.toBundle(), musicItem)
}
```


<span id="b1160e82"></span>
## defaultCameraDirection

The parameter defines a default direction for the camera. It has the `CameraFacingId` as a sub\-parameter.

Available values of `CameraFacingId` include:

```Kotlin
FACING_FRONT
FACING_BACK
```


By default, the `CameraFacingId` is set to `FACING_FRONT`.

<span id="d00eaee3"></span>
## defaultResolution

The parameter defines a default resolution for the camera. It has `ResolutionId` as a sub\-parameter:

Available values of `ResolutionId` include:

```Kotlin
RESOLUTION_540 //540p
RESOLUTION_720 //720p
RESOLUTION_1080 //1080p
RESOLUTION_4K //4K
```


By default, the `ResolutionId` is set to `RESOLUTION_1080`.

<span id="6c4c18ec"></span>
## enableEffectStickerBtn

This parameter defines whether to display the effect sticker button. The default value is data type Boolean and `true`.

<span id="a2f626d6"></span>
## enableAlbumBtn

This parameter defines whether to display the album button. The default value is data type Boolean and `true`.

<span id="5ac2a831"></span>
# Launching the camera page

Use the following code to launch the camera page:

```Kotlin
val recordPermissions = mutableListOf().apply {
    add(Manifest.permission.CAMERA)
    add(Manifest.permission.RECORD_AUDIO)
}
EOUtils.permission.checkPermissions(activity, recordPermissions) {
    EORecordActivity.startRecord(activity)

}
```


Before launching the camera page, you need to apply for permission to use the camera (`CAMERA`)and the audio recorder (`RECORD_AUDIO`). If the hosted activity is derived from FragmentActivity, you can directly use the following code to complete authentication:

```Kotlin
EOUtils.permission.checkPermissions(activity, recordPermissions)
```


If the hosted activity is not derived from FragmentActivity , you need to develop authentication functions on your own. For more information, refer to [Request runtime permissions](https://developer.android.com/training/permissions/requesting).

After you have obtained relevant permissions, call the following function to start the camera page:

```Kotlin
 EORecordActivity.startRecord(activity)
```


<span id="e7c63356"></span>
## RecorderMenuUIConfig

Configure the settings associated with the side\-bar on the camera page as needed.


|**Parameter** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|menuList |List |```Kotlin```<br>```listOf(```<br>```    RecorderItemType.ITEM_FLIP,```<br>```    RecorderItemType.ITEM_FLASH,```<br>```    RecorderItemType.ITEM_COUNTDOWN,```<br>```    RecorderItemType.ITEM_FILTER,```<br>```    RecorderItemType.ITEM_BEAUTY,```<br>```    RecorderItemType.ITEM_SPEED,```<br>```)```<br> |Configure item displayed on the side bar.<br><br>The parameter can be configured with the following data types:<br><br><br>* RecorderItemType.ITEM_FLIP: Flips the camera.<br><br>* RecorderItemType.ITEM_FLASH：Flashlight.<br><br>* RecorderItemType.ITEM_COUNTDOWN：The timer.<br><br>* ecorderItemType.ITEM_FILTER：Filter.<br><br>* RecorderItemType.ITEM_BEAUTY：Beauty effect.<br><br>* RecorderItemType.ITEM_SPEED：Speed changer. |
|unfoldCount |Int | |Set the number of unfolding items on the side bar. If the number of items on the side bar exceeds this limit, it will cause some items to be folded . |
|foldEnabled |Boolean |true |Set whether to turn on the sidebar folding function.<br><br>By default, the sidebar folding function is enabled. |


<span id="93809342"></span>
# Configuring the general panel

The camera and editing modules have several shared panels, including the filter panel, the special effects panel, and the music panel. By default, these resources are managed in an offline manner. If you need to use other resource management methods, you can implement the function by yourself. For more information on the implementation of `DefaultLocalResourceLoader`, refer to [Android resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-resources-import-and-configuration_1_1_0).

**Sample code**

```Kotlin
//Filter panel
EffectOneConfigList.configure(FilterUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
//Special effects panel
EffectOneConfigList.configure(EOBaseStickerUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
//Music panel
EffectOneConfigList.configure(EOBaseMusicUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
    it.showInEditor = true // In the Preview Editor, is the music UI shown
    it.showInRecorder = true // In the camera module, is the music UI shown
}      
```


<span id="82c54415"></span>
# Initializing the beauty effect panel

**Sample code**

```Kotlin
EffectOneConfigList.configure(BeautyUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
    it.defaultBeautyAction = {
        //In the beauty configuration, obtain items which meet the condition that 'defaultOn = 1', and use the items as default items(SDK will automatically filter the items for you. You simply need to import them to the beauty configuration).
        EOResourceManager.syncLoadConfigByPanelKey(EOResourcePanelKey.RECORDER_BEAUTY.value, true).tabs
    }
}
```
