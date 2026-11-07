---
title: "Video editing modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-video-editing-modules-in-android"
---

For video clips, various editing operations are possible. This topic provides some functions and their code samples.

Some functions include adding, deleting, copying, splitting, changing speed, and controlling video playback.

<span id="4250a949"></span>
# Add a Video Segment

This module explains how to add a video segment to the timeline. It retrieves the necessary information from the `MediaItem` and adds it to the track. After making changes, it's important to commit them, and video playback is paused during this process.


* `MediaItem`: An image or video material loaded from local storage, including the material's path, dimensions, type, and other information.


```Kotlin
val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return
val mediaItem = it.firstOrNull() ?: return
val rotationSize = mediaItem.getRotationSize()

firstTrack.addSlot(NLETrackSlot().also { slot ->
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
    slot.startTime = firstTrack.endTime
    slot.endTime = slot.startTime + TimeUnit.MILLISECONDS.toMicros(mediaItem.getPlayDuration())
})

nleEditor.commit()
nleMediaSession.playerApi.pause()
```


<span id="8700e872"></span>
# Copy a Video Segment

This module explains how to copy a video segment and add it after an anchor slot on the timeline. It ensures the new slot is a copy of the original one.

The core method `firstTrack.addSlotAfterSlot(newSlot, anchorSlot)` is used to add a video slot (segment) after an existing slot (anchorSlot) within a video track. This operation allows you to insert a new video segment at a specific position in the track, following an existing segment. It's a key function in video editing, enabling you to place new content within the timeline relative to the existing content.

```Kotlin
val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return
val firstSlot = firstTrack.slots.firstOrNull() ?: return

val anchorSlot = firstTrack.slots.lastOrNull() ?: return

val newSlot = NLETrackSlot.dynamicCast(firstSlot.deepClone(true)).apply {
    this.startTime = firstTrack.endTime
    this.endTime = this.startTime + firstTrack.duration
    audioFilter?.let { filter ->
        filter.startTime = this.startTime
        filter.endTime = this.endTime
    }
}
if (firstTrack.mainTrack) {
    firstTrack.addSlotAfterSlot(newSlot, anchorSlot)
}

nleEditor.commit()
```


<span id="76b2836c"></span>
# Remove a Video Segment

This module explains how to remove a video segment from the timeline.

The core method `firstTrack.removeSlot(slot)` is used to remove a slot from a video track. This operation eliminates the specified slot from the track, effectively removing the associated video segment from the timeline. This method is a fundamental part of video editing, allowing you to delete specific segments from your project.

```Kotlin
val willRemoveSlot = firstTrack.slots.firstOrNull() ?: return
firstTrack.removeSlot(willRemoveSlot)
firstTrack.timeSort()

nleEditor.commit()
```


<span id="10c13a7c"></span>
# Split a Video Segment

This module explains how to split a video segment at a specific position on the timeline.

The core method `firstTrack.splitInSpecificSlot(curPosition, slot)` is used to split a video track into two segments at a specific position (curPosition) within an existing slot (segment). This operation allows you to divide a video segment at a particular point in the timeline, creating two separate segments, which can be useful for editing and applying different operations to different parts of the video.

```Kotlin
val willRemoveSlot = firstTrack.slots.firstOrNull() ?: return
firstTrack.removeSlot(willRemoveSlot)
firstTrack.timeSort()

nleEditor.commit()
```


<span id="31925984"></span>
# Finding a Video Segment:

This module explains how to seek a specific position in a video segment.

```Kotlin
// Find a specific position in the video
val midPosition = nleMediaSession.playerApi.duration / 2

// Use the seekTime method to set the playback position to the midpoint
nleMediaSession.playerApi.seekTime(midPosition, NLESeekFlag.EDITOR_SEEK_FLAG_LastSeek)
```


<span id="23e282d2"></span>
# Change the Speed of a Video Segment:

This module explains how to change the playback speed of a video segment.

```Kotlin
// Increase the playback speed of the video to 1.5x
val speed = 1.5F

// Pause the video playback
nleMediaSession.playerApi.pause()

// Iterate through all tracks in the NLEModel
nleEditor.model.tracks.forEach { nleTrack ->
    // Iterate through all slots in each track
    nleTrack.slots.forEach { nleTrackSlot ->
        // Check if the slot contains a video segment
        NLESegmentVideo.dynamicCast(nleTrackSlot.mainSegment)?.also { videoSeg ->
            // Set the absolute playback speed
            videoSeg.absSpeed = speed

            // Calculate the new duration based on the adjusted speed
            val duration = ((videoSeg.timeClipEnd - videoSeg.timeClipStart) / videoSeg.absSpeed).toLong()

            //
```


<span id="0cc530d5"></span>
# Add Video Animation

This module explains how to add video animations to a video segment.

```Kotlin
// Get the first track from the NLEModel or return if it doesn't exist
val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return

// Get the first slot from the first track or return if it doesn't exist
val firstSlot = firstTrack.slots.firstOrNull() ?: return

// Define the default animation duration in microseconds
val defaultAnimDuration = TimeUnit.MILLISECONDS.toMicros(500)

// Clear any existing video animations from the slot
firstSlot.clearVideoAnim()

// Add a new video animation to the slot
firstSlot.addVideoAnim(NLEVideoAnimation().apply {
    // Set the start and end times of the animation
    startTime = 0
    endTime = defaultAnimDuration

    // Calculate the duration of the animation
    val duration = endTime - startTime

    // Define the animation segment
    segment = NLESegmentVideoAnimation().apply {
        // Set the animation duration
        animationDuration = duration

        // Define the video animation resource
        effectSDKVideoAnimation = NLEResourceNode().apply {
            // Set the resource file path for the animation
            resourceFile = File(context.getExternalFilesDir("assets"), "resource/video_animation.bundle/jianxian_6945244038560759838").absolutePath

            // Specify the resource type as animation video
            resourceType = NLEResResType.ANIMATION_VIDEO

            // Generate a unique resource ID
            resourceId = UUID.randomUUID().toString()

            // Set the duration of the resource
            this.duration = duration
        }
    }
})

// Commit the changes to the NLEEditor
nleEditor.commit()

// Configure the NLEMediaSession's player
nleMediaSession.playerApi.apply {
    // Seek to the beginning of the video
    seekTime(0, NLESeekFlag.EDITOR_SEEK_FLAG_LastSeek)
    
    // Start playback
    play()
}
```


<span id="2c533f31"></span>
# Remove Video Animation

This module explains how to remove video animations from a video segment.

```Kotlin
val firstTrack = nleEditor.model.tracks.firstOrNull() ?: return
val firstSlot = firstTrack.slots.firstOrNull() ?: return

val videoAnimation = firstSlot.videoAnims.firstOrNull() ?: return

firstSlot.removeVideoAnim(videoAnimation)

nleEditor.commit()

nleMediaSession.playerApi.apply {
    seekTime(0, NLESeekFlag.EDITOR_SEEK_FLAG_LastSeek)
    play()
}
```
