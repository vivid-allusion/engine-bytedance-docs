---
title: "Importing in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-importing-in-android"
---

This function involves importing videos and images to the editing environment.

<span id="e7725665"></span>
# Procedure

These are the steps for using the import module:


1. Initialize `SurfaceView`.

   ```Kotlin
   private val nleEditor by lazy { NLEEditor() }
    
   private lateinit var nleMediaSession: NLEMediaSessionPublic
    
   private var hasPrepared = false
   ```
   

2. Initialize the NLESDK using the following sample code as reference:

   ```Kotlin
   private val nleListener = object : NLEEditorListener() {
       override fun onChanged() {
           nleMediaSession.dataSource = nleEditor.model
           if (!hasPrepared) {
               // After setting the model for the first time, you need to call prepare.
               nleMediaSession.playerApi.prepare()
               hasPrepared = true
           }
       }
   }
   private
    
   fun initNLEModel()
    {
         nleMediaSession = NLEMediaSessionPublic.create(NLEMediaConfig(), surfaceView, nleEditor)
         
   // Register the listener
   
         nleEditor.addConsumer(nleListener)
     }
      
     
   override
    
   fun onDestroy()
    {
         
   super
   .onDestroy()
          
         
   // Remove the listener when the Activity is destroyed.
   
         nleEditor.removeConsumer(nleListener)
     }
   ```
   

3. Retrieve the images or videos to be imported.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Bulk import of images or videos is supported.   </div>
   

4. Create an `NLEModel`.

5. Create an `NLETrack`.

6. Add a single video or image  **(addMainTrackSingleMedia):** 

   ```Kotlin
    val nleMainTrack: NLETrack = NLETrack().apply { mainTrack = true }
   
       nleMainTrack.extraTrackType = NLETrackType.VIDEO
   
       val rotationSize = mediaItem.getRotationSize()
   ```
   

7. Initialize the `MainTrack`.

   ```Kotlin
     private fun initMainTrack() {
         val mainTrackMediaList = mutableListOf<MediaItem>()
         intent.getParcelableArrayListExtra<MediaItem>(EditorConstant.EDITOR_MEDIA_PATH_LIST)?.let {
             mainTrackMediaList.addAll(it)
         }
         if (mainTrackMediaList.isEmpty()) {
             finish()
             return
         }
     
         if (mainTrackMediaList.size == 1) {
             videoHelper.addMainTrackSingleMedia(mainTrackMediaList.first())
         } else {
             videoHelper.addMainTrackMultiMedia(mainTrackMediaList)
         }
         nleMediaSession.playerApi.seekTime(0L, NLESeekFlag.EDITOR_SEEK_FLAG_LastSeek)
     }
   ```
   

8. Create one or multiple `NLETrackSlot`.

9. Add the `NLETrackSlot` to `NLETrack`.

   ```Kotlin
   nleMainTrack.addSlot(NLETrackSlot().also { slot ->
           slot.mainSegment = NLESegmentVideo().also { segment ->
               segment.avFile = NLEResourceAV().also { resource ->
                   resource.resourceType = if (mediaItem.isImage()) NLEResType.IMAGE else NLEResType.VIDEO
                   resource.duration = TimeUnit.MILLISECONDS.toMicros(mediaItem.getPlayDuration())
                   resource.resourceFile = mediaItem.path
                   resource.width = rotationSize.first.toLong()
                   resource.height = rotationSize.second.toLong()
               }
               segment.timeClipStart = 0
               segment.timeClipEnd = TimeUnit.MILLISECONDS.toMicros(mediaItem.getPlayDuration())
               segment.keepTone = true
           }
           slot.startTime = 0
           slot.endTime = slot.measuredEndTime
       })
   ```
   

10. Set the `CanvasRatio`for the `NLEModel`.


```Kotlin
 })
    nleEditor.model.run {
        //first:width second:height
        this.canvasRatio = rotationSize.first.toFloat() / rotationSize.second
        addTrack(nleMainTrack)
    }
```



11. Add the `NLETrack` to the `NLEModel`.

12. Add the following to your code: `nleEditor.commit()` and `nleEditor.done()`.


```Kotlin
nleEditor.commit()
nleEditor.done()
```


**Parameters**


|**Parameter Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|veLicensePath |String |Yes |"your_license_file.lic" |Name or path of the authentication file. |
|veAppKey |String |Yes |APP_KEY |Authentication key. |
|veToken |String |Yes |TOKEN |Authentication token . |


<span id="42e4e872"></span>
# Full sample code

This is the full sample code for importing using Android.

```Kotlin
private val nleEditor by lazy { NLEEditor() }

private lateinit var nleMediaSession: NLEMediaSessionPublic

private var hasPrepared = false

private val nleListener = object : NLEEditorListener() {
    override fun onChanged() {
        nleMediaSession.dataSource = nleEditor.model
        if (!hasPrepared) {
            // After setting the model for the first time, you need to call prepare.
            nleMediaSession.playerApi.prepare()
            hasPrepared = true
        }
    }
}

private fun initNLEModel() {
    nleMediaSession = NLEMediaSessionPublic.create(NLEMediaConfig(), surfaceView, nleEditor)
    // Register the listener
    nleEditor.addConsumer(nleListener)
}

override fun onDestroy() {
    super.onDestroy()
    
    // Remove the listener when the Activity is destroyed.
    nleEditor.removeConsumer(nleListener)
}

private fun initMainTrack() {
    val mainTrackMediaList = mutableListOf<MediaItem>()
    intent.getParcelableArrayListExtra<MediaItem>(EditorConstant.EDITOR_MEDIA_PATH_LIST)?.let {
        mainTrackMediaList.addAll(it)
    }
    if (mainTrackMediaList.isEmpty()) {
        finish()
        return
    }

    if (mainTrackMediaList.size == 1) {
        videoHelper.addMainTrackSingleMedia(mainTrackMediaList.first())
    } else {
        videoHelper.addMainTrackMultiMedia(mainTrackMediaList)
    }
    nleMediaSession.playerApi.seekTime(0L, NLESeekFlag.EDITOR_SEEK_FLAG_LastSeek)
}

// Add a single video or image
fun addMainTrackSingleMedia(mediaItem: MediaItem) {
    val nleMainTrack: NLETrack = NLETrack().apply { mainTrack = true }

    nleMainTrack.extraTrackType = NLETrackType.VIDEO

    val rotationSize = mediaItem.getRotationSize()

    nleMainTrack.addSlot(NLETrackSlot().also { slot ->
        slot.mainSegment = NLESegmentVideo().also { segment ->
            segment.avFile = NLEResourceAV().also { resource ->
                resource.resourceType = if (mediaItem.isImage()) NLEResType.IMAGE else NLEResType.VIDEO
                resource.duration = TimeUnit.MILLISECONDS.toMicros(mediaItem.getPlayDuration())
                resource.resourceFile = mediaItem.path
                resource.width = rotationSize.first.toLong()
                resource.height = rotationSize.second.toLong()
            }
            segment.timeClipStart = 0
            segment.timeClipEnd = TimeUnit.MILLISECONDS.toMicros(mediaItem.getPlayDuration())
            segment keepTone = true
        }
        slot.startTime = 0
        slot.endTime = slot.measuredEndTime
    })
    nleEditor.model.run {
        // First: width, Second: height
        this.canvasRatio = rotationSize.first.toFloat() / rotationSize.second
        addTrack(nleMainTrack)
    }
    nleEditor.commit()
    nleEditor.done()
}
```
