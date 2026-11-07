---
title: "Cover image APIs"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-cover-image-apis"
---

This topic covers the cover image API references.

<span id="1668809f"></span>
# Retrieving video frames

The purpose of this function seems to be retrieving video frames based on the provided timestamps and video size, and the results are handled through the `completionBlock`.

<span id="75f6c183"></span>
## API

```Kotlin
fun getVideoFrames(
    timestamps: VecLongLong,
    eoVideoSize: EOVideoSize,
    completionBlock: ((videoFrame: Bitmap?) -> Unit)?=null
) 
```


<span id="35b16b04"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|timestamps |VecLongLong |Yes |[1615200000, 1615210000] |A list of frame position values measured in milliseconds. The system supports extracting one or more frame positions in the video. |
|eoVideoSize |EOVideoSize |Yes |EOVideoSize.LARGE |The width and height of the video. |
|completionBlock |((videoFrame: Bitmap?) \-\> Unit)? |No |null or Example Function |Operations within this block may take a significant amount of time to complete.<br><br>`videoFrame`: If video frame extraction is successful, the bitmap of the frame is returned. This method may be called multiple times, depending on the value of timestamps. |


<span id="c2845831"></span>
## Response parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|videoFrame |Bitmap |Yes |Example Bitmap |Bitmap of the video frame if extraction succeeds. Callbacks are sorted based on timestamps. |


<span id="424a9ad7"></span>
## Full sample code

This is the full sample code for getVideoFrame:

```Kotlin
eoExportManager.getVideoFrames(
    VecLongLong(listOf(0)),
    EOVideoSize(720, 1080)
) { bmp ->
    runOnUiThread {
        bmp?.let {
            //
        }
    }
} 
```


<span id="bb846283"></span>
# Setting thumbnails from videos

This function calls the action of selecting or designating a particular frame from a video to serve as the cover or thumbnail for that video.

<span id="53e16c58"></span>
## API

```Kotlin
fun saveVideoFrame(
    videoSize: EOVideoSize,
    saveToDraft: Boolean = true,
    savedBlock: (( String?, Long) -> Unit)? = null
)  
```


<span id="1b5a02bc"></span>
## Request parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|videoSize |EOVideoSize |None |Yes |The width and height of the video. |
|saveToDraft |Boolean |true |No |Specifies whether to save a video frame as the cover image of the draft box. |
|savedBlock |((String?, Long) \-\> Unit) |null |No |Saves the current video frame. |
|||||`String?`: the path of the saved video frame. |
|||||`Long`: the position of the saved video frame, in ms. |


<span id="e1f96ed6"></span>
## Response parameters


|**Parameter** |**Description** |
|---|---|
|(( String?, Long) \-\> Unit) |* String?:Save video frame path String<br><br>* Long： Video frame position, in milliseconds |


<span id="dfc9d25c"></span>
## Full sample code

This is the full sample code for setting thumbnails from videos:

```Kotlin

eoExportManager.saveVideoFrame(EOVideoSize(720, 1080)）{
 loading, bitmapPath, position ->{
    
    }
} 
```


<span id="2f13b5c0"></span>
# Setting thumbnails from albums

This function calls the action of selecting the cover or thumbnail for that video from the albums.

<span id="3f838b5e"></span>
## API

```Kotlin
fun pickAlbum(saveToDraft: Boolean = true,
    completionBlock: ((String?, String?, Boolean) -> Unit)) 
```


<span id="2e315886"></span>
## Request parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|saveToDraft |Boolean |true |No |Specifies whether to save an image from the album as the cover image of the draft box. |
|completionBlock |((String?, String?, Boolean) \-\> Unit) |None |Yes |Selects an image as the cover image from the album built in BytePlus Video Editor SDK. Only static images can be selected. |


<span id="c748e4cd"></span>
## Response parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|completionBlock |String |N/A |N/A |The path of the selected and cropped image. |
||String |N/A |N/A |Error message. |
||Boolean |N/A |N/A |Specifies whether to cancel the operation. |


<span id="2313905e"></span>
## Full sample code

This is the full sample code for setting thumbnails from albums:

```Kotlin
eoExportManager.pickAlbum { bitmapPath: String?, errorMsg: String?, cancel: Boolean ->
    bitmapPath?.let {
        Log.d("Tag","bitmapPath -> $it ")
    }
}
```
