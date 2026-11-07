---
title: "Transition modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-transition-modules-in-android"
---

The transition module offers a way to add animated transitions between two video clips or images in your video project. This feature enables smooth and engaging visual transitions between scenes, enhancing the overall quality and appeal of your video content.

<span id="679f500c"></span>
# Module description

These are some modules in Transition.


|**Module** |**Description** |
|---|---|
|NLETrack |* A track. An NLEModel contains at least one track (the main track) and can contain multiple sub\-tracks.<br><br>* Tracks are containers for NLETrackSlot. The NLETrackSlots in a track cannot overlap with each other in time.<br><br>* The NLETrackSlots in the main track **must be linked end\-to\-end (except for overlapping transitions)** . The NLETrackSlots in a track other than the main track can be sparse. |
|NLETrackSlot |* A track slot, which can be regarded as a time slot. NLETrackSlots are containers for NLESegments and their derived classes.<br><br>* Each NLETrackSlot can contain only one NLESegment and its derived class. |
|NLESegmentTransition |* The derived class of NLESegment, which describes the information about an animated transition, such as the duration, the resource path of the transition effect, and whether it can be applied to two video clips (isOverLap). |


<span id="57c3c104"></span>
## NLESegmentTransition core API

```Kotlin
public class NLESegmentTransition extends NLESegment {
   //  Indicate whether the transition needs to run from one slot to another.
   // If the transition needs to run from one slot to another for overlapping, the start time of the clips after that clip will be moved forward.
   // If the transition does not need to run from one slot to another, the timeline is not affected.
   public void setOverlap(boolean value) 
   // Set the duration.
   public void setTransitionDuration(long value) 
   // Set the resource for transition.
   public void setEffectSDKTransition(NLEResourceNode object) 
}
```


Generally, transitions are added at the end of a video, which means that you need to set `endTransition` in `NLETrackSlot`.

<span id="d1fd37d2"></span>
# Adding transitions

<span id="db1f6a15"></span>
# ```Kotlin

val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return

val slotSize = firstTrack.slots.size

if (slotSize < 2) {

Toast.makeText(context, "The size of the slot needs to be greater than 1", Toast.LENGTH_SHORT).show()

}

val preTransitionSlot = firstTrack.slots[0]

// The position where the transition is applied on the timeline.

val defaultTransactionDuration = TimeUnit.MILLISECONDS.toMicros(1000)

// The path to the resource used for making a transition.

val resourcePath = File(context.getExternalFilesDir("assets"), "resource/transitions.bundle/fanguang_6945244032276676638").absolutePath

// Indicate whether the transition overlaps. If yes, the start time of the clips after this clip will be moved forward. Otherwise, the timeline is not affected.

val isOverLap = true

val transitionSegment = NLESegmentTransition().also { transition \-\>

```Plain Text
transition.transitionDuration = defaultTransactionDuration
transition.effectSDKTransition = NLEResourceNode().apply {
    resourceFile = resourcePath
    resourceType = NLEResType.TRANSITION
}
transition.overlap = isOverLap
```


}

preTransitionSlot.endTransition = transitionSegment

firstTrack.timeSort()

nleEditor.commit()

```Plain Text

<span id="4e873c44"></span>
# Deleting transitions
```Kotlin
val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return
val slotSize = firstTrack.slots.size
if (slotSize < 2) {
    Toast.makeText(context, "The size of the slot needs to be greater than 1", Toast.LENGTH_SHORT).show()
}

val defaultTransactionDuration = TimeUnit.MILLISECONDS.toMicros(1000)
val isOverLap = true

val preTransitionSlot = firstTrack.slots[0]

preTransitionSlot.endTransition = null

firstTrack.timeSort()

nleEditor.commit()
```


<span id="1e435204"></span>
# Changing transitions

```Kotlin
val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return
val slotSize = firstTrack.slots.size
if (slotSize < 2) {
    Toast.makeText(context, "The size of the slot needs to be greater than 1", Toast.LENGTH_SHORT).show()
}

val defaultTransactionDuration = TimeUnit.MILLISECONDS.toMicros(1000)
// The path to the resource used for making the transition.
val resourcePath = File(context.getExternalFilesDir("assets"), "resource/transitions.bundle/nishizhenxuanzhuan_6945244051956383758").absolutePath
val isOverLap = true

val preTransitionSlot = firstTrack.slots[0]

// Modify the endTransition property.
preTransitionSlot.endTransition?.apply {
    transitionDuration = defaultTransactionDuration
    effectSDKTransition = NLEResourceNode().apply {
        resourceFile = resourcePath
        resourceType = NLEResType.TRANSITION
    }
    overlap = isOverLap
}

firstTrack.timeSort()

nleEditor.commit()
```
