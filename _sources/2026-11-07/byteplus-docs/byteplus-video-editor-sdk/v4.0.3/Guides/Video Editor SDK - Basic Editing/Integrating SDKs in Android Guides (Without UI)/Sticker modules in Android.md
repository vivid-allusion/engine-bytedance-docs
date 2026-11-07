---
title: "Sticker modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sticker-modules-in-android"
---

The Sticker module encompasses two primary types of stickers:


* **Information stickers**: implemented through the loading of encrypted materials (requiring a purchase).

* **Image stickers**: achieved by loading local images (in formats such as png, jpg, gif) as long as their size stays within 1.5MB.


The choice between these two sticker types is made by the business layer based on specific product requirements.

<span id="bb3bdd1f"></span>
# Module description

These are some common modules found in the sticker function.


|**Modules** |**Description** |
|---|---|
|NLETrack |Represents a track, with at least one track required in NLEModel (the main track) and the option for multiple sub\-tracks. \- Serves as a container for NLETrackSlots. Notably, NLETrackSlots on the same track cannot overlap in terms of time. \- On the main track, NLETrackSlots must be contiguous, while on non\-main tracks, they can be sparsely distributed. |
|NLETrackSlot |Denotes a track segment, akin to a time interval, and serves as a container for NLESegment and its derived classes. \- Each NLETrackSlot can accommodate only one NLESegment or one of its derived classes. |
|NLESegmentInfoSticker |A subclass of NLESegment, this class defines the content for information stickers. |
|NLESegmentImageSticker |Another subclass of NLESegment, this class defines the content for image stickers. |


<span id="6402174b"></span>
# Adding stickers

You can add two types of stickers: information stickers and image stickers.

<span id="ae6f5ab6"></span>
## Adding information stickers

In this scenario, we can add a sticker track and insert a segment for an information sticker into the track.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the sake of the sample code demonstration, we have included two sticker materials, but in your own business logic, you can choose to download them from the server.</div>


**To add information stickers:** 


1. Determine the video duration in microseconds.

   ```Kotlin
   /* Get the total playing duration, measured in microseconds (μs).
    * This total duration depends on which track currently has the longest duration.
    */
   val playDuration = nleMediaSession.playerApi.duration
   ```
   

2. Create a sticker track.

   ```Kotlin
   
   /**
    * For demonstration purposes, we will place the newly added stickers on a new track (and as long as two or more stickers do not overlap in time, they can be placed on the same track).
    */
   nleEditor.model.addTrack(NLETrack().apply {
       /**
        * Set whether this is the main track, with the default value being false.
        */
       mainTrack = false
   
       /**
        * Set the track type as a sticker.
        */
       extraTrackType = NLETrackType.STICKER
       addSlot(NLETrackSlot().apply {
           /**
            * The time at which the sticker starts playing, measured in microseconds (μs), is a required setting.
            */
           startTime = 0
   
           /**
            * The time at which the sticker ends playing, measured in microseconds (μs), is a required setting.
            */
           endTime = playDuration
           mainSegment = NLESegmentInfoSticker().apply {
               effectSDKFile = NLEResourceNode().apply {
                   // The path to the information sticker resource on the SD card.
                   resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/sticker.bundle/LateNightDiningRoomAlarmClock_7165698440739028994/LateNightDiningRoomAlarmClock_7165698440739028994"
   
                   // Set the resource type to INFO_STICKER.
                   resourceType = NLEResType.INFO_STICKER
               }
           }
           // Horizontal displacement of the sticker's center on the canvas, measured in float, with values ranging from -1f to 1f. 0f represents the center point on the canvas.
           transformX = 0f
           // Vertical displacement of the sticker's center on the canvas, measured in float, with values ranging from -1f to 1f. 0f represents the center point on the canvas.
           transformY = 0f
           // Rotation angle, measured in float, with clockwise being positive and counterclockwise being negative.
           rotation = 0f
           // Scaling factor, measured in float, with a default value of 1.0f.
           scale = 1.0f
           // Horizontal mirroring, measured in Boolean.
           mirror_X = false
           // Vertical mirroring, measured in Boolean.
           mirror_Y = false
       })
   })
   ```
   

3. Commit the data model changes.

   ```Kotlin
   /**
    * Submit the modified data model. This step is necessary; otherwise, you won't see the effects in the preview video.
    */
   nleEditor.commit()
   ```
   


<span id="cb9f4457"></span>
## Adding image stickers

In this context, you have the option to include an image sticker track.

**To add image stickers:** 


1. Prepare the image stickers. These stickers are stored in the `assets` directory of the provided sample code. During app startup, a copying process transfers them to your device's SD card.

2. Replace the sample code with the actual path of the stickers you want to add.

   ```Kotlin
   val
    playDuration = nleMediaSession.playerApi.duration
   ```
   

3. Add or create a new track for the added image stack and specify that it is not the main track (default is false).

   ```Kotlin
   nleEditor.model.addTrack(NLETrack().apply {
       mainTrack = false // Set as the main track, default is false
       extraTrackType = NLETrackType.STICKER // Set track type as sticker
       addSlot(NLETrackSlot().apply {
           startTime = 0 // Start time of the sticker, in microseconds (μs), must be set
           endTime = playDuration // End time of the sticker, in microseconds (μs), must be set
           mainSegment = NLESegmentImageSticker().apply {
               imageFile = NLEResourceNode().apply {
                   resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/image_sticker.bundle/SpiceGirlsChristmasEveTextSurroundChristmasTree_7165699130890485761.gif"
                   resourceType = NLEResType.IMAGE_STICKER
               }
           }
           // Horizontal displacement of the sticker's center on the canvas, as a float, ranging from -1f to 1f, with 0f representing the center on the canvas
           transformX = 0f
           // Vertical displacement of the sticker's center on the canvas, as a float, ranging from -1f to 1f, with 0f representing the center on the canvas
           transformY = 0f
           // Rotation angle, as a float, positive for clockwise, negative for counterclockwise
           rotation = 0f
           // Scaling factor, as a float, default value is 1.0f
           scale = 1.0f
           // Horizontal mirroring, as a Boolean
           mirror_X = false
           // Vertical mirroring, as a Boolean
           mirror_Y = false
       })
   })
   ```
   

4. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


<span id="a72552dc"></span>
# Deleting stickers

This section explains the process of removing sticker resources.

<span id="9c5e2942"></span>
## Deleting information stickers

You can delete information stickers by finding the corresponding segments for removal by traversing all segments (NLETrackSlot) in NLEModel. If multiple informational stickers were added previously, they will all be removed.

```Kotlin
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.STICKER }.forEach {
    it.sortedSlots.forEach { stickerSlot ->
        val infoStickerSegment = NLESegmentInfoSticker.dynamicCast(stickerSlot.mainSegment)
        if (infoStickerSegment?.effectSDKFile?.resourceType == NLEResType.INFO_STICKER) {
            it.removeSlot(stickerSlot)
        }
    }
    if (it.sortedSlots.size <= 0) {
        nleEditor.model.removeTrack(it)
    }
}
nleEditor.commit()
```


<span id="2ae06cdd"></span>
## Deleting image stickers

In this method, we'll show how to remove image stickers. Similar to the information sticker removal, for the demonstration of removing image sticker tracks, we won't distinguish specific tracks for image stickers, and all previously added image stickers will be removed. Our SDK's architecture is data\-driven, and all data is stored in NLEModel. When we want to delete an image sticker track, we can find the corresponding segments for removal by traversing all segments (NLETrackSlot) in NLEModel.

```Kotlin
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.STICKER }.forEach {
    it.sortedSlots.forEach { stickerSlot ->
        val imageStickerSegment = NLESegmentImageSticker.dynamicCast(stickerSlot.mainSegment)
        if (imageStickerSegment?.imageFile?.resourceType == NLEResType.IMAGE_STICKER) {
            it.removeSlot(stickerSlot)
        }
    }
    if (it.sortedSlots.size <= 0) {
        nleEditor.model.removeTrack(it)
    }
}
nleEditor.commit()
```


<span id="5ec9f90d"></span>
# Modifying stickers

We can modify added information and image stickers.

<span id="22f64319"></span>
## Modifying information stickers

In this method, we'll show how to change existing information stickers. To ensure that only specific parameters are modified and others remain unchanged, we need to use the `deepClone` method to create a new segment. This method does not delete the original track but removes the original segment. This is necessary because modifying only the segment data might not take effect on information stickers.

**To modify information stickers:** 


1. Filter the tracks within the `NLEModel` to find those of the `NLETrackType.STICKER`, which represents sticker tracks.

   ```Kotlin
   nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.STICKER }.forEach { 
   ```
   

2. For each sticker track that matches the filter criteria, iterate through its sorted slots.

   ```Kotlin
   it.sortedSlots.forEach { stickerSlot -> 
   ```
   

3. Check if the current sticker slot contains an information sticker `NLESegmentInfoSticker`.

   ```Kotlin
   val infoStickerSegment = NLESegmentInfoSticker.dynamicCast(stickerSlot.mainSegment)
   if (infoStickerSegment?.effectSDKFile?.resourceType == NLEResType.INFO_STICKER) {
   ```
   

4. Create a new sticker slot `NLETrackSlot` with the same properties as the original slot but with the modified content.

   ```Kotlin
   val
    newStickerSlot = NLETrackSlot.dynamicCast(stickerSlot.deepClone(
   true
   ))
   newStickerSlot.mainSegment = NLESegmentInfoSticker().apply {
       effectSDKFile = NLEResourceNode().apply {
           
   // Informational sticker resource path on SD card
   
           resourceFile = 
   "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/sticker.bundle/VlogDailylifelifehandwritingsimplepenwhite_7165698843190394881/VlogDailylifelifehandwritingsimplepenwhite_7165698843190394881"
   
           
   // Set the resource type to INFO_STICKER
   
           resourceType = NLEResType.INFO_STICKER
       }
   }
   ```
   

5. Remove the old sticker slot from the track and add the new sticker slot.

   ```Kotlin
   it.removeSlot(stickerSlot) 
   it.addSlot(newStickerSlot) 
   ```
   

6. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full code sample**

```Kotlin
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.STICKER }.forEach {
    it.sortedSlots.forEach { stickerSlot ->
        val imageStickerSegment = NLESegmentImageSticker.dynamicCast(stickerSlot.mainSegment)
        if (imageStickerSegment?.imageFile?.resourceType == NLEResType.IMAGE_STICKER) {
            // Create a new segment with modified content
            val newStickerSlot = NLETrackSlot.dynamicCast(stickerSlot.deepClone(true))
            newStickerSlot.mainSegment = NLESegmentImageSticker().apply {
                imageFile = NLEResourceNode().apply {
                    resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/image_sticker.bundle/AutumnVLOGTravelAirfare_7165698623212339201.gif"
                    resourceType = NLEResType.IMAGE_STICKER
                }
            }
            // Set additional transformation parameters
            newStickerSlot.apply {
                transformX = 0.5f
                transformY = 0.5f
            }
            // Remove the old segment first
            it.removeSlot(stickerSlot)
            // Add the new segment
            it.addSlot(newStickerSlot)
        }
    }
}
nleEditor.commit()
```


<span id="55855770"></span>
## Modifying image stickers

In this method, we'll show how to change existing image stickers. Similar to the information sticker modification, we use the `deepClone` method to create a new segment to avoid deleting the original track. This is necessary because modifying only the segment data might not take effect on image stickers.

**To modify image stickers:** 


1. Filter the tracks within the `NLEModel` to find those of the `NLETrackType.STICKER`, representing sticker tracks.

   ```Kotlin
   nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.STICKER }.forEach { 
   ```
   

2. For each sticker track that matches the filter criteria, iterate through its sorted slots.

   ```Kotlin
   it.sortedSlots.forEach { stickerSlot ->
   ```
   

3. Check if the current sticker slot contains an image sticker, `NLESegmentImageSticker`.

   ```Kotlin
   val imageStickerSegment = NLESegmentImageSticker.dynamicCast(stickerSlot.mainSegment)
   if (imageStickerSegment?.imageFile?.resourceType == NLEResType.IMAGE_STICKER) {
   ```
   

4. Create a new sticker slot containing the same properties as the original slot but with modified content.

   ```Kotlin
   val newStickerSlot = NLETrackSlot.dynamicCast(stickerSlot.deepClone(true))
   newStickerSlot.mainSegment = NLESegmentImageSticker().apply {
       imageFile = NLEResourceNode().apply {
           // Image sticker resource path on SD card
           resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/image_sticker.bundle/AutumnVLOGTravelAirfare_7165698623212339201.gif"
           // Set the resource type to IMAGE_STICKER
           resourceType = NLEResType.IMAGE_STICKER
       }
   }
   ```
   

5. If required, adjust the additional parameters for the new image sticker.

   ```Kotlin
   newStickerSlot.apply {
       transformX = 0.5f
       transformY = 0.5f
   }
   ```
   

6. Replace the old sticker slot from the track with the new sticker slot.

   ```Kotlin
   it.removeSlot(stickerSlot)
   it.addSlot(newStickerSlot)
   ```
   

7. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full sample code**

```Kotlin
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.STICKER }.forEach {
    it.sortedSlots.forEach { stickerSlot ->
        val imageStickerSegment = NLESegmentImageSticker.dynamicCast(stickerSlot.mainSegment)
        if (imageStickerSegment?.imageFile?.resourceType == NLEResType.IMAGE_STICKER) {
            // Create a new segment with modified content
            val newStickerSlot = NLETrackSlot.dynamicCast(stickerSlot.deepClone(true))
            newStickerSlot.mainSegment = NLESegmentImageSticker().apply {
                imageFile = NLEResourceNode().apply {
                    resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/image_sticker.bundle/AutumnVLOGTravelAirfare_7165698623212339201.gif"
                    resourceType = NLEResType.IMAGE_STICKER
                }
            }
            // Set additional transformation parameters
            newStickerSlot.apply {
                transformX = 0.5f
                transformY = 0.5f
            }
            // Remove the old segment first
            it.removeSlot(stickerSlot)
            // Add the new segment
            it.addSlot(newStickerSlot)
        }
    }
}
nleEditor.commit()
```
