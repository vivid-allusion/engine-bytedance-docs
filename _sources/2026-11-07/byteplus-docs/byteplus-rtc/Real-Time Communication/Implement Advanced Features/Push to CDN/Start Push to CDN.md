---
title: "Start Push to CDN"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69822"
---

To broadcast your real\-time communication sessions to a wider audience, you can mix multiple audio and video streams from a call into a single stream and push it to a Content Delivery Network (CDN). This guide provides step\-by\-step instructions and code examples for implementing the client\-side Push to CDN feature. Following this guide, you will learn how to start, update, and stop a stream mixing task directly from your application.

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/69822_69822_flow_en.png)

> For details about calling Open API to push to CDN from the server\-side, please refer to [Using the Push to CDN Feature via OpenAPI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-push-to-cdn).

## Prerequisites

* You have already integrated BytePlusRTC SDK and are able to implement basic audio and video calls.

* You are using BytePlusRTC SDK version 3.52 or later.

## To initiate a Push to CDN task from the RTC client\-side

![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/69822_api_en.png)

### 1. Create an engine instance

Create and initialize an audio and video engine class.

> Refer to Building a video application for a detailed guide.

**java**

```java
// IRTCEngineEventHandler rtcEngineEventHandler = new IRTCEngineEventHandler() {
//    @Override public void onWarning(int warn) { ... }
//    @Override public void onError(int err) { ... }
// }

EngineConfig config = new EngineConfig();
config.appID = appId;
config.context = applicationContext;
rtcEngine = RTCEngine.createRTCEngine(config, rtcEngineEventHandler);
rtcEngine.startVideoCapture();
rtcEngine.startAudioCapture();
```

**swift**

```swift
let engineCfg = ByteRTCEngineConfig.init()
engineCfg.appID = appId
engineCfg.parameters = [:]
self.rtcEngine = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)
self?.rtcEngine?.startVideoCapture()
self?.rtcEngine?.startAudioCapture()
```

**cpp**

```cpp
    bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    m_engine = bytertc::IRTCEngine::createRTCEngine(conf, handler.get());
m_engine->startAudioCapture();
m_engine->startVideoCapture();
```

### 2. Enter a room

Once you have created a room instance, you can join the room to publish and subscribe to audio and video streams. We recommend configuring the room's callback interface to monitor status updates for the room and its streams.

**java**

```java
private void joinRoom(String roomId) {
    rtcRoom = rtcEngine.createRTCRoom(roomId);
    rtcRoom.setRTCRoomEventHandler(roomEventHandler);
    String token = requestRoomToken(roomId);
    UserInfo userInfo = new UserInfo(localUid, "");
    boolean isAutoPublishAudio = true;
    boolean isAutoPublishVideo = true;
    boolean isAutoSubscribeAudio = true;
    boolean isAutoSubscribeVideo = true;
    RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_CHAT_ROOM, isAutoPublishAudio, isAutoPublishVideo, isAutoSubscribeAudio, isAutoSubscribeVideo);
    rtcRoom.joinRoom(token, userInfo, true, roomConfig);
}
```

**swift**

```swift
self.rtcRoom = self.rtcEngine?.createRTCRoom(roomId)
self.rtcRoom?.delegate = self
let userInfo = ByteRTCUserInfo.init()
userInfo.userId = userId
let roomCfg = ByteRTCRoomConfig.init()
roomCfg.isPublishAudio = true
roomCfg.isPublishVideo = true
roomCfg.isAutoSubscribeAudio = true
roomCfg.isAutoSubscribeVideo = true
self.rtcRoom?.joinRoom(token, userInfo: userInfo, userVisibility: true, roomConfig: roomCfg)
```

**cpp**

```cpp
bytertc::IRTCRoom *room = engine->createRTCRoom(id);
        bytertc::UserInfo info;
        bytertc::RTCRoomConfig config;
        info.uid = uid.c_str();
        config.is_auto_publish_audio = true;
        config.is_auto_publish_video = true;
        config.is_auto_subscribe_audio = true;
        config.is_auto_subscribe_video = true;
        config.room_profile_type = bytertc::kRoomProfileTypeCommunication;
        int ret = room->joinRoom(token.c_str(), info, true, config);
```

### 3. Start a task

1. After successfully joining an RTC room, call `startPushMixedStream` to initiate a Push to CDN task. Use the room\-entry result callback provided by the SDK for your platform to confirm that the user has joined the room.

**java**

```java
private void startPushCDNStream() {
      MixedStreamPushTargetConfig targetConfig = new MixedStreamPushTargetConfig();
      targetConfig.pushTargetType = MixedStreamPushTargetType.PUSH_TO_CDN;
      targetConfig.pushCDNURL = "CDN_URL";
  
      MixedStreamConfig mixedStreamConfig = MixedStreamConfig.defaultMixedStreamConfig();
      mixedStreamConfig.userID = "USER_ID";
      mixedStreamConfig.roomID = "ROOM_ID";
      mixedStreamConfig.videoConfig.width = 360;
      mixedStreamConfig.videoConfig.height = 640;
      mixedStreamConfig.videoConfig.fps = 15;
      mixedStreamConfig.videoConfig.bitrate = 500000;
      mixedStreamConfig.audioConfig.channels = 2;
      mixedStreamConfig.audioConfig.sampleRate = 48000;
      mixedStreamConfig.audioConfig.bitrate = 64;
      mixedStreamConfig.regions = getLayoutRegions();
      rtcEngine.startPushMixedStream(taskID, targetConfig, mixedStreamConfig);
    }
    IRTCEngineEventHandler engineEventHandler = new IRTCEngineEventHandler() {
        @Override
        public void onMixedStreamEvent(MixedStreamTaskInfo info, MixedStreamTaskEvent event, MixedStreamTaskErrorCode error) {
            super.onMixedStreamEvent(info, event, error);
            String msg = String.format("onMixedStreamEvent,taskId:%s, error:%s, event:%s", info.getTaskId(), error.toString(), event.toString());
            Log.d(TAG, msg);
        }
    };
```

**swift**

```swift
@objc func startPushCDNStream()  {
    let targetConfig = ByteRTCMixedStreamPushTargetConfig.init()
    targetConfig.pushTargetType = .toCDN
    targetConfig.pushCDNURL = CDN_URL

    let mixedStreamConfig = ByteRTCMixedStreamConfig.default()
    mixedStreamConfig?.roomID = roomId
    mixedStreamConfig?.userID = userId
    
    mixedStreamConfig.videoConfig.width = 360
    mixedStreamConfig.videoConfig.height = 640
    mixedStreamConfig.videoConfig.fps = 15
    mixedStreamConfig.videoConfig.bitrate = 500000
    
    mixedStreamConfig.audioConfig.channels = 2
    mixedStreamConfig.audioConfig.sampleRate = 48000
    mixedStreamConfig.audioConfig.bitrate = 64
    
    mixedStreamConfig.regions = getLayoutRegions()

    rtcEngine?.startPushMixedStream(taskId, with:targetConfig, withMixedConfig: mixedStreamConfig)
  }
  func rtcEngine(_ engine: ByteRTCEngine, onMixedStreamEvent event: ByteRTCMixedStreamTaskEvent, withMixedStreamInfo info: ByteRTCMixedStreamTaskInfo, with errorCode: ByteRTCMixedStreamTaskErrorCode) {
            ToastComponents.shared.show(withMessage: "onMixedStreamEvent:\(event.rawValue) taskId:\(info.taskId) errorCode:\(errorCode.rawValue) + mixType:\(info.description)")
        NSLog("onMixedStreamEvent: \(event), info_des: \(info.description), errorcode : \(errorCode)")
  }
```

**cpp**

```cpp
    bytertc::IMixedStreamConfig* mixed_stream_param = getMixedStreamConfig();
    bytertc::MixedStreamPushTargetConfig cf;
    cf.push_cdn_url = url.c_str();
    int ret = m_engine->startPushMixedStream(m_task.c_str(), cf, mixed_stream_param);

void onMixedStreamEvent(MixedStreamTaskInfo info, MixedStreamTaskEvent event, MixedStreamTaskErrorCode error_code) {
        (void)info;
        (void)event;
        (void)error_code;
    }
```

2. This section uses 1x4 and 2x2 layout modes as examples.

**java**

```java
private MixedStreamConfig.MixedStreamLayoutRegionConfig[] getLayoutRegions() {
    int width = 360;
    int height = 640;
    int userNum = userNameList.size();
    MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[userNum];
    int index = 0;
    String mode = layoutMode.getSelectedItem().toString();
    if ("1x4".equals(mode)) {
        for (String uid : userNameList) {
            MixedStreamConfig.MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
            region.setRoomID(roomID);
            region.setUserID(uid);
            region.isLocalUser = (uid.equals(localUid));
            region.setLocationX(index * width / userNum);
            region.setLocationY(50);
            region.setWidth(width / userNum);
            region.setHeight(height);
            region.setAlpha(1);
            region.setZOrder(0);
            region.setRenderMode(MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
            region.setStreamType(MixedStreamVideoType.MIXED_STREAM_VIDEO_TYPE_MAIN);
            region.setMediaType(MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO);
            regions[index] = region;
            index ++;
        }
    } else if ("2x2".equals(mode)) {
        for (String uid : userNameList) {
            MixedStreamConfig.MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
            region.setRoomID(roomID);
            region.setUserID(uid);
            region.isLocalUser = (uid.equals(localUid));
            region.setLocationX((index % 2) * width / userNum);
            region.setLocationY((index / 2) * height / 2 + 50);
            region.setWidth(width / 2);
            region.setHeight(height / 2);
            region.setAlpha(1);
            region.setZOrder(0);
            region.setRenderMode(MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
            region.setStreamType(MixedStreamLayoutRegionConfig.MixedStreamVideoType.MIXED_STREAM_VIDEO_TYPE_MAIN);
            region.setMediaType(MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO);
            regions[index] = region;
            index ++;
        }
    }
    return regions;
}
```

**swift**

```swift
func getMixRegions() -> [ByteRTCMixedStreamLayoutRegionConfig] {
    let roomId = roomSettingItem.text
    let userId = userSettingItem.text
    
    var regions = [ByteRTCMixedStreamLayoutRegionConfig]()
    if self.layoutSheetView.selectedIndex == 0 {
        
        let width = 360/4
        let height = 640
        
        let regionConfig = ByteRTCMixedStreamLayoutRegionConfig.init()
        regionConfig.userID = userId!
        regionConfig.roomID = roomId!
        regionConfig.locationX = 0
        regionConfig.locationY = 0
        regionConfig.width = 360/4
        regionConfig.height = 640
        regionConfig.zOrder = 0
        regionConfig.isLocalUser = true
        regionConfig.mediaType = .audioAndVideo
        
        regions.append(regionConfig)
        
        for (index, item) in self.users.enumerated() {
            if index < 3 {
                let regionConfig = ByteRTCMixedStreamLayoutRegionConfig.init()
                regionConfig.userID = item.userId!
                regionConfig.roomID = item.roomId!
                
                regionConfig.locationX = width*(index+1)
                regionConfig.locationY = 0
                regionConfig.width = width
                regionConfig.height = height
                regionConfig.zOrder = 0
                regionConfig.isLocalUser = false
                regionConfig.mediaType = .audioAndVideo
                
                regions.append(regionConfig)
            }
        }
    } else {
        let width = 360/2
        let height = 640/2
        
        let regionConfig = ByteRTCMixedStreamLayoutRegionConfig.init()
        regionConfig.userID = userId!
        regionConfig.roomID = roomId!
        regionConfig.locationX = 0
        regionConfig.locationY = 0
        regionConfig.width = width
        regionConfig.height = height
        regionConfig.zOrder = 0
        regionConfig.isLocalUser = true
        regionConfig.mediaType = .audioAndVideo
        
        regions.append(regionConfig)
        
        for (index, item) in self.users.enumerated() {
            if index < 3 {
                let regionConfig = ByteRTCMixedStreamLayoutRegionConfig.init()
                regionConfig.userID = item.userId!
                regionConfig.roomID = item.roomId!
                
                let col = (index + 1)%2
                let row = (index + 1)/2
                
                regionConfig.locationX = width*col
                regionConfig.locationY = height*row
                regionConfig.width = width
                regionConfig.height = height
                regionConfig.zOrder = 0
                regionConfig.isLocalUser = false
                regionConfig.mediaType = .audioAndVideo
                
                regions.append(regionConfig)
            }
        }
    }
    
    return regions
}
```

**cpp**

```cpp
bytertc::IMixedStreamConfig* CDNStreamByServer::getMixedStreamConfig()
{
    // audio
    bytertc::MixedStreamAudioConfig audioParam;
    audioParam.audio_codec = bytertc::MixedStreamAudioCodecType::kMixedStreamAudioCodecTypeAAC;
    audioParam.channels = 2;
    audioParam.bitrate = bitrate_a;
    audioParam.sample_rate = 48000;
    audioParam.audio_profile = bytertc::MixedStreamAudioProfile::kMixedStreamAudioProfileLC;

    // video
    bytertc::MixedStreamVideoConfig videoParam;
    videoParam.bitrate = bitrate_v;
    videoParam.fps = 15;
    videoParam.gop = 2;
    videoParam.width = 640;
    videoParam.height = 360;
    videoParam.enable_bframe = false;
    videoParam.video_codec = bytertc::kMixedStreamVideoCodecTypeH264;

    // layout
    bytertc::MixedStreamLayoutRegionConfig* layouts = new bytertc::MixedStreamLayoutRegionConfig[m_rendered_users.size()];
    int i = 0;
    std::map<std::string, UserWidget*>::iterator ite;

    for (ite = m_rendered_users.begin(); ite != m_rendered_users.end(); ite++) {
        bytertc::MixedStreamLayoutRegionConfig lay;
        lay.user_id = ite->first.c_str();
        lay.room_id = m_roomid.c_str();

        lay.location_x = (i % 2) * 0.5 * videoParam.width; //确定每个流的位置
        lay.location_y = (i / 2) * 0.5 *  videoParam.height;

        lay.width = 0.5 * videoParam.width;
        lay.height = 0.5* videoParam.height;

        if (ite->first == m_localid) {
            lay.is_local_user = true;
        }
        else {
            lay.is_local_user = false;
        }

        lay.alpha = 1.0f;
        lay.z_order = 0;

        lay.render_mode = bytertc::MixedStreamRenderMode::kMixedStreamRenderModeHidden;
        lay.stream_type = bytertc::MixedStreamVideoType::kMixedStreamVideoTypeMain;
        lay.media_type = bytertc::MixedStreamMediaType::kMixedStreamMediaTypeAudioAndVideo;
        lay.apply_spatial_audio = false;
        layouts[i++] = lay;
    }

    std::string url = "Your Url";

    bytertc::IMixedStreamConfig* mixed_stream_param = bytertc::IMixedStreamConfig::createMixedStreamConfig();
    mixed_stream_param->setAudioConfig(audioParam);
    mixed_stream_param->setVideoConfig(videoParam);
    mixed_stream_param->setLayoutConfig(layouts, m_rendered_users.size());
    mixed_stream_param->setRoomID(m_roomid.c_str());
    mixed_stream_param->setUserID(m_localid.c_str());

    delete[]layouts;
    return mixed_stream_param;
}
```

### 4. Update a task

The mixed\-stream layout can be updated only after remote video streams are received.

Certain configurations can be updated during push to CDN. Please refer to the API reference for details.

**java**

```java
private void updateCDNStreamConfig() {
    String cdnAddr = cdnAddressInput.getText().toString();
        if (cdnAddr.isEmpty()) {
            ToastUtil.showAlert(this, "cdn address is null");
            return;
        }
        targetConfig.pushCDNURL = cdnAddr;

        mixedStreamConfig.backgroundColor = layoutColorInput.getText().toString();
        mixedStreamConfig.regions = getLayoutRegions();
        rtcEngine.updatePushMixedStream(CDN_TASK_ID, targetConfig, mixedStreamConfig);
}
```

**swift**

```swift
@objc func updatePushConfig()  {
    self.rtcEngine?.updatePushMixedStream(taskId, with: self.targetConfig, withMixedConfig: self.mixConfig!)
}
```

**cpp**

```cpp
bytertc::MixedStreamPushTargetConfig cf;
    cf.push_cdn_url = "Your Url";

    bytertc::IMixedStreamConfig* config = getMixedStreamConfig();
    int ret = m_video->updatePushMixedStream(m_task.c_str(), cf, config);
```

### 5. End a task

You can initiate or stop a Push to CDN task at any time during an RTC session.

**java**

```java
private void stopPushCDNStream() {
    rtcEngine.stopPushMixedStream(CDN_TASK_ID, MixedStreamPushTargetType.PUSH_TO_CDN);
  }
```

**swift**

```swift
@objc func stopPushCDN()  {
    self.rtcEngine?.stopPushMixedStream(taskId, with: .toCDN)
  }
```

**cpp**

```cpp
int ret = m_engine->stopClientMixedStream(m_task.c_str());
```

### 6. Leave a room

**java**

```java
private void leaveRoom() {
    if (rtcRoom != null) {
        rtcRoom.leaveRoom();
        rtcRoom.destroy();
        rtcRoom = null;
    }
}
```

**swift**

```swift
self?.rtcRoom?.leave()
self?.rtcRoom?.destroy()
self?.rtcRoom = nil
```

**cpp**

```cpp
room->leaveRoom();
room->destroyRTCRoom();
room = nullptr;
```

### 7. Destroy the engine

**java**

```java
RTCEngine.destroyRTCEngine();
```

**swift**

```swift
ByteRTCEngine.destroyRTCEngine()
self.rtcEngine = nil
```

**cpp**

```cpp
bytertc::IRTCEngine::destroyRTCEngine();
video = nullptr;
```

## Sample project

* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/video/CDNStreamActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/ImportantComponents/PushCDN/PushCDNViewController.swift)

## FAQ

### 1. How can I use SEI in a Push to CDN stream?

SEI refers to supplemental enhancement information in video encoding formats, which is encapsulated and sent with video encoding frames to achieve synchronization with video frame sending and analysis. When a push task is successfully initiated, information such as image layout and background will be passed through into RTMP streams as SEI. The client that pulls the stream needs to extract and analyze the SEI to perform actions such as updating the image layout.

* The information transmitted from a mixed\-stream interface to live streams will be resent before the I frame of the mixed streams. For example, if the layout of a mixed stream does not change, the same SEI data will be sent repeatedly, and when the layout changes, a new SEI message is generated.

* When enabling/updating a mixed stream, you can configure custom SEI by setting up layoutConfig.userConfigExtraInfo. For details, please refer to [Sending and Receiving Supplemental Enhancement Information] (70140). For instance, in the live streaming question\-answering scenario, information about the questions will be encapsulated in the SEI. This ensures that when co\-hosts hear the host announce a question, they see the question on\-screen simultaneously, preventing latency\-induced mismatches between the audio and the visual information.

A sample of the mixed\-stream SEI structure is shown below, where the custom message is the value of `app_data`.

```json
{
    "app_data": "Custom message",
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

### 2. How should I configure task_id?

When your app needs to enable multiple mixed video streams, use task_id to differentiate between them. If there is only one mixed\-stream video data, you can use an empty string as a placeholder.

The `task_id` used in `startPushMixedStream` and `stopPushMixedStream` must match. If the `task_id` is inconsistent, the mixed stream(s) will not be closed.

### 3. How should I handle re\-login due to an accidental disconnection on the initiating side?

If the client application terminates unexpectedly (for example, due to a page refresh) after a push task has started, the task stops automatically. This occurs when the idle time exceeds the specified threshold (180 seconds by default).

When the client\-side is restarted and it's logged in again, you need to first call `stopPushMixedStream` to end the previous task before starting a new push task. This prevents the new push task from failing due to multiple tasks operating on a single push address.

### 4. Error codes

For details about the error codes returned during the push to CDN, please refer to the API documentation for each platform.

|Android |iOS |Mac |Windows |Electron |Flutter |Web |
|---|---|---|---|---|---|---|
|[MixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70082#mixedstreamtaskerrorcode) |[ByteRTCMixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70085#bytertcmixedstreamtaskerrorcode) |[ByteRTCMixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70091#bytertcmixedstreamtaskerrorcode) |[MixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-70097#mixedstreamtaskerrorcode) |[MixedStreamTaskErrorCode](https://docs.byteplus.com/en/docs/12/docs-85534#mixedstreamtaskerrorcode) |`StreamMixingErrorCode` |[StreamMixingEventErrorCode](https://docs.byteplus.com/en/docs/12/docs-104480#streammixingeventerrorcode) |
