---
title: "Set the Audio Route"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-117836"
---

<span id="overview"></span>
## Overview

> The audio route is the device your app uses for audio playback, such as a built\-in speaker, earpiece, or an external device like wired or Bluetooth headphones.


The RTC SDK has a default strategy for automatically switching the audio route when devices are connected or disconnected. This guide explains this default behavior and shows you how to manually override it by setting a specific audio route to meet your application's needs.


* Built\-in playback device, including a speaker or an earpiece. The speaker is often located at the bottom of the phone and has a louder volume. This enables hands\-free functionality. The earpiece is located at the top of the phone and has a lower volume. You can only hear it clearly by putting your ear close to it, which has better privacy and is suitable for answering calls.

* External devices include wired and Bluetooth headphones.


<span id="switching-default-audio-route-and-behavior-of-switching-routes-when-external-devices-are-connected-disconnected"></span>
## Switching Default Audio Route and Behavior of Switching Routes when External Devices are Connected / Disconnected

The RTC SDK includes built\-in strategies for determining and switching the default audio route. The strategies are as follows:


* When there is no external device, the system will select the built\-in audio route as the playback device. The default audio route (speaker/earpiece) can be specified by calling `setDefaultAudioRoute`.

* When the first external device is connected, the RTC SDK will automatically update the playback device to this device. When multiple external devices are connected, the RTC SDK plays through the last connected device by default. You can obtain the latest audio route by `onAudioRouteChanged` or calling `getAudioRoute`.

* When an external device is disconnected, the SDK will select the last connected external device as the audio route according to the order of device connection. When the last external device is disconnected, the audio route will immediately switch to the default device.


In most scenarios, you only need to specify the default audio route (speaker/earpiece) by calling `setDefaultAudioRoute`, and the SDK will automatically switch the audio route based on device connection and disconnection.

<span id="manually-switching-audio-routes"></span>
## Manually Switching Audio Routes

If the default routing strategy does not meet your needs (for example, if you need to manually switch to the speaker while an external device is connected), follow these steps:


1. Call setAudioRoute to switch the current audio route to the specified device. This only takes effect when the audio route is in **call mode**. You can obtain the volume mode of the current audio route through system APIs.

2. After successfully switching the audio route, `onAudioRouteChanged` callback is triggered to notify you of the audio route change.


Note:


* For Android devices:

   * On some Android devices, when both wired headphones and Bluetooth headphones are connected simultaneously, forcing a switch to wired headphones may result in the actual audio output being prioritized by the system to Bluetooth headphones connected via the A2DP protocol. These devices have a system audio strategy in media mode that prioritizes A2DP devices as the preferred playback device.

   * When only wired headphones are connected, the audio route cannot be switched to the built\-in earpiece even in call mode.

* For iOS devices, only forced switching to the built\-in speaker is supported.


<span id="api-reference"></span>
## API Reference


| |Android |iOS |
|---|---|---|
|Set the default audio playback route |[setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#setdefaultaudioroute) |[setDefaultAudioRoute:](https://docs.byteplus.com/en/docs/12/docs-70086#setdefaultaudioroute) |
|Set the audio playback route manually |[setAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#setaudioroute) |[setAudioRoute:](https://docs.byteplus.com/en/docs/12/docs-70086#setaudioroute) |
|Get the current audio playback route |[getAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#getaudioroute) |[getAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70086#getaudioroute) |


<span id="change-log"></span>
## Change Log


|Version |Description |
|---|---|
|3.60 |Due to changes in audio scenario enumeration values and volume mode configuration rules, the effective audio scenarios for `setAudioRoute` have also changed. Volume mode is determined by audio scenario, audio route, whether audio capture is enabled, and user role. See [What is the difference between in-call volume and media volume?](https://docs.byteplus.com/en/docs/12/docs-651068). |
|3.50 |We recommend using `setDefaultAudioRoute` to set the default audio route. |
|3.42 |`setDefaultAudioRoute` selects the device's earpiece or speaker as the default audio route. `setAudioRoute` supports more audio device types, such as wired headphones, Bluetooth headphones, etc., and only takes effect when the volume mode is call mode, i.e., when the audio scenario is set to `AUDIO_SCENARIO_COMMUNICATION`. |
|3.38 |This feature is supported. |
