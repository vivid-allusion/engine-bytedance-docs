---
title: "Audio editing modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-audio-editing-modules-in-android"
---

This module enables the addition of audio, sound effects, music, and recording capabilities in the editing environment. Essentially, the SDK supports the import of audio files in formats such as mp3, AAC, WAV, FLAC, m4a (iOS), OGG (Android), PCM (Android), and more to support various scenarios like the ones mentioned.

For instance, whether it's a short 1\-2 second sound effect, a 3\-4 minute music track, or a 10\-second recording, for the SDK, it adds an mp3 audio file.

<span id="0aee77ca"></span>
# Term descriptions

These are some of the terms and their descriptions.


|**Terms** |**Description** |
|---|---|
|NLETrack |* A track, at least one track (main track) is required in NLEModel, and there can be multiple sub\-tracks.<br><br>* Tracks serve as containers for NLETrackSlots, and there can be no time overlap among NLETrackSlots within the same track.<br><br>* On the main track, NLETrackSlots must be connected end\-to\-end, while on non\-main tracks, NLETrackSlots can be sparse. |
|NLETrackSlot |* Atime segment and serves as a container for NLESegment and its derived classes.<br><br>* A single NLETrackSlot can only contain one NLESegment or its derived class. |
|NLESegmentAudio |* A derived class of NLESegment, representing audio and music content. |


<span id="d99f32d4"></span>
# Adding audio resources

Here, audio resources refer to audio files in formats such as mp3 and m4a. Regardless of the specific use case, there are several ways to add audio to a video.

<span id="c8931d91"></span>
## Adding a single audio file

In this scenario, you only need to add one audio track with a single audio segment.

```Kotlin
/*
 * Because we don't know the current duration of the video being edited (which depends on the length of the video file you selected from the album), 
 * in the code below, we first get the total playback duration and determine the maximum playback duration of the audio when adding audio based on the current playback duration. 
 * If the current playback duration is less than the audio duration, then the maximum audio playback duration is the current playback duration, otherwise, it defaults to the audio duration.
 */

/**
 * Get the total playback duration, measured in microseconds (μs).
 * This total duration depends on which track currently has the longest duration.
 */
val playDuration = nleMediaSession.playerApi.duration
val audioDuration = 17 * 1000000L
val audioDisplayDuration = if (audioDuration > playDuration) playDuration else audioDuration

/**
 * For demonstration purposes, we will place the newly added audio on a new track (also, as long as two or more audio clips do not overlap in time, they can be placed on the same track).
 */
nleEditor.model.addTrack(NLETrack().apply {
    /**
     * Set whether it is the main track, the default value is false.
     */
    mainTrack = false

    /**
     * Set the track type to audio.
     */
    extraTrackType = NLETrackType.AUDIO
    addSlot(NLETrackSlot().apply {
        /**
         * Start time of audio playback, measured in microseconds (μs), must be set.
         */
        startTime = 0

        /**
         * End time of audio playback, measured in microseconds (μs), must be set.
         */
        endTime = audioDisplayDuration

        mainSegment = NLESegmentAudio().apply {
            // Description of the audio file, including duration, local path, etc.
            avFile = NLEResourceAV().apply {
                /**
                 * Duration of the audio file, measured in microseconds.
                 * Here, because we know the specific duration of the audio, we used a fixed value.
                 * If you replace it with your own environment, you need to set it according to the actual duration of the audio.
                 */
                duration = 17 * 1000000L
                /**
                 * Resource name, can be customized, not required.
                 */
                resourceName = "music"
                /**
                 * Set the resource type to audio.
                 */
                resourceType = NLEResType.AUDIO
                /**
                 * Resource path, because we have embedded the resource, so here we directly use the corresponding path. 
                 * In actual projects, you need to set it to the path of the corresponding audio in your project.
                 */
                resourceFile =
                    "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/music.bundle/jimeng.mp3"
            }

            /**
             * Set the audio volume, 1
```


<span id="c6e19d6c"></span>
## **Adding multiple audios**

You can choose to add multiple audio segments to a single audio track, ensuring that these segments do not overlap in time.

```Kotlin
/**
 * Add an audio track
 */
nleEditor.model.addTrack(NLETrack().apply { 
    /**
     * Set whether it is the main track, the default value is false.
     */
    mainTrack = false

    /**
     * Set the track type to audio.
     */
    extraTrackType = NLETrackType.AUDIO

    // Add the first audio segment, playing in the range of 0 to 8 seconds
    addSlot(NLETrackSlot().apply {
        startTime = 0
        endTime = 8 * 1000000
        ......
    }

    // Add the second audio segment, playing in the range of 8 to 15 seconds
    addSlot(NLETrackSlot().apply {
        startTime = 8 * 1000000
        endTime = 15 * 1000000
        ......
    }
    /**
    * Above, you can see that two video segments are placed on the same track, and the start time of the second segment must be greater than or equal to the end time of the first segment for the effect to take place.
    */
})

/**
 * You must commit the modified data model to see the effect in the preview video.
 */
nleEditor.commit()
```


<span id="684e90b0"></span>
## **Adding multiple audios with overlapping playback**

In this scenario, you can add multiple audio tracks, each containing one or more audio segments.

```Kotlin
/**
* Add the first audio segment
*/
nleEditor.model.addTrack(NLETrack().apply { 
    /**
     * Set whether it is the main track, the default value is false.
     */
    mainTrack = false

    /**
     * Set the track type to audio.
     */
    extraTrackType = NLETrackType.AUDIO

    // Add the first audio segment, playing in the range of 0 to 8 seconds
    addSlot(NLETrackSlot().apply {
        startTime = 0
        endTime = 8 * 1000000
        ......
    }
})

/**
* Add the second audio segment
*/
nleEditor.model addTrack(NLETrack().apply { 
    /**
     * Set whether it is the main track, the default value is false.
     */
    mainTrack = false

    /**
     * Set the track type to audio.
     */
    extraTrackType = NLETrackType.AUDIO

    // Add the first audio segment, playing in the range of 3 to 8 seconds
    addSlot(NLETrackSlot().apply {
        startTime = 3 * 1000000
        endTime = 8 * 1000000
        ......
    }
})

/**
 * You must commit the modified data model to see the effect in the preview video.
 */
nleEditor.commit()
```


<span id="ee44dd69"></span>
# **Adjusting audio volume**

After adding audio, you may need to adjust the audio volume.

<span id="7639edcf"></span>
## **Modifying volume for all audio tracks and segments**

To modify the volume of all audio tracks and segments in the video, you can iterate through the NLEModel's audio tracks and segments.

```Kotlin
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.AUDIO }.forEach { audioTrack ->
    audioTrack.sortedSlots.forEach { audioSlot ->
        // ⚠️ It is essential to use dynamicCast for data type conversion in NLE
        NLESegmentAudio.dynamicCast(audioSlot.mainSegment).apply {
            volume = 0.5f
        }
    }
}

// Remember to commit the modified data model. This step is crucial; otherwise, you won't see the changes in the preview video.
nleEditor.commit()
```


**Modifying volume for specific audio tracks and segments**

If you want to modify the volume for specific audio tracks and segments, you can use UUIDs or custom tags to identify them and make the necessary adjustments.

One approach is to record the UUID of the audio track or audio segment immediately after adding them and categorize this UUID to identify the relevant classification. Later, you can use this UUID to locate the corresponding audio tracks and audio segments for modifications.

**Obtaining UUID:** 


* **Getting the UUID of an audio track (NLETrack)** : NLETrack().getUUID()

* **Getting the UUID of an audio segment (NLETrackSlot)** : NLETrackSlot().getUUID()


<span id="0c6b8b8e"></span>
### **Accessing the Corresponding Audio Track and Segment Using UUID:** 

```Kotlin
nleEditor.model.tracks
    .filter {
        it.extraTrackType == NLETrackType.AUDIO
    }
    .forEach { audioTrack ->
        audioTrack.sortedSlots.forEach { audioSlot ->
            if (audioSlot.uuid == "Your target UUID") {
                // Matching UUID allows you to operate on the corresponding object
                NLESegmentAudio.dynamicCast(audioSlot.mainSegment).apply {
                    volume = 0.5f
                }
                return@forEach
            }
        }
    }
```


Another common approach is to use extra information when adding audio to mark audio tracks or segments. When you need to modify specific audio, match it based on the previously added extra information.

<span id="f9fcec45"></span>
### **Adding extra information to audio tracks**

```Kotlin
NLETrack().apply {
    // Set a custom type, e.g., music, recording, etc.
    setExtra("audio_type", "music")
    ......
}
```


<span id="a7b46e74"></span>
### **Adding extra information to audio segments**

```Kotlin
NLETrackSlot().apply {
    // Set a custom type, e.g., music, recording, etc.
    setExtra("audio_type", "music")
    ......
}
```


You can set the custom type on either the audio track or the audio segment based on your client's requirements.

<span id="bb2b6495"></span>
### **Locating specific audio tracks based on extra information:** 

```Kotlin
nleEditor.model.tracks
    .filter {
        it.extraTrackType == NLETrackType.AUDIO
                && "custom tag" == it.getExtra("extra_key")
    }
    .forEach { audioTrack ->
        audioTrack.sortedSlots.forEach { audioSlot ->
            NLESegmentAudio.dynamicCast(audioSlot.mainSegment).apply {
                volume = 0.5f
            }
        }
    }
```


<span id="c097e37d"></span>
## **Adjusting volume for the original sound of the video's main track**

If you want to adjust the volume of the original sound on the main track, this is done within the main track's video segments.

<span id="7b94390b"></span>
### **Setting the volume of all video segments on the main track to 50%:** 

```Kotlin
nleEditor.model.mainTrack.sortedSlots.forEach { 
    NLESegmentVideo.dynamicCast(it)?.volume = 0.5f
}
```


<span id="e0fa8fda"></span>
### **Muting/Unmuting the Entire Main Track:** 

```Kotlin
nleEditor.model.mainTrack.sortedSlots.forEach {
    val segment = it.getMainSegment<NLESegmentVideo>()
    if (isAllMute) {
        // Disable the original sound, mute all
        segment?.volume = 0f
    } else {
        // Enable the original sound
        val muteVolume = 1f
        segment?.apply {
            volume = if (this.avFile.hasAudio) muteVolume else 0f
            enableAudio = true
        }
    }
}
```


<span id="64410c79"></span>
# **Deleting audio resources**

Deleting audio resources is relatively straightforward. You can locate the audio tracks or segments you want to delete in the NLEModel and remove the corresponding data objects.

```Kotlin
nleEditor.model.tracks
    .filter {
        it.extraTrackType == NLETrackType.AUDIO
    }.forEach {
        nleEditor.model.removeTrack(it)
    }

// Remember to commit the modified data model. This step is crucial; otherwise, you won't see the changes in the preview video.
nleEditor.commit()
```


<span id="8def88fe"></span>
# **Modifying audio resources**

Modifying audio resources often involves replacing music tracks.

<span id="3d24fd4c"></span>
## **Replacing audio resources while keeping existing tracks and segments**

In this scenario, you retain the existing audio tracks and segments but replace the audio resources. You need to ensure that the durations match if you replace the audio resources.

```Kotlin
nleEditor.model.tracks.filter { it.extraTrackType == NLETrackType.AUDIO }.forEach { audioTrack ->
    audioTrack.sortedSlots.forEach { audioSlot ->
        NLESegmentAudio.dynamicCast(audioSlot.mainSegment).apply {
            NLEResourceAV.dynamicCast(avFile).apply {
                resourceName = "music_new"
                resourceFile = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/music.bundle/tianyuan.mp3"
            }
        }
    }
}

// Remember to commit the modified data model. This step is crucial; otherwise, you won't see the changes in the preview video.
nleEditor.commit()
```


<span id="aa9f90d9"></span>
## **Deleting and adding new audio tracks and segments**

In this approach, you first delete the existing audio tracks and segments, then add new ones. After both actions are completed, you should save the changes to start rendering.
