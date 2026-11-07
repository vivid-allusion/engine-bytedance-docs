---
title: "Common NLETrack and NLETrackSlot operations—iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-common-nletrack-and-nletrackslot-operations-ios"
---

This article provides a summary of common operations related to `NLETrack` and `NLETrackSlot`.

An `NLETrack` is a track and an `NLETrackSlot` is a segment within the track. During the editing process, `NLETrackSlot` is the primary object for operations.

<span id="09df2e76"></span>
# Naming conventions

For easier reference, the following names are used to represent related objects:


|**Name** |**Referent Object** |
|---|---|
|nle |Refers to an `NLEInterface_OC` object. |
|modle |Refers to an `NLEModel` object. |
|track |Refers to an `NLETrack_OC` object. |
|slot |Refers to an `NLETrackSlot_OC` object. |


<span id="d72ee40e"></span>
# Module description

The following table introduces classes related to common NLETrack and NLETrackSlot operations.


|**Class Name** |**Description** |
|---|---|
|NLEInterface_OC |The universal interface for NLE. |
|NLEModel |The core data module for NLE. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="c5276555"></span>
# Common operations

This section introduces a summary of common operations related to `NLETrack` and `NLETrackSlot`.

<span id="b06c79a8"></span>
## Getting a slot by slot.uuid

This section introduces how to get a slot by slot.uuid.

**To get a slot by slot.uuid**:


1. To get each track of a video, use `model.getTracks()`.

2. To get each slot of the track, use `track.slots`.

3. To find your target slot, compare the `slot.uuid` of each slot returned by the `track.slots`function.


**Sample code**

```Swift
public func slot(with id: String) -> NLETrackSlot_OC? {
    var slot: NLETrackSlot_OC?
    nle.editor.model.getTracks().forEach { track in
        slot = track.slots.first {
            $0.uuid == id
        }
    }
    return slot
}
```


<span id="87865f14"></span>
## Finding a track that contains a specified slot

This section introduces how to find a track that contains a specified slot.

**To find a track that contains a specified slot**:


1. To acquire each track of a video, use `model.getTracks()`.

2. If the return value of `track.slots` is not null, then it indicates you have found the track that contains your target slot.


**Sample code**

```Swift
public func track(contains slotID: String) -> NLETrack_OC? {
    return nle.editor.model.getTracks().first { track in
        track.slots.contains { $0.uuid == slotID }
    }
}
```


<span id="aeedcd79"></span>
## Deleting a slot

Before deleting a slot, ensure you have obtained the slot object.

**To delete a slot**:


1. Follow the instructions as described in "Finding a track that contains a specified slot" to get a track that contains your target slot.

2. To delete the slot, call `track.removeSlot()`.

3. If the return value of `track.slots` is null, call `model.removeTrack()` to delete the track.

4. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
// get slot and the track that contains slot
let track: NLETrack_OC
let slot: NLETrackSlot_OC

track.removeSlot(slot)

if track.slots.isEmpty {
    nle.editor.model.removeTrack(track)
}

nle.editor.commit()
nle.editor.done()
```


<span id="be8fb85b"></span>
## Spliting a slot

This section introduces how to split a slot.

**To split a slot**:


1. Follow the instructions as described in "Finding a track that contains a specified slot" to get a track that contains your target slot.

2. To get a split slot, call `track.split(fromTime:)`.

3. To commit changes that you have made, call `nle.editor.commit()`.


**Sample code**

```Swift
let track: NLETrack_OC
let time: TimeInterval

let newSlot = track.split(fromTime: time)
nle.editor.commit()
nle.editor.done()
```


<span id="348c1369"></span>
## Coppying a slot

This section introduces how to copy a slot.

**To copy a slot**:


1. Follow the instructions as described in "Finding a track that contains a specified slot" to get a track that contains your target slot.

2. To get a new slot, call `slot.deepClone(true)`.

3. To insert the new slot into the location behind the original slot, call `track.addslot(newSlot, afterSlot: slot)`. If you don't want to insert the new slot into the location behind the original slot, refer to `NLETrack_OC` for more operations that you can take.


**Sample code**

```Swift
// get slot and the track that contains slot
let track: NLETrack_OC
let slot: NLETrackSlot_OC

let newSlot = slot.deepClone(true)
track.addSlot(newSlot, afterSlot: slot)

nle.editor.commit()
nle.editor.done()
```


For more information about the sample code, refer to `CommonHelping` within the demo project.

&nbsp;
