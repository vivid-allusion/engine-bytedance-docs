---
title: "Publish and Subscribe to Public Streams"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-108930"
---

<span id="introduction"></span>
## Introduction

Public streams allow users with the same `appID` to subscribe and play a stream without entering the room, which is ideal for scenarios with a large audience and low interaction, such as


* large\-scale video classrooms

* live shopping.


This guide provides the client\-side implementation steps and code examples you need to publish and subscribe to public streams.

<span id="prerequisite"></span>
## Prerequisite

You have integrated the RTC SDK for basic real\-time functions.

Native: Supported starting from v3.56

Web: Supported starting from v4.60

> The information provided in this article is applicable to the versions before Native SDK V3.60 and Web SDK V4.65.


<span id="api-call-sequence"></span>
## API call sequence

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTC_Communication/publicstreamimplementation.png) </span>

> Note: The steps are the same on different platforms, but the interface and parameter names may differ slightly. The following guide takes the Android RTC SDK as an example. You can refer to the API doc of the corresponding platform for more information.


<span id="to-publish-a-public-stream"></span>
## To publish a public stream


1. Enter the room.


```java
public int joinRoom(String token, UserInfo userInfo, boolean userVisibility, RTCRoomConfig config) {
        return 0;
}
```



2. Call `startPushMixedStream` to start publishing the WTN stream. In addition to the specified `taskId`, you also need to provide the following parameters.

   * `taskId`: Identifies a live stream relay task when `PushTargetType` in `MixedStreamConfig` is 0.

   * `pushTargetConfig`: Configuration parameters for the streaming target, such as setting the streaming address and WTN stream ID. For details, see `MixedStreamPushTargetConfig`.

   * `mixedConfig`: Configuration parameters for live stream forwarding, such as setting merged images, video view layouts, and audio properties.


Sample code for Android:

```java
public int startPushMixedStream(String publicStreamId) {
    MixedStreamPushTargetConfig targetConfig = new MixedStreamPushTargetConfig();
   targetConfig.pushTargetType = MixedStreamPushTargetType.PUSH_TO_WTN;
   targetConfig.pushWTNStreamID = streamID;

   MixedStreamConfig mixedStreamConfig = MixedStreamConfig.defaultMixedStreamConfig();
   mixedStreamConfig.userID = userID_of_task_initiator;
   mixedStreamConfig.roomID = roomID;
   //Video-related parameters
   mixedStreamConfig.videoConfig.width = 360;
   mixedStreamConfig.videoConfig.height = 640;
   mixedStreamConfig.videoConfig.fps = 15;
   mixedStreamConfig.videoConfig.bitrate = 500000;
   //Audio-related parameters
   mixedStreamConfig.audioConfig.channels = 2;
   mixedStreamConfig.audioConfig.sampleRate = 48000;
   mixedStreamConfig.audioConfig.bitrate = 64;
   //Layout-related parameters, using 2 users as an example
   mixedStreamConfig.regions = new MixedStreamLayoutRegionConfig[2];
   for (int i = 0; i < 2; ++i) {
      MixedStreamLayoutRegionConfig region = new MixedStreamLayoutRegionConfig();
      region.roomID = roomID_of_the_ith_user;
      region.userID = userID_of_the_ith_user;
      region.locationX = x_coordinate_of_the_top_left_corner_of_the_ith_video;
      region.locationY = y_coordinate_of_the_top_left_corner_of_the_ith_video;
      region.width = width_of_the_ith_video;
      region.height = height_of_the_ith_video;
      region.alpha = 1;
      region.zOrder = (layer_number_after_composition);
      region.renderMode = (MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
      region.streamType = (MixedStreamVideoType.MIXED_STREAM_VIDEO_TYPE_MAIN);
      region.mediaType = (MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO);
      mixedStreamConfig.regions[i] = region;
   }
   return rtcEngine.startPushMixedStream(taskID, targetConfig, mixedStreamConfig);
}
```


Sample code for iOS:

```objectivec

- (void)startPushPublicStream:(NSString *_Nonnull)streamId {
    ByteRTCMixedStreamPushTargetConfig *targetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
    targetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToWTN;
    targetConfig.pushWTNStreamID = streamID;
    
    ByteRTCMixedStreamConfig *streamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
    streamConfig.userID = @"userID_of_task_initiator";
    streamConfig.roomID = @"roomID";
    //Video-related parameters
    streamConfig.videoConfig.width = 360;
    streamConfig.videoConfig.height = 640;
    streamConfig.videoConfig.fps = 15;
    streamConfig.videoConfig.bitrate = 500000;
    //Audio-related parameters
    streamConfig.audioConfig.channels = 2;
    streamConfig.audioConfig.sampleRate = 48000;
    streamConfig.audioConfig.bitrate = 64;
    //Layout-related parameters, using 2 users as an example
    NSMutableArray<ByteRTCMixedStreamLayoutRegionConfig *> *regions = [[NSMutableArray alloc] init];
    for (int i = 0; i < 2; ++i) {
        ByteRTCMixedStreamLayoutRegionConfig *region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
        region.roomID = roomID_of_the_ith_user;
        region.userID = userID_of_the_ith_user;
        region.locationX = x_coordinate_of_the_top_left_corner_of_the_ith_video;
        region.locationY = y_coordinate_of_the_top_left_corner_of_the_ith_video;
        region.width = width_of_the_ith_video;
        region.height = height_of_the_ith_video;
        region.alpha = 1;
        region.zOrder = layer_number_after_composition;
        region.renderMode = ByteRTCMixedStreamRenderModeHidden;
        region.streamType = ByteRTCMixedStreamVideoTypeMain;
        region.mediaType = ByteRTCMixedStreamMediaTypeAudioAndVideo;
        [regions addObject:region];
    }
    streamConfig.regions = regions;
    [self.rtcEngine startPushMixedStream:@"taskId" withPushTargetConfig:targetConfig withMixedConfig:streamConfig];
```



3. Call `stopPushMixedStream` to stop publishing the WTN stream.


```java
public int stopPushMixedStream(String taskId) {
   if (mRtcEngine != null) {
      mRtcEngine.stopPushMixedStream(taskId, MixedStreamPushTargetType.PUSH_TO_WTN);
   }
  return 0;
}
```


<span id="to-subscribe-to-a-public-stream"></span>
## To subscribe to a public stream


1. Call `setWTNRemoteVideoCanvas` to bind the internal view. If you need to unbind the view, set `videoCanvas` to null.

> If you need to use an external renderer, call `setWTNRemoteVideoSink`. For more information, see [Custom Video Rendering](https://docs.byteplus.com/en/docs/12/docs-81201).


```java
public int setWTNRemoteVideoCanvas(String streamId, VideoCanvas canvas) {...}
```



2. Call `subscribeWTNVideoStream` to subscribe to the WTN stream.

> One client can play up to 5 public streams simultaneously. To avoid exceeding the maximum number of subscribed public streams, call `subscribeWTNVideoStream(subscribe=false)` promptly.


```java
public int subscribeWTNVideoStream(String streamId, boolean subscribe) {...}
```



3. Calling `sendSEIMessage` on the publisher's client inserts the SEI into the video frame, and the SEI in the stream is then transmitted and merged into the public stream.

   * The public stream adds SEI data to 30 consecutive video frames starting from the current video frame, improving the reliability of the SEI.

   * When multiple video streams contain SEI, the SEI in each stream will be transmitted transparently to the public stream. However, a single video frame in the public stream is allowed to carry no more than 4 KB of SEI. If the combined SEI information exceeds 4 KB, the RTC will discard the excess. For example, A, B, and C are the SEI carried in the video frame of the three video streams that make up the public stream. When `A + B + C > 4 KB` and `A + B < 4 KB`, the public stream will only carry the SEI data from streams A and B.

   * You must implement the SEI processing logic.


```java
public void onWTNRemoteSEIMessageReceived(String streamId, ByteBuffer message) {
    RTCCallEngineController controller = getController();
    String callbackLog = "onWTNRemoteSEIMessageReceived[streamid:" + streamId

                    + " sei:" + RtmpUrlUtils.byteBufferToString(message) + "]";
    controller.log(callbackLog);
}
```



4. Call `subscribeWTNVideoStream(subscribe=false)` to unsubscribe from the public stream.


```java
public int subscribeWTNVideoStream(String streamId, boolean subscribe) {...}
```


<span id="api-reference"></span>
## API reference


|Funtion |Android |iOS |
|---|---|---|
|Publish WTN stream |[startPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#startpushmixedstream) |[startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#startpushmixedstream-withpushtargetconfig-withmixedconfig) |
|Stop publishing WTN stream |[stopPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#stoppushmixedstream) |[stopPushMixedStream:withPushTargetType:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stoppushmixedstream-withpushtargettype) |
|Update WTN stream publishing parameters |[updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#updatepushmixedstream) |[updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig) |
|Subscribe/unsubscribe WTN stream |[subscribeWTNVideoStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#IWTNStream-subscribewtnvideostream) |[subscribeWTNVideoStream:subscribe:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCWTNStream-subscribewtnvideostream-subscribe) |
|Bind WTN stream playback view |[setWTNRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#IWTNStream-setwtnremotevideocanvas) |[setWTNRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCWTNStream-setwtnremotevideocanvas-withcanvas) |
|Bind external renderer for WTN stream |[setWTNRemoteVideoSink](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#setwtnremotevideosink) |[setWTNRemoteVideoSink:withSink:withConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#setwtnremotevideosink-withsink-withconfig) |
|Receive SEI information contained in WTN stream |[onWTNSEIMessageReceived](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onwtnseimessagereceived) |[onWTNSEIMessageReceived:andChannelId:andMessage:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#onwtnseimessagereceived-andchannelid-andmessage) |
