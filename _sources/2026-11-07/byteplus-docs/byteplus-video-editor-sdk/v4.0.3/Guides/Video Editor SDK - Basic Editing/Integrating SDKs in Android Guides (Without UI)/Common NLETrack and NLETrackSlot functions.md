---
title: "Common NLETrack and NLETrackSlot functions"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-common-nletrack-and-nletrackslot-functions"
---

This document explains the fundamental concepts and common operations related to `NLETrack` and `NLETrackSlot`, which are integral components in the NLE (Non\-Linear Editing) process. It provides a simplified overview of these components and their interactions within the context of video editing, including the use of extra flags and methods for finding tracks and slots.

An `NLETrack` is a track, and an `NLETrackSlot` is a segment within the track. During the editing process, `NLETrackSlot` is the primary object for operations.

<span id="07130998"></span>
# Naming conventions

For easier reference, the following names are used to represent related objects:


|**Term** |**Represents** |
|---|---|
|"model" |The NLEModel object |
|"track" |The NLETrack object |
|"slot" |The NLETrackSlot object |


**Setting Extra Flags for Track and Slot**

This allows you to associate custom key\-value pairs with both `NLETracks` and `NLETrackSlots`. These key\-value pairs, known as "extra" flags, provide a way to attach additional information or metadata to the tracks and slots for later retrieval or identification.

```Kotlin
track.setExtra("key", "value")
slot.setExtra("key", "value")
```


<span id="56b85891"></span>
## **Finding a Track**

This involves searching for a specific `NLETrack` within the `NLEModel`. You can use criteria such as ID or extra flags to identify the track you want to work with. Once found, you can perform various operations on that track.

```Kotlin
// You can search for the desired track for operations using criteria like ID, extra, etc.
val allTracks = nleEditor.model.tracks
allTracks.find { }
```


<span id="86e55488"></span>
## **Finding a Slot**

After locating the target track, you can further search for the specific slot you want to manipulate based on criteria like ID or extra flags within the track's collection of slots.

```Kotlin
// Once you have found the corresponding track,
// you can search for the desired slot for operations using criteria like ID or extra flags.
val slot = track.slots.find {  }
```
