---
title: "Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-125706"
---

<span id="_4-53"></span>
## 4.53

<span id="keytype"></span>
### Keytype


|Type |Keytype |Notes |
|---|---|---|
|Modified |[VideoRenderMode](https://docs.byteplus.com/en/docs/12/docs-104481#videorendermode) |The default rendering mode for main stream changed from `RENDER_MODE_FIT` to `RENDER_MODE_HIDDEN`. |


<span id="_4-52"></span>
## 4.52

<span id="api"></span>
### API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Replaced |Video Processing |`enable: () => void;` |[enableBeauty: () => void;](https://docs.byteplus.com/en/docs/12/docs-148646#enablebeauty) | |
|Replaced |Video Processing |`disable: () => void;` |[disableBeauty: () => void;](https://docs.byteplus.com/en/docs/12/docs-148646#enablebeauty) | |


<span id="_4-51"></span>
## 4.51

<span id="api"></span>
### API


|Type |Function Module |Previous |Current |Notes |
|---|---|---|---|---|
|Modified |Audio Management |`setAudioProfile: (profile: AudioProfileType) => void;` |[setAudioProfile: (profile: AudioProfileType) => Promise;](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioprofile) | |
|Modified |Video Management |* `setVideoCaptureConfig: (config: TrackCaptureConfig) => Promise<MediaTrackSettings>;`<br><br>* `setVideoEncoderConfig: (descriptions: VideoEncoderConfig \\| VideoEncoderConfig[]) => Promise<void>;` |[setVideoEncoderConfig: (descriptions: VideoEncoderConfig \| VideoEncoderConfig[]) => Promise;](https://docs.byteplus.com/en/docs/12/docs-104478#setvideoencoderconfig) |Merged video capture and encoder configurations to improve compatibility. Changed the default sending resolution to 640 × 480 px. |


<span id="keytype"></span>
### Keytype


|Type |Keytype |Notes |
|---|---|---|
|Deleted |[RoomConfig](https://docs.byteplus.com/en/docs/12/docs-104481#roomconfig) |Deleted property `roomProfileType`. |
|Modified |[VideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104481#videoencoderconfig) |Changed the type of property `width` and `height`from `number` to `ConstrainULong`.<br><br>Changed the type of property `frameRate` from `number` to `ConstrainDouble`. |
|Modified |[ScreenEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104481#screenencoderconfig) |Changed the type of property `width` and `height`from `number` to `ConstrainULong`.<br><br>Changed the type of property `frameRate` from `number` to `ConstrainDouble`. |


<span id="error-code"></span>
### Error Code


|Type |Error Code |Notes |
|---|---|---|
|New |[ErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#errorcode) |Added constant `USER_MESSAGE_EXCEED_QPS`. |
