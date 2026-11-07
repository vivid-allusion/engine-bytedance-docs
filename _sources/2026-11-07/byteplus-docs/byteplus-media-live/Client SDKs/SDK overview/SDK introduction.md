---
title: "SDK introduction"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction"
---

BytePlus MediaLive provides the Player SDK for Android, iOS, React Native, and Flutter.

BytePlus MediaLive SDKs provide three types of licenses: basic, premium, and trial.


* **Basic license**: Suitable for live streaming scenarios that require only basic stream pulling features, such as sports events, entertainment, e\-commerce, and education.

* **Premium license**: Suitable for live streaming scenarios that require basic stream pulling features as well as advanced features such as Adaptive Bitrate (ABR) streaming, Super\-resolution (SR), and [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media). For more information, see [Features](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction#2a8ebace).

* **Trial license**: Suitable for trial scenarios such as testing. It includes all features of BytePlus MediaLive SDKs.


<span id="2a8ebace"></span>
## Features

The features supported by Player SDK are as follows.


|Feature ||Description |Android & iOS |Flutter |React Native |
|---|---|---|---|---|---|
|Playback format |FLV |Supports playing FLV streams with a latency of 6 to 10 seconds. |Supported |Supported |Supported |
||FLV (low latency) |Supports playing FLV streams with a latency of 2 to 3 seconds. |Only supported by the premium or trial license |Not supported |Not supported |
||HLS |Supports playing HLS streams. |Supported |Supported |Supported |
||RTM |Supports playing high\-concurrency, low\-latency RTM streams. |Only supported by the premium or trial license |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Audio\-only or video\-only streams are not supported.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Audio\-only or video\-only streams are not supported.</div><br> |
||RTMP |Supports playing RTMP streams. |Supported |Supported |Supported |
||CMAF |Supports playing CMAF streams. |* iOS: Not supported<br><br>* Android: Only supported by the premium or trial license |* iOS: Not supported<br><br>* Android: Supported |* iOS: Not supported<br><br>* Android: Supported |
|Transmission protocol |TCP |Supports TCP protocol. |Supported |Supported |Supported |
||QUIC |Supports the QUIC protocol, effectively improving video transmission efficiency. |Only supported by the premium or trial license |Supported |Supported |
||TLS |Supports TLS protocol. |Supported |Supported |Supported |
||HTTP 2.0 |Supports HTTP 2.0 protocol.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">RTM streams are not supported.</div><br> |Supported |Supported |Supported |
||HTTP header |Supports custom HTTP headers when requesting video resources. |Supported |Not supported |Supported |
|Video decoding |H.264 hardware decoding |Supports H.264 hardware decoding. |Supported |Supported |Supported |
||H.264 software decoding |Supports H.264 software decoding. |Supported |Supported |Supported |
||H.265 hardware decoding |Supports H.265 hardware decoding. By optimizing the usage of H.265 hardware decoding through features such as device blocklists and smart playback strategies, it reduces live streaming costs and enhances video quality when used with H.265 transcoding. |Only supported by the premium or trial license |Only supported by the premium or trial license |Only supported by the premium or trial license |
||H.265 software decoding |Supports H.265 software decoding to improve compatibility with low\-end devices, helping reduce live streaming costs and enhance the viewing experience. |Only supported by the premium or trial license |Only supported by the premium or trial license |Only supported by the premium or trial license |
||H.265 downgrade |If H.265 hardware decoding fails, the player automatically falls back by first attempting to switch to a configured H.264 backup stream, and if that is not available, attempting to use H.265 software decoding. |Supported |Supported |Supported |
||H.266 software decoding |Supports H.266 software decoding to improve compatibility with low\-end devices, helping reduce live streaming costs and enhance the viewing experience. |* iOS: Not supported<br><br>* Android: Only supported by the premium or trial license |Not supported |Not supported |
||AAC\-HE |Supports AAC\-HE audio encoding format. |Supported |Supported |Supported |
||AAC\-LC |Supports AAC\-LC audio encoding format. |Supported |Supported |Supported |
|Playback control |Start and stop playback |Supports starting or stopping playback. |Supported |Supported |Supported |
||Pause and resume playback |Supports pausing or resuming playback. |Supported |Supported |Supported |
||Get current playback status |Supports getting the current playback status. |Supported |Supported |Supported |
||Manual quality switching |Supports manual switching between different quality levels. |Supported |Not supported |Supported |
||Set player buffer time |The player pre\-downloads a certain amount of data to ensure continuity and smoothness of playback. The longer the buffer time, the better the player can maintain uninterrupted video or audio playback during network fluctuations or latency.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To implement this feature, contact BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">technical support</a>.</div><br> |Supported |Not supported |Supported |
|Video effects |Configure rendering view |Configure the rendering view to display the player's video. |Supported |Supported |Supported |
||Screen fill mode |Supports adjusting the fill mode of the playback screen. |Supported |Supported |Supported |
||Screen rotation angle |Supports configuring the rotation angle of the playback screen, allowing clockwise rotation at 0°, 90°, 180°, and 270°. |Supported |Supported |Supported |
||Mirroring |Supports configuring the mirroring mode of the playback screen, such as horizontal and vertical mirroring. |Supported |Not supported |Supported |
||Picture\-in\-Picture (PiP) playback |By minimizing the player window and placing it in a corner of the interface, the audience can browse other content or open other apps while watching the live stream, enhancing user experience. |Supported |Supported |Supported |
||SDR (Standard Dynamic Range) video playback |Supports the playback of SDR video. |Supported |Supported |Supported |
||Super\-resolution |Super\-resolution refers to the process of reconstructing high\-resolution images from observed low\-resolution ones. Real\-time mobile super\-resolution utilizes algorithmic techniques to reconstruct low\-resolution frames in real time on the device, producing high\-resolution frames displayed on the screen. This improves the detail and contrast of video content, optimizing the overall clarity and viewing experience. |Only supported by the premium or trial license |Not supported |Only supported by the premium or trial license |
||Video sharpening |Video sharpening is an image processing technique used to enhance the clarity and detail of video images. Through sharpening, the edges and details within the video become more pronounced, making the visuals appear clearer and more vivid. |Only supported by the premium or trial license |Not supported |Supported |
|Audio effects |Volume adjustment |Supports adjusting the playback volume. |Supported |Supported |Supported |
||Mute |Supports muted playback. |Supported |Supported |Supported |
||Get mute status |Supports getting the current mute status. |Supported |Supported |Supported |
||Background audio playback |Allows audio to continue playing when the app switches to the background. |Supported |Supported |Supported |
||Pure audio playback |Supports playing pure audio. |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Applicable only to FLV and RTM streams.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Applicable only to FLV streams.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Applicable only to FLV streams.</div><br> |
||Stereo audio |Supports playing stereo audio. |Supported |Supported |Supported |
|Playback strategy |Retry on playback failure |If the live stream is interrupted due to network issues or other problems, the player attempts to retry. |Supported |Supported |Supported |
||Local DNS pre\-resolution |Enabling local DNS pre\-resolution can optimize the player's startup time. |Supported |Supported |Supported |
||Configure one or more playback addresses |Supports configuring one or more playback addresses. By configuring multiple playback addresses, features that rely on multiple streams, such as ABR streaming and primary\-backup stream switching, can be achieved. |Supported |Supported |Supported |
||ABR streaming |ABR is a streaming technology that uses a series of algorithmic strategies to dynamically switch between different quality media streams. This adaptation to network bandwidth changes helps prevent stuttering during the live stream and enhances both playback quality and viewing experience. |Only supported by the premium or trial license<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Applicable only to RTM\-ABR and FLV streams.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Applicable only to FLV streams.</div><br> |Supported<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Applicable only to FLV streams.</div><br> |
||IP address streaming |Supports streaming by using the IP address of the playback domain directly to reduce the time to the first frame. |Supported |Not supported |Supported |
||Primary\-backup stream switching |If the primary stream address fails or encounters playback errors, the player automatically switches to the backup stream address. If the backup stream address fails or encounters playback errors, the player switches back to the primary stream address. |Only supported by the premium or trial license |Supported |Supported |
||Multiple instances |Supports adding multiple players to one interface for simultaneous playback. |Supported |Supported |Supported |
||Dynamic frame chasing |During the live stream, video streams may experience latency or stuttering due to network fluctuations or other factors. Dynamic frame chasing technology adjusts the playback speed of frames or skips certain frames to synchronize with the live stream, reducing latency. |Supported |Supported |Supported |
||Instant playback optimization |Reduces the time to first frame to achieve instant playback.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To implement this feature, contact BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">technical support</a>.</div><br> |Supported |Not supported |Supported |
|Additional features |Screenshots |Supports capturing the current live\-stream image within the player. |Supported |Not supported |Supported |
||SEI message reception |SEI embeds text data within the audio and video stream, which is sent by the host and received by the audience, ensuring precise synchronization between the text and the audio/video content. |Only supported by the premium or trial license |Supported |Supported |
||Configure event listeners |By configuring event listeners, you can receive internal status information from the player, including playback status, error information, audio/video first\-frame callbacks, and periodic statistical data. |Supported |Supported |Supported |
||Subscribe to audio and video data |Subscribe to receive decoded audio and video frames for custom processing or rendering. |Supported |Not supported |Not supported |
|Video security |Commercial DRM (Digital Rights Management) |Supports playing DRM\-encrypted streams by providing DRM solutions including Widevine, FairPlay, and PlayReady. |Only supported by the premium or trial license |Not supported |Not supported |
|Quality assurance |Log reporting |Supports reporting SDK logs, and collecting and analyzing playback tracking data related to audio and video live streaming. |Supported |Supported |Supported |


<span id="db2409b9"></span>
## Using the SDKs

The following table lists the topics you may find useful while integrating each SDK:


|**SDK** |**Topics** |
|---|---|
|Player SDK for Android |* [Integrating the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android)<br><br>* [Initializing the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android)<br><br>* [Player SDK for Android: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2)<br><br>* [Player SDK for Android: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)<br><br>* [Player SDK for Android: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-overview) |
|Player SDK for iOS |* [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios)<br><br>* [Initializing the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios)<br><br>* [Player SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3)<br><br>* [Player SDK for iOS: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)<br><br>* [Player SDK for iOS: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-overview) |
|Player SDK for React Native |* [Integrating the Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn)<br><br>* [Initializing the Player SDK for React Native](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn)<br><br>* [Player SDK for React Native: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-basic-features)<br><br>* [Player SDK for React Native: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features)<br><br>* [Player SDK for React Native: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api-overview) |
|Player SDK for Flutter |* [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* [Initializing the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter)<br><br>* [Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features)<br><br>* [Player SDK for Flutter: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features) |


<span id="f202fd8c"></span>
## Glossary

For explanations of terms related to the SDKs, refer to the [Glossary](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary).
