---
title: "Canvas modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-canvas-modules-in-android"
---

Canvas, as the name implies, refers to the visual area for displaying and editing audio and video content. The SDK provides APIs that allow you to set this area and implement the following functionalities:


* **Set the canvas ratio**: You can set the canvas ratio to a common ratio such as 1:1, 16:9, 9:16, 3:4, and 4:3, or keep the ratio same as that of the imported video.

* **Set the canvas color**: You can set the custom color value.

* **Set the canvas background**: You can load a local image and set it as the background of the canvas.

* **Blur the canvas**: You can configure the blurriness setting of the canvas and blur the current video frame to display the background.


<span id="9ef9089c"></span>
# Module description

These are some common modules found in the canvas function.


|**Module** |**Description** |
|---|---|
|NLEModel |* A data class, which saves all the editing data of audio and video files. Normally, you can re\-play the whole video if you know what data this data class contains.<br><br>* At least one track is required in a NLEModel, which is the main track, NLETrack. |
|NLESegmentVideo |* The video content class, which contains the canvasStyle field. |
|NLESegmentImage |* The image content class, which contains the canvasStyle field. |
|NLEStyCanvas |* The content class of canvas parameters, which can be used to specify the canvas color, background image, and blur radius. |


<span id="d0ae2eab"></span>
# Setting multimedia canvas ratio

The parameter used for setting the canvas ratio is located in the `NLEModel` data structure. You can set the `NLEModel.canvasRatio` field to set the canvas ratio. This field is required. Otherwise, you cannot properly render the preview video.

**To set up the canvas ratio for multimedia:** 


1. Process a list of media items in`mediaList`.

   ```Kotlin
   fun addMainTrackMultiMedia(mediaList: List<MediaItem>) {
       // Additional code for processing media items...
   }
   ```
   

2. Set the canvas ratio based on the dimensions of the first media item.

   ```Kotlin
   nleEditor.model.run {
       // Calculate the canvas ratio based on the first media item's dimensions.
       this.canvasRatio = firstMediaRotationSize.first.toFloat() / firstMediaRotationSize.second
   }
   ```
   

3. Add the main track `nleMainTrack` to the NLE model.

   ```Kotlin
   addTrack(nleMainTrack)
   ```
   

4. Commit the changes.

   ```Kotlin
   nleEditor.commit()
   ```
   


**Full code sample**

```Kotlin
fun addMainTrackMultiMedia(mediaList: List<MediaItem>) {
    ......
    nleEditor.model.run {
        //first:width second:height
        this.canvasRatio = firstMediaRotationSize.first.toFloat() / firstMediaRotationSize.second
        addTrack(nleMainTrack)
    }
    nleEditor.commit()
    ......
}
```


<span id="c6873cf9"></span>
# Setting single media canvas ratio

The parameter used for setting the single media canvas ratio is located in the `NLEModel` data structure. You can set the `NLEModel.canvasRatio` field to set the canvas ratio. This field is required. Otherwise, you cannot properly render the preview video.

**To set up the canvas ratio for single media:** 


1. Process a list of media items in`mediaList`.

   ```Kotlin
   fun addMainTrackSingleMedia(mediaItem: MediaItem) {
       // Additional code for processing the single media item...
   }
   ```
   

2. Set the canvas ratio based on the dimensions of the first media item.

   ```Kotlin
   nleEditor.model.run {
       // Calculate the canvas ratio based on the dimensions of the single media item.
       this.canvasRatio = rotationSize.first.toFloat() / rotationSize.second
   }
   ```
   

3. Add the main track `nleMainTrack` to the NLE model.

   ```Kotlin
   addTrack(nleMainTrack)
   ```
   

4. Commit the changes.

   ```Kotlin
   nleEditor.commit()
   ```
   


**Full code sample**

```Kotlin
fun addMainTrackSingleMedia(mediaItem: MediaItem) {
    ......
    nleEditor.model.run {
        //first:width second:height
        this.canvasRatio = rotationSize.first.toFloat() / rotationSize.second
        addTrack(nleMainTrack)
    }
    nleEditor.commit()
    ......
}
```


<span id="a6ffa8c7"></span>
# Setting canvas color

Unlike the canvas ratio, which affects the entire video, settings for canvas color, canvas background, and canvas blurriness apply to specific video clips or image segments. These settings are governed by the `canvasStyle` field within `NLESegmentVideo`/`NLESegmentImage`, where the type is `NLEStyCanvas`, providing comprehensive details about the canvas. To make adjustments to canvas color, background image, and canvas blurriness, you'll need to make modifications within the `NLEStyCanvas` class.

**To set canvas color:** 


1. Obtain the content class of the first video clip.

   ```Kotlin
   val
    firstSegment = nleEditor.model.mainTrack.sortedSlots.firstOrNull()?.mainSegment?.let {
       NLESegmentVideo.dynamicCast(it)
   }
   ```
   

2. Set the `canvasStyle` property to a new `NLEStyCanvas`.

   ```Kotlin
   firstSegment?.canvasStyle = NLEStyCanvas().apply {
   ```
   

3. Specify setting the canvas color.

   ```Kotlin
       type = NLECanvasType.COLOR
   ```
   

4. Define the color using the hexadecimal representation.

   ```Kotlin
       color = Color.parseColor(
   "#FFE36E55"
   ).toLong()
   ```
   

5. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full code sample**

```Kotlin
// Step 1: Obtain the content class of the first video clip.
val firstSegment = nleEditor.model.mainTrack.sortedSlots.firstOrNull()?.mainSegment?.let {
    NLESegmentVideo.dynamicCast(it)
}

// Step 2: Set the canvasStyle property for the firstSegment to a new NLEStyCanvas instance.
firstSegment?.canvasStyle = NLEStyCanvas().apply {
    // Step 3: Specify that you are setting the canvas color.
    type = NLECanvasType.COLOR

    // Step 4: Define the desired color using its hexadecimal representation.
    color = Color.parseColor("#FFE36E55").toLong()
}

// Step 5: Submit the modified data model to view the effect in the preview video.
nleEditor.commit()
```


<span id="f5b50f33"></span>
# Setting canvas background

These steps guide you through the process of setting the canvas background with an image for a specific video clip or image segment in your project using Kotlin code examples.

**To set canvas background:** 


1. Obtain the content class of the first video clip.

   ```Kotlin
   val firstSegment = nleEditor.model.mainTrack.sortedSlots.firstOrNull()?.mainSegment?.let {
       NLESegmentVideo.dynamicCast(it)
   }
   ```
   

2. Fill in the canvas background with an image:

   ```Kotlin
   firstSegment?.canvasStyle = NLEStyCanvas().apply {
       
   // Specify that you are setting the canvas background with an image.
   
       type = NLECanvasType.IMAGE
   ```
   

3. Define the image resource to be used for the canvas background.

   ```Kotlin
       image = NLEResourceNode().apply {
   ```
   

4. Set the resource type to IMAGE.

   ```Kotlin
           resourceType = NLEResType.IMAGE
   ```
   

5. Provide the file path to the image resource on your device.

   ```Kotlin
           resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/canvas.bundle/canvasCover.png"
   ```
   

6. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full code sample**

```Kotlin
// Step 1: Obtain the content class of the first video clip.
val firstSegment = nleEditor.model.mainTrack.sortedSlots.firstOrNull()?.mainSegment?.let {
    NLESegmentVideo.dynamicCast(it)
}

// Step 2: Set the canvasStyle property for the firstSegment to a new NLEStyCanvas instance.
firstSegment?.canvasStyle = NLEStyCanvas().apply {
    // Step 3: Specify that you are setting the canvas color.
    type = NLECanvasType.COLOR

    // Step 4: Define the desired color using its hexadecimal representation.
    color = Color.parseColor("#FFE36E55").toLong()
}

// Step 5: Submit the modified data model to view the effect in the preview video.
nleEditor.commit()
```


<span id="db975532"></span>
# Blurring the canvas

Discover the process of applying a blur effect to the canvas in your video or image content. This concise guide outlines the steps to obtain the content class, set the canvas blurriness, and commit the changes, allowing you to achieve the desired blurring effect in your project.

**To blur the canvas:** 


1. Obtain the content class of the first video clip.

   ```Kotlin
   val firstSegment = nleEditor.model.mainTrack.sortedSlots.firstOrNull()?.mainSegment?.let {
       NLESegmentVideo.dynamicCast(it)
   }
   ```
   

2. Indicate that the image shown on the canvas is the video frame.

   ```Kotlin
   firstSegment?.canvasStyle = NLEStyCanvas().apply {
       // Indicate that the image shown on the canvas is the video frame.
       type = NLECanvasType.VIDEO_FRAME
   ```
   

3. Adjust the blur radius.

   ```Kotlin
       blurRadius = 14f * 0.75f // Adjust the blur radius as needed
   }
   ```
   

4. Commit the changes.

   ```Kotlin
   nleEditor.commit() 
   ```
   


**Full code sample**

```Kotlin
/**
 * The canvas parameter applies to the video or image content class. Therefore, before blurring the canvas, we must first get the video clip or image segment to be adjusted.
 * For demonstration, in this method, we only blur the first video clip or image segment in the main track.
 */

/**
 * Obtain the content class of the first video clip.
 */
val firstSegment = nleEditor.model.mainTrack.sortedSlots.firstOrNull()?.mainSegment?.let {
    NLESegmentVideo.dynamicCast(it)
}

/**
 * The canvas is blurred by setting the blur radius.
 */
firstSegment?.canvasStyle = NLEStyCanvas().apply {
    // Indicate that the image shown on the canvas is the video frame.
    type = NLECanvasType.VIDEO_FRAME
    blurRadius = 14f * 0.75f
}

/**
 * Submit the modified data model. This step must be performed. Otherwise, you cannot view the effect in the preview video.
 */
nleEditor.commit()
```


<span id="4fe89d3a"></span>
# FAQs


1. **How can I set the canvas ratio to a fixed value like 16:9 instead of the original media size?** 

   Setting the canvas ratio to a fixed value, such as 16:9, is straightforward. You need to specify a float parameter. Keep in mind that this parameter represents the ratio of width to height, which is calculated by dividing the width by height. By setting this parameter to the desired fixed ratio, like 16:9, you can achieve the desired canvas aspect ratio.

   ```Kotlin
   // Set the canvas ratio to 16:9.
   nleEditor.model.canvasRatio = 16f / 9f
   // Set the canvas ratio to 1:1.
   nleEditor.model.canvasRatio = 1f
   ```
   

2. **How can I set the same canvas color for the entire edited video if I have multiple video clips or image segments?** 

   When working with multiple video clips or image segments in your edited video and you want to apply the same canvas color to all of them, you can achieve this by traversing and modifying each segment in the NLEModel. Below is an example of how to set the same canvas parameter for all video clips in the main track:

   ```Kotlin
   nleEditor.model.mainTrack.sortedSlots.forEach {
       NLESegmentVideo.dynamicCast(it.mainSegment)?.canvasStyle = NLEStyCanvas().apply {
           // type =
           // color =
           // image = 
           // blurRadius = 
       }
   }
   
   /**
    * Submit the modified data model. This step must be performed. Otherwise, you cannot view the effect in the preview video.
    */
   nleEditor.commit()
   ```
