---
title: "Sound Attenuation"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114727"
---

<span id="introduction"></span>
## Introduction

The Sound Attenuation feature adjusts the sound output based on the listener's position. Within the voice reception range in an RTC room, this feature allows you to specify how you want a specific sound to change volume as its distance from the listener increases. It is specifically designed for games like PUBG and Battle Royale, where the volume of sound can be used to estimate the distance of other players.

It is recommended to use this feature in combination with [Spatial Audio](https://docs.byteplus.com/6uofwzl3/14136) to create a more immersive experience.

<span id="topology-diagram"></span>
## Topology Diagram

The following figure shows the volumes of different voice sources within a certain range.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4cc7a59a0c4336a933c2f092a46368fc) </span>


* Within the voice range r, the volumes of different voice sources will remain unchanged. For user P, the volumes from user A and user B are the same.

* Within the voice range R, the volumes will decrease with distance. For user P, the volume from user C is higher than that from user D.

* Outside the voice range R, the volume is 0. User P cannot hear user E.


<span id="to-enable-range-audio"></span>
## To enable Range Audio

> You can enable/disable this function before or after entering an RTC room.


1. Call getRangeAudio to create a Range Audio instance.

2. Call updatePosition to update the coordinates in the room.

> When you use Spatial Audio, use the same coordinates of the user.


3. Call updateReceiveRange to update the audio reception range.

4. Call enableRangeAudio to enable Range Audio.

5. Call `setAttenuationModel` to set the sound attenuation model.

> Note:

> If you manually subscribe to audio streams, call registerRangeAudioObserver to register the onRangeAudioInfo callback. This callback provides the attenuation factor after you call updatePosition, updateReceiveRange, or setAttenuationModel.


<span id="api-reference"></span>
## API Reference

See the following table for API details and parameters.


|Steps |Android |iOS |Windows |
|---|---|---|---|
|Create a Range Audio instance |[getRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70080#getrangeaudio) |[getRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70086#getrangeaudio) |[getRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-getrangeaudio) |
|Update the coordinates of local users in the room |[updatePosition](https://docs.byteplus.com/en/docs/12/docs-70080#updateposition) |[updatePosition:](https://docs.byteplus.com/en/docs/12/docs-70086#updateposition) |[updatePosition](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-updateposition) |
|Enable the range voice |[enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70080#enablerangeaudio) |[enableRangeAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#enablerangeaudio) |[enableRangeAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-enablerangeaudio) |
|Update the voice reception range |[updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70080#updatereceiverange) |[updateReceiveRange:](https://docs.byteplus.com/en/docs/12/docs-70086#updatereceiverange) |[updateReceiveRange](https://docs.byteplus.com/en/docs/12/docs-70095#IRangeAudio-updatereceiverange) |
|Set the sound attenuation model |[setAttenuationModel](https://docs.byteplus.com/en/docs/12/docs-70080#setattenuationmodel) |[setAttenuationModel:coefficient:](https://docs.byteplus.com/en/docs/12/docs-70086#setattenuationmodel-coefficient) |/ |


<span id="changelog"></span>
## Changelog

This feature is available in SDK v3.45 and later.
