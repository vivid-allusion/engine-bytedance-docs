---
title: "Video editing module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-video-editing-module-in-ios"
---

For video clips, various editing operations are possible. This article provides some functions and their code samples. Some functions include adding, deleting, copying, splitting, changing speed, and controlling video playback. The video editing feature corresponds with the Video category within the demo project.

<span id="163fde8d"></span>
# Naming conventions

For easier reference, the following names are used to represent related objects:


|**Name** |**Referent Object** |
|---|---|
|nle |Refers to an `NLEInterface_OC` object. |
|modle |Refers to an `NLEModel` object. |
|track |Refers to an `NLETrack_OC` object. |
|slot |Refers to an `NLETrackSlot_OC` object. |


<span id="65072799"></span>
# Module description

The following table introduces classes related to the video editing module.


|**Class Name** |**Description** |
|---|---|
|NLEInterface_OC |The universal interface for NLE. |
|NLEModel |The core data module for NLE. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the video. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |
|NLEVideoAnimation_OC |Provides animation information for the video. |
|NLEResourceAV_OC |The resource module used to construct resources and record resource information. |
|NLESegmentVideo_OC |The video segment. It is linked to a specific resource and information about video segmentation. |
|NLESegmentVideoAnimation_OC |Provides detailed animation information for the video. |


<span id="93492b22"></span>
# Deleting a video segment

For instructions on how to delete a video segment, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="ece526d4"></span>
# Splitting a video segment

For instructions on how to split a video segment, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="0f7691f1"></span>
# Copying a video segment

For instructions on how to copy a video segment, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="eeffe730"></span>
# Adding a slot

For instructions on how to add a video segment, refer to "Importing in iOS".

If you want to import the slot into a specified location, refer to `addSlot` function of the `NLETrack_OC` class.

<span id="b84da91a"></span>
# Modifying the sequence of a slot

Before modifying the sequence of a slot, ensure that there are at least two slots.

**To modify the sequence of a slot**:


1. Delete a slot.

2. To import the slot into a specified location, call `track.addSlot(slot, at:index)`. `index` indicates that the subscript of `track.slots`, which starts from zero.

3. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
// get slot and the track that contains slot
let track: NLETrack_OC
let slot: NLETrackSlot_OC
let index: Int

track.removeSlot(slot)
track.addSlot(slot, at: index)

nle.editor.commitAndRender()
nle.editor.done()
```


<span id="9fa46a71"></span>
# Setting up speed changes

Before setting up speed changes, ensure that you have obtained the slot object. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To set up speed changes**:


1. To get videoSegment (class type:`NLESegmentVideo_OC`), use `slot.segment`.

2. To set up speed, call `videoSegment.setSpeed()`.

3. To configure tone changes, call `videoSegment.setKeepTone()`.

4. To modify ending time, call `slot.setEnd()`.

5. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
let slot: NLETrackSlot_OC
let videoSegment = slot.segment
let speed = Float
let shouldKeepTone: Bool

videoSegment.setSpeed(CGFloat(speed))
videoSegment.setKeepTone(shouldKeepTone)
slot.setEnd(CMTimeAdd(slot.startTime(), videoSegment.duration))
nle.editor.commitAndRender()
nle.editor.done()
```


<span id="9fa46a71"></span>
# Adding an animation

Before adding an animation to your video, ensure that you have obtained the address of your target slot and animation.

**To add an animation**:


1. Construct a resource object (class type: `NLEResourceAV_OC`) with the address that you have obtained.

2. Add the resource object to a segment object (class type: `NLESegmentVideoAnimation_OC`).

3. Add the segment object to an animation object (class type: `NLEVideoAnimation_OC`).

4. To add the animation to your video, call `slot.addVideoAnim()`.

5. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
let slot: NLETrackSlot_OC
let url: URL

let resource = NLEResourceNode_OC()
resource.resourceId = UUID().uuidString
resource.resourceFile = url.absoluteString
resource.resourceType = .animationVideo
resource.resourceName = url.deletingPathExtension().lastPathComponent

let segment = NLESegmentVideoAnimation_OC()
segment.animationDuration = CMTimeMakeWithSeconds(Double(duration), preferredTimescale: Int32(NSEC_PER_SEC))
segment.effectSDKVideoAnimation = resource

let animation = NLEVideoAnimation_OC()
animation.segmentVideoAnimation = segment
animation.setStart(CMTime.zero)

slot.addVideoAnim(animation)
nle.editor.commitAndRender()
nle.editor.done()
```


<span id="e7f763e2"></span>
# Deleting an animation

Before deleting an animation, ensure that you have obtained the address of your target slot. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To delete an animation**:


1. If you have not obtained an animation object (class type: `NLEVideoAnimation_OC`), use `slot.getVideoAnims()` to get the object by `animation.uuid`.

2. To delete an animation, call `slot.removeVideoAnim()`.

3. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
let slot: NLETrackSlot_OC
let animationID: String

let animation = slot.getVideoAnims().first {
    if let animation = $0 as? NLEVideoAnimation_OC {
        return animation.uuid == animationID
    } else {
        return false
    }
}
guard let animation = animation as? NLEVideoAnimation_OC else {
    return
}
slot.removeVideoAnim(animation)
nle.editor.commitAndRender()
nle.editor.done()
```


<span id="7b0cffea"></span>
# Playback control

This section introduces some functions related to playback control, including playback, pause and seek to a specified time.

<span id="7bc01ffb"></span>
## Playback

To realize the playback function, call `nle.play()`. For more information, refer to `NLEInterface.h`.

<span id="65c340b4"></span>
## Pause

To realize the pause function, call `nle.pause()`. For more information, refer to `NLEInterface.h`.

<span id="160c04c2"></span>
## Seek to a specified time

To realize this function, call `nle.seek(to:)` and input a `CMTime` object. For more information, refer to `NLEInterface.h`.

**Sample code**

```Swift
let seconds: Float64
nle.seek(to: CMTimeMakeWithSeconds(seconds, preferredTimescale: Int32(NSEC_PER_SEC)))
```


&nbsp;
