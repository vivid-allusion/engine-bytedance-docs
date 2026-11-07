---
title: "Transition module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-transition-module-in-ios"
---

The transition module offers a way to add animated transitions between two video clips or images in your video project. This feature enables smooth and engaging visual transitions between scenes, enhancing the overall quality and appeal of your video content. When using the transition function, you can add, delete, and modify transitions.

<span id="ab618be9"></span>
# Module description

The following table introduces data classes related to the transition module.


|**Class Name** |**Description** |
|---|---|
|NLEResourceAV_OC |The resource module used to construct resources and record resource information. |
|NLESegmentTransition_OC |The transition segment. It is linked to a specific `NLEResourceAV_OC` object. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific transition segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="2fab0629"></span>
# Adding a transition

Before adding a transition, ensure that you have had the path to your target transition.

**To add a transition**:


1. Construct an `NLEResourceAV_OC` object with the path that you have obtained.

2. Add `NLEResourceAV_OC` to `NLESegmentTransition_OC`.

3. Add `NLESegmentTransition_OC` to your target `NLETrackSlot_OC`.

4. To commit changes that you have made and render the transition effect, call `NLEInterface_OC.editor.commitAndRender()`.

5. To complete the addition process, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
    public func addTransition(with slotID: String, path: String, duration: Float64, isOverlap: Bool) -> String? {
        guard let url = URL(string: path), let slot = slot(with: slotID) else {
            return nil
        }
        
        let track = track(contains: slotID)
        guard let track = track else {
            return nil
        }
        if !track.isMainTrack {
            return nil
        }
        
        // 1. make NLEResourceAV_OC
        let resource = NLEResourceNode_OC()
        resource.resourceId = UUID().uuidString
        resource.resourceFile = url.absoluteString
        resource.resourceType = .transition
        resource.resourceName = url.deletingPathExtension().lastPathComponent
        resource.duration = CMTimeMake(value: Int64(duration * Float64(USEC_PER_SEC)), timescale: Int32(USEC_PER_SEC));

        // 2. add resource to segment
        let segmentTransition = NLESegmentTransition_OC()
        segmentTransition.overlap = isOverlap
        segmentTransition.transitionDuration = CMTimeMake(value: Int64(duration * Float64(USEC_PER_SEC)), timescale: Int32(USEC_PER_SEC));
        segmentTransition.effectSDKTransition = resource

        if let lastSlotId = track.slots.last?.uuid, lastSlotId == slotID {
            assertionFailure("Transition cannot be added to the last slot")
            return nil
        }
        
        let maxDuration = maxTransitionTimeForSlot(with: slotID)
        if duration > maxDuration {
            assertionFailure("The transition duration exceeds the maximum transition duration limit for the slot, which is \(maxDuration)s")
            return nil
        }
        
        // 3. set transition to slot
        slot.endTransition = segmentTransition
        
        // 4. sort slots
        track.timeSort()
        
        // 5. commit changes
        nle.editor.commitAndRender()
        nle.editor.done()
        
        return segmentTransition.uuid
    }
```


<span id="3de46493"></span>
# Deleting a transition

Before deleting a transition, ensure that you have had your target NLETrackSlot_OC.

**To delete a transition**:


1. Set up `NLETrackSlot_OC.endTransition` as `nil`.

2. To commit changes and render the effect, call `NLEInterface_OC.editor.commitAndRender()`.

3. To complete the deletion process, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
    public func removeTransition(with slotID: String) {
        guard let slot = slot(with: slotID) else {
            return
        }
        
        let track = track(contains: slotID)
        guard let track = track else {
            return
        }
        
        // 1. set nil
        slot.endTransition = nil

        // 2. sort slots
        track.timeSort()

        // 3. commit changes
        nle.editor.commitAndRender()
        nle.editor.done()
    }
```


<span id="42ef5bb7"></span>
# Modifying a transition


1. Delete your target transition. For instructions on how to delete a transition, refer to "Deleting a transition".

2. Add a new transition. For instructions on how to add a transition, refer to "Adding a transition".
