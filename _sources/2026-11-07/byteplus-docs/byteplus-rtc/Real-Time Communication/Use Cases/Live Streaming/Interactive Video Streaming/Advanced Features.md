---
title: "Advanced Features"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113693"
---

1. Smart beautify effects: In interaction scenarios, users often want to configure the beautification feature, or add various cool stickers to enhance their experience. You can call the interface about video effects to achieve this easily.

2. Room background music: Playing background music in a live room can enhance the mood. RTC provides audio mixing interfaces to add music to the room.



|**Video effects** |**Android API/Callback** |**iOS API /Callback** |
|---|---|---|
|Set the model path of the video effect algorithm |setVideoEffectAlgoModelPath |setVideoEffectAlgoModelPath: |
|Enable or disable the video effect engine |enableVideoEffect |enableVideoEffect: |
|Set the video effect resource package |setVideoEffectNodes |setVideoEffectNodes: |
|Configure the color filter |setVideoEffectColorFilter |setVideoEffectColorFilter: |
|Set the intensity of the color filter |setVideoEffectColorFilterIntensity |setVideoEffectColorFilterIntensity: |
|Configure the effect level |updateVideoEffectNode |updateVideoEffectNode:nodeKey:nodeValue: |
|**Background music** | | |
|Get media player |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#getmediaplayer) |[getMediaPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#getmediaplayer) |
|Start audio mixing |[open](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-open) |[open](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-open-config) |
|Set audio mixing volume |[setVolume](https://docs.byteplus.com/en/docs/12/docs-70080#IMediaPlayer-setvolume) |[setVolume](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCMediaPlayer-setvolume-type) |
