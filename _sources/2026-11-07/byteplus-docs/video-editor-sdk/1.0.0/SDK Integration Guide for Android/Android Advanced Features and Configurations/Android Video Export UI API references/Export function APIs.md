---
title: "Export function APIs"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-export-function-apis"
---

These are the export function API references.

BytePlus Video Editor SDK exclusively accepts input from local paths, and input from `res` resources is not supported. Consequently, it is imperative to pre\-download watermark images to the local SD card or embed them into the app, followed by copying to the SD card.

The default display of the watermark spans the entire video. In the first half, the watermark appears in the top\-left corner, and in the second half, it is positioned in the bottom\-right corner.

<span id="d67e808d"></span>
# Adding watermarks

You can add watermark images by calling the following API.

<span id="c9ed65ad"></span>
## API

```Kotlin
fun shouldAddWaterMark(shouldAddWaterMark: Boolean = true)
```


<span id="12608798"></span>
## Request parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|shouldAddWaterMark |Boolean |true |No |Specifies whether to add a watermark to the exported video. |


<span id="82910ad9"></span>
## Full sample code

This is the full sample code for adding a watermark to a video:

```Kotlin
eoExportManager.shouldAddWaterMark(true)
```


<span id="0e8d2a82"></span>
# Setting watermark images

You can set watermark images by calling the following API.

<span id="be6a318f"></span>
## API

```Kotlin
fun setWaterMarkPath(waterMarkPath: String?)
```


<span id="12c8c814"></span>
## Request parameter


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|waterMarkPath |String |None |Yes |The path of the watermark image for a video to be exported. |


<span id="fd109c88"></span>
## Full sample code

This is the full sample code for setting watermark images:

```Kotlin
eoExportManager.setWaterMarkPath("/sdcard/Download/waterMark/eo-waterMark.jpg")
```


<span id="03b170fc"></span>
# Setting watermark size

You can set the watermark size by calling the following API.

<span id="abd67067"></span>
## API

```Kotlin
fun setWaterMarkSize(videoSize: EOVideoSize)
```


<span id="339954ec"></span>
## Request parameters


|**Parameter** |**Data type** |**Default value** |**Required** |**Description** |
|---|---|---|---|---|
|videoSize |EOVideoSize |EEOVideoSize(134,32) |Yes |Set the size of the exported video watermark image:：<br><br>Unit：dp，dependent on the size given by the UI designer. Only a difference of (24,32) is allowed. This cannot be changed. |


<span id="cfd16e85"></span>
## Sample code

```Kotlin
eoExportManager.setWaterMarkSize(EOVideoSize(width = 29, height = 31))
```


<span id="63382fd2"></span>
# Exporting videos

This function allows you to export your videos.

<span id="fc028646"></span>
## API

```Kotlin
fun exportVideo(
    outputPath: String,
    outputSetting: EoOutputVideoSettings= EOOutputVideoSettings(),
    exportListener: IEoExportListener? = null
)
```


<span id="76ded6d6"></span>
## Request parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|outputPath |String |None |Yes |The path to which a video is to be exported, such as the album. |
|outputSetting |EoOutputVideoSettings |EOOutputVideoSettings() |No |The export settings. |
|exportListener |IEoExportListener |Null |No |The callback for video exports.<br><br>```Kotlin```<br>```interface IEOExportListener {```<br>```    /**```<br>```     * Error in exporting```<br>```     * @param error code```<br>```     * @param msg message```<br>```     */```<br>```    fun onError(error: Int, msg: String?)```<br>```    /**```<br>```     * Export success```<br>```     */```<br>```    fun onDone()```<br>```    /**```<br>```     * Error in exporting```<br>```     * @param progress 0~1```<br>```     */```<br>```    fun onProgress(progress: Float)```<br>```}```<br><br><br>For more information on the parameter, refer to [Export callback (IEOExportListener)](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-dependency-data-models#export-callback-ieoexportlistener). |


<span id="f604856d"></span>
### EoOutputVideoSetting


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|outputFps |EOFps |FPS_30 |No |Output frames per second. |
|outputRes |EOResolution |RES_720P |No |Output resolution. |
|useSoftwareDecode |Boolean |true |No |Indicates whether to use software decoding; adjust based on device performance. |
|useHWEncoder |Boolean |true |No |Indicates whether to use hardware encoding. |


**Sample code**

```Kotlin
data class EOOutputVideoSettings(
    var outputFps: EOFps = EOFps.FPS_30,
    var outputRes: EOResolution = EOResolution.RES_720P,
    // Whether to use software decoding, low-end machines or hardware decoding and encoding capabilities are insufficient, adjust according to the business party, and soft decoding is enabled by default.
    var useSoftwareDecode: Boolean = true,
    // Whether to use hard coding, default enabled
    var useHWEncoder: Boolean = true,
)
```


<span id="8a1a111e"></span>
### Full sample code

This is the full sample code for exporting videos:

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
    object : EOExportListenerAdapter() {
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


<span id="83650d65"></span>
# Cancel exporting videos

This function cancels your videos from exporting.

<span id="dcbc6d62"></span>
## API

```Kotlin
fun cancelExport()
```


<span id="54c687c8"></span>
# Full sample code

This is the full sample code to cancel your videos from exporting:

```Kotlin
eoExportManager.cancelExport()
```
