---
title: "Get Raw Audio Data"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178324"
---

You can get raw audio data in PCM format and process it. For example, store the data locally to record audio on the client\-side.

## Use cases

* Local audio recording, where the app stores raw audio data to the local device.

* Client\-side content detection, where sound data is obtained and passed to a third\-party SDK for audio content detection.

## Prerequisite

You have already integrated RTC SDK and are able to implement basic audio and video calls.

For details about the SDK that supports getting raw audio data, see API and Callbacks.

## To get raw audio data

> The sequence diagram below uses the API names in the Android SDK as examples. API or callback names may differ across platforms. Refer to the API and Callbacks section for the definitive names.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/1178324_api_en.png)

### 1. Create an engine

Create and initialize an audio and video engine class.

**java**

```java
rtcVideo = RTCVideo.createRTCVideo(this, Constants.APP_ID, videoEventHandler, null, null);
```

**swift**

```swift
self?.rtcVideo = ByteRTCVideo.createRTCVideo(kAppID, delegate: self, parameters: [:])
self?.rtcVideo?.startAudioCapture()
```

### **2. Inherit AudioFrameObserver**

Inherit from the callback class and implement its callback methods.

**java**

```java
private IAudioFrameObserver audioFrameObserver = new IAudioFrameObserver() {
    @Override
    public void onRecordAudioFrame(IAudioFrame audioFrame) {
        Log.i(TAG, "onRecordAudioFrame:");
    }

    @Override
    public void onPlaybackAudioFrame(IAudioFrame audioFrame) {
        Log.i(TAG, "onPlaybackAudioFrame:");
    }

    @Override
    public void onRemoteUserAudioFrame(RemoteStreamKey streamKey, IAudioFrame audioFrame) {
        Log.i(TAG, "onRemoteUserAudioFrame:");
    }

    @Override
    public void onMixedAudioFrame(IAudioFrame audioFrame) {
        Log.i(TAG, "onMixedAudioFrame:");
    }
};
```

**swift**

```swift
// ByteRTCAudioFrameObserver
func onRecord(_ audioFrame: ByteRTCAudioFrame) {

}

func onPlaybackAudioFrame(_ audioFrame: ByteRTCAudioFrame) {

}

func onMixedAudioFrame(_ audioFrame: ByteRTCAudioFrame) {

}

func onRemoteUserAudioFrame(_ streamKey: ByteRTCRemoteStreamKey, audioFrame: ByteRTCAudioFrame) {

}
```

### **3. Enable callback**

1. Register the audio data callback through `registerAudioFrameObserver`.

2. Call `enableAudioFrameCallback` to set the callback format for the audio data to be received. Only one of the audio data formats can be set for each call.

> * When the target audio data is for recording, playback, or audio mixing, you must specify the sampling rate and number of channels in the audio parameter format.

> * When the target audio data is a remote audio stream, the audio parameter format `format` needs to be set to automatic.

3. In the `RawAudioDataObserver`, you will receive the corresponding type of audio callback data, where you can implement audio recording and other operations.

**java**

```java
rtcVideo.registerAudioFrameObserver(audioFrameObserver);

AudioFormat format = new AudioFormat(AudioSampleRate.AUDIO_SAMPLE_RATE_48000, AudioChannel.AUDIO_CHANNEL_MONO);
rtcVideo.enableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_RECORD, format);
rtcVideo.enableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_MIXED, format);
rtcVideo.enableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_PLAYBACK, format);

AudioFormat audioFormat = new AudioFormat(AudioSampleRate.AUDIO_SAMPLE_RATE_AUTO, AudioChannel.AUDIO_CHANNEL_AUTO);
rtcVideo.enableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_REMOTE_USER, audioFormat);
```

**swift**

```swift
self.rtcVideo!.registerAudioFrameObserver(self)

let audioFormat = ByteRTCAudioFormat.init()
audioFormat.sampleRate = .rate44100 
audioFormat.channel = .stereo 
audioFormat.samplesPerCall = 0 
self.rtcVideo?.enableAudioFrameCallback(.record, format: audioFormat)
```

### **4. Disable callback**

When the audio data is no longer needed, pass a null parameter to `registerAudioFrameObserver` to disable the callback.

**java**

```java
rtcVideo.disableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_RECORD);
rtcVideo.disableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_MIXED);
rtcVideo.disableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_PLAYBACK);
rtcVideo.disableAudioFrameCallback(AudioFrameCallbackMethod.AUDIO_FRAME_CALLBACK_REMOTE_USER);
```

**swift**

```swift
self.rtcVideo?.disableAudioFrameCallback(.record)
self.rtcVideo?.registerAudioFrameObserver(nil)
```

### **5. Destroy engine**

After the call is completed, destroy the audio and video engine.

> If you have joined a room, you must destroy all room instances before destroying the audio and video engine.

**java**

```java
RTCVideo.destroyRTCVideo();
```

**swift**

```swift
ByteRTCVideo.destroyRTCVideo()
self.rtcVideo = nil
```

## Sample project

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/audio/RawAudioDataActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/AudioManager/AudioRawData/AudioRawDataViewController.swift)

## **API and callback**

The following client SDKs all support getting raw audio data. You can use the appropriate SDK for your platform to implement this function, following the descriptions and examples provided.

> Note: The API interface for macOS in the table is Objective\-C, while the macOS sample project uses the C++ API, which is the same API used by the Windows SDK.

|Platform |Android |iOS |macOS |Windows |Linux (available since V3.58) |Electron | |
|---|---|---|---|---|---|---|---|
|Register audio data callback observer |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080) |[registerAudioFrameObserver:](https://docs.byteplus.com/en/docs/12/docs-70086) |[registerAudioFrameObserver:](https://docs.byteplus.com/en/docs/12/docs-70092) |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095) |[registerAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85516) |N/A |N/A |
|Set and enable the specified audio data frame callback |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70080) |[enableAudioFrameCallback:format:](https://docs.byteplus.com/en/docs/12/docs-70086) |[enableAudioFrameCallback:format:](https://docs.byteplus.com/en/docs/12/docs-70092) |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70095) |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85516) |[enableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudioframecallback) | |
|Disable audio data frame callback |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70080) |[disableAudioFrameCallback:](https://docs.byteplus.com/en/docs/12/docs-70086) |[disableAudioFrameCallback:](https://docs.byteplus.com/en/docs/12/docs-70092) |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-70095) |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85516) |[disableAudioFrameCallback](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-disableaudioframecallback) | |
|Audio data callback |[IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70081) |[ByteRTCAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70087) |[ByteRTCAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70093) |[IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70096) |[IAudioFrameObserver](https://docs.byteplus.com/en/docs/12/docs-85517) |[onRecordAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordaudioframe) [onPlaybackAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onplaybackaudioframe) [onRemoteUserAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremoteuseraudioframe) [onMixedAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onmixedaudioframe) [onRecordScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onrecordscreenaudioframe) | |

## FAQ

### Q1: What should I do if the API call to enable callbacks succeeds, but I don't receive any callbacks?

A: Confirm whether the parameters `method` and `format` passed in during the call to `enableAudioFrameCallback` are correct. Refer to the following table.

|Parameter Meaning |Parameter Name |Parameter Value Combination 1 |Parameter Value Combination 2 |
|---|---|---|---|
|Audio callback method |`method` |`0`: Local microphone `1`: All remote mixing `2`: Local and remote mixing |`3`: Single remote user audio stream |
|Audio format |`format` |Specify the sample rate and channel |`-1`: Automatic |

### Q2: How do I process audio data before it is sent to remote users?

A: Processing the data obtained from this callback does not affect the audio sent to remote users. If you want to process the audio data and then send it back to RTC for encoding and transmission, use the `registerAudioProcessor` method.
