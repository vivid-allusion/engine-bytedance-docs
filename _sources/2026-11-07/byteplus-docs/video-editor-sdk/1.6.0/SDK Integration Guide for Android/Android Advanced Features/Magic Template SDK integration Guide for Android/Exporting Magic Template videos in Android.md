---
title: "Exporting Magic Template videos in Android"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-exporting-magic-template-videos-in-android"
---

Exporting Magic Template videos involves saving the created content in the desired format or platform, ensuring compatibility and quality for distribution or further editing.

<span id="8762ed20"></span>
# Export the video to the local storage

Export the video to the local storage.

<span id="5397a359"></span>
## API definition

```Kotlin
fun compileNLEModel(outFilePath: String, compileParam: CompileParam?, listener: CompileListener)
/** 
 * Cancel the API of exporting video
 */ 
fun cancelCompile()
```


<span id="cdd4aba2"></span>
### Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|outFilePath |String |N/A |Yes |The location where the exported file will be saved. |
|compileParam |CompileParam |N/A |Yes |Contains export parameters such as resolution, bitrate, and encoding settings. |
|listener |ExportStatusListener |N/A |Yes |A callback interface to track the status of the export process. |


<span id="81a1aa2b"></span>
## Data class

```Kotlin
data class CompileParam( 
    val resolution: ExportResolution,
    val supportHwEncoder: Boolean,
    val bps: Int,
    val fps: Int,
    val gopSize: Int,
    val swMaxRate: Long,
    val swCRF: Int,
    val bitrateMode: VEVideoEncodeSettings.ENCODE_BITRATE_MODE
) : Parcelable
    
                        
 enum class ExportResolution(val label: String, val width: Int, val height: Int, val level: Int) {
    V_4K("4K", 3840, 2160, 4000),
    V_2K("2K", 2560, 1440, 2000),
    V_1080P("1080p", 1920, 1080, 1080),
    V_720P("720p", 1280, 720, 720),
    V_480P("480p", 858, 480, 480)
}
```


<span id="6deb8e0f"></span>
### Parameters


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|resolution |ExportResolution |Yes |Specifies the resolution of the export. |
|supportHWEncoder |boolean |true |Indicates if hardware encoding is supported (`true`) or not (`false`). |
|bps |Int |500000 |Bits per second (bitrate) for the encoding. |
|fps |Int |30 |Frames per second for the export. |
|gopSize |Int |60 |Size of the group of pictures (GOP) for the encoding. |
|swMaxRate |Long |10000000 |Maximum rate for software encoding. |
|swCFR |Int |23 |Constant Rate Factor (CRF) for software encoding. |
|bitrateMode |VEVideoEncodeSettings.ENCODE_BITRATE_MODE |VEVideoEncodeSettings.ENCODE_BITRATE_MODE_VBR |Mode for bitrate encoding (defined in `VEVideoEncodeSettings`). |


<span id="1316bb93"></span>
## Sample code

```Kotlin
val param = createCompileParam()
val outputVideoPath = "/storage/emulated/0/camera/20210528143142.mp4"
cutSamePlayer?.compileNLEModel(outputVideoPath, param, object : CompileListener {
        override fun onCompileDone() {
            Log.d(TAG, "onCompileDone")
            // Compile done
        }
  
        override fun onCompileProgress(progress: Float) {
            //Compile progress
        }

        override fun onCompileError(
            error: Int,
            ext: Int,
            f: Float,
            msg: String?
        ) {
            // Compile error
        }
    })
```


<span id="e78242dd"></span>
# Video frame extraction

Get a screenshot of a specific time stamp.

<span id="60847659"></span>
## API definition

```Kotlin
fun getVideoFrameWithTime(timeStamps: IntArray, width: Int, height: Int, listener: GetImageListener) 
```


<span id="9cde21d5"></span>
## Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|timeStamps |Long |1500 |Yes |The time stamp, unit: milliseconds. |
|width |Int |1920 |Yes |Width of the frame. |
|height |Int |1080 |Yes |Height of the frame. |
|listener |CallbackInterface |N/A |Yes |Callback interface for frame extraction. |


<span id="b005fb0b"></span>
## Sample code

```Kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
cutSamePlayer?.getVideoFrameWithTime(timeStamps, width,height,
    object :GetImageListener{
        override fun onGetImageData(  
            bytes: ByteArray?,
            pts: Int,
            width: Int,
            height: Int,
            score: Float
        ) {
            if (bytes != null) {
                val bmp = Bitmap.createBitmap(width, height, Bitmap.Config.ARGB_8888)
                bmp.copyPixelsFromBuffer(ByteBuffer.wrap(bytes))
                listener?.frameBitmap(pts.toString(), bmp)
            } else {
                cutSamePlayer?.cancelGetVideoFrames() // After frame extraction is complete, you need to cancel; otherwise, it will remain in the frame extraction state.
            }
        }

    })
```
