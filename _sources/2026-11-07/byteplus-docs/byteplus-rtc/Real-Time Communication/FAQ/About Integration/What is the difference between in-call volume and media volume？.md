---
title: "What is the difference between in-call volume and media volume？"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-651068"
---

<span id="what-is-the-difference-between-in-call-volume-and-media-volume"></span>
## What is the difference between in\-call volume and media volume?

The volume control of a cell phone is divided into in\-call volume and media volume. These two types of volume are independent and can be controlled separately. The channels that use different volumes are called the in\-call channel and the media channel respectively. Each has different characteristics, and you need to ensure that the selected channel satisfies the requirements of the business scenarios. You can refer to the table below for differences.


|Volume type |Suitable scenarios |Features |System selected volume mode |
|---|---|---|---|
|In\-call volume |Used to control the volume during a call. |* The human voice is more prominent, but the sound of music playing may be dry.<br><br>* The echo cancellation effect is better.<br><br>* Due to system limitations, the volume can not be adjusted to 0. |* iOS：[AVAudioSessionModeVoiceChat](https://developer.apple.com/documentation/avfaudio/avaudiosessionmodevoicechat), [AVAudioSessionModeVideoChat](https://developer.apple.com/documentation/avfaudio/avaudiosessionmodevideochat)<br><br>* Android：[MODE_IN_COMMUNICATION](https://developer.android.com/reference/android/media/AudioManager#MODE_IN_COMMUNICATION) |
|Media volume |Used to control the volume of games, music, movies, or system output. |* The sound is more expressive and more natural.<br><br>* Applicable to scenes with certain requirements for sound quality, or music\-related scenes.<br><br>* The playback volume can be adjusted to 0. |* iOS：[AVAudioSessionModeDefault](https://developer.apple.com/documentation/avfaudio/avaudiosessionmodedefault)<br><br>* Android：[MODE_NORMAL](https://developer.android.com/reference/android/media/AudioManager#MODE_NORMAL) |


BytePlus RTC SDK provides various preset audio scenario types on the mobile end, including musical scenario, high\-quality communication scenario, and video game scenario. Taking Android SDK for example, you can call [setAudioScenario](https://docs.byteplus.com/en/docs/12/docs-70080#setaudioscenario) to choose an audio scenario.

<span id="why-you-should-try-to-avoid-switching-between-media-volume-and-in-call-volume-during-a-call"></span>
## Why you should try to avoid switching between media volume and in\-call volume during a call?

With their separate volume controls, if there exists a substantial disparity in volume levels when switching between them, it can result in a sudden surge in the audio, also known as a 'sudden burst'. Across various audio scenarios, different volume modes are applied corresponding to the user's microphone being turned on or off. For the default audio scenarios and their matching volume types, please refer to tables below. If users are anticipated to frequently switch their microphones on and off, it is recommended to opt for scenarios that apply the same mode for both states, like the high\-quality chat scenario.


|Audio scenario |Audio route |One of multiple audio publishers in the room | |Unique audio publisher in the room | |User who only listens without publishing in the room |
|---|---|---|---|---|---|---|
| | |Collection off |Collection on |Collection off |Collection on |Collection off |
|[Default] `DEFAULT(0)` |Speaker |Media |Call |Media |Media |Media |
| |Earpiece |Call |Call |Media |Call |Call |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Call |Media |Call |Media |
|`CHATROOM(1)` |Speaker |Call |Call |Call |Call |Call |
| |Earpiece |Call |Call |Call |Call |Call |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Call |Media |Call |Media |
|`GAMESTREAMING(2)` |Speaker |Media |Media |Media |Media |Media |
| |Earpiece |Call |Call |Media |Call |Call |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Call |Media |Call |Media |
|`CHORUS(3)` |Speaker |Media |Media |Media |Media |Media |
| |Earpiece |Call |Call |Media |Call |Call |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Call |Media |Call |Media |


<span id="ios"></span>
### iOS


|Audio scenario |Audio route |One of multiple audio publishers in the room | |Unique audio publisher in the room | |User who only listens without publishing in the room |
|---|---|---|---|---|---|---|
| | |Collection off |Collection on |Collection off |Collection on |Collection off |
|[Default] `ByteRTCAudioScenarioTypeDefault` = `0` |Speaker |Media |Call |Media |Media |Media |
| |Earpiece |Media |Call |Media |Media |Media |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Call |Media |Call |Media |
|`ByteRTCAudioScenarioTypeChatRoom` = `1` |Speaker |Call |Call |Call |Call |Call |
| |Earpiece |Call |Call |Call |Call |Call |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Call |Call |Call |Call |Call |
|`ByteRTCAudioScenarioTypeGameStreaming` = `2` |Speaker |Media |Media |Media |Media |Media |
| |Earpiece |Media |Media |Media |Media |Media |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Media |Media |Media |Media |
|`ByteRTCAudioScenarioTypeChorus` = `3` |Speaker |Media |Media |Media |Media |Media |
| |Earpiece |Media |Media |Media |Media |Media |
| |Wired headphones/USB headphones/External sound card |Media |Media |Media |Media |Media |
| |Bluetooth headphones |Media |Media |Media |Media |Media |


<span id="can-the-volume-modes-for-audio-input-and-output-be-different"></span>
## Can the volume modes for audio input and output be different?

At any given time, the volume modes for audio input and output must be consistent. For example, a scenario where the input is in the in\-call channel the output is also in the in\-call channel.

<span id="why-does-bluetooth-headset-not-collect-sound-while-it-can-play-normally"></span>
## Why does Bluetooth headset not collect sound, while it can play normally?


* When a Bluetooth headset is connected and set to media channel, due to Android system restrictions, audio can only be collected via the phone’s microphone. Therefore, the microphone of the Bluetooth headset does not collect sound, which is unsuitable for scenarios such as a "phone\-in\-bag voice call".

* In the default case of the iOS system, Bluetooth headsets can collect sound using the HFP protocol. However, if you have switched to the A2DP protocol by [setBluetoothMode:](https://docs.byteplus.com/en/docs/12/docs-70086#setbluetoothmode), the audio input will be sourced through the phone's microphone rather than the Bluetooth headset's microphone. Consequently, the Bluetooth headset will be unable to collect sound.


<span id="what-are-the-differences-in-volume-modes-after-upgrading-to-native-sdk-v3-60-and-later-versions"></span>
## What are the differences in volume modes after upgrading to Native SDK V3.60 and later versions?

We upgraded various audio scenarios in Native SDK V3.60. In previous versions, the volume mode was determined by the audio scenario, audio route, and whether the user enabled audio collection. After the upgrade, user roles will also affect the actual volume mode. User roles include:


* **One of multiple audio publishers in the room**: There are multiple users publishing audio streams in the room, and you are one of the users publishing an audio stream.

* **Unique audio publisher in the room**: You are the only user publishing an audio stream in the room.

* **User who only listens without publishing in the room**: You only subscribe to other users' audio streams in the room without publishing audio streams.


The following tables show the differences in volume modes under different conditions on Android and iOS platforms before and after the upgrade.

<span id="android"></span>
### Android


|V3.58 and earlier versions | | |Audio route |V3.60 and later versions | | | | | |
|---|---|---|---|---|---|---|---|---|---|
|Audio scenario |Collection off |Collection on | |Audio scenario |One of multiple audio publishers in the room | |Unique audio publisher in the room | |User who only listens without publishing in the room |
| | | | | |Collection off |Collection on |Collection off |Collection on |Collection off |
|[Default] `AUDIO_SCENARIO_MUSIC(0)` |Media |Call |Built\-in speaker |[Default] `DEFAULT(0)` |Media |Call |Media |**Media** |Media |
| |Call |Call |Built\-in earpiece | |Call |Call |**Media** |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Media |Media |Bluetooth headphones | |Media |**Call** |Media |**Call** |Media |
|`AUDIO_SCENARIO_HIGHQUALITY_COMMUNICATION(1)` |Media |Call |Built\-in speaker |`DEFAULT(0)` |Media |Call |Media |**Media** |Media |
| |Call |Call |Built\-in earpiece | |Call |Call |**Media** |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Call |Call |Bluetooth headphones | |**Media** |Call |**Media** |Call |**Media** |
|`AUDIO_SCENARIO_COMMUNICATION(2)` |Call |Call |Built\-in speaker |`CHATROOM(1)` |Call |Call |Call |Call |Call |
| |Call |Call |Built\-in earpiece | |Call |Call |Call |Call |Call |
| |Call |Call |Wired headphones/USB headphones/External sound card | |**Media** |**Media** |**Media** |**Media** |**Media** |
| |Call |Call |Bluetooth headphones | |**Media** |Call |**Media** |Call |**Media** |
|`AUDIO_SCENARIO_MEDIA(3)` |Media |Media |Built\-in speaker |`GAMESTREAMING(2)` |Media |Media |Media |Media |Media |
| |Call |Call |Built\-in earpiece | |Call |Call |**Media** |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Media |Media |Bluetooth headphones | |Media |**Call** |Media |**Call** |Media |
|`AUDIO_SCENARIO_GAME_STREAMING(4)` |Media |Media |Built\-in speaker |`GAMESTREAMING(2)` |Media |Media |Media |Media |Media |
| |Call |Call |Earpiece | |Call |Call |**Media** |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Call |Call |Bluetooth headphones | |**Media** |Call |**Media** |Call |**Media** |
|`AUDIO_SCENARIO_HIGHQUALITY_CHAT(5)` |Call |Call |Built\-in speaker |`CHATROOM(1)` |Call |Call |Call |Call |Call |
| |Call |Call |Earpiece | |Call |Call |Call |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Call |Call |Bluetooth headphones | |**Media** |Call |**Media** |Call |**Media** |


<span id="ios"></span>
### iOS


|V3.58 and earlier versions | | |Audio route |V3.60 and later versions | | | | | |
|---|---|---|---|---|---|---|---|---|---|
|Audio scenario |Collection off |Collection on | |Audio scenario |One of multiple audio publishers in the room | |Unique audio publisher in the room | |User who only listens without publishing in the room |
| | | | | |Collection off |Collection on |Collection off |Collection on |Collection off |
|[Default] `ByteRTCAudioScenarioMusic` = `0` |Media |Call |Built\-in speaker |[Default] `ByteRTCAudioScenarioTypeDefault` = `0` |Media |Call |Media |**Media** |Media |
| |Media |Call |Built\-in earpiece | |Media |Call |Media |**Media** |Media |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Media |Media |Bluetooth headphones | |Media |**Call** |Media |**Call** |Media |
|`ByteRTCAudioScenarioHighqualityCommunication` = `1` |Media |Call |Built\-in speaker |`ByteRTCAudioScenarioTypeDefault` = `0` |Media |Call |Media |**Media** |Media |
| |Media |Call |Built\-in earpiece | |Call |Call |Media |**Media** |Media |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Call |Call |Bluetooth headphones | |**Media** |Call |**Media** |Call |**Media** |
|`ByteRTCAudioScenarioCommunication` = `2` |Call |Call |Built\-in speaker |`ByteRTCAudioScenarioTypeChatRoom` = `1` |Call |Call |Call |Call |Call |
| |Call |Call |Built\-in earpiece | |Call |Call |Call |Call |Call |
| |Call |Call |Wired headphones/USB headphones/External sound card | |**Media** |**Media** |**Media** |**Media** |**Media** |
| |Call |Call |Bluetooth headphones | |Call |Call |Call |Call |Call |
|`ByteRTCAudioScenarioMedia` = `3` |Media |Media |Built\-in speaker |`ByteRTCAudioScenarioTypeGameStreaming` = `2` |Media |Media |Media |Media |Media |
| |Media |Media |Built\-in earpiece | |Media |Media |Media |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Media |Media |Bluetooth headphones | |Media |Media |Media |Media |Media |
|`ByteRTCAudioScenarioGameStreaming` = `4` |Media |Media |Built\-in speaker |`ByteRTCAudioScenarioTypeGameStreaming` = `2` |Media |Media |Media |Media |Media |
| |Media |Media |Earpiece | |Media |Media |Media |Media |Media |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Call |Call |Bluetooth headphones | |**Media** |**Media** |**Media** |**Media** |**Media** |
|`ByteRTCAudioScenarioHighqualityChat` = `5` |Call |Call |Built\-in speaker |`ByteRTCAudioScenarioTypeChatRoom` = `1` |Call |Call |Call |Call |Call |
| |Call |Call |Earpiece | |Call |Call |Call |Call |Call |
| |Media |Media |Wired headphones/USB headphones/External sound card | |Media |Media |Media |Media |Media |
| |Call |Call |Bluetooth headphones | |Call |Call |Call |Call |Call |
