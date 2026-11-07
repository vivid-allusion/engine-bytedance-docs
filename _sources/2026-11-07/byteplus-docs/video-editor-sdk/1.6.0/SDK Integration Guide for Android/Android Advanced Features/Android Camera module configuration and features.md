---
title: "Android Camera module configuration and features"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-android-camera-module-configuration-and-features"
---

Learn the configuration and features of the camera module in this topic.

<span id="54bd2245"></span>
# Initializing the camera module

The initialization of the camera module includes the overall initialization of the camera page, the configuration of general panel and the configuration of beauty effect panel. This section introduces how to initialize the camera module.

**To Initialize the camera module**:

```Kotlin
//  Do record init in your activity before launching the record
class HostActivity : AppCompatActivity { 
    ...  
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        ...
        // Initialize the recording module
        EffectOneConfigList.configure(RecorderInitConfig()) {
            it.finishAction = { activity, list, musicItem, ext ->
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
                } as ArrayList, null, musicItem, ext)
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
            val recordPermissions = mutableListOf().apply {
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
        } as ArrayList)
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
    val maxSelectCount: Int = 35, // Restricted internally by the SDK to not exceed 35.
    val minSelectCount: Int = 1,
    val minDuration: Long = 0L,
    val maxDuration: Long = Long.MAX_VALUE,
    val enableDocker: Boolean = true,
    var confirmTextResId: Int = 0,
    val finishClazz: Class = DefaultFinishImpl::class.java
) : Parcelable 
```


<span id="a5c132b4"></span>
### Sample code

```Kotlin
AlbumConfig(
    allEnable = true,
    imageEnable = true, 
    videoEnable = true,
    maxSelectCount = EffectOneSdk.albumMaxSelectedCount,
    // maxDuration Unit:ms 
    maxDuration = 60 * 60 * 1000L,
    finishClazz = StartEditorFinishImpl::class.java
)  
```


<span id="a5f1350f"></span>
## finishAction

This parameter defines the response sent back by the callback function when users complete their photo\-shooting or video\-shooting operations.

<span id="475f71b0"></span>
### Class definition

```Kotlin
((Activity, List, EOBaseMusicItem?, Bundle?) -> Unit)   
```


**Parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|RecordMediaItem |MediaItem |Captured video/album content |
|EOBaseMusicItem |MusicItem |Music selection information. |


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

The parameter defines a default direction for the camera. By default, the `CameraFacingId` is set to `FACING_FRONT`. The values include:


* `FACING_FRONT`.

* `FACING_BACK`.


<span id="d00eaee3"></span>
## defaultResolution

The parameter defines a default resolution for the camera. Available values of `ResolutionId` include:

```Kotlin
RESOLUTION_540 // 540p
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

<span id="4924ba03"></span>
## selectModelFactory

This parameter defines the recording model of the camera page. The record duration can be customized according to your needs.

```Kotlin
open class DefaultEORecordSelectModelFactory: IEORecordSelectModelFactory {
    override fun getDefaultSelectIndex(): Int {
        return 2
    }

    override fun getSupportModelList(): List<IEOModelItem> {
        return listOf(
            Record2MINModel(), Record30SModel(), Record15SModel(), RecordPhotoModel()
        )
    }
}
```


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
|unfoldCount |Int |5 |Set the number of unfolding items on the side bar. If the number of items on the side bar exceeds this limit, it will cause some items to be folded . |
|foldEnabled |Boolean |true |Set whether to turn on the sidebar folding function.<br><br>By default, the sidebar folding function is enabled. |


<span id="93809342"></span>
# Configuring the general panel

The camera and editing modules have several shared panels, including the filter panel, the special effects panel, and the music panel. By default, these resources are managed in an offline manner. If you need to use other resource management methods, you can implement the function by yourself. For more information on the implementation of `DefaultLocalResourceLoader`, refer to [Android resources import and configuration](https://docs.byteplus.com/docs/video-editor-sdk/160-android-resources-import-and-configuration).

**Sample code**

```Kotlin
// Filter panel
EffectOneConfigList.configure(FilterUIConfig()> { 
    it.resourceLoader = DefaultLocalResourceLoader.instance
}  
// Special effects panel
EffectOneConfigList.configure(EOBaseStickerUIConfig()> {
    it.resourceLoader = DefaultLocalResourceLoader.instance
}
// Music panel
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
        // In the beauty configuration, obtain items which meet the condition that 'defaultOn = 1', and use the items as default items(SDK will automatically filter the items for you. You simply need to import them to the beauty configuration).
        EOResourceManager.syncLoadConfigByPanelKey(EOResourcePanelKey.RECORDER_BEAUTY.value, true).tabs
    } 
} 
```


<span id="639b4acc"></span>
# Video Duet function

The Video Duet function allows users to start the pick from their album, select a video file for collaborative shooting, and smoothly transition to the shooting page to begin the collaborative shooting process. For detailed configuration specifics, please refer to `business/EODuetInitHelper.kt`.

The general process is as follows:

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI1MDVweCIgaGVpZ2h0PSI2NXB4IiB2aWV3Qm94PSItMC41IC0wLjUgNTA1IDY1Ij48ZGVmcy8+PGc+PHBhdGggZD0iTSAxMjIgMzIgTCAxODUuNjMgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxOTAuODggMzIgTCAxODMuODggMzUuNSBMIDE4NS42MyAzMiBMIDE4My44OCAyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5MYXVuY2ggdGhlIHBob3RvIGFsYnVtPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDMxMiAzMiBMIDM3NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM4MC44OCAzMiBMIDM3My44OCAzNS41IEwgMzc1LjYzIDMyIEwgMzczLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxOTIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDE5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5TZWxlY3QgYSB2aWRlbyBmaWxlIGZvciBkdWV0IHZpZGVvIHJlY29yZGluZzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzgyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzODNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+TmF2aWdhdGUgdG8gdGhlIGNhbWVyYSBmb3IgZHVldCB2aWRlbyByZWNvcmRpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />

<span id="ea0188c0"></span>
## Step 1: Initializing the Video Duet function

```Kotlin
EffectOneConfigList.configure((RecorderDuetUIConfig())) { 
    it.resourceLoader = DefaultLocalResourceLoader.instance
    it.defaultDuetAction = {
        EOResourceManager.syncLoadConfigByPanelKey(EOResourcePanelKey.RECORDER_DUET.value, true).tabs
    } 
} 
```


<span id="0e965e04"></span>
## Step 2: Loading default layout resources of Video Duet

Before entering the Video Duet recording page for the first time, you need to copy the default layout resources to ensure the correct effect of the recording page.

```Kotlin
CoroutineScope(Dispatchers.IO).launch { 
    loadDefaultDuet()
}

/**
 * Load the default duet layout resources using EOResourceManager
 * @return : Returns the loading result (true: success; false: failure)
 */
private suspend fun loadDefaultDuet(): Boolean {
    DefaultLocalResourceLoader.instance.loadResourceList(EOResourcePanelKey.RECORDER_DUET.value, "")
    val duetItems = EOResourceManager.syncLoadConfigByPanelKey(
        EOResourcePanelKey.RECORDER_DUET.value,
        true
    ).tabs.firstOrNull()
    duetItems?.subItems?.let { subItems ->
        if (subItems.isNotEmpty()) {
            DefaultLocalResourceLoader.instance.loadResourceItem(subItems.first())
            return true
        }
    }
    return false
}
```


<span id="174b1e8c"></span>
## Step 3: duetAlbumConfig

This configuration defines settings for selecting a video file intended for video duet collaboration. It restricts selection to videos only, allows selecting a single file, and specifies behavior after selection, directing to the recording page for duet creation. The hint text guides users to select a video suitable for video duet collaboration.

**Parameters**


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|allEnable |Boolean |false |Indicates whether all types of media (both images and videos) are enabled for selection. |
|imageEnable |Boolean |false |Indicates whether images are enabled for selection. |
|videoEnable |Boolean |true |Indicates whether videos are enabled for selection. |
|maxSelectCount |Int |1 |Specifies the maximum number of media items that can be selected for Video Duet creation. |
|finishClazz |Class |StartRecordFinishImpl::class.java |Class reference specifying the implementation to handle actions upon finishing media selection. |
|hintText |String |Please select a video file for duet. |Hint text displayed to guide the user in selecting a video for duet creation. |


**Sample code:** 

```Kotlin
val duetAlbumConfig = AlbumConfig(
    allEnable = false, 
    imageEnable = false, 
    videoEnable = true,    // Only video files can be selected
    maxSelectCount = 1,    // Only one video file can be selected for duet
    finishClazz = StartRecordFinishImpl::class.java,    // After selection, the recording page will be launched.
    hintText = "(Example) Please select a video file for duet"
)
 
// For details on StartRecordFinishImpl, refer to Step 6: Video Duet screen configuration
class StartRecordFinishImpl : IAlbumFinish {
    override suspend fun finishAction(activity: Activity, mediaList: List<IMaterialItem>, albumConfig: AlbumConfig) {
        val videoPath = ""
        val audioPath = ""

        val bundle = Bundle()
        bundle.putBoolean("isDuet", true)
        bundle.putString("duetVideoPath", videoPath)
        bundle.putString("duetAudioPath", audioPath)        
        EOQuickInitHelper.startRecorder(activity as FragmentActivity, bundle)

        if (!activity.isFinishing) {
            activity.finish()
        }
    }
}
```


<span id="6e5fcc0f"></span>
## Step 4: StartRecordFinishImpl

This class (`StartRecordFinishImpl`) implements the `IAlbumFinish` interface to handle actions after selecting media from the album for duet mode. It retrieves the selected media's path, prepares parameters for starting the recorder in duet mode, and initiates the recording process.

**Sample code**

```Kotlin
// Details for StartRecordFinishImpl
class StartRecordFinishImpl : IAlbumFinish { 
    override suspend fun finishAction(activity: Activity, mediaList: List<IMaterialItem>, albumConfig: AlbumConfig) {
        val duetMediaUri = if (mediaList.isNotEmpty()) mediaList[0].path else ""
        val duetMediaPath = EOUtils.pathUtil.getAbsolutePathFromUri(activity, duetMediaUri)
 
        val bundle = Bundle() 
        bundle.putBoolean("isDuet", true)
        bundle.putString("duetVideoPath", duetMediaPath)
        bundle.putString("duetAudioPath", duetMediaPath)
        EOQuickInitHelper.startRecorder(activity as FragmentActivity, bundle)

        if (!activity.isFinishing) {
            activity.finish()
        }
    }
}
```


<span id="f80f173a"></span>
## Step 5: Media selection and permission handling for album screens

This code checks for permissions required to access media, including images, videos, and audio. It then checks camera and audio recording permissions for launching the recording page after selecting media. If permissions are granted, it starts the media selection process using `AlbumEntrance.startChooseMedia`. If not, it shows permission tips using `AlbumEntrance.showAlbumPermissionTips`.

```Kotlin
val albumPermissions = mutableListOf().apply {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {
        add(Manifest.permission.READ_MEDIA_IMAGES) 
        add(Manifest.permission.READ_MEDIA_VIDEO)
        add(Manifest.permission.READ_MEDIA_AUDIO)
    } else { 
        add(Manifest.permission.READ_EXTERNAL_STORAGE)
        add(Manifest.permission.WRITE_EXTERNAL_STORAGE)
    }
    // Camera and audio recording permissions are used to start recording after selecting media
    add(Manifest.permission.CAMERA)
    add(Manifest.permission.RECORD_AUDIO)
} 
EOUtils.permission.checkPermissions(activity, albumPermissions, {
    AlbumEntrance.startChooseMedia(
        activity, 1001, duetAlbumConfig
    )
}, {
    AlbumEntrance.showAlbumPermissionTips(activity)
})
```


<span id="13d8cdbe"></span>
## Step 6: Video Duet screen configuration

When entering the camera module through the Video Duet feature, additional Bundle configuration parameters are required to enable Video Duet\-related functionalities within the camera module.


|**Bundle Key** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|isDuet |Boolean |true |Enables Video Duet mode. |
|duetVideoPath |String |N/A |An absolute file path of a Video Duet file. To accurately convert URI paths to their respective absolute file paths, use: `EOUtils.pathUtil.getAbsolutePathFromUri()`. |
|duetAudioPath |String |N/A |If the selected video file contains an audio track, you can also pass the absolute path of the selected video file. |


<span id="9383609b"></span>
# Customizing recording button

The recording button has four states as shown below. You can customize the appearance of the recording button as needed.


|Photo taking |Video recording\-Initial State |Video recording\-<br><br>Recording |Video recording\- Paused |
|---|---|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df1a325880ae4935a7f9425e655e605e~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f9cb1e5d9c45dc836e98f34acb7a81~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e94807db1b274eb7b7718e5788004274~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a9b2f73c4ff48cb8a5edf6a504447f1~tplv-goo7wpa0wc-image.image) </span> |


<span id="5b6243f1"></span>
## Attributes

Use the attributes listed in the table to customize the appearance of the recording button.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Do <strong>not</strong> change the size of the recording (EORecordButton). Both the width and height must be 96dp.</div>



|**State** |**Attributes** |**Description** |**Example** |
|---|---|---|---|
|Photo taking |picBorderColor |The color of the outer circular border when taking a photo. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ec3c75597b540fd8fa8145d5e1cbde2~tplv-goo7wpa0wc-image.image) </span> |
||picPanelColor |The color of the inner circular panel when taking a photo. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5672037b4f143c88f326fc37bb89e3a~tplv-goo7wpa0wc-image.image) </span> |
|Video recording \-Initial State |videoStartBorderColor |The color of the outer circular border when recording a video. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31e2877a9072498baed79c8b53d31372~tplv-goo7wpa0wc-image.image) </span> |
||videoStartPanelColor |The color of the inner circular border when recording a video. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a88cbd48eeb34ff4b62692cefff158c6~tplv-goo7wpa0wc-image.image) </span> |
|Video recording \-Recording |videoRecordingBorderColor |The color of the progress bar when recording a video. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd53b6e3f6f343808557a6983359dc9f~tplv-goo7wpa0wc-image.image) </span> |
||videoRecordingOutPanelColor |The color of the recording panel when recording a video. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5396f4ca927f4549b7d84a8d6e495011~tplv-goo7wpa0wc-image.image) </span> |
||To maintain consistency, the color of the middle panel is the same as recording panel (videoStartPanelColor) and cannot be changed separately. ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddd3448fd62f44dfaa92edfc4016dc1f~tplv-goo7wpa0wc-image.image) </span> |
|Video recording \-Paused |videoPauseEndPointColor |The color of the stop point marker during multi\-segment shooting or when recording is paused. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/099e41ce4aa34fb6968eb4a85a2cfa72~tplv-goo7wpa0wc-image.image) </span> |


<span id="813e9b2a"></span>
## Sample code

```XML
<com.volcengine.effectone.recorderui.widget.EORecordButton
    android:id="@+id/eo_recorder_start_record"
    android:layout_width="@dimen/eo_recorder_record_button_size"
    android:layout_height="@dimen/eo_recorder_record_button_size"
    android:layout_marginBottom="15dp"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:picBorderColor="#03A9F4"
    app:picPanelColor="#FFEB3B"
    app:videoPauseEndPointColor="#9C27B0"
    app:videoRecordingBorderColor="#009688"
    app:videoRecordingOutPanelColor="#334CAF50"
    app:videoStartBorderColor="#3F51B5"
    app:videoStartPanelColor="#EA0505" />
```
