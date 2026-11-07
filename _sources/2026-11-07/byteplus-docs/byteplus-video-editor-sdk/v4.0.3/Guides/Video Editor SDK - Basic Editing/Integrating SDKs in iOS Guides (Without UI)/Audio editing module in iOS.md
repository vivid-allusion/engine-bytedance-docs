---
title: "Audio editing module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-audio-editing-module-in-ios"
---

This module enables the addition, deletion and substitution of audio, volume modification, and recording capabilities in the editing environment. This module helps you provide an engaging listening experience for your target audience.

<span id="6f5e3cb4"></span>
# Module description

The following table introduces classes related to the audio editing module.


|**Class Name** |**Description** |
|---|---|
|NLEResourceAV_OC |The resource module used to construct audio resources and record audio resource information. |
|NLESegmentAudio_OC |The audio segment. It is linked to a specific resource and information about audio segmentation. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="5e583350"></span>
# Adding an audio file

Before adding an audio file, ensure that you have got the path to your target audio file.

**To add an audio file**:


1. Construct an `NLEResourceAV_OC` object with the path you have got.

2. Add the `NLEResourceAV_OC` object to an `NLESegmentAudio_OC` object.

3. Add the `NLESegmentAudio_OC` object to an `NLETrackSlot_OC` object.

4. Add the `NLETrackSlot_OC` object to an `NLETrack_OC` object.

5. To commit changes that you have made and render the audio effect, call `NLEInterface_OC.editor.commitAndRender()`.

6. To complete the addition of the audio file, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
// 1. Get audio path
let path

// 2. make NLEResourceAV_OC
let r = NLEResourceAV_OC()

// 3. add resource to segment
let segment = NLESegmentAudio_OC()
segment.audioFile = resource
segment.setTimeClipStart(CMTime.zero)
segment.setTimeClipEnd(duration)

// 4. add segment to slot
let slot = NLETrackSlot_OC()
slot.setSegmentAudio(segment)
slot.setStart(CMTime.zero)
slot.layer = 0

// 5. add slot to track
let track = NLETrack_OC()
track.layer = 0
track.extraTrackType = .AUDIO
track.addSlot(slot)

// 6. commit change
nle.editor.commitAndRender()

// 7. add completed
nle.editor.done()
```


<span id="5c4d144f"></span>
# Deleting an audio file

For instructions on how to delete an audio file, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="dba4de9e"></span>
# Substituting an audio file

Before substituting an audio file, ensure that you have obtained the path to a new audio.

**To substitute an audio file**:


1. Delete the original audio file by `slotID`. For instructions on how to delete an audio file, refer to "Deleting an audio file".

2. Add a new audio file using the path you have obtained. For instructions on how to add an audio file, refer to "Adding an audio file".


<span id="2ca6e0d9"></span>
# Modifying the volume of an audio

This section introduces how to modify the volume of an audio.

**To modify the volume of an audio**:


1. Find your target `NLETrackSlot_OC` object by slotID.

2. Find an`NLESegmentAudio_OC` object that corresponds with your target `NLETrackSlot_OC` object.

3. Modify the `volume` parameter of the `NLESegmentAudio_OC` object.

4. To commit changes that you have made and render the audio volume effect, call `NLEInterface_OC.editor.commitAndRender()`.

5. To complete the volume modification process, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
// 1. find NLETrackSlot_OC base on slotID
// 2. find NLESegmentAudio_OC base on NLETrackSlot_OC
guard let slot = slot(with: slotID),
    let segment = slot.segment as? NLESegmentAudio_OC else {
    return
}

// 3. change NLESegmentAudio_OC volume
segment.setVolume(volume)
      
// 4. commit change
nle.editor.commitAndRender()

// 5. add completed
nle.editor.done()
```


<span id="aa6c925a"></span>
# Audio recording

This section introduces how to use the audio recording capability in your project.

**To perform audio recording**:


1. To process audio recording, create a `VEAudioRecorder` instance.

2. To initiate audio recording process after the preparation is completed, call `startRecord()` of your`VEAudioRecorder` instance.

3. To stop the audio recording process and obtain the filepath of the audio, call `stopRecord()` of `VEAudioRecorder` instance.

4. Add an audio file using the path you have obtained. For instructions on how to add an audio file, refer to "Adding an audio file".


**Sample code**

```Swift
// 1. create VEAudioRecorder
private lazy var recorder: VEAudioRecorder = VEAudioRecorder(waveformConfig: nil)

// 2. start record
recorder.prepare { [weak self] success, error in
    if success {
        self?.recorder.startRecord()
    } else {
    print("Error preparing audio recorder: \(error?.localizedDescription ?? "")")
    }
}

// 3. stop record and return file path
let fileURL = recorder.stopRecord()
return fileURL.path

// 4. add recorded audio
// Refer to 4.1 add audio
```


&nbsp;
