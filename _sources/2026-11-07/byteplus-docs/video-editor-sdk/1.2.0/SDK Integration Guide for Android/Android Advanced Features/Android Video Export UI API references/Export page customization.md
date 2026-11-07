---
title: "Export page customization"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-export-page-customization"
---

Learn about BytePlus Video Editor SDK's export page in this topic.

<span id="a99d83bb"></span>
# UI structure

The UI consists of three layers, among which the bottom layer has three scenarios.


1. Topbar

2. Preview pane

3. Bottom bar


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07b114cb1dff407889a56dbf4cc3a639~tplv-goo7wpa0wc-image.image) </span>

<span id="bc3959a7"></span>
## Topbar


|**PageScenes** |**LayoutID** |**Helper** |**Fragment** |
|---|---|---|---|
|DEFAUTL |eo_main_layout_export_top_bar |EffectOneExportTopBarHelper |EffectOneExportFragment |
|COVER_EDITOR ||||
|EXPORT ||||


<span id="231f9f0b"></span>
## Preview pane


|**Control** |**LayoutID** |**Helper** |**Fragment** |
|---|---|---|---|
|SurfaceView |eo_main_fragment_export |EffectOneExportPreviewHelper |EffectOneExportFragment |
|ImageView ||||


<span id="dffa4598"></span>
## Bottom bar

The bottom bar is managed by using a fragment in XML. It has three UI states:


1. Default UI: DEFAULT

2. Cover editor UI: COVER_EDITOR

3. Export UI: EXPORT



|**PageScenes** |**LayoutID** |**Helper** |**Fragment** |
|---|---|---|---|
|DEFAULT |eo_main_layout_export_bottom_content |EffectOneExportBottomBarHelper |EffectOneExportDefaultFragment |
|COVER_EDITOR |eo_main_layout_export_cover_editor |EffectOneExportBottomBarHelper |EffectOneCoverEditorFragment |
|EXPORT |eo_main_fragment_export_progress |EffectOneExportBottomBarHelper |EffectOneExportProgressFragment |


<span id="bfc50641"></span>
# Data model

<span id="dd7ef535"></span>
## PageScenes

```Kotlin
/**
 * PageScenes controls UI display and interactive logics.
 * @see DEFAULT :Default UI of the export page, containing the back button, the settings of cover photo, export, and resolution.
 * @see COVER_EDITOR：The settings page for the cover photo：ViewPager2+TabLayout, including the frame tab and the album tab. 
 * @see EXPORT：The export page in which you can view the export progress and cancel the export task.
 *
 */
enum class PageScenes {
    DEFAULT,
    COVER_EDITOR,
    EXPORT,
}
```


<span id="b6d3e53e"></span>
## Cover photo TabType

```Kotlin
/** 
 * The tab for cover phtoto editing
 * @see FRAME :The frame tab
 * @see ALBUM :The album tab
 */
enum class TabType {
    FRAME,
    ALBUM,
}
```


<span id="2e5648a6"></span>
# Customizing the export page

These are the sample codes and steps for export page customization in Video Editor SDK.

<span id="8e4ac8bc"></span>
## Configure startup action

```Kotlin
const val ACTION_EXPORT_ACTIVITY = "com.volcengine.effectone.Launch.EOExport"
// AndroidManifest.xml

    android:name=".export.EffectOneExportActivity"
    android:exported="true"
    android:screenOrientation="portrait"
    android:theme="@style/Theme.EffectOne">
    
        "com.volcengine.effectone.Launch.EOExport" />
        "android.intent.category.DEFAULT" />
    

```


<span id="55ecd052"></span>
## Configuring the file metadata

This function (`setMetadata`) is designed to accept a `Map<String, String>` containing key\-value pairs that define custom metadata. Each key corresponds to a specific metadata tag, and its associated value represents the metadata content. This interface is essential for applications needing to modify file metadata dynamically, facilitating customization of metadata attributes such as title, artist, and album for media files.

<span id="d7832c2e"></span>
### API

```Kotlin
fun setMetadata(metadata: Map<String, String>)
```


<span id="a0dee967"></span>
### **Request parameters**


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|metadata |Map<String, String\> |None |Yes |Custom metadata data is passed in the form of <key, value\> pairs. |


<span id="37e663b8"></span>
### Full sample code

```Kotlin
val customMetadata = mutableMapOf<String, String>()
customMetadata["metadata_key_1"] = "metadata_value_1"
customMetadata["metadata_key_2"] = "metadata_value_2"
customMetadata["metadata_key_3"] = "metadata_value_3"

eoExportManager.setMetadata(customMetadata)    // Needs to be called before exporting the video
// ... 
eoExportManager.exportVideo()
```


<span id="76f12225"></span>
## Prepare watermark resources (optional)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ff684f41d434d7aa6d062817a89bbd4~tplv-goo7wpa0wc-image.image) </span>

The BytePlus Video Editor SDK exclusively accepts input from local paths, and input from `res` resources is not supported. Consequently, it is necessary to download watermark images to the local SD card in advance or embed them into the app. Afterward, the images should be copied to the SD card for usage.

```Kotlin
//  Assuming business watermark resources are in the assets directory
// Business is responsible for implementing the copyWaterMark method
EffectOneExportActivity.copyWaterMark(this)
```


This code is a placeholder indicating where the `copyWaterMark` method should be called. The actual implementation details would be found in the `EffectOneExportActivity` class or elsewhere in the sample code.

<span id="01cb90ee"></span>
## Step 1: Initialize EOExportManager

```Kotlin
private lateinit var eoExportManager:EOExportManager

override fun onViewCreated(
    view: View,
    savedInstanceState: Bundle?,
) {
    super.onViewCreated(view, savedInstanceState)
    // >>>> step1 Initialize EOExportManager
    eoExportManager.init(requireActivity(), view.findViewById(R.id.export_cover_preview)) { suc ->
        if (!suc) {
            requireActivity().finish()
        }
    }
}
```


<span id="dc523b4e"></span>
## Step 2: Export videos

```Kotlin
val saveDir = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DCIM).absolutePath
val dateFormat = SimpleDateFormat("yyyyMMdd-HHmmss", Locale.getDefault())
val exportFileName = "eo-${dateFormat.format(Date())}.mp4"

val exportFilePath = "$saveDir${File.separator}$exportFileName"
 eoExportManager.exportVideo(
    outputPath = exportFilePath,
    outputSetting = EOOutputVideoSettings(),
    exportListener = iEOExportListenerImpl,
)



private val iEOExportListenerImpl by lazy {
    object : EOExportDefaultListener() {
        override fun onDone() {
            Log.d(TAG, "onCompileDone()")
        }

        override fun onError(error: Int,  msg: String?) {
            Log.d(TAG,"onCompileError() error = $error, msg = $msg")
        }

        override fun onProgress(progress: Float) {
            Log.d( TAG,"onCompileProgress() progress =${progress.times(100).toInt()}" )
        }
    }
} 
```
