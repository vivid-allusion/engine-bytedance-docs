---
title: "在 Android 上實現互動式直播功能"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-interactive-live-for-android-zh-TW"
---

本主題提供完整且逐步的指引，協助你將互動式直播功能整合至 Android 應用程式。你將會看到針對主播與觀眾的核心功能實現的詳細程式碼範例，包括開啟直播、啟用主播 PK 對戰，以及讓觀眾成為聯合主播。

<span id="d0660c19"></span>
## 先決條件


* 已啟用 [BytePlus 帳戶](http://console.byteplus.com/)、[BytePlus MediaLive](https://console.byteplus.com/live) 和 [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC)。如需更多資訊，請參閱 [註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)、[啟用 MediaLive 服務](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-TW#da5a6a63)，以及 [啟用 RTC 服務](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。

* 你已整合所需的 SDK：

   * BytePlus RTC SDK 版本 3.60.104 或以上。如需更多資訊，請參閱 [整合 Android RTC SDK](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70134)。

   * BytePlus MediaLive SDK，無特定版本要求。如需更多資訊，請參閱 [整合 Android Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-TW) 和 [初始化 Android 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android-zh-TW)。


<span id="86abfd57"></span>
## 主播播端功能實現

本節提供主播播端實現互動式直播功能的指引。

<span id="33f82960"></span>
### 開啟直播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2347c01157542d89c81f6a4ec544765~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


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


**程式碼範例**


1. 建立 RTC 引擎與 RTC 房間，並加入 RTC 房間。

   ```Java
   // Create an RTC engine.設定 rtcEngineHandler 以接收與 RTC 引擎相關的回調。
   EngineConfig config = new EngineConfig();
   config.parameters = new JSONObject();
   config.context = mContext;
   config.appID = RTC_APP_ID; // 將 RTC_APP_ID 替換為你建立 BytePlus RTC 應用後取得的 AppID。
   mRTCEngine = RTCEngine.createRTCEngine(config, rtcEngineHandler);
   
   // 建立 RTC 房間。設定 rtcRoomHandler 以接收與 RTC 房間相關的回調。
   mRTCRoom = mRTCEngine.createRTCRoom(roomid);
   mRTCRoom.setRTCRoomEventHandler(rtcRoomHandler);
   
   // 加入 RTC 房間。房間設定必須設為直播設定，即 ROOM_PROFILE_LIVE。
   mUserId = userId;
   mRoomId = roomId;
   UserInfo userInfo = new UserInfo(userId, null);
   RTCRoomConfig roomConfig = new RTCRoomConfig(ROOM_PROFILE_LIVE,
           true, true, true);
   mRTCRoom.joinRoom(token, userInfo, true, roomConfig);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如需瞭解如何取得 AppID，請參閱<a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid">建立 BytePlus RTC 應用並取得 AppID</a>。   </div>
   

2. 設定本地預覽畫面與視訊編碼參數。

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
   

3. 啟動音訊與視訊擷取。

   ```Java
   // Start video capture.
   mRTCEngine.startVideoCapture();
   
   // Start audio capture.
   mRTCEngine.startAudioCapture();
   ```
   

4. 開始推流。

   ```Java
   // 設定推流配置，包括 要推流的 URL。
   MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
   pushTargetConfig.pushCDNURL = mTargetUrl;
   pushTargetConfig.pushTargetType = PUSH_TO_CDN;
   
   // 設定視訊編碼參數以進行轉碼。
   MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
   videoconfig.fps = mConfig.mmVideoEncoderFps;
   videoconfig.height = mConfig.mVideoEncoderHeight;;
   videoconfig.width = mConfig.mVideoEncoderWidth;;
   videoconfig.bitrate = mVideoEncoderKBitrate;
   videoconfig.gop = mConfig.mVideoGopVal;
   
   // 設定音訊編碼參數以進行轉碼。
   MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
   audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
   audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
   audioConfig.bitrate = 128;
   audioConfig.channels = 2;
   audioConfig.sampleRate = 48000;
   
   // 設定推流至 CDN的版面配置。由於房間內僅有主持人，將主持人的版面配置設為全畫布佔滿。
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
   
   // 將已配置的音訊與視訊參數傳入最終結構。
   MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
   streamConfig.audioConfig = audioConfig;
   streamConfig.videoConfig = videoconfig;
   streamConfig.roomID = mRTCRoom.getRoomId();
   streamConfig.userID = localUid;
   streamConfig.regions = regions;
   
   String taskId = ""; // A  unique ID for the push-to-CDN task, which does not exceed 127 bytes.
   
   // Start pushing the stream.透過建立 RTC 引擎時設定的 rtcEngineHandler 接收串流推送狀態資訊。
   mRTCEngine.startPushMixedStream(taskId, pushTargetConfig, streamConfig);
   ```
   


<span id="fb003e2e"></span>
### （選用）為主播啟用美顏 AR

請參閱 [視訊特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)，了解如何為主播啟用美顏 AR 功能的詳細指引。

<span id="91ff8ccd"></span>
### 開啟主播 PK 對戰

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ee305921cc46feabe545fa0af2131c~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#startforwardstreamtorooms)

* [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged)

* [onUserJoined](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserjoined)

* [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

* [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

* [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

* [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)


**程式碼範例**


1. 當主播 A 成功收到開啟 PK 對戰通知時，呼叫 `startForwardStreamToRooms`，將主播 A 的串流推送至主播 B 的房間，並將主播 B 的串流推送至主播 A 的房間。

   ```Java
   // Push Host A's stream to Host B's room.
   mRTCRoom1.startForwardStreamToRooms(room2ID, token);
   
   // Push Host B's stream to Host A's room.
   mRTCRoom2.startForwardStreamToRooms(room1ID, token);
   ```
   

2. 當主播播端收到 `onUserJoined` 回呼時，更新房間設定與推送至 CDN 的版面配置。當主播播端收到 `onUserPublishStreamVideo` 回呼時，更新遠端用戶畫面。

   ```Java
   // 對於主持人A
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserJoined(UserInfo userInfo) {
           // 設定房間為聯合直播模式，即ROOM_PROFILE_LINKMIC。
           mRTCRoom1.setRoomProfile(ROOM_PROFILE_LINKMIC);
           
           // 設定串流推送配置，包括要推送混合串流的 URL。一般建議與啟動直播時的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 設定視訊編碼參數以進行轉碼。一般建議與啟動直播時的配置保持一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mConfig.mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 設定音訊編碼參數以進行轉碼。一般建議與啟動直播時的配置保持一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 將推流至 CDN 的版面配置由單人配置更新為雙人配置。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主持人 A 的使用者 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 僅供參考。
           region.setLocationY(0.0); // 僅供參考。
           region.setWidthProportion(0.5); // 僅供參考。
           region.setHeightProportion(0.5); // 僅供參考。
           region.setAlpha(1.0); // 僅供參考。
           region.setZOrder(0); // 僅供參考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // 主持人 B 的使用者 ID。
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // 僅供參考。
           regionRemote.setLocationY(0.0); // 僅供參考。
           regionRemote.setWidthProportion(0.5); // 僅供參考。
           regionRemote.setHeightProportion(0.5); // 僅供參考。
           regionRemote.setAlpha(1.0); // 僅供參考。
           regionRemote.setZOrder(0); // 僅供參考。
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
           
           // 更新串流推送參數。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // 新增遠端使用者畫面。
               TextureView renderView = new TextureView(Env.getApplicationContext());
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = renderView;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   // 對於主持人 B
           ...
           // 將推流至 CDN 的版面配置由單人配置更新為雙人配置。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主持人 B 的使用者 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 僅供參考。
           region.setLocationY(0.0); // 僅供參考。
           region.setWidthProportion(0.5); // 僅供參考。
           region.setHeightProportion(0.5); // 僅供參考。
           region.setAlpha(1.0); // 僅供參考。
           region.setZOrder(0); // 僅供參考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // 主持人 A 的使用者 ID。
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // 僅供參考。
           regionRemote.setLocationY(0.0); // 僅供參考。
           regionRemote.setWidthProportion(0.5); // 僅供參考。
           regionRemote.setHeightProportion(0.5); // 僅供參考。
           regionRemote.setAlpha(1.0); // 僅供參考。
           regionRemote.setZOrder(0); // 僅供參考。
           regionRemote.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[1] = regionRemote;
           ...
   ```
   


<span id="91a69d1c"></span>
### 結束主播 PK 對戰

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b655a753b164cda9efbd7239b2eb908~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-stopforwardstreamtorooms)

* [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged)

* [onUserLeave](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserleave)

* [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

* [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

* [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

* [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)


**程式碼範例**


1. 當主播 A 成功收到結束 PK 對戰通知時，呼叫 `stopForwardStreamToRooms`，停止將主播 A 的串流推送至主播 B 的房間，或將主播 B 的串流推送至主播 A 的房間。

   ```Java
   // Stop pushing Host A's stream to Host B's room.
   mRTCRoom1.stopForwardStreamToRooms();
   
   // Stop pushing Host B's stream to Host A's room.
   mRTCRoom2.stopForwardStreamToRooms();
   ```
   

2. 當主播播端收到 `onUserLeave` 回呼時，更新房間設定與推送至 CDN 的版面配置。當主播播端收到 `onUserPublishStreamVideo` 回呼時，移除遠端用戶畫面。

   ```Java
   // For Host A
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserLeave(String uid, int reason) {
           // 設定房間為直播模式，即ROOM_PROFILE_LIVE。
           mRTCRoom1.setRoomProfile(ROOM_PROFILE_LIVE);
           
           // 設定串流推送配置，包括要推送混合串流的 URL。一般建議與啟動直播時的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 設定視訊編碼參數以進行轉碼。一般建議與啟動直播時的配置保持一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 設定音訊編碼參數以進行轉碼。一般建議與啟動直播時的配置保持一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 將推流至 CDN 的版面配置由雙人配置更新為單人配置。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主持人 A 的使用者 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 僅供參考。
           region.setLocationY(0.0); // 僅供參考。
           region.setWidthProportion(0.5); // 僅供參考。
           region.setHeightProportion(0.5); // 僅供參考。
           region.setAlpha(1.0); // 僅供參考。
           region.setZOrder(0); // 僅供參考。
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
           
           // 更新推流參數。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // 移除遠端用戶畫面。
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   // 針對主播 B
            ...
           // 將推流到 CDN 的版面配置由雙人佈局更新為單人佈局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播 B 的用戶 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 僅供參考。
           region.setLocationY(0.0); // 僅供參考。
           region.setWidthProportion(0.5); // 僅供參考。
           region.setHeightProportion(0.5); // 僅供參考。
           region.setAlpha(1.0); // 僅供參考。
           region.setZOrder(0); // 僅供參考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           ...
   ```
   


<span id="33d6c35f"></span>
### 結束直播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e525b9e474634955a1b1859dc16d0a69~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) 和 [回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stoppushmixedstream)

* [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopvideocapture)

* [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startaudiocapture)

* [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

* [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-destroy)

* [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-destroyrtcengine)


**程式碼範例**


1. 停止推流。

   ```Java
   mRTCEngine.stopPushMixedStream(taskId, PUSH_TO_CDN);
   ```
   

2. 停止視訊與音訊擷取，並移除本地預覽畫面。

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
   

3. 銷毀 RTC 房間與 RTC 引擎。

   ```Java
   // Destroy the RTC room.
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine.
   mRTCEngine.destroyRTCEngine();
   mRTCEngine = null;
   ```
   


<span id="ec36bcae"></span>
## 觀眾端功能實現

本節提供觀眾端實現互動式直播功能的指引。

<span id="935dd891"></span>
### 觀看直播

觀眾使用播放器觀看直播。

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c1f1f3e252648aaa05fda30502ad6f3~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回調如下。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)與[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。


* [setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig)

* [setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver)

* [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)

* [setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl)

* [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play)


**範例程式碼**


1. 建立並設定播放器。

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
   

2. 設定播放器視圖與拉流地址，並啟動播放。

   ```Java
   // Set the player view.
   mLivePlayer.setSurfaceHolder(holder);
   
   // Set the pull stream address.
   mLivePlayer.setPlayUrl(mPullUrl);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<span id="148f2373"></span>
### （可選）為觀眾啟用美顏 AR

請參閱[視訊特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)，瞭解如何為觀眾啟用美顏 AR 功能的詳細操作。

<span id="c6e434d1"></span>
### 成為聯播主播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f085b77054334c1585a68383690539b7~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回調如下。


* MediaLive SDK。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)與[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop)

* RTC SDK。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080)與[回調](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

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


**範例程式碼**


1. 停止播放並移除播放器視圖。

   ```Java
   // Stop playback.
   mLivePlayer.stop();
   ```
   

2. 建立 RTC 引擎，設定本地預覽視圖與視訊編碼參數，並啟動視訊與音訊擷取。

   ```Java
   // Create an RTC engine.設置 rtcEngineHandler 以接收與 RTC 引擎相關的回調。
   EngineConfig config = new EngineConfig();
   config.parameters = new JSONObject();
   config.context = mContext;
   config.appID = RTC_APP_ID;
   mRTCEngine = RTCEngine.createRTCEngine(config, rtcEngineHandler);
   
   // 設置本地預覽畫面。
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = renderView;
   videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCEngine.setLocalVideoCanvas(StreamIndex.STREAM_INDEX_MAIN, videoCanvas);
   
   // 設置視頻編碼參數。
   VideoEncoderConfig config = new VideoEncoderConfig(
           mConfig.mVideoEncoderWidth, mConfig.mVideoEncoderHeight, mConfig.mVideoEncoderFps, mConfig.mVideoEncoderKBitrate * 1000);
   mRTCEngine.setVideoEncoderConfig(config);
   
   // 開始音視頻採集。
   mRTCEngine.startVideoCapture();
   mRTCEngine.startAudioCapture();
   ```
   

3. 建立並加入 RTC 房間，使用與主播相同的 RoomID。

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
   

4. 當觀眾收到`onUserPublishStreamVideo`回調時，呼叫`setRemoteVideoCanvas`調整遠端用戶視圖。

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
   

5. 當主播收到`onUserJoined`回調時，更新房間設定與推流至 CDN 的佈局。當主播收到`onUserPublishStreamVideo`回調時，更新遠端用戶視圖。

   ```Java
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserJoined(UserInfo userInfo) {
           // 設置房間型態為聯播型態，即 ROOM_PROFILE_LINKMIC。
           mRTCRoom.setRoomProfile(ROOM_PROFILE_LINKMIC)
       
           // 設置推流配置，包括推送混流的URL。一般建議與開始直播時的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 設置轉碼用的視頻編碼參數。一般建議與開始直播時的配置保持一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 設置轉碼用的音頻編碼參數。一般建議與開始直播時的配置保持一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 將推流到 CDN 的版面配置由單人佈局更新為雙人佈局。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主播的用戶 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 僅供參考。
           region.setLocationY(0.0); // 僅供參考。
           region.setWidthProportion(0.5); // 僅供參考。
           region.setHeightProportion(0.5); // 僅供參考。
           region.setAlpha(1.0); // 僅供參考。
           region.setZOrder(0); // 僅供參考。
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // 聯播者的用戶 ID。
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // 僅供參考。
           regionRemote.setLocationY(0.0); // 僅供參考。
           regionRemote.setWidthProportion(0.5); // 僅供參考。
           regionRemote.setHeightProportion(0.5); // 僅供參考。
           regionRemote.setAlpha(1.0); // 僅供參考。
           regionRemote.setZOrder(0); // 僅供參考。
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
           
           // 更新推流參數。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // 添加遠端用戶畫面。
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
### 停止聯播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65e0b0f83f7d4812bc0a798855b637e0~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回調如下。


* MediaLive SDK。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)與[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。

   * [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)

   * [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play)

* RTC SDK。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080)與[回調](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [leaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTSRoom-leaveroom)

   * [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

   * [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)

   * [onUserLeave](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserleave)

   * [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

   * [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

   * [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

   * [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopvideocapture)

   * [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopaudiocapture)


**範例程式碼**


1. 離開 RTC 房間，停止視訊與音訊擷取，並移除本地預覽視圖與遠端用戶視圖。

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
   

2. 設定播放器視圖並啟動播放。

   ```Java
   // Set the player view.
   mLivePlayer.setSurfaceHolder(holder);
   // Start playback.
   mLivePlayer.play();
   ```
   

3. 當主播收到`onUserLeave`回調時，更新房間設定與推流至 CDN 的佈局。當主播收到`onUserPublishStreamVideo`回調時，移除遠端用戶視圖。

   ```Java
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserLeave(String uid, int reason) {
           // 設置房間型態為直播型態，即 ROOM_PROFILE_LIVE。
           mRTCRoom.setRoomProfile(ROOM_PROFILE_LIVE)
           
           // 設置推流配置，包括推送混流的URL。一般建議與開始直播時的配置保持一致。
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // 設置轉碼用的視頻編碼參數。一般而言，請保持配置與啟動直播時所使用的配置一致。
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // 設置音訊編碼參數以進行轉碼。一般而言，請保持配置與啟動直播時所使用的配置一致。
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // 將推流至 CDN 的版面從雙人版面更新為單人版面。
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // 主持人的用戶 ID。
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // 僅供參考.
           region.setLocationY(0.0); // 僅供參考.
           region.setWidthProportion(0.5); // 僅供參考.
           region.setHeightProportion(0.5); // 僅供參考.
           region.setAlpha(1.0); // 僅供參考.
           region.setZOrder(0); // 僅供參考.
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
           
           // 更新推流參數。
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // 移除遠端用戶視圖。
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
### 離開直播間

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c877eaadfb9e4304995c4d6a787ef6df~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回調如下。


* MediaLive SDK。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference)與[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop)

   * [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy)

* RTC SDK。如需瞭解其他 API 與回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080)與[回調](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-destroy)

   * [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-destroyrtcengine)


**範例程式碼**


1. 停止播放，移除播放器視圖並銷毀播放器。

   ```Java
   // Stop playback.
   mLivePlayer.stop();
   
   // Destroy the player.
   mLivePlayer.destroy();
   mLivePlayer = null;
   ```
   

2. 銷毀 RTC 房間與 RTC 引擎。

   ```Java
   // Destroy the RTC room.
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine.
   RTCEngine.destroyRTCEngine();
   RTCEngine = null;
   ```
