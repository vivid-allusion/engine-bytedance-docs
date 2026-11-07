---
title: "Supplemental Enhancement Information (SEI)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70140"
---

To send time\-synchronized metadata like lyrics or game data with your audio and video streams, you can use Supplemental Enhancement Information (SEI). This guide provides detailed instructions for multiple implementation methods, helping you choose the best solution for your needs. You will learn how to insert SEI into SDK\-captured or external video streams, use audio RTP header extensions for audio\-only scenarios, and embed SEI in mixed streams for CDN delivery.

You can insert SEI (Supplemental Enhancement Information) into H.264 video streams and receive such information on the subscription\-side.

Besides, you can also send data information through the **audio RTP header extension**.

You should pick an applicable solution to implement the feature based on your business needs.

## Use cases

* Online Karaoke scenario where lyric synchronization, progress display, and certain information are needed.

* In duel shows where two hosts compete, the audience can see which host is currently streaming and decide whether to load that host's video feed. Health bars are displayed in real time based on the SEI.

* Real\-time communication during game play

   * Compressed algorithmic data for facial recognition is transferred with SEI, and the receiving client uses this data to render corresponding video effects.

   * In live streaming question\-and\-answer games, when hosts announce questions, the questions can be synchronized to remote clients, allowing users to submit their answers.

   * Viewers are able to perceive the layout information of the streaming images and determine if any co\-host has joined the game and whether to load or unload the co\-host seat widget.

   * Volume information for each stream can be acquired and used to show users' volume in the push of the mixed stream to CDN.

* When external encoders and decoders are used, it can be used to transmit encoder parameters.

* When custom video capture is enabled, it can be used to transmit camera parameters.

## Prerequisite

You have already integrated the RTC SDK and are able to implement basic audio and video calls.

## Insert SEI into SDK\-captured video streams

With the SDK's internal video capture, you can insert various types of client\-side information into video or audio\-only apps, such as lyrics, progress, questions, and more.

In a Push to CDN scenario, SEI added by means of this solution is also passed through to the mixed stream to show the volume, health bars, and other information for each party.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/70140_external.png)

1. Make sure that an internal video capture module is currently in use: `VIDEO_SOURCE_TYPE_INTERNAL`. Internal capturing is enabled by default, but if external capturing is currently in use, you should first call `setVideoSourceType` to configure the video source and screen streams.

2. The sending side calls the SEI sending interface `sendSEIMessage` to send SEI with video frames.

   For audio\-only apps, SDKs automatically generate black frames to carry SEI messages. However, in manual launch mode, you need to launch the black frame video streams manually.

   **java**

```java
    EngineConfig config = new EngineConfig();
    config.appID = appId;
    config.context = applicationContext;
    rtcEngine = RTCEngine.createRTCEngine(config, rtcEngineEventHandler);
    rtcEngine.startAudioCapture();
    rtcEngine.startVideoCapture();
    rtcEngine.sendSEIMessage(msg.getBytes(StandardCharsets.UTF_8), 3, SEICountPerFrame.SEI_COUNT_PER_FRAME_SINGLE);
   ```

   **swift**

```swift
    let engineCfg = ByteRTCEngineConfig.init()
    engineCfg.appID = appId
    engineCfg.parameters = [:]
    self.rtcEngine = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)
    self.rtcEngine?.startVideoCapture()
    self.rtcEngine?.startAudioCapture()
    self.rtcEngine?.sendSEIMessage(data, andRepeatCount: 3, andCountPerFrame: .single)
   ```

   **cpp**

```cpp
    bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    m_engine = bytertc::IRTCEngine::createRTCEngine(conf, handler.get());
    m_engine->startAudioCapture();
    m_engine->startVideoCapture();
    m_engine->sendSEIMessage((uint8_t*)str_text.c_str(), str_text.size(), 2, bytertc::kSEICountPerFrameSingle);
   ```

3. The receiving\-side receives an SEI callback: `onSEIMessageReceived`.

4. For audio\-only apps, when black frame video streams are used to send SEI data, remote\-side users will be notified by `onSEIStreamUpdate` of the sending status of the streams. You need to subscribe to the black frame video streams under the manual subscription mode.

   **java**

```java
    IRTCEngineEventHandler rtcEngineEventHandler = new IRTCEngineEventHandler() {
        @Override
        public void onSEIMessageReceived(String streamId, StreamInfo streamInfo, ByteBuffer message) {
            Charset charset = Charset.defaultCharset();
            String dataString = charset.decode(message).toString();
            ToastUtil.showLongToast(SEIMessageActivity.this, "onSEIMessageReceived：" + dataString);
        }
        };
   ```

   **swift**

```swift
    func rtcEngine(_ engine: ByteRTCEngine, onSEIMessageReceived streamId: String, info:  ByteRTCStreamInfo, andMessage: String, length: Int) {
    }
   ```

   **cpp**

```cpp
    void ByteRTCEventHandler::onSEIMessageReceived(const char* stream_id, const bytertc::StreamInfo& stream_info, const uint8_t *message, int length){
    }
   ```

## Insert SEI into external\-sourced video streams

If your apps use external video sources, you can use the following interfaces to send and receive SEI.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/70140_sei.png)

1. Call `GLTextureVideoFrameBuilder-setExternalDataInfo` to configure SEI data of returning frames of video data in texture formats.

2. Call `CpuBufferVideoFrameBuilder-setExternalDataInfo` to configure SEI data of CpuBuffer video frames.

3. Call `pushExternalVideoFrame` to encapsulate video frame data with `VideoFrame` and then transmit it to the SDK.

4. Call `getExternalDataInfo` to acquire SEI data.

## Use audio RTP header extensions

For audio\-only call apps, the universal solution can be adopted to send SEI with black frames, but you can also use audio RTP header extensions to send this data. By using this solution, you can achieve higher sync granularity, 0\-20 ms technically, than that of the universal solution.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/70140_rtp.png)

1. Call `sendStreamSyncInfo` to send SEI.

   * The maximum length supported for SEI transmission is 255B. If you have higher requirements for message length, please refer to the universal solution.

   * RTC users' SEI data will not be pushed to CDN streams.

   * The call frequency is 50 times per second per SDK.

   **java**

```java
    private void sendMsg(String msg) {
        StreamSyncInfoConfig config = new StreamSyncInfoConfig(0, StreamSyncInfoConfig.SyncInfoStreamType.SYNC_INFO_STREAM_TYPE_AUDIO);
        rtcEngine.sendStreamSyncInfo(msg.getBytes(StandardCharsets.UTF_8), config);
    }
   ```

   **swift**

```swift
    let config = ByteRTCStreamSyncInfoConfig.init()
    config.streamType = .audio
    config.repeatCount = 0
    self.rtcEngine?.sendStreamSyncInfo(data, config: config)
   ```

   **cpp**

```cpp
    bytertc::StreamSyncInfoConfig config;
    config.stream_type = bytertc::kSyncInfoStreamTypeAudio;
    config.repeat_count = 0;
    int ret = m_engine->sendStreamSyncInfo((const uint8_t*)str.c_str(), str.size(), config);
   ```

2. Upon successful calls, remote users receive an SEI callback: `onStreamSyncInfoReceived`.

   **java**

```java
    IRTCEngineEventHandler rtcEngineEventHandler = new IRTCEngineEventHandler() {
        @Override
        public void onStreamSyncInfoReceived(String streamId, StreamInfo streamInfo, StreamSyncInfoConfig.SyncInfoStreamType streamType, ByteBuffer data) {
            super.onStreamSyncInfoReceived(streamId, streamType, data);
            Charset charset = Charset.defaultCharset();
            String dataString = charset.decode(data).toString();
        }
    };
   ```

   **swift**

```swift
    func rtcEngine(_ engine: ByteRTCEngine, onStreamSyncInfoReceived streamId: String, info: ByteRTCStreamInfo, streamType: ByteRTCSyncInfoStreamType, data: Data) {
    }
   ```

   **cpp**

```cpp
    void bytertc::IRTCEngineEventHandler::onStreamSyncInfoReceived(const char* stream_id, const bytertc::StreamInfo& stream_info, SyncInfoStreamType stream_type, const uint8_t* data, int32_t length) {
    }
   ```

## Insert SEI into the mixed stream videos

With this solution, SEI is sent with mixed stream videos, making it more suitable for information with lower update frequency, such as layout changes when the number of co\-hosts changes, or positioning of PK health bars.

For the integration guideline and complete sample code of Push to CDN, please refer to [Push to CDN](https://docs.byteplus.com/en/docs/12/docs-69822). In this section, we will focus on SEI insertion and extraction in Push to CDN.

> It's recommended to add information with higher update frequency, such as volume and PK health bars, from the client\-side of each co\-host. Please refer to the universal solution for details.

1. Construct SEI messages. The SEI structure of mixed streams is shown as below. You can assign custom messages to `app_data`.

   ```json
    {
        "app_data": "Custom message data",
        "canvas": {
            "bgnd": "#000000",
            "h": 640,
            "w": 360
        },
        "regions": [
            {
                "alpha": 1.0,
                "contentControl": 0,
                "height": 640,
                "locationX": 0,
                "locationY": 50,
                "renderMode": 1,
                "uid": "user_343",
                "width": 360,
                "zorder": 0
            }
        ],
        "ts": 1705994199709
    }
   ```

2. When the host\-side calls the `startPushMixedStream` and `updatePushMixedStream` interfaces to initiate and update Push to CDN tasks, information such as mixed stream layout and background will be passed through into RTMP streams as SEI.

> Notifications of layout updates for mixed streams will also be sent via SEI.

**java**

```java
 MixedStreamConfig mixedStreamConfig = new MixedStreamConfig();
 mixedStreamConfig.userID = localUid;
 mixedStreamConfig.roomID = roomID;
 mixedStreamConfig.backgroundColor = "0x00000000";
 mixedStreamConfig.regions = getLayoutRegions();
 mixedStreamConfig.userConfigExtraInfo = msg;
```

**swift**

```swift
 self.mixedStreamConfig?.roomID = roomId!
 self.mixedStreamConfig?.userID = userId!
 self.mixedStreamConfig?.backgroundColor = "#FFFFFF"
 self.mixedStreamConfig?.regions = self.getMixRegions()
 self.mixedStreamConfig?.userConfigExtraInfo = msg
```

## Sample Project

### Insert SEI into SDK\-captured video streams

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/messaging/SEIMessageActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/SEI/SEIViewController.swift)

### Use audio RTP header extensions

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/messaging/StreamSyncInfoActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/SEI/AudioSEIViewController.swift)

## API reference

| |Android |iOS |macOS |Windows |Linux |Electron |Unity |Web |
|---|---|---|---|---|---|---|---|---|
|Send SEI |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendseimessage) |[sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe) |[sendSEIMessage:andRepeatCount:andCountPerFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-sendseimessage-andrepeatcount-andcountperframe) |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendseimessage) |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendseimessage) |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendseimessage) |[SendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-191859#sendseimessage) |[sendSEIMessage](https://docs.byteplus.com/en/docs/12/docs-104478#sendseimessage) |
|Receive SEI |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onseimessagereceived) |[rtcEngine:onSEIMessageReceived:info:andMessage:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onseimessagereceived-info-andmessage) |[rtcEngine:onSEIMessageReceived:info:andMessage:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onseimessagereceived-info-andmessage) |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onseimessagereceived) |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onseimessagereceived) |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onseimessagereceived) |[OnSEIMessageReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onseimessagereceivedeventhandler) |[onSEIMessageReceived](https://docs.byteplus.com/en/docs/12/docs-104479#engineevents-onseimessagereceived) |
|Send data messages via audio header extension |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendstreamsyncinfo) |[sendStreamSyncInfo:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendstreamsyncinfo-config) |[sendStreamSyncInfo:config:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-sendstreamsyncinfo-config) |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendstreamsyncinfo) |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-sendstreamsyncinfo) |[sendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-sendstreamsyncinfo) |[SendStreamSyncInfo](https://docs.byteplus.com/en/docs/12/docs-191859#sendstreamsyncinfo) |\- |
|Receive data messages from audio header extension |[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onstreamsyncinforeceived) |[rtcEngine:onStreamSyncInfoReceived:info:streamType:data:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onstreamsyncinforeceived-info-streamtype-data) |[rtcEngine:onStreamSyncInfoReceived:info:streamType:data:](https://docs.byteplus.com/en/docs/12/docs-70093#rtcengine-onstreamsyncinforeceived-info-streamtype-data) |[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onstreamsyncinforeceived) |[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85517#IRTCEngineEventHandler-onstreamsyncinforeceived) |[onStreamSyncInfoReceived](https://docs.byteplus.com/en/docs/12/docs-85533#rtcvideocallback-onstreamsyncinforeceived) |[OnStreamSyncInfoReceivedEventHandler](https://docs.byteplus.com/en/docs/12/docs-191860#onstreamsyncinforeceivedeventhandler) |\- |
|Start Push to CDN |[startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-startpushmixedstream) |[startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#startpushmixedstream-withpushtargetconfig-withmixedconfig) |[startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#startpushmixedstream-withpushtargetconfig-withmixedconfig) |[startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-startpushmixedstream) |\- |[startPushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startpushmixedstream) |\- |[startLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#startlivetranscoding) |
|Update Push to CDN |[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updatepushmixedstream) |[updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig) |[updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig) |[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatepushmixedstream) |\- |[updatePushMixedStream](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatepushmixedstream) |\- |[updateLiveTranscoding](https://docs.byteplus.com/en/docs/12/docs-104478#updatelivetranscoding) |

## FAQ

### Q1: How can I acquire SEI if I fail to receive the `onSEIMessageReceived` callback when using external capturing and rendering?

You can acquire SEI with `onSEIMessageReceived` only when you send an SEI message using `sendSEIMessage`.

### Q2: Why do I fail to receive the `onSEIMessageReceived` callback when sending SEI in the audio\-only call scenario?

When you send SEI in an audio\-only call using `sendSEIMessage`, the SDK automatically generates black frame video streams. If you are using manual publishing and subscribing, you must manually publish the black frame video stream, and subscribers must manually subscribe to it.

### Q3: How can I insert SEI into a Push to CDN stream via a server\-side API?

SEI insertion is currently not supported by the server\-side Open API `StartTranscode`. Please refer to [About Pushing to CDN](https://docs.byteplus.com/docs/byteplus-rtc/docs-69821) for details about sending SEI from the client\-side.

## Change log

1. Starting with client\-side SDK v3.27, the feature of sending and receiving SEI in live streams is supported.
