---
title: "Detailed Development Guide - Android - Magic Template"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-detailed-development-guide-android-magic-template-v.4.0.2"
---

<span id="API call process"></span>
# **API** **call process**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/cd08169a50564c8399a01e205748604b~tplv-em5hxbkur4-noop.image?width=1403&height=708) </span>

<span id="API description"></span>
## **API description**

<span id="Configure authentication settings"></span>
### **Configure authentication settings**

<span id="Feature"></span>
#### **Feature**

Configures the authentication settings, including the app ID for license application and the path of the license file.

<span id="API definition"></span>
#### **API definition**

```kotlin
class AuthorityConfig internal constructor(builder: Builder){

    val licensePath: String // The path of the license file.

    val appId: String // The app ID for license application.

    val authorityListener: AuthorityListener? // The callback API for listening for the authentication status.

 }
interface AuthorityListener{

    fun onError(errorCode: Int, errorMsg: String)// The authentication failure callback.

}



// The authentication status code.

public enum State {

     SUCCESS(0), //  The authentication succeeded.

     INVALID_FUNCNAME(1), // The method name is invalid.

     INVALID_PATH(2), // The specified license path is invalid.

     INVALID_APPID(3), // The specified app ID is invalid.

     FILE_ERROR(4), // Failed to open the license file.

     TYPE_NOT_MATCH(5), // The license file type does not match.

     INVALID_VERSIONS(6), // The version of the license is not supported.

     INVALID_BLOCK_COUNT(7), // The license block is invalid.

     LICENSE_STATUS_INVALID(8), // The license status is invalid.

     LICENSE_STATUS_EXPIRED(9), // The license has expired.

     LICENSE_NO_FUNC(10), //  The specified method name does not exist.

     LICENSE_STATUS_NO_MATCH(11), // The status of the license does not match.

     LICENSE_STATUS_ID_NOT_MATCH(12), // The status ID does not match.

     UN_KNOW_ERROR(13); // Unknown error.

 }
```


<span id="Sample code"></span>
#### **Sample code**

See SDK initialization.

<span id="Configure template fetching"></span>
### **Configure template fetching**

<span id="Feature"></span>
#### **Feature**

You can call this API to set the common parameters such as the **host** and **pagesize** for template fetching.

<span id="API definition"></span>
#### **API definition**

```kotlin
class TemplateFetcherConfig{

    val host: String  // The domain name of the server.

    val pageSize: Int   // The number of items fetched each time. 

    val extraCommonMap: Map<String,Any> // The custom common parameters.

}
```


<span id="Sample code"></span>
#### **Sample code**

See SDK initialization.

<span id="Configure effect fetching"></span>
### **Configure effect fetching**

<span id="Feature"></span>
#### **Feature**

Sets the host of the effect fetching service, path for effect fetching, and path for algorithm model fetching.

<span id="API definition"></span>
#### **API definition**

```kotlin
class EffectFetcherConfig {

    val host: String // The domain name of the server.

    val effectLitPath: String // The path of the effect assets.

    val modelPath: String // The path of the algorithm models.

    }
```


<span id="Sample code"></span>
### **Sample code**

See SDK initialization.

<span id="SDK initialization"></span>
## **SDK** **initialization**

<span id="Feature"></span>
### **Feature**

Initializes the CutSameIF SDK. You must initialize the CutSameIF SDK before you can use it.

<span id="API definition"></span>
### **API definition**

```kotlin
/**

 * @param context                                The context that you need to provide.

 * @param authorityConfig                The authentication settings.

 * @param templateFetcherConfig  The template fetching settings.

 * @param effectFetcherConfig       The effect fetching settings.

 * @return 

 */

fun init(context: Context, authorityConfig: AuthorityConfig, templateFetcherConfig: TemplateFetcherConfig, effectFetcherConfig: EffectFetcherConfig)

) 
```


<span id="Sample code"></span>
### **Sample code**

```kotlin
CutSameSolution.init(

    context = application,

    authorityConfig = AuthorityConfig.Builder()

        .appId("com.cutsame.demo")

        .licensePath(getLicenseFilePath())

        .authorityListener(object : AuthorityConfig.AuthorityListener{

            override fun onError(errorCode: Int, errorMsg: String) {

                Log.d(TAG, "Authentication FailedonError $errorCode $errorMsg")

            }

        }).build(),



    templateFetcherConfig = TemplateFetcherConfig.Builder()

        .host("http://xxxx.xxxx.net")

        .pageSize(20)

        .build(),


    effectFetcherConfig =  EffectFetcherConfig.Builder()

        .host("http://xxxx.xxxx.net")

        .modelPath("/xxx/xxxxx")

        .effectLitPath("/xxx/xxxx")

        .build()
```


<span id="Template fetching"></span>
## **Template fetching**

<span id="Create an object for template fetching"></span>
### **Create an object for template fetching**

<span id="Feature"></span>
#### **Feature**

Creates an object for template fetching. This object supports two APIs that are used to fetch template categories and templates.

<span id="API definition"></span>
#### **API definition**

```kotlin
fun getTemplateFetcher(): TemplateFetcher
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
private val fetcher = CutSameSolution.getTemplateFetcher()
```


<span id="Fetch template categories"></span>
### **Fetch template categories**

<span id="Feature"></span>
#### **Feature**

Fetches template categories.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param path            The path for fetching template categories.

 * @param extraMap  The custom parameters for fetching template categories.

 * @param callback    The callback API for fetching template categories.

 */

fun loadCategoryList(

    path: String,

    extraMap: Map<String, Any>?,

    callback: CategoryLoadCallback

)
// The callback API for fetching the templates.

interface CategoryLoadCallback {

    // Template categories fetched successfully.

    fun onSuccess(categoryList: List<TemplateCategory>)

    // Failed to fetch template categories.

    fun onError(errorCode: String, errorMsg: String)

}
```


<span id="Structure definition"></span>
#### **Structure definition**

```kotlin
@Parcelize

data class TemplateCategory(

    @SerializedName("id") val id: Int = -1, //  The ID of the category.

    @SerializedName("name") val name: String = "" //  The name of the category.

) : Parcelable
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
templateFetcher.loadCategoryList(CATEGORY_LIST_PATH, callback = object : CategoryLoadCallback {

    override fun onSuccess(categoryList: List<TemplateCategory>) {

        // Template categories fetched successfully.

        this@TemplateNetModel.categoryList.postValue(categoryList)

    }



    override fun onError(errorCode: String, errorMsg: String) {

        // Failed to fetch template categories.

        this@TemplateNetModel.categoryList.postValue(emptyList())

    }

})
```


<span id="Request for the template list"></span>
### **Request for the template list**

<span id="Feature"></span>
#### **Feature**

Fetches the template list.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param path:            The path for fetching template categories.

 * @param category     The template categories.

 * @param cursor         The cursor used to fetch templates in pagination mode, which is 0 for the first call of this API.

 * @param extraMap   The custom parameters for fetching the template list.

 * @param callback      The callback API for fetching the template list.

 */

fun loadTemplateList(

    path: String,

    category: TemplateCategory,

    cursor: Int,

    extraMap: Map<String, Any>?,

    callback: TemplateLoadCallback

)
// The callback API for fetching the template list.

interface TemplateLoadCallback {

    // Template list fetched successfully.

    fun onSuccess(templateList: List<TemplateItem>, hasMore: Boolean, nextCursor: Int)

    // Failed to fetch the template list.

    fun onError(errorCode: String, errorMsg: String)

}
```


<span id="Structure definition"></span>
#### **Structure definition**

```kotlin
@Parcelize

data class TemplateItem(

    @SerializedName("id") val id: Long = -1, //  The ID of the template.

    @SerializedName("short_title") val shortTitle: String = "", // The short title of the template.

    @SerializedName("title") val title: String = "", //  The full title of the template.

    @SerializedName("duration") val duration: Long = 0, //  The length of the video.

    @SerializedName("fragment_count") val fragmentCount: Int = 0, //  The number of template segments.

    @SerializedName("template_url") val templateUrl: String = "", //  The URL of the template.

    @SerializedName("create_time") val createTime: Long = 0, // The time when the template was created.

    @SerializedName("md5") val md5: String? = "", //  The MD5 string of the template file.

    @SerializedName("extra") val extra: String = "", //  Other description.

    @SerializedName("cover") val cover: Cover? = null, //  The thumbnail information.

    @SerializedName("video_info") val videoInfo: UrlModel? = null, //  The information about the transcoded video.

    @SerializedName("origin_video_info") val oriVideoInfo: UrlModel? = null, //  The information about the original video.

    @SerializedName("counter_data") val counterData: CounterData? = null, //  The custom counter.

    @SerializedName("author") val author: Author? = null, // The author information.

    @SerializedName("limit") val limit: Limit? = null,  //  The limit for uploading the template.

    @SerializedName("template_tags") val templateTags: String = "", //  The tags of the template.

    @SerializedName("status") val status: Int = -1 //  The status of the template. Valid values: 1 and 2. A value of 1 indicates that the template is online. A value of 2 indicates that the template is offline.

) : Parcelable
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
templateFetcher.loadTemplateList(TEMPLATE_LIST_PATH, category, nextCursor, callback = object :

    TemplateLoadCallback {

    override fun onSuccess(

        templateList: List<TemplateItem>,

        hasMore: Boolean,

        nextCursor: Int

    ) {

         // Template list fetched successfully.

        this@TemplateNetPageModel.nextCursor = nextCursor

        hasMoreTemplate.postValue(hasMore)

        val oldValue = templateItems.value ?: ArrayList()

        if (refresh) {

            templateItems.postValue(templateList)

        } else {

            templateItems.postValue(oldValue + templateList)

        }

    }



    override fun onError(errorCode: String, errorMsg: String) {

        Log.d(TAG, "loadFeedList: error $errorCode $errorMsg")

        // Failed to fetch the template list.

        templateItems.postValue(emptyList())

    }

})
```


<span id="Asset management"></span>
## **Asset management**

<span id="Obtain an asset management object"></span>
### **Obtain an asset management object**

<span id="Feature"></span>
#### **Feature**

Provides an asset processing API for playback object creation. One template video production process uses one **source** object.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param sourceUrl  The download URL of the template.

 */

fun getCutSameSource(sourceUrl: String):CutSameSource?
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
private var cutSameSource = CutSameSolution.getCutSameSource(sourceUrl)
```


<span id="Note"></span>
#### **Note**

After you use CutSameSource, call the release() method to release the resources.

<span id="Process media assets"></span>
### **Process media assets**

<span id="Feature"></span>
#### **Feature**

Processes selected assets.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param processMediaItems          The list of selected assets.

 * @param compressSourceListener  The API for listening for the asset processing status.

 */

fun composeSource(

    processMediaItems: ArrayList<MediaItem>,

    compressSourceListener: ComposeSourceListener)
// The API for listening for the asset processing status.

interface ComposeSourceListener {

    // Processing failed.

    fun onError(errorCode: Int, message: String?)

    //  The processing progress.

    fun onProgress(progress: Int)

    //  Processing succeeded.

    fun onSuccess(mediaItems: ArrayList<MediaItem>?)

}
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
cutSameSource?.composeSource(data, object : ComposeSourceListener {

    override fun onError(errorCode: Int, message: String?) {

        // Failed to process the assets.

        setResult(Activity.RESULT_CANCELED, Intent().apply {

            putExtra(CutSameUiIF.ARG_CUT_COMPRESS_SOURCE, sourceUrl)

        })

        finish()

    }

    override fun onProgress(progress: Int) {

        // The asset processing progress.

        updateProgress(progress)

    }

    override fun onSuccess(mediaItems: ArrayList<MediaItem>?) {

        // The assets are processed successfully.

        val dataIntent = Intent().apply {

            CutSameUiIF.setCompressResultData(this, mediaItems!!)

        }

        setResult(Activity.RESULT_OK, dataIntent)

        finish()

    }

})
```


<span id="Playback object management"></span>
## **Playback object management**

<span id="Create a preview object"></span>
### **Create a preview object**

<span id="Feature"></span>
#### **Feature**

Provides APIs for video preview and video export.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 *  Create CutSamePlayer.

 * @param surfaceView   The playback objects.

 * @param sourceUrl       The download URL of the template.

 */

fun createCutSamePlayer(surfaceView: SurfaceView, sourceUrl: String): CutSamePlayer?



/**

 *  Fetches the CutSamePlayer that you created.

 * @param sourceUrl      The download URL of the template.

 */

fun getCutSamePlayer(url: String): CutSamePlayer?
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
cutSamePlayer = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)
```


<span id="Note:"></span>
#### **Note:** 

\*\*1、\*\*CutSamePlayer depends on CutSameSource. Therefore, you must create CutSameSource first. Otherwise, CutSamePlayer cannot be created.

\*\*2、\*\*After you use CutSamePlayer, call the release() method to release the resources.

<span id="Listen for playback events"></span>
### **Listen for playback events**

<span id="Feature"></span>
#### **Feature**

Generates video preview based on the template and processed assets data.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**
 * @param mediaItems  The media assets.
 * @param textItems      The text assets.
 * @param listener         The callback API for adding the playback status.
 */
fun preparePlay(mediaItems: List<MediaItem>?, textItems: List<TextItem>?, listener: PlayerStateListener)
  

```


```kotlin
// The callback API for listening for the playback status.
interface PlayerStateListener {
    companion object {
        // The player is idle.
        const val PLAYER_STATE_IDLE = 1001
       // The player is prepared.
        const val PLAYER_STATE_PREPARED = 1002
        // The player is paused.
        const val PLAYER_STATE_PAUSED = 1004
        // The player is playing.
        const val PLAYER_STATE_PLAYING = 1005
        // The player encounters an error.
        const val PLAYER_STATE_ERROR = 1006
        // The player is destroyed.
        const val PLAYER_STATE_DESTROYED = 1007

    }
    // The first frame is rendered.
    fun onFirstFrameRendered()
    // The status of the player is changed.
    fun onChanged(player: BasePlayer, state: Int)
    // The playback progress.
    fun onPlayProgress(player: BasePlayer, process: Long)
    // The playback is ended.
    fun onPlayEof()
    // The player encounters a playback object error.
    fun onPlayError(player: BasePlayer, what: Int, extra: Int)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
cutSamePlayer?.preparePlay(mediaItemList, textItemList, object : PlayerStateListener {

    override fun onFirstFrameRendered() {

        onPlayerFirstFrameOk()

    }

    override fun onChanged(player: BasePlayer, state: Int) {

        when (state) {

            PlayerStateListener.PLAYER_STATE_PREPARED -> {

                Log.d(TAG, "PLAYER_STATE_PREPARED")

                val textItems = cutSamePlayer?.getTextItems()

                if(textItems != null ){

                    // The player is prepared.

                    mutableTextItemList = textItems

                }

                onPlayerPrepareOk()

                if(!isScreenOn(this@CutPlayerActivity)){

                    return

                }

                cutSamePlayer?.start()

            }

            PlayerStateListener.PLAYER_STATE_PLAYING -> {

                // The player is playing.

                onPlayerPlaying(true)

            }

            PlayerStateListener.PLAYER_STATE_ERROR -> {

                // The player encounters an error.

                onPlayerPlaying(false)

            }

            PlayerStateListener.PLAYER_STATE_IDLE -> {

                // The player is idle.

                onPlayerPlaying(false)

            }

            PlayerStateListener.PLAYER_STATE_PAUSED -> {

                // The player is paused.

                onPlayerPlaying(false)

            }

            PlayerStateListener.PLAYER_STATE_DESTROYED -> {

                // The player is destroyed.

                onPlayerDestroy()

            }

        }

    }



    override fun onPlayEof() {

        // The playback is ended.

        onPlayerPlaying(false)

    }



    override fun onPlayError(player: BasePlayer, what: Int, extra: Int) {

        // The player encounters a playback object error.

    }



    override fun onPlayProgress(player: BasePlayer, process: Long) {

        // The playback progress.

        onPlayerProgress(process)

    }

})
```


<span id="Export a video"></span>
### **Export a video**

<span id="Feature"></span>
#### **Feature**

Exports a played video to a local directory.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 *  The video export API.

 * @param outFilePath        The export path.

 * @param compileParam  The export code parameter.

 * @param listener              The export status listener.

 */

fun compile(outFilePath: String, compileParam: CompileParam?, listener: CompileListener)

/**

  * The API for canceling the video export.

 */

fun cancelCompile()
```


```kotlin
/**

 *  The data structure of the video export encoding parameters.

 * @param resolution                   The resolution.

 * @param supportHwEncoder   true: Hardware encoding. false: Software encoding.

 * @param bps                              The video bitrate.

 * @param fps                               The video frame rate.

 * @param gopSize                      The size of the group of pictures (GOP).

 */

 data class CompileParam(val resolution: ExportResolution, 

                        val supportHwEncoder: Boolean, 

                        val bps: Long,  

                        val fps: Long, 

                        val gopSize: Long) : Parcelable

    

                        

 enum class ExportResolution(val label: String, val width: Int, val height: Int, val level: Int) {

    V_4K("4K", 3840, 2160, 4000),

    V_2K("2K", 2560, 1440, 2000),

    V_1080P("1080p", 1920, 1080, 1080),

    V_720P("720p", 1280, 720, 720),

    V_480P("480p", 858, 480, 480)

}
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val param = createCompileParam()

val outputVideoPath = "/storage/emulated/0/相机/20210528143142.mp4"

cutSamePlayer

    ?.compile(outputVideoPath, param, object : CompileListener {

        override fun onCompileDone() {

            Log.d(TAG, "onCompileDone")

            // Scan the album after the export is completed.

            MediaUtil.notifyAlbum(this@ExportActivity, tarFilePath)

            showFinishToast()

            onExportFinish()

        }



        override fun onCompileProgress(progress: Float) {

            // The export progress.

        }



        override fun onCompileError(

            error: Int,

            ext: Int,

            f: Float,

            msg: String?

        ) {

            // Export failed.

        }



    })
```


<span id="Obtain a text asset for playback"></span>
### **Obtain a text asset for playback**

<span id="Feature"></span>
#### **Feature**

Obtains text asset from the template.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 *  Obtain text asset from the template.

 */

fun getTextItems(): ArrayList<TextItem>?
```


```kotlin
/**

 *  The data structure of the text asset.

 */

data class TextItem(

    /**

     *  The duration of the asset.

     */

    val duration: Long = 0,

    /**

     *  Specifies whether the text asset can be modified.

     */

    val mutable: Boolean = false,

    /**

     *  The Asset ID.

     */

    val materialId: String = "",

    /**

     *  The rotation angle.

     */

    val rotation: Double = 0.0,

    /**

     *  The start time for display.

     */

    val targetStartTime: Long = 0L,

    /**

     *  Enter the text content.

     */

    var text: String = ""

)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)

val textItems = cutSamePlayer?.getTextItems()
```


<span id="Update a text asset in the template"></span>
### **Update a text asset in the template**

<span id="Feature"></span>
#### **Feature**

Allows you to edit text in the template.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 *  Update text assets

 * @param materialId  The Asset ID.

 * @param text             The text to be modified.

 */

fun updateText(materialId: String, text: String)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)

val textItems = cutSamePlayer?.updateText(materialId, " Modifies the text.")
```


<span id="Obtain a media asset from the template"></span>
### **Obtain a media asset from the template**

<span id="Feature"></span>
#### **Feature**

Obtains a media asset from the template

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 *  Obtain a media asset from the template.

 */

fun getMediaItems(): ArrayList<MediaItem>?
```


```kotlin
/**

 *  The data structure of the media asset.

 */

data class MediaItem(

    // ********* Attributes **************************

    var materialId  //  Used for seeking project segments.

    : String,

    var targetStartTime //  The start time of the video.

    : Long = 0,

    var isMutable     // True: The media asset can be edited. You can select a video to replace it.

    : Boolean,

    var alignMode //  The alignment type of the video asset, which can be align_video or align_canvas.

    : String = "",

    var isSubVideo //  Indicates whether the media asset is an auxiliary video track.

    : Boolean = false,

    var isReverse //  Indicates whether to play the video asset backward.

    : Boolean = false,

    var cartoonType //  The cartoon effect.

    : Int = 0,

    // ********* Constraints **************************

    var width     // The width.

    : Int,

    var height    //  The height.

    : Int,

    var duration  //  The length.

    : Long,

    // ********* Parameters **************************

    var source

    : String = "", //  The asset URI string or file path.

    var sourceStartTime // The crop start time.

    : Long = 0,

    var cropScale: Float = 0f,

    var crop          //  The crop area.

    : ItemCrop = ItemCrop(0f,0f,0f,0f),

    /**

     * [TYPE_VIDEO], [TYPE_PHOTO]

     */

    val type    //  The asset type, which can be photo or video.

    : String = "",



    val mediaSrcPath //  The original path of the asset.

    : String = ""

)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)

val mediaItems = cutSamePlayer?.getMediaItems()
```


<span id="Update a media asset"></span>
### **Update a media asset**

<span id="Feature"></span>
#### **Feature**

Replaces a video clip.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 *  Update a media asset

 * @param materialId  The Asset ID.

 * @param mediaItem The media asset.

 */

fun updateMedia(materialId: String, mediaItem: MediaItem)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)

// mediaItem is the asset selected on the asset replacing screen.

cutSamePlayer?.updateMedia(materialId,mediaItem)
  
```


<span id="Extract a video frame"></span>
### **Extract a video frame**

<span id="Feature"></span>
#### **Feature**

Extracts the video frame at the specified time point in the timeline.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * Extract a video frame

 * @param timeStamps  The time point to be obtained in the unit of millisecond.

 * @param width             The frame width to be obtained.

 * @param width             The frame height to be obtained.

 * @param listener          The frame fetching callback API.

 */

fun getVideoFrameWithTime(timeStamps: IntArray, width: Int, height: Int, listener: GetImageListener)
  
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)

cutSamePlayer?.getImages(timeStamps, width,height,

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

                cutSamePlayer?.cancelGetVideoFrames() // Cancel the method after video frame extracting; otherwise, the status remains at frame extracting.

                listener?.frameBitmap("", null)

            }

        }



    })
```


<span id="Control playback"></span>
### **Control playback**

<span id="Feature"></span>
#### **Feature**

Controls playback, including starting and pausing.

<span id="API definition"></span>
#### **API definition**

```kotlin
// Start playback.

fun start()

// Pause playback.

fun pause()

/**

 *  Drag the slider on the progress bar to the specified time point for playback.

 * @param position        Indicates the slider position, in milliseconds.

 * @param isAutoPlay   Specifies whether to enable automatic playback.

 */

fun seekTo(position: Int, isAutoPlay: Boolean)
```


```kotlin
// The callback of this API is also triggered when the playback control API is called.
interface PlayerStateListener {

    companion object {

        // The player is idle.

        const val PLAYER_STATE_IDLE = 1001

       // The player is prepared.

        const val PLAYER_STATE_PREPARED = 1002

        // The player is paused.

        const val PLAYER_STATE_PAUSED = 1004

        // The player is playing.

        const val PLAYER_STATE_PLAYING = 1005

        // The player encounters an error.

        const val PLAYER_STATE_ERROR = 1006

        // The player is destroyed.

        const val PLAYER_STATE_DESTROYED = 1007



    }

    // The first frame is rendered.

    fun onFirstFrameRendered()

    // The status of the player is changed.

    fun onChanged(player: BasePlayer, state: Int)

    // The playback progress.

    fun onPlayProgress(player: BasePlayer, process: Long)

    // The playback is ended.

    fun onPlayEof()

    // Playback error.

    fun onPlayError(player: BasePlayer, what: Int, extra: Int)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
val cutSamePlayer: CutSamePlayer? = CutSameSolution.createCutSamePlayer(videoSurfaceView, sourceUrl)

cutSamePlayer?.seekTo(timePos, true)

cutSamePlayer?.start()

cutSamePlayer?.pause()
```


<span id="UI API call process"></span>
## **UI API call process**

Content that is being loaded cannot be copied.

<span id="Template display screen"></span>
### **Template display screen**

<span id="Feature"></span>
#### **Feature**

Creates an intent for switching to the template display screen.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param context  The context that you need to provide.

 */

fun createTemplateUIIntent(context: Context)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
CutSameUiIF.createTemplateUIIntent(this)?.apply {

    startActivity(this)

}
```


<span id="Preview generation screen"></span>
### **Preview generation screen**

<span id="Feature"></span>
#### **Feature**

Creates an intent for switching to the preview generation screen.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param context             The context that you need to provide.

 * @param templateUrl     The download URL of the template.

 * @param templateItem  The template object.

 */

fun createCutUIIntent(context: Context, templateUrl: String, templateItem: TemplateItem)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
CutSameUiIF.createCutUIIntent(context, templateItem.templateUrl, templateItem)?.apply {

    putExtras(requireActivity().intent)

    this.setPackage(context.packageName)

    startActivity(this)

}
```


<span id="Asset selection screen"></span>
### **Asset selection screen**

<span id="Feature"></span>
#### **Feature**

Creates an intent for switching to the asset selection screen.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param context         The context that you need to provide.

 * @param mediaItems The list of assets that needs to be specified.

 */

fun createGalleryUIIntent(context: Context, mediaItems: ArrayList<MediaItem>)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
CutSameUiIF.createGalleryUIIntent(this,itemList)?.apply {

    putExtra(ARG_CUT_SOURCE_URL, sourceUrl)

    addFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP)

    startActivityForResult(this, REQUEST_CODE_PICKER)

}
```


<span id="Asset processing screen"></span>
### **Asset processing screen**

<span id="Feature"></span>
#### **Feature**

Creates an intent for switching to the asset processing screen.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param context          The context that you need to provide.

 * @param mediaItems  The list of assets to be processed.

 * @param templateUrl  The download URL of the template.

 */

fun createCompressUIIntent(context: Context, mediaItems: ArrayList<MediaItem>, templateUrl: String)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
CutSameUiIF.createCompressUIIntent(this, ArrayList(items), sourceUrl).apply {

    startActivityForResult(this, REQUEST_COMPRESS)

}
```


<span id="Asset editing screen"></span>
### **Asset editing screen**

<span id="Feature"></span>
#### **Feature**

Creates an intent for switching to the asset editing screen.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param context        The context that you need to provide.

 * @param mediaItem  The list of assets to be edited.

 */

fun createClipUIIntent(context: Context, mediaItem: MediaItem)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
CutSameUiIF.createClipUIIntent(this, item)?.apply {

    startActivityForResult(this, REQUEST_CODE_REPLACE)

}
```


<span id="Video export screen"></span>
### **Video export screen**

<span id="Feature"></span>
#### **Feature**

Creates an intent for switching to the video export screen.

<span id="API definition"></span>
#### **API definition**

```kotlin
/**

 * @param context            The context that you need to provide.

 * @param templateUrl   The download URL of the template.

 * @param canvasSize     The canvas size.

 */

fun createExportUIIntent(context: Context, templateUrl: String, canvasSize: Size)
```


<span id="Sample code"></span>
#### **Sample code**

```kotlin
CutSameUiIF.createExportUIIntent(this, templateUrl, cutSamePlayer.getConfigCanvasSize())?.apply {

    startActivityForResult(this, REQUEST_CODE_NEXT)

}
```


<span id="Note"></span>
### **Note**

For customization, you can add labels when you register custom activities in AndroidManifest.xml. Example:
