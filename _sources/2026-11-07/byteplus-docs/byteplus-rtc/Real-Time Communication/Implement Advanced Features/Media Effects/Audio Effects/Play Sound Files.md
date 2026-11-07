---
title: "Play Sound Files"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178326"
---

In interactive entertainment scenarios like games, sounds can be used to lighten up the atmosphere and make it more entertaining. Local users and other members in the room are able to hear the sounds through the sound player interface.

Audio clips shorter than 20 seconds are generally considered sounds, for which you should use the sound\-playing interface. Examples of sounds include applause, cheering, and whistles.

> For longer audio or PCM data, the music player interface should be used. Please refer to [Playing Music Files](https://docs.byteplus.com/en/docs/12/docs-70141) for more details.

## Prerequisite

You have already integrated RTC SDK and are able to implement basic audio and video calls.

Refer to API and Callback for a list of SDKs that support playing sounds.

## To play a sound

In addition to basic audio controls, the RTC SDK supports features such as volume and channel adjustment, and playback progress control.

### **Create an engine**

After creating the audio and video engine instance, you can create a sound player instance.

**java**

```java
EngineConfig engineConfig = new EngineConfig();
    engineConfig.context = this;
    engineConfig.appID = APP_ID;
    rtcVideo = RTCEngine.createRTCEngine(engineConfig, videoEventHandler);
    rtcVideo.startAudioCapture();
    
    effectPlayer = rtcVideo.getAudioEffectPlayer();
```

**swift**

```swift
let engineCfg = ByteRTCEngineConfig.init()
    engineCfg.appID = kAppID
    engineCfg.parameters = [:]
    self.rtcVideo = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)
    self.rtcVideo?.startAudioCapture()
    self.effectPlayer = self.rtcVideo?.getAudioEffectPlayer()
```

**cpp**

```cpp
m_handler.reset(new ByteRTCEventHandler());
    bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    m_video = bytertc::IRTCEngine::createRTCEngine(conf, m_handler.get());
    m_video->startAudioCapture();
    m_player = m_video->getAudioEffectPlayer();
    m_player->setEventHandler(m_handler.get());
```

### **Set callback**

After calling `setEventHandler`, you will receive callbacks about the sound's playback status.

**java**

```java
effectPlayer.setEventHandler(effectPlayerEventHandler);
```

**swift**

```swift
weak var weakSelf = self
     self.effectPlayer?.setEventHandler(weakSelf)
```

**cpp**

```cpp
m_player->setEventHandler(m_handler.get());;
void Handler::onAudioEffectPlayerStateChanged(int effect_id, bytertc::PlayerState state, bytertc::PlayerError error){
    //effect_id Audio effect ID
    //state Audio effect playing state
    //error Error code
}
```

### **Preload local sound files**

We recommend using `preload` for local sound files to avoid repeatedly loading and unloading them from memory, especially when the same sound is used multiple times.

If a sound is no longer needed, call `unload` to free up its memory.

> Loading online URL audio files is not supported.

**java**

```java
effectPlayer.preload(EFFECT_ID, effectFilePath)
```

**swift**

```swift
self.effectPlayer?.preload(effectId, filePath: filePath)
```

**cpp**

```cpp
int ret = m_player->preload(id, "path");
```

### **Start playing sounds**

To play multiple sound files simultaneously or to overlay sounds, call `start` multiple times, each with a different mixing ID and `file path`. If you preloaded a file, ensure the mixing ID you use to play it matches the ID used for preloading.

**java**

```java
private void startEffect(int effectId, String path) {
    AudioEffectPlayerConfig playerConfig = new AudioEffectPlayerConfig();
    playerConfig.type = AudioMixingType.AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH;
    playerConfig.startPos = 0;
    playerConfig.playCount = 1; 
    playerConfig.pitch = 0;
    effectPlayer.start(effectId, path, playerConfig);
}
```

**swift**

```swift
let filePath = Bundle.main.path(forResource: "rtc_test", ofType: "aac")

let config = ByteRTCAudioEffectPlayerConfig.init()
    config.type = .playoutAndPublish
    config.playCount = 1 
    
    let code = self.effectPlayer?.start(effectId, filePath: filePath, config: config)
    print("start play effect code = \(code!)")
```

**cpp**

```cpp
bytertc::AudioEffectPlayerConfig config;
config.pitch = 0;
config.play_count = 1;
config.start_pos = 0;
config.type = static_cast<bytertc::AudioMixingType>(type);
int ret = m_player->start(id, "path1", config);
```

### **Stop playing sounds**

To stop the sounds, call `stop` or `stopAll`.

**java**

```java
effectPlayer.stop(EFFECT_ID);
effectPlayer.stopAll();
```

**cpp**

```cpp
int ret = m_player->stop(id);
int ret = m_player->stopAll();
```

### **Pause or resume sound playback**

**java**

```java
effectPlayer.pause(EFFECT_ID)
effectPlayer.pauseAll()
effectPlayer.resume(EFFECT_ID)
effectPlayer.resumeAll()
```

**swift**

```swift
self.effectPlayer?.pause(effectId)

self.effectPlayer?.pauseAll() 

 self.effectPlayer?.resume(effectId) 
self.effectPlayer?.resumeAll() 
```

**cpp**

```cpp
int ret = m_player->pause(id); 
int ret = m_player->pauseAll(); 
int ret = m_player->resume(id); 
int ret = m_player->resumeAll();
```

### **Get and set sound properties**

All audio mixing settings, such as volume and starting position, only take effect after the sound starts playing and before it stops.

On mobile platforms, volume adjustment for all mixed audio is available only through the `setVolumeAll` method. On PC, you can adjust the volume of specific mixed audio files using the `setVolume` method.

> Note: When working with the same audio file, you must use the same audio mixing ID for all operations.

**java**

```java
effectPlayer.setPosition(EFFECT_ID, position)
int pos = effectPlayer.getPosition(EFFECT_ID)

effectPlayer.getDuration(EFFECT_ID)
effectPlayer.setVolume(EFFECT_ID, volume)
effectPlayer.setVolumeAll(volume)
int volume = effectPlayer.getVolume(EFFECT_ID)
```

**swift**

```swift
self.effectPlayer?.setPosition(effectId, position: position)
let position = self.effectPlayer?.getPosition(effectId)

let totalTime = self.effectPlayer?.getDuration(effectId)

self.effectPlayer?.setVolume(effectId, volume: volume)
self.effectPlayer?.setVolumeAll(volume)
let currentVolume = self.effectPlayer?.getVolume(effectId)
```

**cpp**

```cpp
int ret = m_player->setPosition(id, position);
int position = m_player->getPosition(id);
int duration = m_player->getDuration(id);
ret = m_player->setVolume(id, volume);
ret = m_player->setVolumeAll(volume);
int volume = m_player->getVolume(id);
```

## Sample project

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/audio/mixing/AudioEffectMixingActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/AudioManager/AudioEffectMixing/AudioEffectMixingViewController.swift)

## **API and callback**

> Note: The macOS API listed in the table is for Objective\-C, while the macOS sample project uses the C++ API from the Windows SDK.

|平台 |Android |iOS |macOS |Windows |Linux |Electron |Flutter |Web |
|---|---|---|---|---|---|---|---|---|
|初始化音效管理类 |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#getaudioeffectplayer) |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getaudioeffectplayer) |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-getaudioeffectplayer) |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70095#getaudioeffectplayer) |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getaudioeffectplayer) |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getaudioeffectplayer) |getAudioEffectPlayer |[getAudioMixingManager](https://docs.byteplus.com/en/docs/12/docs-104478#getaudiomixingmanager) |
|音效混音管理类 |[IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#iaudioeffectplayer) |[ByteRTCAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#bytertcaudioeffectplayer) |[ByteRTCAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70092#bytertcaudioeffectplayer) |[IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70095#IAudioEffectPlayer-iaudioeffectplayer) |[IAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85516#IAudioEffectPlayer-iaudioeffectplayer) |[RTCAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-85532#rtcaudioeffectplayer) |RTCAudioEffectPlayer |[AudioMixingManager](https://docs.byteplus.com/en/docs/12/docs-104478#audiomixingmanager) |
|音效播放器回调 |[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |onAudioEffectPlayerStateChanged:state:error: |onAudioEffectPlayerStateChanged:state:error: |[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85517#IAudioEffectPlayerEventHandler-onaudioeffectplayerstatechanged) |[onAudioEffectPlayerStateChanged](https://docs.byteplus.com/en/docs/12/docs-85533#rtcaudioeffectplayercallback-onaudioeffectplayerstatechanged) |onAudioEffectPlayerStateChanged | |

## **Change log**

1. From client\-side SDK 3.32, channel settings of music files are supported.

2. From client\-side SDK 3.36, mixing of online audio files is supported across the platform.

3. As of client\-side SDK v3.38, you can adjust the playback speed of audio files used during audio and video calls.

4. As of client\-side SDK v3.45.4, you can get the actual playback duration of mixed audio files. This duration is unaffected by pauses, skips, seeking, or stalling.

5. From client\-side SDK 3.52, mixed audio files of 24kHz mp3 are supported. For versions previous to 3.52, only audio files of the following sampling rates are supported: 8kHz, 16kHz, 22.05kHz, 32kHz, 44.1kHz, 48kHz, 64kHz, 96kHz and 192kHz.

6. As of client\-side SDK v3.54, all original audio mixing classes on native platforms have been deprecated and replaced by separate sound mixing and music mixing classes, each with its own controls.
