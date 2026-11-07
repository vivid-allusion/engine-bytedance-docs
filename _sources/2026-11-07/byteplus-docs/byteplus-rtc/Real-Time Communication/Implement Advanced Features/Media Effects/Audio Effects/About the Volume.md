---
title: "About the Volume"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-81268"
---

You can add the following features to your Apps via the audio volume callback.

* Visualize sounds using the changing volume.

* Identify the active speaker.

* Remind users to turn on their microphone to be heard.

You can adjust the system volume or call the API to change the volume for captured audio, playback, or audio mixing.

> For information on changing the audio mixing volume, refer to [Mixed Audios](https://docs.byteplus.com/en/docs/12/docs-70141).

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/%E9%9F%B3%E9%87%8Fen.png)

## Prerequisites

* Your app has integrated the RTC SDK and can make RTC calls.

* Your app uses the RTC built\-in module to handle audio data from the local microphone.

## Get the volume

1. Call `enableAudioPropertiesReport` to activate audio volume callbacks and set the notification period.

2. Get the volume for local users from `onLocalAudioPropertiesReport` and for remote users from `onRemoteAudioPropertiesReport`.

> Refer to [API Reference](https://docs.byteplus.com/en/docs/12/docs-70083#audiopropertiesinfo) for the value explanation.

### Sample code

**objectivec**

```objectivec
// Invoke periodic volume callbacks.
- (void)enableAudioPropertiesReport {
    ByteRTCAudioPropertiesConfig *audioPropertiesConfig = [[ByteRTCAudioPropertiesConfig alloc] init];
    audioPropertiesConfig.interval = 300;
    [self.rtcVideo enableAudioPropertiesReport:audioPropertiesConfig];
}
/**
  * Callback containing the volume of the mic and the screen audio
  * @param engine ByteRTCVideo object
  *  @param audioPropertiesInfos Volume of the local audio. Refer to LocalAudioPropertiesInfo for more details.
  */
- (void)rtcEngine:(ByteRTCVideo *)engine onLocalAudioPropertiesReport:(NSArray<ByteRTCLocalAudioPropertiesInfo *> *)audioPropertiesInfos {
    // Callback containing the volume of the local microphone
}

/**
  * Callback containing the volume of a remote user
  * @param engine ByteRTCVideo object
  *  @param audioPropertiesInfos Volume of remote users. Refer to ByteRTCRemoteAudioPropertiesInfo for more details.
* @param totalRemoteVolume The total volume of all subscribed remote users. The value ranges from 0 to 255.
  */
- (void)rtcEngine:(ByteRTCVideo *)engine onRemoteAudioPropertiesReport:(NSArray<ByteRTCRemoteAudioPropertiesInfo *> *)audioPropertiesInfos totalRemoteVolume:(NSInteger)totalRemoteVolume {
    // Volume callback of remote users
}
/**
 * Callback containing information about the active speaker
* @param engine ByteRTCVideo object
 * @param roomId Room ID
 * @param uid User ID of the active speaker
  */
- (void)rtcEngine:(ByteRTCVideo *)engine onActiveSpeaker:(NSString *)roomId uid:(NSString *)uid {
    // Information of the active speaker
}
```

**java**

```java
// Invoke periodic volume callbacks.
public void enableAudioPropertiesReport() {
    AudioPropertiesConfig config = new AudioPropertiesConfig(300);
    mRTCVideo.enableAudioPropertiesReport(config);
}

private final IRTCVideoEventHandler mRTCVideoEventHandle = new IRTCVideoEventHandler() {
    /**
     * Callback containing the volume of the mic and the screen audio
     * @param audioPropertiesInfos Volume of the local audio. Refer to LocalAudioPropertiesInfo for more details.
     */
    @Override
    public void onLocalAudioPropertiesReport(LocalAudioPropertiesInfo[] audioPropertiesInfos) {
        // Callback containing the volume of the local microphone
    }


    /**
     * Callback containing the volume of a remote user
     * @param audioPropertiesInfos Volume of remote users. Refer to RemoteAudioPropertiesInfo for more details.
     * @param totalRemoteVolume The total volume of all remote users
     */
    @Override
    public void onRemoteAudioPropertiesReport(RemoteAudioPropertiesInfo[] audioPropertiesInfos, int totalRemoteVolume) {
        // Volume callback of remote users
    }


    /**
     * Callback containing information about the active speaker
     * @param roomId Room ID
     * @param uid User ID of the active speaker
     */
    @Override
    public void onActiveSpeaker(String roomId, String uid) {
// Information about the most active user in the room
    }

    ...
  }
```

**cpp**

```cpp
// Invoke periodic volume callbacks.
void RtcEngineWrap::enableAudioPropertiesReport() {
    bytertc::AudioPropertiesConfig config;
    config.interval = 300;
    video_engine_->enableAudioPropertiesReport(config);
}

 /**
  * Callback containing the volume of the mic and the screen audio
  * @param audio_properties_infos Volume of local audio sources, such as the microphone.
  * @param audio_properties_info_number Length of the array
  */
void RtcEngineWrap::onLocalAudioPropertiesReport(
    const LocalAudioPropertiesInfo * audio_properties_infos,
    int audio_properties_info_number) {
    // Callback containing the volume of the local microphone
}

/**
 * Callback containing the volume of a remote user
 * @param audio_properties_infos Volume of remote users.
 * @param audio_properties_info_number Length of the array
 * @param total_remote_volume Total volume of the remote users, ranging from [0, 255]
 */
void RtcEngineWrap::onRemoteAudioPropertiesReport(
        const bytertc::RemoteAudioPropertiesInfo* audio_properties_infos,
        int audio_properties_info_number, int total_remote_volume) {
    // Volume callback of remote users
}
/**
 * Get the active speaker
 * @param room_id  Room ID
 * @param uid User ID of the active speaker
 */
void RtcEngineWrap::onActiveSpeaker(
    const char* room_id,
    const char* uid) {
    // Information of the active speaker
}
```

### API Reference

| |Android |iOS |macOS |Windows |Linux |Electron |Web |
|---|---|---|---|---|---|---|---|
|Enable periodic volume callbacks. |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#enableaudiopropertiesreport) |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#-enableaudiopropertiesreport) |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70092#-enableaudiopropertiesreport) |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#enableaudiopropertiesreport) |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85516#enableaudiopropertiesreport) |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-enableaudiopropertiesreport) |[enableAudioPropertiesReport()](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport) |
|Local audio volume callback. |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalaudiopropertiesreport) |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onlocalaudiopropertiesreport) |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onlocalaudiopropertiesreport) |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#onlocalaudiopropertiesreport) |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#onlocalaudiopropertiesreport) |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onlocalaudiopropertiesreport) |[onLocalAudioPropertiesReport()](https://docs.byteplus.com/en/docs/12/docs-104479#onlocalaudiopropertiesreport) |
|Volume callback for remote audio. |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onremoteaudiopropertiesreport) |[rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onremoteaudiopropertiesreport-totalremotevolume) |[rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onremoteaudiopropertiesreport-totalremotevolume) |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#onremoteaudiopropertiesreport) |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85517#onremoteaudiopropertiesreport) |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onremoteaudiopropertiesreport) |[onRemoteAudioPropertiesReport()](https://docs.byteplus.com/en/docs/12/docs-104479#onremoteaudiopropertiesreport) |
|Callback of the active speakers. |[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70081#onactivespeaker) |[rtcEngine:onActiveSpeaker:uid:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onactivespeaker-uid) |[rtcEngine:onActiveSpeaker:uid:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onactivespeaker-uid) |[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-70096#onactivespeaker) |[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85517#onactivespeaker) |[onActiveSpeaker](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onactivespeaker) |[onActiveSpeaker()](https://docs.byteplus.com/en/docs/12/docs-104479#onactivespeaker) |
|Get the instant audio volume. |None |None |None |None |None |None |[getAudioVolume](https://docs.byteplus.com/en/docs/12/docs-104478#getaudiovolume) |

## Adjust capture volume

Audio capture is the process of capturing sounds from local devices, such as microphones, and storing them locally.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/%E9%87%87%E9%9B%86%E9%9F%B3%E9%87%8Fen.png)

Call `setCaptureVolume` to adjust the capture volume.

The `volume` ranges from 0 to 400.

* 0: Silent

* 100: Original volume

* 400: Amplify the audio. At most, the volume can be 4 times the original.

### Sample code

**objectivec**

```objectivec
[self.rtcEngine setCaptureVolume:120];
```

**java**

```java
mRTCEngine.setCaptureVolume(120);
```

**cpp**

```cpp
video_engine_->setCaptureVolume(120);
```

### API Reference

| |Android |iOS |macOS |Windows |Linux |Electron |Web |
|---|---|---|---|---|---|---|---|
|Capture volume. |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70080#setcapturevolume) |[setCaptureVolume:](https://docs.byteplus.com/en/docs/12/docs-70086#setcapturevolume) |[setCaptureVolume:](https://docs.byteplus.com/en/docs/12/docs-70092#setcapturevolume) |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70095#setcapturevolume) |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85516#setcapturevolume) |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setcapturevolume) |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-104478#setcapturevolume) |

## Adjust playback volume

Playback is the process of receiving remote audio and playing it on a local speaker.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/%E6%92%AD%E6%94%BE%E9%9F%B3%E9%87%8Fen.png)

* Volume of all users: Call `setPlaybackVolume` to change the volume of mixed audio of all remote users.

* Volume of a user: Call `setRemoteAudioPlaybackVolume` to change the volume of a user.

   * To specify volumes for multiple users, call `setRemoteAudioPlaybackVolume` multiple times and pass different `streamId`s and `volume`s.

   * To change the volume of a user repeatedly, call `setRemoteAudioPlaybackVolume` multiple times and pass the same `streamId` and different `volume`s.

**objectivec**

```objectivec
int volume = 120;
[self.rtcEngine setPlaybackVolume:volume];
[self.rtcEngine setRemoteAudioPlaybackVolume:streamId volume:volume];
```

**java**

```java
int volume = 120;
mRTCEngine.setPlaybackVolume(volume);
mRTCEngine.setRemoteAudioPlaybackVolume(streamId, volume);
```

**cpp**

```cpp
int volume = 120;
video_engine_->setPlaybackVolume(volume);
video_engine_->setRemoteAudioPlaybackVolume(streamId, volume);
```

### API Reference

| |Android |iOS |macOS |Windows |Linux |Electron |Web |
|---|---|---|---|---|---|---|---|
|Volume of all users |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#setplaybackvolume) |[setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/docs-70086#setplaybackvolume) |[setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/docs-70092#setplaybackvolume) |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#setplaybackvolume) |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85516#setplaybackvolume) |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setplaybackvolume) |None |
|Volume of a user |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70080#setremoteaudioplaybackvolume) |[setRemoteAudioPlaybackVolume:volume:](https://docs.byteplus.com/en/docs/12/docs-70086#setremoteaudioplaybackvolume-volume) |[setRemoteAudioPlaybackVolume:volume:](https://docs.byteplus.com/en/docs/12/docs-70092#setremoteaudioplaybackvolume-volume) |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-70095#setremoteaudioplaybackvolume) |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85516#setremoteaudioplaybackvolume) |[setRemoteAudioPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setremoteaudioplaybackvolume) |[setPlaybackVolume](https://docs.byteplus.com/en/docs/12/docs-104478#setplaybackvolume) |

## FAQ

Q: On Android, no callbacks are received after calling `enableAudioPropertiesReport`.

A: The RTC SDK holds a weak reference to the callback instance, so you must manage its lifecycle. For example, define the callback as a member variable instead of an anonymous inner class to prevent it from being garbage collected prematurely.
