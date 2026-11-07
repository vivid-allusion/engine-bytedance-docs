---
title: "Importing in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-importing-in-ios"
---

This article introduces how to import videos and images to your editing environment through the import feature of BytePlus Video Eidtor SDK. The import feature corresponds with the Import category within the demo project. For more information, refer to the ImportHelper within the demo project.

<span id="e1a9abd3"></span>
# Prerequisite

Before importing videos and images, ensure that you have obtained the address of your target video or image.

<span id="291ddb87"></span>
# Module description

The following table introduces classes related to the import feature of VE SDK.


|**Class Name** |**Description** |
|---|---|
|NLEResourceAV_OC |The resource module used to construct resources and record resource information. |
|NLESegmentVideo_OC |The video segment. It is linked to a specific resource and information about video segmentation. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="90f89b44"></span>
# Procedure


1. Construct an `NLEResourceAV_OC` object.

   ```Swift
   // 1. make NLEResourceAV_OC
   let res // NLEResourceAV_OC
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The way to construct an NLEResourceAV_OC object for a video or picture is different. For detailed information, refer to <code>ImportHelper.videoResource(with:)</code> and <code>ImportHelper.videoResource(with:)</code>.   </div>
   

2. Add the `NLEResourceAV_OC` object to an `NLESegmentVideo_OC` object.

   ```Swift
   // 2. add resource to segment
   let duration = res.duration
   let segment = NLESegmentVideo_OC()
   segment.videoFile = res
   segment.setTimeClipStart(CMTimeMakeWithSeconds(0, preferredTimescale: Int32(NSEC_PER_SEC)))
   segment.setTimeClipEnd(duration)
   if res.resourceType == .video {
       segment.setVolume(1)
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to import a video, include <code>segment.setVolume(1)</code> in your code.   </div>
   

3. Add the `NLESegmentVideo_OC` object to an `NLETrackSlot_OC` object.

   ```Swift
   // 3. add segment to slot
   let slot = NLETrackSlot_OC()
   slot.setSegmentVideo(segment)
   slot.setStart(CMTimeMakeWithSeconds(startTime, preferredTimescale: Int32(NSEC_PER_SEC)))
   slot.layer = 0
   ```
   

4. Add the `NLETrackSlot_OC` object to an `NLETrack_OC` object.

   ```Swift
   // 4. add slot to main track
   let track = NLETrack_OC()
   track.layer = 0
   track.isMainTrack = true
   track.addSlot(slot)
   startTime += CMTimeGetSeconds(duration)
   ```
   

5. Call `NLEInterface_OC.editor.commit` to commit the changes.

   ```Swift
   nle.editor.commit()
   ```
   

   If you want to instantly view the changes that you have made, execute the following command on your terminal.

   ```Swift
   nle.editor.commitAndRender()
   ```
   


**Full sample code**

```Swift
// 1. make NLEResourceAV_OC
let res // NLEResourceAV_OC

// 2. add resource to segment
let duration = res.duration
let segment = NLESegmentVideo_OC()
segment.videoFile = res
segment.setTimeClipStart(CMTimeMakeWithSeconds(0, preferredTimescale: Int32(NSEC_PER_SEC)))
segment.setTimeClipEnd(duration)
if res.resourceType == .video {
    segment.setVolume(1)
}

// 3. add segment to slot
let slot = NLETrackSlot_OC()
slot.setSegmentVideo(segment)
slot.setStart(CMTimeMakeWithSeconds(startTime, preferredTimescale: Int32(NSEC_PER_SEC)))
slot.layer = 0

// 4. add slot to main track
let track = NLETrack_OC()
track.layer = 0
track.isMainTrack = true
track.addSlot(slot)
startTime += CMTimeGetSeconds(duration)

// 5. add track
nle.editor.model.addTrack(track)

// 6. commit changes
nle.editor.commit()
```


&nbsp;
