---
title: "Advanced Features"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-152576"
---

<span id="video-enhancement-effects"></span>
## Video enhancement effects

In interaction scenarios, users often want to set the Image Enhancement feature, or add cool stickers to enhance their experience. To achieve this, you can easily implement the video effect feature by calling the interface for video effects.


|**Video Effects** |**Android** **API/Callback** |**iOS** **API/Callback** |
|---|---|---|
|Set model path of the video effect algorithm |setVideoEffectAlgoModelPath |setVideoEffectAlgoModelPath: |
|Create/destroy video effect engine |[enableVideoEffect](https://docs.byteplus.com/en/docs/12/docs-70080#enablevideoeffect) |[enableVideoEffect:](https://docs.byteplus.com/en/docs/12/docs-70086#enablevideoeffect) |
|Set video effect asset package |setVideoEffectNodes |setVideoEffectNodes: |
|Set color filter |setVideoEffectColorFilter |setVideoEffectColorFilter: |
|Set color filter intensity |setVideoEffectColorFilterIntensity |setVideoEffectColorFilterIntensity: |
|Set video effect intensity |updateVideoEffectNode |updateVideoEffectNode:nodeKey:nodeValue: |


<span id="room-background-music"></span>
## Room background music

Playing background music in a live room can enhance the ambiance. RTC provides audio\-mixing interfaces to add music in live rooms.


|**Background Music** |Android |iOS |
|---|---|---|
|Get the media player for audio mixing |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#getmediaplayer) |
|Start audio mixing |[open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open) |[open](https://docs.byteplus.com/en/docs/12/docs-70086#open-config) |
|Set audio mixing volume |[setVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setvolume) |[setVolume](https://docs.byteplus.com/en/docs/12/docs-70086#setvolume-type) |


<span id="removing-a-co-host-or-guest"></span>
## Removing a co\-host or guest

To remove a co\-host or guest from an RTC room, see [BanRoomUser](https://docs.byteplus.com/en/docs/12/docs-336038).

<span id="record"></span>
## Record

Apart from live streaming, you may need to record audio and video interactions for future playback or content moderation. RTC provides [cloud recording](https://docs.byteplus.com/en/docs/12/docs-115526). With this feature, you can record audio and video interactions and save them to the cloud. A cloud service powered by RTC is used for the recording process, which does not utilize the computing power of your business server or that of your client device.
