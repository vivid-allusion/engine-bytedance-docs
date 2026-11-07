---
title: "Advanced Features"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-117922"
---

<span id="advanced-features"></span>
## Advanced Features

<span id="set-voice-changer-reverberation-and-music-vocal-pitch"></span>
### Set voice changer, reverberation, and music/vocal pitch

You can also set special effects such as voice change, reverb, vocal/music pitch, etc. to add fun.


|**Business Logic** |**Android** **API** |**iOS** **API** |
|---|---|---|
|Set voice changer type |[setVoiceChangerType](https://docs.byteplus.com/en/docs/12/docs-70080#setvoicechangertype) |[setVoiceChangerType:](https://docs.byteplus.com/en/docs/12/docs-70086#setvoicechangertype) |
|Set reverb effect type |[setVoiceReverbType](https://docs.byteplus.com/en/docs/12/docs-70080#setvoicereverbtype) |[setVoiceReverbType:](https://docs.byteplus.com/en/docs/12/docs-70086#setvoicereverbtype) |
|Enable local voice pitch |[setLocalVoicePitch](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvoicepitch) |[setLocalVoicePitch:](https://docs.byteplus.com/en/docs/12/docs-70086#setlocalvoicepitch) |


<span id="get-audio-raw-data"></span>
### Get audio raw data

In some scenarios, you may need to get the original audio data for speech recognition and other processing. You can use [registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#registeraudioframeobserver) to register the data observer, and then obtain the audio PCM data through the callback:


* Obtain the PCM data collected by the microphone through the [onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioFrameObserver-onrecordaudioframe) callback

* Use the [onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70081#onplaybackaudioframe) callback to get the mixed audio PCM data from all remote users.


<span id="cloud-recording"></span>
### Cloud recording

If you need to record users' audio and video for subsequent playback and content review, use the RTC cloud recording function. For details, see [StartRecord](https://docs.byteplus.com/en/docs/12/docs-115526).
