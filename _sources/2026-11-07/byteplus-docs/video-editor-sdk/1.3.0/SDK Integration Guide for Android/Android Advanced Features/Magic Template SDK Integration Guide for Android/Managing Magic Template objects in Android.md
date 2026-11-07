---
title: "Managing Magic Template objects in Android"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-managing-magic-template-objects-in-android"
---

Managing the template objects involves handling their creation, modification, and usage within the application, ensuring they are utilized effectively for generating or editing content.

<span id="8a272f5a"></span>
# Create template objects

Provide a material processing interface. Use the same template object within the production cycle of a template video. This object is needed when creating a `CutSameSource` object for the first time.

<span id="edd93c6b"></span>
#### API definition

```Kotlin
/**
 * Template resource objects
 * The template supports importing either a zip package or an extracted folder; you can choose to pass in either of the two fields, but if both are provided, the zipPath will be prioritized.
 * @param md5: template file md5
 * @param zipPath
 * @param unzipPath

 */
data class SourceInfo(
    val md5: String,
    val zipPath: String = "",
    val unzipPath: String = ""
)
```


```Kotlin
/**
 * @param sourceInfo: template resource object
 */
fun createCutSameSource(sourceInfo: SourceInfo): CutSameSource 
```


<span id="be1a0932"></span>
#### Sample code

```Kotlin
//Invoke the interface to create a `CutSameSource` object using the `SourceInfo` object.
cutSameSource = CutSameSolution.createCutSameSource(
    SourceInfo(
        templateItem.md5,
        templateItem.zipPath,
        templateItem.unZipPath
    )
)
```


<span id="d262a714"></span>
# Parsing template information

Parse the template to get the slot information of the template.

<span id="e950ff71"></span>
#### API definition

```Kotlin
fun prepareSource(
    listener: PrepareSourceListener)
    
    
 interface PrepareSourceListener {
     //Template preparation progress
     fun onProgress(progress: Float)
     //Template preparation successful, returning slot information
     fun onSuccess(mediaItemList: ArrayList<MediaItem>?,
                   textItemList: ArrayList<TextItem>?,
                   model: NLEModel
     )
     //Template preparation failed
     fun onError(code: Int, message: String?)
}
```


<span id="d4b5c67b"></span>
#### Sample code

```Kotlin
cutSameSource?.prepareSource(object : PrepareSourceListener {
    override fun onProgress(progress: Float) {
    }

    override fun onSuccess(
        mediaItemList: ArrayList<MediaItem>?,
        textItemList: ArrayList<TextItem>?,
        model: NLEModel
    ) {
        //Populate the relevant fields in the `mediaItemList`
    }

    override fun onError(code: Int, message: String?) {
      
    }
})
```


<span id="bd2bf7a8"></span>
# Material composition processing

Perform compression, reverse playback, and other treatments on the selected material after selection.

<span id="85e2a69d"></span>
#### API definition

```Kotlin
/**
 * @param processMediaItems: selected material list
 * @param compressSourceListener: material processing status interface
 */
fun composeSource(
    processMediaItems: ArrayList<MediaItem>,
    compressSourceListener: ComposeSourceListener
)
```


```Kotlin
// Material processing status interface
interface ComposeSourceListener {
    // Processing failed
    fun onError(errorCode: Int, message: String?)
    // Prosessing progress
    fun onProgress(progress: Int)
    // Processing successful
    fun onSuccess(mediaItems: ArrayList<MediaItem>?)
}
```


<span id="9db65174"></span>
#### Sample code

```Kotlin
cutSameSource?.composeSource(data, object : ComposeSourceListener {
    override fun onError(errorCode: Int, message: String?) {
        // Material processing failed
    }

    override fun onProgress(progress: Int) {
        // Material processing progress
    }

    override fun onSuccess(mediaItems: ArrayList<MediaItem>?) {
        // Material processing successful
    }
})
```


<span id="ed4ea54d"></span>
# Create CutSamePlayer objects

Create a `CutSamePlayer` object, which provides capabilities such as video preview, slot editing, text editing, and video export.

<span id="e26fac88"></span>
#### API definition

```Kotlin
/**
 * Create CutSamePlayer
 * @param surfaceView: Player object
 * @param cutSameSource: Material Operation Object, this parameter can be null in the case of importing a draft
 */
fun createCutSamePlayer(surfaceView: SurfaceView, cutSameSource: CutSameSource?): CutSamePlayer
```


<span id="8e2b83f6"></span>
#### Sample code

```Kotlin
cutSamePlayer = CutSameSolution.createCutSamePlayer(videoSurfaceView, cutSameSource)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Creating a <code>cutSamePlayer</code> depends on the creation of a <code>cutSameSource</code> object, so you need to create the <code>cutSameSource</code> object first.</div>


<div data-tips="true" data-tips-type="tip">After using <code>cutSamePlayer</code>, you must call <code>release()</code> to free up resources.</div>


<span id="557f0170"></span>
# Replay

Generate a real\-time preview video based on the template and processed materials.

<span id="c6bf76c6"></span>
#### API definition

```Kotlin
/**
 * @param mediaItems: Media material
 * @param textItems: Text material
 * @param listener: Add a player state callback interface
 */
fun preparePlay(mediaItems: List<MediaItem>?, textItems: List<TextItem>?)

//PlayerStateListener registration method
fun registerPlayerStateListener(playerStateListener: PlayerStateListener)
fun unRegisterPlayerStateListener(playerStateListener: PlayerStateListener)
```


```Kotlin
//Player state callback interface
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
    fun onChanged(state: Int)
    // Play progress
    fun onPlayProgress( process: Long)
    // End play
    fun onPlayEof()
    // Player object error
    fun onPlayError(what: Int, extra: Int)
}
```


<span id="1af5fc09"></span>
#### Sample code

```Kotlin
val listener = object : PlayerStateListener {
    override fun onFirstFrameRendered() {
    
    }

    override fun onChanged(player: BasePlayer, state: Int) {
        when (state) {
            PlayerStateListener.PLAYER_STATE_PREPARED -> {
                Log.d(TAG, "PLAYER_STATE_PREPARED")
                cutSamePlayer?.start()
            }
            PlayerStateListener.PLAYER_STATE_PLAYING -> {
                // Player state playing
            }
            PlayerStateListener.PLAYER_STATE_ERROR -> {
                // Player state error
            }
            PlayerStateListener.PLAYER_STATE_IDLE -> {
                // Player state idle
            }
            PlayerStateListener.PLAYER_STATE_PAUSED -> {
                // Player state pause
            }
            PlayerStateListener.PLAYER_STATE_DESTROYED -> {
                // Player state destroyed
            }
        }
    }

    override fun onPlayEof() {
        // End play
    }

    override fun onPlayError(player: BasePlayer, what: Int, extra: Int) {
        // Player object error
    }

    override fun onPlayProgress(player: BasePlayer, process: Long) {
        // Play progress
    }
}

cutSamePlayer?.preparePlay(mediaItemList, textItemList)
```
