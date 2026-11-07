---
title: "Preview Editor Android APIs"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-preview-editor-android-apis_1_1_0"
---

These are the Preview Editor Android API references.

<span id="cf7e0da5"></span>
# Retrieving video cover image information

The `getVideoCoverImage` API is used to retrieve information about the cover image of a video. It provides details such as the image's path (`draftImg`), its position in the video (`framePosition`), and whether it's sourced from the album or video frames (`isAlbumCover`).

<span id="e6fa06b4"></span>
## API

```Kotlin
fun getVideoCoverImage(
    videoSize: EOVideoSize,
    completionBlock: (draftImg: String, framePosition: Long, isAlbumCover: Boolean) -> Unit
)
```


<span id="9a2790da"></span>
## **Request Parameters**


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|`videoSize` |`EOVideoSize` |N/A |Yes |The size of the video frame to be used as the cover image. |
|`completionBlock` |`(draftImg: String, framePosition: Long, isAlbumCover: Boolean) -> Unit` |N/A |Yes |The callback for retrieving the video frame. If the desired video frame is not available from upstream intent, the system uses the first frame of the video. |


<span id="76aaf2c9"></span>
### completionBlock

This callback retrieves draft cover images and video frame images.

**Parameters**


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|draftImg |String |image_path |Specifies whether the image is from the draft box or video frames. |
|framePosition |Long (unit: ms) |500 |A non\-zero value indicates the position of the draft image in the video. 0 indicates that the draft image is taken from the album. |
|isAlbumCover |Boolean |true |The value `true` indicates that the draft image is from the album, and `false` indicates that the draft image is from video frames. |


<span id="35479116"></span>
## Full sample code

This is the full sample code for get `VideoCoverImage`:

```Kotlin
eoExportManager.getVideoCoverImage { draftImg, framePosition, isAlbumCover ->
    if (isAlbumCover) {
        //updateCoverAlbum(draftImg)
    } else {
        //updateCoverFrame(draftImg, framePosition)
    }
}
```


<span id="f729795e"></span>
# Pausing video exports

The `eoExportManager.pause()` function likely pauses or suspends an ongoing process within the `EOExportManager`. In the context of video editing or export manager, this could be used to temporarily halt the processing of video export, allowing the user or system to control when to resume or continue the export operation.

<span id="ec71f6d2"></span>
## API

```Kotlin
fun pause()
```


<span id="ab3b3842"></span>
## Sample code

```Kotlin
eoExportManager.pause()
```


<span id="f50f54bc"></span>
# Navigating to a specific time within a video

This function allows you to navigate to a particular time point within the video, either smoothly or instantly based on the value of the `isSmooth` parameter.

<span id="b31ac79b"></span>
## API

```Kotlin
fun seekTo(position: Long, isSmooth: Boolean = false)
```


<span id="90333453"></span>
## Request parameters


|**Parameter** |**Type** |**Default Value** |**Required** |**Description** |
|---|---|---|---|---|
|position |Long |None |Yes |The position in the SeekBar in milliseconds. |
|isSmooth |Boolean |false |No |Specifies whether the video starts exactly at the seeked\-to position. |


<span id="58d8936f"></span>
## Sample code

This is the sample code for navigating to a particular time point within the video.

```Kotlin
eoExportManager.seekTo(position, isSmooth)
```


<span id="c8031b96"></span>
# Retrieving video sizes

`getVideoSize` is used to retrieve the size of a video from `EOExportManager`.

<span id="626df6d8"></span>
## API

```Kotlin
fun getVideoSize(): EOVideoSize?
```


<span id="569384f6"></span>
## Request parameters


|**Parameter** |**Description** |
|---|---|
|EOVideoSize? |Retrieves the size of the video. Returns `null` if not available. |


<span id="a040b2bd"></span>
## Sample code

This is the sample code for `getVideoSize`:

```Kotlin

val eoVidoeSize = eoExportManager.getVideoSize()
eoVidoeSize?.let{
    Log.d("Tag"," width = ${eoVidoeSize.width}, height = ${eoVidoeSize.height}")
}
```


<span id="63e7bdf8"></span>
# Calculating video duration

`geTotalVideoDuration` is used to calculate the total video duration.

<span id="2840fbc8"></span>
## API

```Kotlin
fun geTotalVideoDuration(): Long?
```


<span id="5c8b878c"></span>
## Response parameters


|**Parameters** |**Description** |
|---|---|
|Long |Retrieves the video duration. |


<span id="7e9ba7c9"></span>
## Sample code

```Kotlin
val videoDuration = eoExportManager.geTotalVideoDuration()
eoVidoeSize?.let{
    Log.d("Tag"," videoDuration = $videoDuration")
}
```


<span id="e0cf335c"></span>
# Retrieving source model

This API retrieves the source model from `EOExportManager`.

<span id="291b4ff8"></span>
## API

```Kotlin
fun getEOExportModel(): EOExportModel?
```


<span id="519f4945"></span>
## Response parameters


|**Parameter** |**Type** |**Default Value** |**Description** |
|---|---|---|---|
|draftImg |String |N/A |The path of the cover image on the draft page. |
|isAlbumCover |Boolean |false |Indicates whether the cover image is from the album (`true`) or video frames (`false`). |
|framePosition |Long |0 |The position of the cover image in video frames. Defaults to `0`. |


<span id="de5683a8"></span>
## Full sample code

This is the full sample code for getEOExportModel:

```Kotlin
val exportViewModel = eoExportManager.getEOExportModel() ?: return
val totalDuration = eoExportManager.geTotalVideoDuration() ?: return

exportViewModel.takeIf { !it.isAlbumCover }?.let {
    //If saving a video frame as a cover and exiting the page, reopening it, and reselecting a video frame,
    // seek to the position where the video frame was previously saved.
    eoExportManager.seekTo(it.framePosition, false)
}
```
