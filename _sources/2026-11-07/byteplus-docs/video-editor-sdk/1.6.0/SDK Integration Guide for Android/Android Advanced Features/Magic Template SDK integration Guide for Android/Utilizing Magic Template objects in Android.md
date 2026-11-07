---
title: "Utilizing Magic Template objects in Android"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-utilizing-magic-template-objects-in-android"
---

Utilizing Magic Template's template objects involves effectively integrating and leveraging them within your application to streamline content creation and customization processes.

<span id="52ea9d29"></span>
# Get template media material

Get the template's media materials, that is, the information of the template's variable slots.

<span id="0b204d49"></span>
## API definition

```Kotlin
/**
 * Get template media material 
 * cutSamePlayer.getMediaItems()
 */ 
fun getMediaItems(): ArrayList?
```


<span id="4f7e9e55"></span>
## Parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Non\-business Assigned</strong>: The business does not need to modify or assign values to the fields related to <code>extra</code> or the <code>List</code> returned by <code>CutSameSource.prepareSource()</code>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Business Assigned</strong>: The business needs to modify or assign values to the fields related to <code>extra</code> or the <code>List</code> returned by <code>CutSameSource.prepareSource()</code>.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Conditional Business Assignment</strong>: \*\*\*\* Depending on the business requirements, modify the fields related to <code>extra</code> or the <code>List</code> returned by <code>CutSameSource.prepareSource()</code>.</div>




|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|materialId |string |12345 |Yes |Used for locating the project segment. No business assignment needed. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|targetStartTime |Long |0 |Yes |Material slot position in the template start time. No business assignment needed. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|isMutable |Boolean |True |Yes |The material slot is variable, with `true` indicating variability. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|alignMode |String |`align_video` |Yes |Video material alignment method. "align_video" or "align_canvas". Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|isSubVideo |Boolean |False |No |Whether it is subvideo. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|isReverse |Boolean |False |Yes |Whether reverse is needed. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|cartoonType |Int |0 |No |Cartoon face effect. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|width |Int |1920 |Yes |Width. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|height |Int |1080 |Yes |Height. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|duration |Long |60000 |Yes |Duration. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|oriDuration |Long |60000 |Yes |Duration of replaced material. Business assigned. Needs to be added in when filling in the template slot information. |
|source |String |"path/to/source" |Yes |Path of material. Business assigned. Needs to be passed in when filling in the template slot information. |
|sourceStartTime |Long |0 |Yes |Time cropping start point. Determine whether to assign a value based on business requirements. Assign if present in `extra` or the callback of `CutSameSource.prepareSource()`. |
|cropScale |Float |1.0 |Yes |Material scaling. Determine whether to assign a value based on business requirements. Assign if present in `extra` or the callback of `CutSameSource.prepareSource()`. |
|crop |ItemCrop |ItemCrop(0f, 0f, 0f, 0f) |Yes |Spatial cropping area. Determine whether to assign a value based on business requirements. Assign if present in `extra` or the callback of `CutSameSource.prepareSource()`. |
|type |String |"video" |Yes |Video type, "photo" or "video". Business assigned. Needs to be passed in when filling in the template slot information. |
|mediaSrcPath |String |"path/to/media" |Yes |Source path of material. Business assigned. Needs to be passed in when filling in the template slot information. |
|targetEndTime |Long |60000 |Yes |Material's end time in the template. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |
|volume |Float |1.0 |Yes |Volume. Determine whether to assign a value based on business requirements. Assign if present in `extra` or the callback of `CutSameSource.prepareSource()`. |
|relationVideoGroup |String |"group1" |Yes |Slot grouping. Non\-business assigned. Can be obtained from `extra` or the callback of `CutSameSource.prepareSource()`. |


<span id="451919fe"></span>
## Sample code

```Kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
val mediaItems = cutSamePlayer?.getMediaItems()  
```


<span id="b7f21e33"></span>
# Update media material

Support the feature of replacing media materials, that is, replacing slot materials.

<span id="18ed8070"></span>
## API definition

```Kotlin
fun updateMedia(materialId: String, mediaItem: MediaItem) 
```


<span id="f494e8ef"></span>
## Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|materialId |String |Yes |12345 |The identifier for the media material to be updated. |
|mediaitem |MediaItem |Yes |N/A |The `MediaItem` object containing the updated media details. |


<span id="c8230cf5"></span>
## Sample code

```Kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
// repalcedMediaItem is the material selected through material replacement page
 cutSamePlayer?.updateMedia(materialId, repalcedMediaItem) 
```


<span id="c2a40152"></span>
# Retrieving the text material in player

Retrieve the text material.

<span id="6eb402e3"></span>
#### API definition

```Kotlin
/** 
 * Get template text material
 */ 
fun getTextItems(): ArrayList?
```


<span id="b4d48e45"></span>
#### Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|duration |Long |3600 |Yes |Duration of the text display in milliseconds |
|mutable |Boolean |false |No |Whether the text is mutable |
|materialId |String |"12345abc" |No |Unique identifier for the text material |
|rotation |Double |90.0 |No |Rotation angle of the text in degrees |
|targetStartTime |Long |1200 |No |Start time of display in milliseconds |
|text |String |"Hello, World" |No |The actual text content |


<span id="91b86e67"></span>
#### Sample code

```Kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
val textItems = cutSamePlayer?.getTextItems()  
```


<span id="462d2e8f"></span>
# Update template text material

Support the feature of editing template text.

<span id="913b718f"></span>
## API definition

```Kotlin
/**
 * Update text
 * @param materialId: material ID
 * @param text: text need to be modified
 */  
fun updateText(materialId: String, text: String)
```


<span id="d2cd4d2d"></span>
## Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|materialId |String |12345 |Yes |The identifier for the media material to be updated. |
|text |String |N/A |No |Optional text associated with the media item. |


<span id="884246f5"></span>
## Sample code

```Kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
val textItems = cutSamePlayer?.updateText(materialId, "text need to be modified")   
```


<span id="4b061bc2"></span>
# Play control

Support play control, such as starting, pausing, and seeking a specific time.

<span id="aee788e3"></span>
## API definition

```Kotlin
//Start to play 
fun start()
//Pause
fun pause()
/** 
 * Drag to a specific time to play
 * @param position: The position to drag to, unit: ms
 * @param isAutoPlay: Autoplay or not
 */
fun seekTo(position: Int, isAutoPlay: Boolean)
```


```Kotlin
// Invoking the play control interface will also trigger the callback of this interface
interface PlayerStateListener {  
    companion object { 
        // Player state idle
        const val PLAYER_STATE_IDLE = 1001
       // Player state prepared
        const val PLAYER_STATE_PREPARED = 1002
        // Player state paused
        const val PLAYER_STATE_PAUSED = 1004
        // Player state playing
        const val PLAYER_STATE_PLAYING = 1005
        // Player state error
        const val PLAYER_STATE_ERROR = 1006
        // Player state destroyed
        const val PLAYER_STATE_DESTROYED = 1007

    }
    // First frame rendered
    fun onFirstFrameRendered()
    // Player state changed
    fun onChanged(player: BasePlayer, state: Int)
    // Play progress
    fun onPlayProgress(player: BasePlayer, process: Long)
    // End play
    fun onPlayEof()
    // Play error
    fun onPlayError(player: BasePlayer, what: Int, extra: Int)
```


<span id="68fc9435"></span>
## Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|position |Int |10 |No |The position of the media material, if applicable. |
|isAutoPlay |Boolean |True |No |Indicates whether the media should autoplay. |


<span id="3b902f35"></span>
## Sample code

```Kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
cutSamePlayer?.seekTo(timePos, true)
cutSamePlayer?.start() 
cutSamePlayer?.pause() 
```


<span id="c48c0f7b"></span>
# Set the volume of a specific segment

<span id="fe40f4fe"></span>
## API definition

```Kotlin
fun setVolume(materialId: String, volume: Float)  
```


<span id="08fff18d"></span>
## Parameters


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|materialId |String |12345 |N/A |The identifier for the media material for the volume to be set. |
|volume |Float |0.1 |N/A |The volume to be set. |


<span id="af1a6af0"></span>
## Sample code

```Kotlin

volumeSliderView.setOnSliderChangeListener(object : OnSliderChangeListener() {
    override fun onChange(value: Int) { 
        //....
    }   

    override fun onBegin(value: Int) {
        //....
    }

    override fun onFreeze(value: Int) {
        selectMediaItem?.let {
            // Set volume
            cutSamePlayer?.setVolume(it.materialId, value.toFloat() / 100)
        }
    }
})
```


<span id="c9e4b6ec"></span>
# Get the volume of a specific segment

<span id="d8ba3311"></span>
## API definition

```Kotlin
/**
 * @param materialId: material ID. 
 * @return Float: volume value
 */ 
fun getVolume(materialId: String): Float
```


<span id="b2ad32da"></span>
## Sample code

```Kotlin
// Get the volume when the volume view is displayed
private fun showSlotVolumeLayout() { 
    if (volumeLayout.visibility == View.GONE) {
        selectMediaItem?.let { 
            // Get volume
            val volume = cutSamePlayer?.getVolume(it.materialId)?.times(100)?.toInt() ?: 0
            volumeSliderView.currPosition = volume
        }
        volumeLayout.visibility = View.VISIBLE
    }
}
```


<span id="42c4d8a3"></span>
# Background audio replacement and volume adjustment

<span id="2b0c6026"></span>
## API definition

```Kotlin
interface ICutSameAudio { 
    companion object {
        const val SUCCESS = 0
 
        /** 
         * Input parameters do not meet the conditions
         */
        const val PARAMS_ERROR = -1

        /**
         * Invalid audio file information
         */
        const val AUDIO_INFO_INVALID = -2

        /**
         * Invalid volume value
         */
        const val INVALID_VOLUME = -1.0f
    }

    /**
     * Set custom audio for template
     * @param path The local path of the audio file
     * @param audioName The name of the audio, an optional parameter
     * @param fromTimeMs  The starting point in the audio file from which to begin playback. For example, if the original audio file is 3 minutes long (180 seconds), but the template audio only requires 10 seconds
     * If you wish to select the chorus part, which might be from 100 to 110 seconds, then the parameter should be set to 100 * 1000, with the unit being milliseconds. If you want to start from the beginning, just set it to 0.
     *
     * @return error code
     */
    fun setCustomAudio(path: String, audioName: String = "", fromTimeMs: Long): Int

    /**
     * Get the start time of the template audio
     * @return Unit: ms
     */
    fun getTemplateAudioStartTime(): Long

    /**
     * Get the duration of the template audio
     * @return Unit:ms
     */
    fun getTemplateAudioDuration(): Long

    /**
     * Reset to the template audio
     */
    fun resetAudio(): Int

    /**
     * Set the volume. If there is custom music, only set the volume for the custom music track. If there is no custom music track, then set the volume for the original music track.
     * @param volume 0.0 - 1.0
     *
     * @return error code
     */
    fun setAudioVolume(volume: Float): Int

    /**
     * Retrieve the current volume. First, obtain the volume that has been set through the `setAudioVolume(volume)` interface.
     * If it has not been called, first retrieve the volume of the custom audio
     *If custom audio has not been set, then obtain the original audio volume of the template Priority is given to retrieving the volume of the first keyframe, followed by the original audio volume.
     
     
     * @return The corresponding volume value; if it cannot be found, return the result
     * @see INVALID_VOLUME
     */
    fun getAudioVolume(): Float
}
```


<span id="5c62cedc"></span>
## Sample code

```Kotlin
// From CutSamplayer Get audio operation interface
val cutSameAudio: ICutSameAudio = cutSamePlayer.getAudioManager()
 
// Replace the background music.
cutsameAudio.setCustomAudio("/sdcard/Android/data/[pacakge]/music.mp3", "audioName", 0L)
 
// Set the audio at 0.0~0.1 float
cutsameAudio.setAudioVolume(0.8f)

// Reset audio
cutsameAudio.resetAudio() 

//Get the current audio volume
cutsameAudio.getAudioVolume()
```
