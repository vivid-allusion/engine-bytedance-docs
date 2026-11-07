---
title: "Android dependency data models"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-android-dependency-data-models"
---

These are some dependency data models code samples that you can refer to when developing Video Editor SDK.

<span id="f668370a"></span>
# Export configuration parameters

```Kotlin
/**
 * Export configuration parameters，
 * @property previewCompileFinishPage Preview and export functions, once the export is completed, the finish page will be displayed.
              SurfaceView cannot be empty
 * @property autoReleaseCompileDone Will memory be automatically released after export is completed?
 */
data class EOExportInitConfig(
    var previewCompileFinishPage :Boolean = false, 
    var autoReleaseCompileDone :Boolean = true
)
```


<span id="c94d6815"></span>
# Preview and export (EOExportModel)

```Kotlin
@Parcelize
data class EOExportModel(
    var draftData: String = "",
    var draftImg: String, // Address of the cover image for the draft page, needs to be passed back when the business is closed
    var draftId: String,
    var isAlbumCover: Boolean = false, // Flag indicating the source of the cover image, whether it's from an album (true) or a video frame (false), needs to be passed back when the business is closed
    var framePosition: Long = 0 // Position of the video frame used for the cover image, needs to be passed back when the business is closed
) : Parcelable
```


<span id="dd3cddbc"></span>
# Video size (EOVideoSize)

```Kotlin
data class EoVideoSize(
    @androidx.annotation.IntRange(from = 1) val width: Int = 720,
    @androidx.annotation.IntRange(from = 1) val height: Int = 1280
) 
```


<span id="e244385f"></span>
# Export settings (EOOutputVideoSettings)

```Kotlin
data class EOOutputVideoSettings(
    var outputFps: EOFps = EOFps.FPS_30,
    var outputRes: EOResolution = EOResolution.RES_720P,
    // Whether to use software decoding; adjust based on device performance, default is to enable software decoding for low-end devices or insufficient hardware decoding/hardware encoding
    var useSoftwareDecode: Boolean = true,
    // Whether to use hardware encoding, default is to enable hardware encoding
    var useHWEncoder: Boolean = true
) 
```


<span id="d3ce5873"></span>
# Exported video resolution (EOResolution)

```Kotlin
enum class EOResolution(
    val resValue: String,
) {
    RES_540P("540p"),
    RES_720P("720p"),
    RES_1080P("1080p"),
    RES_4K("4k"),;
} 
```


<span id="f6744b7f"></span>
# Exporting FPS (EOFps)

```Kotlin
enum class EOFps(val fpsValue: String, val value: Int) {
    FPS_25("25 FPS", 25),
    FPS_30("30 FPS", 30),
    FPS_50("50 FPS", 50),
    FPS_60("60 FPS", 60),
} 
```


<span id="2732c374"></span>
# Export callback (IEOExportListener)

```Kotlin
interface IEOExportListener {
    /**
     * Export error
     * @param error Error code
     * @param msg Error message
     */
    fun onError(error: Int, msg: String?)

    /**
     * Export successful
     */
    fun onDone()

    /**
     * Export error
     * @param progress Progress 0~1
     */
    fun onProgress(progress: Float)
} 
```
