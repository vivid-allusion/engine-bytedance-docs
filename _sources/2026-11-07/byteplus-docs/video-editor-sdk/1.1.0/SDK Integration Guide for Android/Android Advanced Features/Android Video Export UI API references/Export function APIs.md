---
title: "Export function APIs"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-export-function-apis_1_1_0"
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
|exportListener |IEoExportListener |Null |No |The callback for video exports.<br><br>```Kotlin```<br>```interface IEOExportListener {```<br>```    /**```<br>```     * Error in exporting```<br>```     * @param error code```<br>```     * @param msg message```<br>```     */```<br>```    fun onError(error: Int, msg: String?)```<br>```    /**```<br>```     * Export success```<br>```     */```<br>```    fun onDone()```<br>```    /**```<br>```     * Error in exporting```<br>```     * @param progress 0~1```<br>```     */```<br>```    fun onProgress(progress: Float)```<br>```}```<br><br><br>For more information on the parameter, refer to [Export callback (IEOExportListener)](https://docs.byteplus.com/en/docs/video-editor-sdk/docs-android-dependency-data-models_1_1_0#export-callback-ieoexportlistener). |


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


<span id="a28f842f"></span>
# Exporting photos

The image export functionality is implemented based on the `exportVideo()` function, which exports videos. After completing the video export, image export is achieved by exporting video frames.

<span id="476fb781"></span>
## API

```Kotlin
fun exportVideo(
    outputPath: String,
    outputSetting: EoOutputVideoSettings= EOOutputVideoSettings(),
    exportListener: IEoExportListener? = null
) 
```


<span id="d2eee384"></span>
## Request parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|outputPath |String |None |Yes |The path to which a video is to be exported, such as the album. |
|outputSetting |EoOutputVideoSettings |EOOutputVideoSettings() |No |The export settings.<br><br>```Kotlin```<br>```data class EOOutputVideoSettings(```<br>```    var outputFps: EOFps = EOFps.FPS_30,```<br>```    var outputRes: EOResolution = EOResolution.RES_720P,```<br>```    // Whether to use software decoding; adjust according to low-end device capabilities or insufficient hardware decoding and encoding capabilities. Default is software decoding enabled.```<br>```    var useSoftwareDecode: Boolean = true,```<br>```    // Whether to use hardware encoding. Default is enabled.```<br>```    var useHWEncoder: Boolean = true,```<br>```    // Bitrate setting; default is high bitrate.```<br>```    // Adjust as needed; bitrate settings can refer to the "Video Production Bitrate Reference Table."```<br>```    var bps: Int? = null```<br>```)```<br> |
|exportListener |IEoExportListener |Null |No |The callback for video exports.<br><br>```Kotlin```<br>```interface IEOExportListener {```<br>```    /**.```<br>```     * Error in exporting```<br>```     * @param error code```<br>```     * @param msg message```<br>```     */```<br>```    fun onError(error: Int, msg: String?)```<br>```    /**```<br>```     * Export success```<br>```     */```<br>```    fun onDone()```<br>```    /**```<br>```     * Error in exporting```<br>```     * @param progress 0~1```<br>```     */```<br>```    fun onProgress(progress: Float)```<br>```}```<br><br><br>For more information on the parameter, refer to [Export callback (IEOExportListener)](https://docs.byteplus.com/docs/video-editor-sdk/docs-android-dependency-data-models_1_1_0#2732c374). |


<span id="3d65a022"></span>
## Full sample code

```Kotlin
// Creating temporary video file and exporting photo file
val dateFormat = SimpleDateFormat("yyyyMMdd-HHmmss", Locale.getDefault())

// Temporary video file path
val exportTempFileName = "eo-${dateFormat.format(Date())}.mp4"
val tempFileDir = EOUtils.pathUtil.externalDir("temp_export").absolutePath
val tempPath = File(tempFileDir, exportTempFileName)

// Photo file path for exporting image
val exportFileName = "eo-${dateFormat.format(Date())}.jpg"
val photoFileDir = Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DCIM)?.toString()
val photoPath = File(photoFileDir, exportFileName)

// Executing video export
eoExportViewModel.eoExportManager.exportVideo(
    outputPath = tempPath.absolutePath,
    outputSetting = EOOutputVideoSettings().apply {
        eoVideoEncodeViewModel.resolutionFps.value?.let {
            outputRes = it.first
            outputFps = it.second
        }
        useSoftwareDecode = true
        useHWEncoder = true
    },
    exportListener = EOExportImageListener(activity, photoPath)
)

// Listener for handling exported video files
class EOExportImageListener(
    private val activity: Activity,
    private val photoPath: File,
) : EOExportDefaultListener() {

    // Called when video export is complete
    override fun onDone(outputPath: String) {
        saveFrameAsPhoto(outputPath, photoPath)

        // Deleting temporary video file
        val tempVideoFile = File(outputPath)
        if (tempVideoFile.exists()) {
            tempVideoFile.delete()
            // Scan the deleted file so it reflects in media library
            MediaScannerConnection.scanFile(activity,
                arrayOf(tempVideoFile.absolutePath),
                null
            ) { _, _ ->
                LogKit.d(TAG, "Temp video file deleted successfully: ${tempVideoFile.absolutePath}")
            }
        }
    }

    // Called when an error occurs during export
    override fun onError(error: Int, msg: String?) {
        LogKit.d(TAG, "onCompileError() called with: error = $error, msg = $msg")
    }

    // Called to report export progress
    override fun onProgress(progress: Float) {
        LogKit.d(TAG, "onCompileProgress() : progress = ${progress.times(100).roundToInt()}")
    }

    // Extracts the first frame from the exported video and saves it as a photo
    private fun saveFrameAsPhoto(tempPath: String?, photoPath: File) {
        if (tempPath == null) return

        val retriever = MediaMetadataRetriever()
        try {
            retriever.setDataSource(tempPath)
            val frameBitmap = retriever.getFrameAtTime(0)

            val outStream = FileOutputStream(photoPath)
            frameBitmap?.compress(Bitmap.CompressFormat.JPEG, 100, outStream)
            outStream.close()

            // Scan the saved photo so it reflects in media library
            MediaScannerConnection.scanFile(activity, arrayOf(photoPath.absolutePath), null) { _, _ ->
                LogKit.d(TAG, "Photo saved successfully: $photoPath")
            }
        } catch (e: Exception) {
            LogKit.e(TAG, "Failed to get first frame from video.", e)
        } finally {
            retriever.release()
        }
    }
}
```
