---
title: "Set Subscription Mode"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-129241"
---

In real\-time audio and video interactions, after users enter an RTC room, they need to subscribe to the corresponding media streams to watch other users' videos, shared screens, and listen to audio. Depending on the number of participants and use cases, there are usually different requirements for subscription relationships. This article provides guidance on how to subscribe to media streams on the client side in different scenarios.

> This article applies to SDK version V3.60 and later.


<span id="feature-description"></span>
## Feature description


* Subscribe to media streams

   You need to subscribe to published media streams in the room to listen to other users' audio and watch their videos. Media streams include audio streams captured by microphones and video streams captured by cameras, as well as video and audio streams from screen sharing.

* Set subscription mode

   You can choose automatic subscription or manual subscription mode when joining a room. After joining the room, you can modify the subscription mode through `subscribeAllStreamsAudio` or `subscribeAllStreamsVideo`.

   * Automatic subscription: The SDK will automatically subscribe to published media streams in the room.

      * When users join the room, they automatically subscribe to audio streams being published in the room.

      * When other users join the room and publish streams, your client automatically subscribes to the newly added streams.

   * Manual subscription: Unlike automatic subscription, this mode requires you to manually subscribe to specific media streams by calling APIs.


<span id="scenario-1-online-education"></span>
## Scenario 1: Online education

In scenarios like online classrooms, where speaking privileges must be managed, you need to control which users can be heard.


1. Call `joinRoom` to join the room, select user visibility and set automatic publishing and **manual** subscription mode.


```java
// User can publish streams
boolean userVisibility = true;
// Automatic publishing
boolean isPublishAudio = true;
boolean isPublishVideo = true;
// Manual audio subscription
boolean isAutoSubscribeAudio = false;
// Automatic video subscription
boolean isAutoSubscribeVideo = true;
RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_CHAT_ROOM, isPublishAudio, isPublishVideo, isAutoSubscribeAudio, isAutoSubscribeVideo);
// Join room
rtcRoom1.joinRoom(token, userInfo, userVisibility, roomConfig);
```



2. Manually subscribe to the audio stream published by the teacher.


```java
rtcRoom1.subscribeStreamAudio(user_id_1, true);
```



3. Manually subscribe to the audio stream of the designated speaker. After the user finishes speaking, cancel the subscription to their stream.


```java
// Subscribe to the audio stream published by the student
rtcRoom1.subscribeStreamAudio(user_id_2, true);
// Speaking ends, cancel subscription
rtcRoom1.subscribeStreamAudio(user_id_2, false);
```


<span id="scenario-2-call-interruption-and-resumption"></span>
## Scenario 2: Call interruption and resumption

During real\-time audio and video calls, the audio and video modules may be interrupted by system phone calls, third\-party applications, or other system behaviors. At this time, you need to pay attention to the remote audio and video playback status when interrupting and resuming. For details, see [Call Interruption and Resumption](https://docs.byteplus.com/en/docs/12/docs-111590). For interruptions that cannot be automatically restored, you can handle them in the following ways:


1. When users start using system or third\-party applications that will occupy the device's audio and video modules, call [pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#pauseallsubscribedstreamvideo) and/or [pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#pauseallsubscribedstreamaudio) to pause subscription to all users' video/audio streams.

2. When users finish using system or third\-party applications, call [resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#resumeallsubscribedstreamvideo) and/or [resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#resumeallsubscribedstreamaudio) to restore the subscription state before the interruption.


<span id="scenario-3-scene-switching-during-calls"></span>
## Scenario 3: Scene switching during calls

During real\-time audio and video calls, scene switching may be required. For example, to increase interaction and fun, a karaoke singing competition segment is added to the voice chat scenario. After a user becomes the active speaker by clicking a button, all other users in the room need to subscribe to that user's stream.


1. Call `joinRoom` to join the room, select user visibility and set automatic publishing and automatic subscription mode. After users enter the room, they automatically subscribe to all streams in the room for voice chat calls.


```java
// User can publish streams
boolean userVisibility = true;
// Automatic audio publishing
boolean isPublishAudio = true;
// Voice chat room does not need to publish video
boolean isPublishVideo = false;
// Automatic audio subscription
boolean isAutoSubscribeAudio = true;
// Voice chat room does not need to subscribe to video
boolean isAutoSubscribeVideo = true;
RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_CHAT_ROOM, isPublishAudio, isPublishVideo, isAutoSubscribeAudio, isAutoSubscribeVideo);
// Join room
rtcRoom1.joinRoom(token, userInfo, userVisibility, roomConfig);
```



2. When the karaoke activity starts and user A becomes the active speaker, other users should first call `subscribeAllStreamsAudio` to cancel all current subscriptions, and then call `subscribeStreamAudio` to manually subscribe only to user A's stream.

3. When the singing competition segment ends, all users in the room call `subscribeAllStreamsAudio` to subscribe to all streams in the room and continue voice chat calls.


<span id="scenario-4-audio-selection"></span>
## Scenario 4: Audio selection

In some large\-scale meetings and interactive entertainment scenarios, thousands of users in the same room may need to participate in audio and video interactions simultaneously. When there is no need to specify subscriptions, we recommend enabling the audio selection feature through the console. Once enabled, the audio subscription relationships of users in the room will be intelligently managed by RTC, which will push streams to you from users with the highest audio levels in the room.

In this scenario, we still recommend choosing automatic subscription mode to ensure you can receive the selected streams. Additionally, this mode supports manually unsubscribing from streams \- after calling this, you will not receive a stream even if the unsubscribed stream is selected.

For more detailed information about audio selection, see [Audio Selection](https://docs.byteplus.com/en/docs/12/docs-113547).

<span id="api-reference"></span>
## API reference

You can flexibly combine and use the following APIs to implement more audio and video interactive features.


|Description |Android |iOS |macOS |Windows |Linux |
|---|---|---|---|---|---|
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#joinroom-userinfo-uservisibility-roomconfig) |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#joinroom-userinfo-uservisibility-roomconfig) |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-joinroom) |
|Subscribe/unsubscribe to specified video streams in the room, captured by camera |[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#subscribestreamvideo) |[subscribeStreamVideo:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#subscribestreamvideo-subscribe) |[subscribeStreamVideo:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70092#subscribestreamvideo-subscribe) |[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribestreamvideo) |[subscribeStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamvideo) |
|Subscribe/unsubscribe to specified audio streams in the room, captured by microphone |[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#subscribestreamaudio) |[subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70086#subscribestreamaudio-subscribe) |[subscribeStreamAudio:subscribe:](https://docs.byteplus.com/en/docs/12/docs-70092#subscribestreamaudio-subscribe) |[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribestreamaudio) |[subscribeStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribestreamaudio) |
|Subscribe/unsubscribe to all video streams in the room |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70080#subscribeallstreamssvideo) |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70086#subscribeallstreamsvideo) |[subscribeAllStreamsVideo:](https://docs.byteplus.com/en/docs/12/docs-70092#subscribeallstreamsvideo) |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribeallstreamsvideo) |[subscribeAllStreamsVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribeallstreamsvideo) |
|Subscribe/unsubscribe to all audio streams in the room |[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-70080#subscribeallstreamsaudio) |[subscribeAllStreamsAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#subscribeallstreamsaudio) |[subscribeAllStreamsAudio:](https://docs.byteplus.com/en/docs/12/docs-70092#subscribeallstreamsaudio) |[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-subscribeallstreamsaudio) |[subscribeAllStreamsAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-subscribeallstreamsaudio) |
|Pause subscription to video streams from remote users |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#pauseallsubscribedstreamvideo) |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70086#pauseallsubscribedstreamvideo) |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70092#pauseallsubscribedstreamvideo) |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamvideo) |[pauseAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseallsubscribedstreamvideo) |
|Pause subscription to audio streams from remote users |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#pauseallsubscribedstreamaudio) |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70086#pauseallsubscribedstreamaudio) |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70092#pauseallsubscribedstreamaudio) |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-pauseallsubscribedstreamaudio) |[pauseAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-pauseallsubscribedstreamaudio) |
|Resume subscription to video streams from remote |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70080#resumeallsubscribedstreamvideo) |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70086#resumeallsubscribedstreamvideo) |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70092#resumeallsubscribedstreamvideo) |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamvideo) |[resumeAllSubscribedStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeallsubscribedstreamvideo) |
|Resume subscription to audio streams from remote |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70080#resumeallsubscribedstreamaudio) |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70086#resumeallsubscribedstreamaudio) |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70092#resumeallsubscribedstreamaudio) |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-resumeallsubscribedstreamaudio) |[resumeAllSubscribedStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-resumeallsubscribedstreamaudio) |


<span id="faq"></span>
## FAQ

<span id="_1-will-billing-continue-during-the-pause-of-media-stream-subscription"></span>
### 1. Will billing continue during the pause of media stream subscription?

A: No. Whether you unsubscribe from media streams or pause media stream subscription through `pauseAllSubscribedStreamVideo` or `pauseAllSubscribedStreamAudio`, the user will not incur charges for subscribing to media streams during the pause period.

<span id="_2-what-is-the-difference-between-pausing-a-subscription-and-unsubscribing-and-when-should-you-use-each-method"></span>
### 2. What is the difference between pausing a subscription and unsubscribing, and when should you use each method?

A: Both pausing (`pauseAllSubscribedStreamVideo` or `pauseAllSubscribedStreamAudio`, hereinafter referred to as "pause all subscriptions") and unsubscribing from all media streams (`subscribeAllStreamsVideo` or `subscribeAllStreamsAudio`, hereinafter referred to as "unsubscribe all") can be used to pause subscriptions to media streams.


* Pause and resume all media stream subscriptions (`resumeAllSubscribedStreamVideo` or `resumeAllSubscribedStreamAudio`, hereinafter referred to as "resume all subscriptions") APIs must be used in pairs. While the subscribe all APIs can be used independently.

* After calling the resume all subscriptions API, it will restore to the subscription state before calling the pause all media streams API. While the subscribe all media streams API both updates the user's automatic subscription state in the room and simultaneously subscribes to all streams in the room.


Therefore, pause all subscriptions and resume all subscriptions are suitable for scenarios where you need to continue subscribing after pausing, such as when an RTC application is interrupted by a system call and then resumes audio and video interaction. You can directly restore through the resume all subscriptions API without needing to record the subscription relationships before pausing.

While the subscribe all and unsubscribe all APIs are suitable for implementing scene switching within the same room, such as switching from free speech to designated user speech.
