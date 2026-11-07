---
title: "Audio Effect and Denoiser"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178327"
---

To enhance user engagement in interactive scenarios like Karaoke or online gaming, you can implement various audio effects. This guide provides step\-by\-step instructions and code examples for adding voice changers, reverb, custom vocal effects, and both traditional and AI\-powered noise cancellation to your RTC application.

<span id="prerequisites"></span>
## Prerequisites

You have already integrated RTC SDK and can implement basic audio and video calls.

For SDKs that support this function, refer to the API Reference for details.

<span id="glossary"></span>
## Glossary

Noise cancellation includes traditional and AI noise cancellation. AI noise cancellation mainly suppresses non\-stationary noise, such as sounds from keyboard tapping or moving chairs. Traditional noise cancellation mainly suppresses stationary noise, such as air conditioning noise and fan noise.

<span id="to-set-up-voice-improvements-and-effects"></span>
## To set up voice improvements and effects

> The time series chart below uses the API names in the Android SDK as examples. API or callback names may differ slightly across SDKs for different platforms. See API Reference for the correct names.


<span id="_1-create-an-engine"></span>
### **1. Create an engine**

Create and initialize the audio and video engine.

> If you need to obtain remote audio data, you also need to join a room and publish audio streams. Refer to [Building an RTC App](https://docs.byteplus.com/en/docs/12/docs-70123) for detailed steps.


```mixin-react
const list = [
  {
    "lang": "java",
    "text": `EngineConfig config = new EngineConfig();
    config.appID = appId;
    config.context = applicationContext;
    rtcEngine = RTCEngine.createRTCEngine(config, rtcEngineEventHandler);`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `let engineCfg = ByteRTCEngineConfig.init()
    engineCfg.appID = appId
    engineCfg.parameters = [:]
    self.rtcEngine = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)`, 
  },
  {
    "lang": "cpp",
    "text": `bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    engine = bytertc::IRTCEngine::createRTCEngine(conf, this);
`, 
  }
]
return (<PreCodeTabs list={list} />);
```


<span id="_2-enable-audio-capturing"></span>
### **2. Enable audio capturing**

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `rtcEngine.startAudioCapture();`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `self.rtcEngine?.startAudioCapture()`, 
  },
  {
    "lang": "cpp",
    "text": `engine->startAudioCapture();`, 
  }
]
return (<PreCodeTabs list={list} />);
```


<span id="_3-customize-pitch-up-and-reverb-effects"></span>
### **3. Customize pitch\-up and reverb effects**

If the preset effects cannot meet your business needs, you can also customize the vocal effects through `enableLocalVoiceReverb` and `setLocalVoiceReverbParam`.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `
    rtcEngine.setLocalVoicePitch(pitch);
    rtcEngine.enableLocalVoiceReverb(true);
    rtcEngine.setLocalVoiceReverbParam(config);`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `
    self.rtcEngine?.setLocalVoicePitch(pitch)
    
    self.rtcEngine?.enableLocalVoiceReverb(true)
    self.rtcEngine?.setLocalVoiceReverbParam(config)`, 
  }, 
  {
     "lang": "cpp",
     "text": `
ret = engine->setLocalVoicePitch(value); 
ret = engine->enableLocalVoiceReverb(true); 
ret = engine->setLocalVoiceReverbParam(config);`,
  }
]
return (<PreCodeTabs list={list} />);
```


<span id="_4-set-noise-cancellation-mode"></span>
### **4. Set noise cancellation mode**

You can call setAnsMode to select the appropriate noise reduction mode based on your scenario requirements:


* AI noise reduction: Primarily suppresses non\-stationary noise, such as sounds from keyboard tapping or moving chairs, and more.

> In versions prior to V3.57.1, AI noise reduction only takes effect in specific room modes. For details, see [Room mode restrictions for AI noise reduction](https://docs.byteplus.com/6uofwzl3/22949).


* Traditional noise reduction: Primarily suppresses stationary noise, such as air conditioning sounds, fan sounds, and more.


```mixin-react
const list = [
  {
    "lang": "java",
    "text": `rtcEngine.setAnsMode(mode);`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `self.rtcEngine?.setAnsMode(mode)`, 
  }, 
  {
     "lang": "cpp",
     "text": `ret = engine->setAnsMode(mode);`,
  }
]
return (<PreCodeTabs list={list} />);
```


<span id="room-mode-restrictions-for-ai-noise-reduction"></span>
## Room mode restrictions for AI noise reduction

In versions prior to V3.57.1, when calling setAnsMode to enable AI noise reduction, its effectiveness depends on the room mode (RoomProfileType). AI noise reduction only takes effect when the client is set to one of the following room modes:


* In\-game chat mode: `kRoomProfileTypeGame`

* High sound quality game mode: `kRoomProfileTypeGameHD`

* Cloud gaming mode: `kRoomProfileTypeCloudGame`

* One\-on\-one audio and video call: `kRoomProfileTypeChat`

* Multi\-client synchronous playback of audio and video: `kRoomProfileTypeLwTogether`

* Personal devices in cloud meetings: `kRoomProfileTypeMeeting`

* Classroom interaction mode: `kRoomProfileTypeClassroom`

* Meeting room systems in cloud meetings: `kRoomProfileTypeMeetingRoom`


<span id="sample-project"></span>
## Sample project


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/audio/VoiceEffectActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/AudioManager/SoundEffects/SoundEffectsViewController.swift)
