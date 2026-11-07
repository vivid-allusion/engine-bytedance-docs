---
title: "Sticker module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sticker-module-in-ios"
---

Sticker module is used to add various sticker elements to videos or images to enhance visual effects and convey intent. When using the sticker function, you can add, delete, and modify sticker elements.

The Sticker module encompasses two primary types of stickers: **Information stickers and Image stickers**. Differences between these two types of stickers are as follows:


* **Different content classes linked to** **`NLETrackSlot_OC`**: Information stickers are implemented through adding `NLESegmentInfoSticker_OC` to `NLETrackSlot_OC` while image stickers are achieved through adding `NLESegmentImageSticker_OC` to `NLETrackSlot_OC`.

* **Different properties**: As displayed in the following code, `NLESegmentInfoSticker_OC` and `NLESegmentImageSticker_OC` are both subclasses of `NLESegmentSticker_OC`. However, `NLESegmentImageSticker_OC` has a `crop` property (class type: `NLEStyCrop_OC`), which enables the image stickers to configure clipping information.

   **Sample code for information stickers**

   ```Kotlin
   @interface NLESegmentInfoSticker_OC : NLESegmentSticker_OC
   @property (nonatomic, strong) NLEResourceNode_OC *effectSDKFile;
   @property (nonatomic, assign) BOOL addWithBuffer;
   - (NLEResourceNode_OC *)getResNode;
   @end
   ```
   

   **Sample code for image stickers**

   ```Kotlin
   @interface NLESegmentImageSticker_OC : NLESegmentSticker_OC
   @property (nonatomic, strong) NLEStyCrop_OC *crop;
   @property (nonatomic, strong) NLEResourceNode_OC *imageFile;
   - (NLEResourceNode_OC *)getResNode;
   @end
   ```
   


In most cases,`NLESegmentInfoSticker_OC` and `NLESegmentImageSticker_OC` can be used together in a track as long as their times do not overlap.

<span id="fe315123"></span>
# Module description

The following table introduces data classes related to the sticker module.


|**Class Name** |**Description** |
|---|---|
|NLEResourceNode_OC |The resource module used to construct resources and record resource information. |
|NLESegmentInfoSticker_OC |The sticker segment. It is linked to a specific sticker. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific sticker segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="d36031c1"></span>
# Adding an information sticker

Before adding an information sticker, ensure that you have obtained the path to your target information sticker.

**To add an information sticker**:


1. Construct an `NLEResourceNode_OC` object with the path that you have obtained.

2. Add `NLEResourceNode_OC` to `NLESegmentInfoSticker_OC`.

3. Add `NLESegmentInfoSticker_OC` to `NLETrackSlot_OC`.

4. Add `NLETrackSlot_OC` to `NLETrack_OC`.

5. To commit changes that you have made and render sticker effect, call `NLEInterface_OC.editor.commitAndRender()`.

6. To complete the process of adding an information sticker, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
// 1. Get sticker path
let path 

// 2. make NLEResourceNode_OC
let url = URL(fileURLWithPath: path)
let name = url.deletingPathExtension().lastPathComponent
let resource = NLEResourceNode_OC()
resource.resourceId = UUID().uuidString
resource.resourceFile = url.absoluteString
resource.resourceTag = .amazing
resource.resourceType = .sticker
resource.resourceName = name

// 3. add resource to segment
let segment = NLESegmentInfoSticker_OC()
segment.effectSDKFile = resource

// 4. add segment to slot
let slot = NLETrackSlot_OC()
slot.segment = segment
slot.setStart(CMTime.zero)
slot.layer = 0
slot.setEnd(CMTime(seconds: 3, preferredTimescale: Int32(NSEC_PER_SEC)))
slot.setScale(1)
slot.setRotation(0)
let point = CGPoint(x: 0.75, y: 0.33)
slot.setTransformX(Float(point.x))
slot.setTransformY(Float(point.y))

// 5. add slot to track
let track = NLETrack_OC()
track.layer = 0
track.extraTrackType = .STICKER
track.addSlot(slot)
nle.editor.model.addTrack(track)

// 6. commit change
nle.editor.commitAndRender()

// 7. add completed
nle.editor.done()
```


<span id="4b6d7615"></span>
# Adding an image sticker

Before adding an image sticker, ensure that you have obtained the path to your target image sticker.

**To add an image sticker**:


1. Construct an `NLEResourceNode_OC` object with the path that you have obtained.

2. Add `NLEResourceNode_OC` to `NLESegmentImageSticker_OC`.

3. Add `NLESegmentImageSticker_OC` to `NLETrackSlot_OC`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For image stickers, set up <code>NLETrackSlot_OC.scale</code> with a small number, such as 0.4.</div>



4. Add `NLETrackSlot_OC` to `NLETrack_OC`.

5. To commit changes that you have made and render sticker effect, call `NLEInterface_OC.editor.commitAndRender()`.

6. To complete the process of adding an image sticker, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
// 1. Get sticker path
let path 

// 2. make NLEResourceNode_OC
let url = URL(fileURLWithPath: path)
let name = url.deletingPathExtension().lastPathComponent
let resource = NLEResourceNode_OC()
resource.resourceId = UUID().uuidString
resource.resourceFile = url.absoluteString
resource.resourceTag = .amazing
resource.resourceType = .sticker
resource.resourceName = name

// 3. add resource to segment
let segment = NLESegmentImageSticker_OC()
segment.imageFile = resource

// 4. add segment to slot
let slot = NLETrackSlot_OC()
slot.segment = segment
slot.setStart(CMTime.zero)
slot.layer = 0
slot.setEnd(CMTime(seconds: 3, preferredTimescale: Int32(NSEC_PER_SEC)))
// The scale of the image sticker should be smaller by default.
slot.setScale(0.4)
slot.setRotation(0)
let point = CGPoint(x: 0.75, y: 0.33)
slot.setTransformX(Float(point.x))
slot.setTransformY(Float(point.y))

// 5. add slot to track
let track = NLETrack_OC()
track.layer = 0
track.extraTrackType = .STICKER
track.addSlot(slot)
nle.editor.model.addTrack(track)

// 6. commit change
nle.editor.commitAndRender()

// 7. add completed
nle.editor.done()
```


<span id="6fd8968b"></span>
# Deleting a sticker

For instructions on how to delete a sticker, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="776e22e5"></span>
# Substituting a sticker

Before substituting a sticker, ensure that you have obtained the path to a new sticker.

**To substitute a sticker**:


1. Delete the original sticker by slotID. For instructions on how to delete a sticker, refer to "Common NLETrack and NLETrackSlot operations—iOS".

2. Add a new sticker using the path that you have obtained. For instructions on how to add a sticker, refer to "Common NLETrack and NLETrackSlot operations—iOS".


&nbsp;
