---
title: "Send Simulcast Streams in V3.58 and Earlier Versions"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70139"
---

For the same video stream, the publisher can use the Simulcast feature to simultaneously encode and push multiple video streams with the same content yet different specifications to other users in the room at the same time. This meets the different needs of the subscriber.

<span id="applicable-scenarios"></span>
## Applicable scenarios

You may need to use the Simulcast feature in the following scenarios:


* High\-resolution video streaming stutters under a poor network connection.

* Sub\-optimal device performance leads to choppy decoding of high\-resolution video streams;

* The video profile should be set according to the receiver's window size. For example, use high\-resolution streams for full\-screen display and standard\-definition streams for smaller windows.


<span id="prerequisites"></span>
## Prerequisites


* Contact technical support to enable the allowlist.

* You have integrated the RTC SDK and implemented basic audio and video calls.

   * Native SDK V3.36 to V3.58

   * Web SDK V4.42 to V4.62


<span id="settings-on-publishers"></span>
## Publisher\-Side Settings

A single publisher can use the RTC SDK to send up to 4 video streams with different encoding specifications to meet the needs of various subscribers. You can:

> Web SDK supports up to 3 video streams with different specifications.


* Call `setVideoEncoderConfig` to set 1 video stream with the maximum resolution you intend to publish (the high\-quality stream). The default video stream parameters are:

   * Resolution: 640px × 360px

   * Frame rate: 15fps

   * Bit rate: 600kbps

* Before entering the room, call `setLocalSimulcastMode(mode)` to enable the Simulcast feature. By default, one low stream is set with the following parameters:

   * Resolution: 160px × 90px

   * Frame rate: 15fps

* If you need to specify the encoding parameters of these video streams, call `setLocalSimulcastMode(mode, streamConfig)` before entering the room to enable and set up to 3 video stream parameters, including resolution upper limits. Set the poor, low, and medium stream video parameters in sequence.

   You need to ensure that the video width, height, and bit rate of the video stream are all lower than the previous level.

   You can refer to the following table to set the video stream encoding parameters for high, medium, low, and poor streams respectively.

   
   |Video stream level |Height (px) |Width (px) |Frame rate (fps) |Maximum bit rate (kbps) |
   |---|---|---|---|---|
   |High stream |1920 |1080 |30 |3000 |
   ||1280 |720 |30 |1200 |
   ||1120 |630 |30 |1000 |
   ||960 |540 |30 |900 |
   |Medium stream |800 |450 |30 |800 |
   ||640 |360 |30 |600 |
   ||480 |270 |15 |400 |
   |Low stream |320 |180 |15 |300 |
   ||256 |144 |15 |200 |
   |Poor stream |160 |90 |15 |100 |
   

> Note: When stream fallback is enabled, the published video stream will be degraded according to the network environment and the above table. For details, please refer to the [Stream fallback](https://docs.byteplus.com/en/docs/12/docs-70137). Otherwise, the SDK will only send the stream with a set resolution value.


<span id="subscribe-to-multi-resolution-video-streams"></span>
## Subscribe to multi\-resolution video streams

The subscriber can call `setRemoteVideoConfig` to set the expected resolution of the video stream to subscribe to.


* If the publisher has enabled the Simulcast feature, the subscriber can choose to subscribe to video streams of different resolutions based on their network conditions, device performance, and more.

* If the publisher has not enabled the Simulcast feature, the subscriber's settings will have no effect, and they can only receive the video stream published by the publisher.


<span id="use-server-side-configuration"></span>
## Use server\-side configuration

You can enable the Simulcast feature for users in a specified room by using server\-side configuration.

Server\-side configuration has a higher priority than client\-side settings. If you enable simulcast via server\-side configuration, it is active for the client even without a corresponding API call.

<span id="video-stream-level-division-examples"></span>
## Video Stream Level Examples

<span id="publisher"></span>
### Publisher

The publisher enables the Simulcast feature and sets up 3 video streams:


* High stream: Resolution 640px × 360px, frame rate 15fps, bit rate 600kbps

* Medium stream: Resolution 480px × 270px, frame rate 15fps, bit rate 400kbps

* Low stream: Resolution 320px × 180px, frame rate 15fps, bit rate 300kbps

* Example 1: If the publisher sets 3 resolution upper limits as 720p, 360p, and 144p respectively, the level division will be automatically adjusted as shown in the table below:



|Video stream level |Height (px) |Width (px) |Frame rate (fps) |Maximum bit rate (kbps) |
|---|---|---|---|---|
|High stream |1280 |720 |30 |1200 |
||1120 |630 |30 |1000 |
||960 |540 |30 |900 |
||800 |450 |30 |800 |
|Medium stream |640 |360 |30 |600 |
||480 |270 |15 |400 |
||320 |180 |15 |300 |
|Low stream |256 |144 |15 |200 |
|Poor stream |160 |90 |15 |100 |



* Example 2: If the publisher sets 3 resolution upper limits as 720p, 630p, and 540p respectively, the level division will be automatically adjusted as shown in the table below:



|Video stream level |Length (px) |Width (px) |Frame rate (fps) |Maximum bit rate (kbps) |
|---|---|---|---|---|
|High stream |1280 |720 |30 |1200 |
|Medium stream |1120 |630 |30 |1000 |
|Low stream |960 |540 |30 |900 |
||800 |450 |30 |800 |
||640 |360 |30 |600 |
||480 |270 |15 |400 |
||320 |180 |15 |300 |
||256 |144 |15 |200 |
|Poor stream |160 |90 |15 |100 |



* Example 3: When setting up to three streams, if there is a twofold or greater difference between adjacent resolutions, the SDK automatically inserts an intermediate stream. If multiple such gaps exist, the SDK prioritizes inserting a stream between the lower\-resolution pair. For example, if the publisher sets 3 resolution upper limits as 1080p, 360p, and 90p respectively, priority will be given to inserting a level between 360p and 90p, and the level division will be automatically adjusted as shown in the table below:



|Video stream level |Height (px) |Width (px) |Frame rate (fps) |Maximum bit rate (kbps) |
|---|---|---|---|---|
|High stream |1920 |1080 |30 |3000 |
||1280 |720 |30 |1200 |
||1120 |630 |30 |1000 |
||960 |540 |30 |900 |
||800 |450 |30 |800 |
|Medium stream |640 |360 |30 |600 |
||480 |270 |15 |400 |
|Low stream |320 |180 |15 |300 |
||256 |144 |15 |200 |
|Poor stream |160 |90 |15 |100 |



* Example 4: If the publisher sets fewer than 3 resolution upper limit values, the SDK will automatically add intermediate levels. For example, when the user sets the resolution upper limit value to 360p, the level division will be automatically adjusted as shown in the table below:



|Video stream level |Length (px) |Width (px) |Frame rate (fps) |Maximum bit rate (kbps) |
|---|---|---|---|---|
|High stream |640 |360 |30 |600 |
|Medium stream |480 |270 |15 |400 |
|Low stream |320 |180 |15 |300 |
||256 |144 |15 |200 |
|Poor stream |160 |90 |15 |100 |


<span id="subscriber"></span>
### Subscriber

The subscriber can choose to subscribe to video streams of different resolutions based on their network conditions, device performance, and more.


* If the subscriber chooses to subscribe to the High stream, they will receive the High stream video published by the publisher.

* If the subscriber sets to subscribe to the medium stream, they will receive the medium stream video published by the publisher.

* If the subscriber sets to subscribe to the low stream, they will receive the low stream video published by the publisher.


When the publisher's settings are as shown in Example 1:


* Example 5: If a subscriber requests a non\-standard resolution, such as 639px × 363px, they receive the closest available stream (640px × 360px)

* Example 6: If the subscriber has three settings of 1080p, 720p, and 630p, all subscribers will ultimately receive a stream with a resolution of 1120px × 630px.


<span id="api-reference"></span>
## API References

Please refer to the [API References Archive](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-api-references-for-previous-versions).
