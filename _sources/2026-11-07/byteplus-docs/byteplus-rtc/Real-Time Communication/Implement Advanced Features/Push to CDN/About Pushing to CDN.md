---
title: "About Pushing to CDN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69821"
---

The Push to CDN feature allows you to distribute an audio or video RTC session to a wider audience via an RTMP server. You can either push a single, unprocessed stream for direct distribution or combine multiple streams from one or more rooms into a single mixed stream. This guide covers common use cases and provides detailed procedures for implementing the Push to CDN task using both SDK and Open API.


* Including a single stream: you can specify a single stream to push it to the RTMP server for further distribution through CDN without encoding and decoding during the process.

* Including multiple streams: you can combine the audio or video content from one or more rooms into one stream and push it to the RTMP server for further distribution through CDN. To achieve this, the RTC service has to decode the streams and encode the mixed stream before transcoding over RTMP and sending to the RTMP server.


<span id="use-cases"></span>
## Use cases

**Interactive live streaming**: Hosts and co\-hosting audience members can interact in real time within the same RTC room or across different rooms. Audiences outside the RTC rooms can watch the interaction.

**Online education**: During online live open classes, teachers and students in the same RTC room are allowed to conduct video interaction, and such audio or video stream of interaction can be distributed to more audiences via CDN.

<span id="pricing"></span>
## Pricing

The Push to CDN feature is billed as a value\-added service. Please refer to [Billing Rules](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69871) for detailed rates and billing rules.

<span id="d0408324"></span>
## **Try it Online**

We offer a web\-based demo that allows you to experience the feature without writing any code. [Try It Now](https://demo.byteplus.com/rtc/advance/liveTranscode)

<span id="procedure"></span>
## Procedure

You can choose to initiate the Push to CDN task with the SDK API or the Open API. The RTC service handles this task on the server.

<span id="by-sdk-api"></span>
### By SDK API

Push streams to the CDN from the server side by calling the SDK API. Please refer to [Using the Push-to-CDN Feature by Calling SDK API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69822) for details.

<span id="by-open-api-to-push-a-single-stream"></span>
### By Open API to push a single stream

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/69821_api_single_en.png) </span>


1. Enable **Push to CDN** in the [RTC console](https://console.byteplus.com/rtc/cloudRTC?&tab=live).

2. (Optional) Add the `Push to CDN` event to the [notification service](https://console.byteplus.com/rtc/cloudRTC?&tab=callback) to receive the task status notification.

3. Initiate the Push to CDN task with [StartPushSingleStreamToCDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153583).

4. (Optional) Query the task status using [GetPushSingleStreamToCDNTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-3w06olaa6w).

5. End the task using [StopPushStreamToCDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153582).


<span id="by-open-api-to-push-a-multiple-streams"></span>
### By Open API to push multiple streams

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/69821_api_mix_en.png) </span>


1. Enable Push to CDN in the [RTC console](https://console.byteplus.com/rtc/cloudRTC?&tab=live).

2. (Optional) To receive the task status notification, add the `Push to CDN` event to the [notification service](https://console.byteplus.com/rtc/cloudRTC?&tab=callback).

3. Initiate the Push to CDN task with [StartPushMixedStreamToCDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69850).

4. (Optional) To update the task settings, use [UpdatePushMixedStreamToCDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69849).

5. (Optional) Query the task status using [GetPushMixedStreamToCDNTask](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-w5q4dtjbde).

6. End the task using [StopPushStreamToCDN](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153582).


<span id="faq"></span>
## FAQ

<span id="q1-in-what-circumstances-do-video-frames-carry-sei-is-the-frequency-of-sei-carrying-fixed"></span>
### Q1: In what circumstances do video frames carry SEI? Is the frequency of SEI\-carrying fixed?

A1: Normally, SEI is only carried in key frames. The frequency of SEI arrival depends on the `GOP`, which you can configure. In the following scenarios, SEI is carried in additional video frames:


* RTC service will extract the SEI from the target stream and include it in the latest video frame.

* RTC service will generate a key frame with SEI on every layout change.

* When the volume indicator is on, the volume of the target stream will be included in the key frames as SEI following the interval set in `VolumeIndicationInterval`. Furthermore, any volume change of the target stream will be included in the latest video frame immediately.


<span id="q2-why-is-it-possible-that-1-video-frame-from-a-push-to-cdn-stream-carries-multiple-sei-sent-through-rtc-sdk-api"></span>
### Q2: Why can a single video frame in a Push to CDN stream carry multiple SEI messages sent via the RTC SDK API?

A2: In the Push to CDN scenario, if a user calls `sendSEIMessage` of RTC SDK API to insert SEI, the Push to CDN server\-side will subscribe to the user's streams and extract SEI from the video frames for passthrough. In case that one single user sends multiple SEI messages by calling `sendSEIMessage` in a short period, or that multiple users call `sendSEIMessage` to send SEI messages at the same time, the Push to CDN server\-side will pass through all SEI messages from the subscribed streams, which may cause multiple SEI included in 1 video frame of the Push to CDN stream.

<span id="q3-why-is-there-sei-passed-through-from-rtc-client-side-and-auto-generated-sei-from-server-side-in-the-sei-of-a-push-to-cdn-stream"></span>
### Q3: Why does the SEI in a Push to CDN stream contain data from both the RTC client and the server?

A3: When server\-side generates SEI automatically while a user calls `sendSEIMessage` of client\-side SDK API to insert SEI at the same time, multiple SEI will be included in the Push to CDN stream.
