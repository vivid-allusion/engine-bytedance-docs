---
title: "在 Android 上实现互动直播"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-interactive-live-for-android-zh-CN"
---

本主题为 Android 应用程序构建互动直播功能提供全面的分步说明。你将找到实现主播和观众核心功能的详细代码示例，包括开启直播流、支持连麦 PK，以及允许观众成为连麦主播。

<span id="d0660c19"></span>
## 前提条件


* 已激活 [BytePlus 账号](http://console.byteplus.com/)、[BytePlus MediaLive](https://console.byteplus.com/live) 和 [火山引擎实时音视频](https://console.byteplus.com/rtc/workplaceRTC)。更多信息，请参见 [注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)、[激活 MediaLive 服务](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-CN#da5a6a63)，以及 [激活 RTC 服务](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。

* 你已集成所需的 SDK：

   * 火山引擎实时音视频 SDK 版本 3.60.104 或更高。更多信息，请参见 [集成 Android RTC SDK](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70134)。

   * BytePlus MediaLive SDK，无特定版本要求。更多信息，请参见 [集成 Android 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-CN) 和 [初始化 Android 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android-zh-CN)。


<span id="86abfd57"></span>
## 为主播实现该功能

本节提供为主播实现互动直播功能的说明。

<span id="33f82960"></span>
### 开启直播流

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2347c01157542d89c81f6a4ec544765~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [createRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#creatertcengine)

* [createRTCRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-creatertcroom)

* [joinRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#joinroom)

* [onRoomStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#onroomstatechanged)

* [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

* [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setvideoencoderconfig)

* [startVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startvideocapture)

* [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startaudiocapture)

* [startPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startpushmixedstream)

* [onMixedStreamEvent](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCEngineEventHandler-onmixedstreamevent)


**示例代码**


1. 创建 RTC 引擎和 RTC 房间，并加入 RTC 房间。

   ```Java
   // Create an RTC engine.设置 rtcEngineHandler 以接收与 RTC 引擎相关的回调。
   EngineConfig config = new EngineConfig();
   config.parameters = new JSONObject();
   config.context = mContext;
   config.appID = RTC_APP_ID; // 用你创建火山引擎实时音视频应用后获得的 RTC_APP_ID 替换。
   mRTCEngine = RTCEngine.createRTCEngine(config, rtcEngineHandler);
   
   // 创建 RTC 房间。设置 rtcRoomHandler 以接收与 RTC 房间相关的回调。
   mRTCRoom = mRTCEngine.createRTCRoom(roomid);
   mRTCRoom.setRTCRoomEventHandler(rtcRoomHandler);
   
   // 加入 RTC 房间。必须将房间配置设置为直播流配置，即 ROOM_PROFILE_LIVE。
   mUserId = userId;
   mRoomId = roomId;
   UserInfo userInfo = new UserInfo(userId, null);
   RTCRoomConfig roomConfig = new RTCRoomConfig(ROOM_PROFILE_LIVE,
           true, true, true);
   mRTCRoom.joinRoom(token, userInfo, true, roomConfig);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">关于如何获取 AppID 的更多信息，请参见<a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid">创建火山引擎实时音视频应用并获取 AppID</a>。   </div>
   

2. 设置本地预览视图和视频编码参数。

   ```Java
   // Set the local preview view.
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = view;
   videoCanvas.renderMode = RENDER_MODE_FIT;
   mRTCEngine.setLocalVideoCanvas(STREAM_INDEX_MAIN, videoCanvas);
   
   // Set video encoding parameters.
   VideoEncoderConfig videoEncConfig = new VideoEncoderConfig();
   mRTCEngine.setVideoEncoderConfig(videoEncConfig);
   ```
   

3. 开始音视频采集。

   ```Java
   // Start video capture.
   mRTCEngine.startVideoCapture();
   
   // Start audio capture.
   mRTCEngine.startAudioCapture();
   ```
   

4. 开始推流。

   ```Java
   // 设置推流配置，包括 待推送流的 URL。
   MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
   pushTargetConfig.pushCDNURL = mTargetUrl;
   pushTargetConfig.pushTargetType = PUSH_TO_CDN;
   
   // 设置视频编码参数用于转码。
   MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
   videoconfig.fps = mConfig.mmVideoEncoderFps;
   videoconfig.height = mConfig.mVideoEncoderHeight;;
   videoconfig.width = mConfig.mVideoEncoderWidth;;
   videoconfig.bitrate = mVideoEncoderKBitrate;
   videoconfig.gop = mConfig.mVideoGopVal;
   
   // 设置音频编码参数用于转码。
   MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
   audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
   audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
   audioConfig.bitrate = 128;
   audioConfig.channels = 2;
   audioConfig.sampleRate = 48000;
   
   // 设置推流到 CDN 的布局。由于房间内只有主播，将主播的布局设置为占据整个画布。
   MixedStreamLayoutRegionConfig[] regions = new MixedStreamLayoutRegionConfig[1];
   MixedStreamLayoutRegionConfig region = new MixedStreamLayoutRegionConfig();
   region.roomID = mRTCRoom.getRoomId();
   region.userID = localUid;
   region.streamType = (MixedStreamVideoType.MIXED_STREAM_VIDEO_TYPE_MAIN);
   region.mediaType = (MixedStreamMediaType.MIXED_STREAM_MEDIA_TYPE_AUDIO_AND_VIDEO);
   region.renderMode = MIXED_STREAM_RENDER_MODE_FIT;
   region.locationX = 0;
   region.locationY = 0;
   region.width = videoconfig.width;
   region.height = videoconfig.height;
   regions[0] = region;
   
   // 将已配置的音视频参数传入最终结构体。
   MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
   streamConfig.audioConfig = audioConfig;
   streamConfig.videoConfig = videoconfig;
   streamConfig.roomID = mRTCRoom.getRoomId();
   streamConfig.userID = localUid;
   streamConfig.regions = regions;
   
   String taskId = ""; // A  unique ID for the push-to-CDN task, which does not exceed 127 bytes.
   
   // Start pushing the stream.通过创建 RTC 引擎时设置的 rtcEngineHandler 接收流推送状态信息。
   mRTCEngine.startPushMixedStream(taskId, pushTargetConfig, streamConfig);
   ```
   


<span id="fb003e2e"></span>
### （可选）为主播启用美颜

请参见 [视频特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)，获取为主播启用美颜功能的详细说明。

<span id="91ff8ccd"></span>
### 开启连麦 PK

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ee305921cc46feabe545fa0af2131c~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#startforwardstreamtorooms)

* [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged)

* [onUserJoined](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserjoined)

* [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

* [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

* [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

* [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)


**示例代码**


1. 当主播 A 成功收到开启 PK 通知时，调用 `startForwardStreamToRooms`，将主播 A 的流推送到主播 B 的房间，将主播 B 的流推送到主播 A 的房间。

   ```Java
   // Push Host A's stream to Host B's room.
   mRTCRoom1.startForwardStreamToRooms(room2ID, token);
   
   // Push Host B's stream to Host A's room.
   mRTCRoom2.startForwardStreamToRooms(room1ID, token);
   ```
   

2. 主播收到 `onUserJoined` 回调时，更新配置文件和推流到 CDN布局。主播收到 `onUserPublishStreamVideo` 回调时，更新远端用户视图。

   ```Java
   // 针对主播A
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserJoined(UserInfo userInfo) {
           // 将房间模式设置为连麦（主播与主播）模式，即ROOM_PROFILE_LINKMIC。
           mRTCRoom1.setRoomProfile(ROOM_PROFILE_LINKMIC);
           
           // 设置流推送配置，包括要推送的混流 URL。一般建议与开始直播流时的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 设置视频编码参数用于转码。一般建议与开始直播流时的配置保持一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mConfig.mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 设置音频编码参数用于转码。一般建议与开始直播流时的配置保持一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 将推流到 CDN 的布局从单人布局更新为双人布局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播 A 的用户 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 仅供参考。
           region.setLocationY(0.0); // 仅供参考。
           region.setWidthProportion(0.5); // 仅供参考。
           region.setHeightProportion(0.5); // 仅供参考。
           region.setAlpha(1.0); // 仅供参考。
           region.setZOrder(0); // 仅供参考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // 主播 B 的用户 ID。
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // 仅供参考。
           regionRemote.setLocationY(0.0); // 仅供参考。
           regionRemote.setWidthProportion(0.5); // 仅供参考。
           regionRemote.setHeightProportion(0.5); // 仅供参考。
           regionRemote.setAlpha(1.0); // 仅供参考。
           regionRemote.setZOrder(0); // 仅供参考。
           regionRemote.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[1] = regionRemote;
   
           // Pass the configured audio and video parameters into the final structure.
           MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
           streamConfig.audioConfig = audioConfig;
           streamConfig.videoConfig = videoconfig;
           streamConfig.roomID = mRTCRoom.getRoomId();
           streamConfig.userID = localUid;
           streamConfig.regions = regions;
           
           String taskId = ""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
           
           // 更新流推送参数。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // 添加远端用户视图。
               TextureView renderView = new TextureView(Env.getApplicationContext());
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = renderView;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   // 针对主播 B
           ...
           // 将推流到 CDN 的布局从单人布局更新为双人布局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播 B 的用户 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 仅供参考。
           region.setLocationY(0.0); // 仅供参考。
           region.setWidthProportion(0.5); // 仅供参考。
           region.setHeightProportion(0.5); // 仅供参考。
           region.setAlpha(1.0); // 仅供参考。
           region.setZOrder(0); // 仅供参考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // 主播 A 的用户 ID。
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // 仅供参考。
           regionRemote.setLocationY(0.0); // 仅供参考。
           regionRemote.setWidthProportion(0.5); // 仅供参考。
           regionRemote.setHeightProportion(0.5); // 仅供参考。
           regionRemote.setAlpha(1.0); // 仅供参考。
           regionRemote.setZOrder(0); // 仅供参考。
           regionRemote.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[1] = regionRemote;
           ...
   ```
   


<span id="91a69d1c"></span>
### 结束连麦 PK

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b655a753b164cda9efbd7239b2eb908~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-stopforwardstreamtorooms)

* [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged)

* [onUserLeave](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserleave)

* [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

* [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

* [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

* [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)


**示例代码**


1. 当主播 A 成功收到结束 PK 通知时，调用 `stopForwardStreamToRooms`，停止将主播 A 的流推送到主播 B 的房间或主播 B 的流推送到主播 A 的房间。

   ```Java
   // Stop pushing Host A's stream to Host B's room.
   mRTCRoom1.stopForwardStreamToRooms();
   
   // Stop pushing Host B's stream to Host A's room.
   mRTCRoom2.stopForwardStreamToRooms();
   ```
   

2. 主播收到 `onUserLeave` 回调时，更新配置文件和推流到 CDN 布局。主播收到 `onUserPublishStreamVideo` 回调时，移除远端用户视图。

   ```Java
   // For Host A
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserLeave(String uid, int reason) {
           // 将房间模式设置为直播流模式，即ROOM_PROFILE_LIVE。
           mRTCRoom1.setRoomProfile(ROOM_PROFILE_LIVE);
           
           // 设置流推送配置，包括要推送的混流 URL。一般建议与开始直播流时的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 设置视频编码参数用于转码。一般建议与开始直播流时的配置保持一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 设置音频编码参数用于转码。一般建议与开始直播流时的配置保持一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 将推流到 CDN 的布局从双人布局更新为单人布局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播 A 的用户 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 仅供参考。
           region.setLocationY(0.0); // 仅供参考。
           region.setWidthProportion(0.5); // 仅供参考。
           region.setHeightProportion(0.5); // 仅供参考。
           region.setAlpha(1.0); // 仅供参考。
           region.setZOrder(0); // 仅供参考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
   
           // Pass the configured audio and video parameters into the final structure.
           MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
           streamConfig.audioConfig = audioConfig;
           streamConfig.videoConfig = videoconfig;
           streamConfig.roomID = mRTCRoom.getRoomId();
           streamConfig.userID = localUid;
           streamConfig.regions = regions;
           
           String taskId = ""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
           
           // 更新流推送参数。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // 移除远端用户视图。
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   // 针对主播 B
            ...
           // 将推流到 CDN 的布局从两人布局更新为单人布局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播 B 的用户 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 仅供参考。
           region.setLocationY(0.0); // 仅供参考。
           region.setWidthProportion(0.5); // 仅供参考。
           region.setHeightProportion(0.5); // 仅供参考。
           region.setAlpha(1.0); // 仅供参考。
           region.setZOrder(0); // 仅供参考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           ...
   ```
   


<span id="33d6c35f"></span>
### 结束直播流

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e525b9e474634955a1b1859dc16d0a69~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stoppushmixedstream)

* [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopvideocapture)

* [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startaudiocapture)

* [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

* [销毁](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-destroy)

* [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-destroyrtcengine)


**示例代码**


1. 停止推流。

   ```Java
   mRTCEngine.stopPushMixedStream(taskId, PUSH_TO_CDN);
   ```
   

2. 停止音视频采集，并移除本地预览视图。

   ```Java
   // Stop video capture.
   mRTCEngine.stopVideoCapture();
   
   // Stop audio capture.
   mRTCEngine.stopAudioCapture();
   
   // Remove the local preview view.
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = null;
   videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCEngine.setLocalVideoCanvas(StreamIndex.STREAM_INDEX_MAIN, videoCanvas);
   ```
   

3. 销毁 RTC 房间和 RTC 引擎。

   ```Java
   // Destroy the RTC room.
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine.
   mRTCEngine.destroyRTCEngine();
   mRTCEngine = null;
   ```
   


<span id="ec36bcae"></span>
## 为观众实现该功能

本节提供为观众实现互动直播功能的说明。

<span id="935dd891"></span>
### 观看直播流

观众使用播放器观看直播流。

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c1f1f3e252648aaa05fda30502ad6f3~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。


* [setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig)

* [setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver)

* [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)

* [setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl)

* [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play)


**示例代码**


1. 创建并设置播放器。

   ```Java
   // Create a player.
   VeLivePlayer mLivePlayer = new VideoLiveManager(Env.getApplicationContext());
   
   // Set player callbacks.
   mLivePlayer.setObserver(mLivePlayerObserver);
   
   // Set player parameters.
   VeLivePlayerConfiguration config = new VeLivePlayerConfiguration();
   config.enableStatisticsCallback = true;
   config.enableLiveDNS = true;
   mLivePlayer.setConfig(config);
   ```
   

2. 设置播放器视图和拉流地址，并开始回放。

   ```Java
   // Set the player view.
   mLivePlayer.setSurfaceHolder(holder);
   
   // Set the pull stream address.
   mLivePlayer.setPlayUrl(mPullUrl);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<span id="148f2373"></span>
### （可选）为观众开启美颜

有关为观众开启美颜功能的详细操作，请参见[视频特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)。

<span id="c6e434d1"></span>
### 成为连麦（主播与主播）

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f085b77054334c1585a68383690539b7~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。


* MediaLive SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop)

* RTC SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080)和[回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [createRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#creatertcengine)

   * [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

   * [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setvideoencoderconfig)

   * [startVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startvideocapture)

   * [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startaudiocapture)

   * [createRTCRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-creatertcroom)

   * [joinRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#joinroom)

   * [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

   * [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)

   * [onUserJoined](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserjoined)

   * [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

   * [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)


**示例代码**


1. 停止回放并移除播放器视图。

   ```Java
   // Stop playback.
   mLivePlayer.stop();
   ```
   

2. 创建 RTC 引擎，设置本地预览视图和视频编码参数，并开始视频和音频采集。

   ```Java
   // Create an RTC engine.设置 rtcEngineHandler 以接收与 RTC 引擎相关的回调。
   EngineConfig config = new EngineConfig();
   config.parameters = new JSONObject();
   config.context = mContext;
   config.appID = RTC_APP_ID;
   mRTCEngine = RTCEngine.createRTCEngine(config, rtcEngineHandler);
   
   // 设置本地预览视图。
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = renderView;
   videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCEngine.setLocalVideoCanvas(StreamIndex.STREAM_INDEX_MAIN, videoCanvas);
   
   // 设置视频编码参数。
   VideoEncoderConfig config = new VideoEncoderConfig(
           mConfig.mVideoEncoderWidth, mConfig.mVideoEncoderHeight, mConfig.mVideoEncoderFps, mConfig.mVideoEncoderKBitrate * 1000);
   mRTCEngine.setVideoEncoderConfig(config);
   
   // 开始音视频采集。
   mRTCEngine.startVideoCapture();
   mRTCEngine.startAudioCapture();
   ```
   

3. 创建并加入 RTC 房间，使用与主播相同的 RoomID。

   ```Java
   // Create an RTC room.
   mRTCRoom = mRTCEngine.createRTCRoom(roomId);
   mRTCRoom.setRTCRoomEventHandler(mIRtcRoomEventHandler);
   
    // Set user information.
   UserInfo userInfo = new UserInfo(userId, null);
   RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_COMMUNICATION,
           true, true, true);
       
   // Join the RTC room.
   mRTCRoom.joinRoom(token, userInfo, roomConfig);
   ```
   

4. 当观众收到`onUserPublishStreamVideo`回调时，调用`setRemoteVideoCanvas`调整远端用户视图。

   ```Java
   private RtcRoomEventHandlerAdapter mIRtcRoomEventHandler = new RtcRoomEventHandlerAdapter() {
       @Override
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // Add the remote user view.
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = renderVide;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           } else {
               // Remove the remote user view.
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   };
   ```
   

5. 当主播收到`onUserJoined`回调时，更新房间配置和推流到 CDN 的布局。当主播收到`onUserPublishStreamVideo`回调时，更新远端用户视图。

   ```Java
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserJoined(UserInfo userInfo) {
           // 设置房间为连麦（主播与主播）场景，即 ROOM_PROFILE_LINKMIC。
           mRTCRoom.setRoomProfile(ROOM_PROFILE_LINKMIC)
       
           // 设置流推送配置，包括要推送混流的 URL。通常与启动直播流时的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 设置转码的视频编码参数。通常与启动直播流时的配置保持一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 设置转码的音频编码参数。通常与启动直播流时的配置保持一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 将推流到 CDN 的布局从单人布局更新为两人布局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播的用户 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 仅供参考。
           region.setLocationY(0.0); // 仅供参考。
           region.setWidthProportion(0.5); // 仅供参考。
           region.setHeightProportion(0.5); // 仅供参考。
           region.setAlpha(1.0); // 仅供参考。
           region.setZOrder(0); // 仅供参考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // 连麦（主播与主播）的用户 ID。
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // 仅供参考。
           regionRemote.setLocationY(0.0); // 仅供参考。
           regionRemote.setWidthProportion(0.5); // 仅供参考。
           regionRemote.setHeightProportion(0.5); // 仅供参考。
           regionRemote.setAlpha(1.0); // 仅供参考。
           regionRemote.setZOrder(0); // 仅供参考。
           regionRemote.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[1] = regionRemote;
   
           // Pass the configured audio and video parameters into the final structure.
           MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
           streamConfig.audioConfig = audioConfig;
           streamConfig.videoConfig = videoconfig;
           streamConfig.roomID = mRTCRoom.getRoomId();
           streamConfig.userID = localUid;
           streamConfig.regions = regions;
           
           String taskId = ""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
           
           // 更新流推送参数。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // 添加远端用户视图。
               TextureView renderView = new TextureView(Env.getApplicationContext());
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = renderView;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   ```
   


<span id="6da5f01e"></span>
### 停止连麦（主播与主播）

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65e0b0f83f7d4812bc0a798855b637e0~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。


* MediaLive SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。

   * [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)

   * [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play)

* RTC SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080)和[回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [leaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTSRoom-leaveroom)

   * [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

   * [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)

   * [onUserLeave](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserleave)

   * [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

   * [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

   * [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

   * [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopvideocapture)

   * [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopaudiocapture)


**示例代码**


1. 离开 RTC 房间，停止视频和音频采集，并移除本地预览视图和远端用户视图。

   ```Java
   // Leave the RTC room.
   mRTCRoom.leaveRoom();
   
   // Stop video capture.
   mRTCEngine.stopVideoCapture();
   
   // Stop audio capture.
   mRTCEngine.stopAudioCapture();
   
   // Remove the local preview view.
   VideoCanvas canvas = new VideoCanvas(null, RENDER_MODE_HIDDEN, mRoomId, mUserId, false);
   mRTCEngine.setLocalVideoCanvas(mUserId, StreamIndex.STREAM_INDEX_MAIN, canvas);
   
   // Remove the remote user view.
   VideoCanvas canvas = new VideoCanvas();
   canvas.renderView = null;
   canvas.renderMode = RENDER_MODE_HIDDEN;
   RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
   mRTCEngine.setRemoteVideoCanvas(key, canvas);
   ```
   

2. 设置播放器视图并开始回放。

   ```Java
   // Set the player view.
   mLivePlayer.setSurfaceHolder(holder);
   // Start playback.
   mLivePlayer.play();
   ```
   

3. 当主播收到`onUserLeave`回调时，更新房间配置和推流到 CDN 的布局。当主播收到`onUserPublishStreamVideo`回调时，移除远端用户视图。

   ```Java
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserLeave(String uid, int reason) {
           // 设置房间为直播流场景，即 ROOM_PROFILE_LIVE。
           mRTCRoom.setRoomProfile(ROOM_PROFILE_LIVE)
           
           // 设置流推送配置，包括要推送混流的 URL。通常与启动直播流时的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 设置转码的视频编码参数。通常，保持配置与启动直播流时所用配置一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 设置用于转码的音频编码参数。通常，保持配置与启动直播流时所用配置一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 将推流到 CDN 的布局从双人布局更新为单人布局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播的用户 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 仅供参考.
           region.setLocationY(0.0); // 仅供参考.
           region.setWidthProportion(0.5); // 仅供参考.
           region.setHeightProportion(0.5); // 仅供参考.
           region.setAlpha(1.0); // 仅供参考.
           region.setZOrder(0); // 仅供参考.
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
   
           // Pass the configured audio and video parameters into the final structure.
           MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
           streamConfig.audioConfig = audioConfig;
           streamConfig.videoConfig = videoconfig;
           streamConfig.roomID = mRTCRoom.getRoomId();
           streamConfig.userID = localUid;
           streamConfig.regions = regions;
           
           String taskId = ""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
           
           // 更新流推送参数。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // 移除远端用户视图。
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   ```
   


<span id="ac44053d"></span>
### 离开直播间

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c877eaadfb9e4304995c4d6a787ef6df~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。


* MediaLive SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop)

   * [销毁](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy)

* RTC SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080)和[回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [销毁](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-destroy)

   * [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-destroyrtcengine)


**示例代码**


1. 停止回放，移除播放器视图，并销毁播放器。

   ```Java
   // Stop playback.
   mLivePlayer.stop();
   
   // Destroy the player.
   mLivePlayer.destroy();
   mLivePlayer = null;
   ```
   

2. 销毁 RTC 房间和 RTC 引擎。

   ```Java
   // Destroy the RTC room.
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine.
   RTCEngine.destroyRTCEngine();
   RTCEngine = null;
   ```
