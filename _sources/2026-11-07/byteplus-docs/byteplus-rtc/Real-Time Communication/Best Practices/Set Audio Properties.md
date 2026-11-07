---
title: "Set Audio Properties"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-97706"
---

<span id="applicable-scenarios"></span>
## Applicable scenarios

You can adjust the audio properties according to the needs of the project to give users a better audio experience. This article describes how to config different audio settings according to the scenario.

<span id="prerequisites"></span>
## Prerequisites

You have already integrated RTC SDK and implemented basic audio and video calls.

<span id="introduction"></span>
## Introduction

<span id="room-mode"></span>
### Room mode

> Note:

> The steps are the same across platforms, but interface and parameter names may differ slightly. This guide uses the Android RTC SDK as an example. For more information, refer to the API documentation for your target platform.


When calling joinRoom to enter a room, you can set the channelProfile according to your project needs. The room mode, configured via the `channelProfile` parameter, specifies recommended settings for network transmission, video properties, and audio processing algorithms based on your business scenario. This includes configurations like enabling 3A features and optimizing for different device models. You can contact technical support to help you configure the room mode on the RTC server.

> Note:

> Cloud\-side configurations take precedence over client\-side API settings.


<span id="sound-quality-settings"></span>
### Sound quality settings

Sound quality profile AudioProfileType contains audio encoding parameters such as sample rate, bit rate, number of channels, frame rate, etc. You can switch AudioProfileType by calling setAudioProfile. However, due to the limitations of device performance and the influence of network environment, under the same network and device conditions, higher audio quality may result in a decrease in other performance indicators, such as playback smoothness and resilience to poor network conditions.

Once the channelProfile is set, there is usually no need to further adjust the audio quality for the current room mode. The default audio profile AUDIO_PROFILE_DEFAULT(0) for each channelProfile is the recommended audio configuration for a specific scenario. It is designed to meet the business requirements without excessively consuming performance or requiring ideal network conditions.

> Note:

> You can contact technical support to get the default audio parameters for the room mode.


* If your business scenario does not require high audio quality in the current channel profile, you can call setAudioProfile to switch the audio quality to a lower level and reduce device performance consumption. If you need to restore the initial settings after switching to another audio profile, you can call setAudioProfile again to switch the audio quality back to the default audio profile AUDIO_PROFILE_DEFAULT(0).

* As `setAudioProfile` can only adjust the encoding parameters and does not affect the sampling parameters, calling this API to switch the audio quality to a higher level may not result in a significant improvement in sound quality. Therefore, if your business scenario requires higher audio quality than the current room mode, it is recommended to select a channel profile corresponding to **Musical** quality when calling `joinRoom`, rather than using `setAudioProfile` to switch the audio quality.

   The channel profiles corresponding to different audio qualities are listed in the table below.



|Quality |PC |Mobile |
|---|---|---|
|Musical |`CHANNEL_PROFILE_KTV(11)` `CHANNEL_PROFILE_CHORUS(12)` `CHANNEL_PROFILE_GAME_STREAMING(14)` `CHANNEL_PROFILE_LAN_LIVE_STREAMING(15)` |`CHANNEL_PROFILE_KTV(11)` `CHANNEL_PROFILE_CHORUS(12)` `CHANNEL_PROFILE_GAME_STREAMING(14)` `CHANNEL_PROFILE_LAN_LIVE_STREAMING(15)` |
|Standard |`CHANNEL_PROFILE_COMMUNICATION(0)` `CHANNEL_PROFILE_CLOUD_GAME(3)` `CHANNEL_PROFILE_LOW_LATENCY(4)` `CHANNEL_PROFILE_CHAT(5)` `CHANNEL_PROFILE_CHAT_ROOM(6)` `CHANNEL_PROFILE_LW_TOGETHER(7)` `CHANNEL_PROFILE_GAME_HD(8)` `CHANNEL_PROFILE_CO_HOST(9)` `CHANNEL_PROFILE_INTERACTIVE_PODCAST(10)` `CHANNEL_PROFIEL_VR_CHAT(13)` `CHANNEL_PROFIEL_MEETING(16)` `CHANNEL_PROFILE_MEETING_ROOM(17)` `CHANNEL_PROFILE_CLASSROOM(18)` |`CHANNEL_PROFILE_CLOUD_GAME(3)` `CHANNEL_PROFILE_LOW_LATENCY(4)` `CHANNEL_PROFILE_CHAT_ROOM(6)` `CHANNEL_PROFILE_LW_TOGETHER(7)` `CHANNEL_PROFILE_GAME_HD(8)` `CHANNEL_PROFILE_CO_HOST(9)` `CHANNEL_PROFILE_INTERACTIVE_PODCAST(10)` `CHANNEL_PROFIEL_VR_CHAT(13)` `CHANNEL_PROFILE_MEETING_ROOM(17)` |
|Fluent |`CHANNEL_PROFILE_GAME(2)` |`CHANNEL_PROFILE_COMMUNICATION(0)` `CHANNEL_PROFILE_GAME(2)` `CHANNEL_PROFILE_CHAT(5)` `CHANNEL_PROFIEL_MEETING(16)` `CHANNEL_PROFILE_CLASSROOM(18)` |


<span id="api-reference"></span>
## API reference


|Platform |Android |iOS |macOS |Windows |Web |
|---|---|---|---|---|---|
|Set the room mode |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#joinroom-userinfo-uservisibility-roomconfig) |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#joinroom-userinfo-uservisibility-roomconfig) |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#joinroom) |
|Set the sound quality level |[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70080#setaudioprofile) |[setAudioProfile:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setaudioprofile) |[setAudioProfile:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setaudioprofile) |[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70095#setaudioprofile) |[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioprofile) |
