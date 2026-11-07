---
title: "在 iOS 上實現互動式直播"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-interactive-live-for-ios-zh-TW"
---

本主題提供完整且逐步的指引，協助你將互動式直播功能整合至 iOS 應用程式。你將會看到針對主持人與觀眾核心功能的詳細程式碼範例，包括啟動直播、開啟主持人 PK 對戰，以及允許觀眾成為共同主持人。

<span id="bac8e2f8"></span>
## 先決條件


* 需擁有有效的[BytePlus 帳戶](http://console.byteplus.com/)，並已啟用[BytePlus MediaLive](https://console.byteplus.com/live)與[BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC)。如需更多資訊，請參閱[註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)、[啟用 MediaLive 服務](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-TW#da5a6a63)，以及[啟用 RTC 服務](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。

* 你已整合必要的 SDK：

   * BytePlus RTC SDK 版本 3.60.104 或以上。如需更多資訊，請參閱[在 iOS 整合 RTC SDK](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133)。

   * BytePlus MediaLive SDK，無特定版本要求。如需更多資訊，請參閱[整合 iOS 的 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios-zh-TW)與[初始化 iOS 版 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios-zh-TW)。


<span id="fd484c24"></span>
## 為主持人實現功能

本節說明如何為主持人實現互動式直播功能。

<span id="56ca198e"></span>
### 啟動直播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0d89fd738774914b44489e419af1509~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)與[回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-creatertcengine-delegate)

* [createRTCRoom:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-creatertcroom)

* [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig)

* [rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo)

* [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

* [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setvideoencoderconfig)

* [startVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-startvideocapture)

* [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-startaudiocapture)

* [startPushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-startpushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcEngine:onMixedStreamEvent:withMixedStreamInfo:withErrorCode:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCEngineDelegate-rtcengine-onmixedstreamevent-withmixedstreaminfo-witherrorcode)


**程式碼範例**


1. 建立 RTC 引擎與 RTC 房間，並加入 RTC 房間。

   ```objectivec
   // 設置 ByteRTCEngineDelegate 和 ByteRTCRoomDelegate 以接收與 RTC 引擎及 RTC 房間相關的回調。
   @interface VELPushInnerNewViewController () <
   ByteRTCEngineDelegate,
   ByteRTCRoomDelegate
   ......
   
   // Create an RTC engine.
   ByteRTCEngineConfig* engineConfig = [[ByteRTCEngineConfig alloc] init];
   engineConfig.appID = RTC_APP_ID; // Replace the RTC_APP_ID with the AppID you get after you create a BytePlus RTC app.
   engineConfig.isGameScene = FALSE;
   engineConfig.parameters = params;
   
   self.rtcEngine = [ByteRTCEngine createRTCEngine:engineConfig delegate:self];
   
   // 建立 RTC 房間。
   self.rtcRoom = [self.rtcEngine createRTCRoom:roomid];
   
   // 加入 RTC 房間。必須將房間配置設為直播配置，即ByteRTCRoomProfileLive。
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = @"zzx123";
   ByteRTCRoomConfig *roomConfig = [[ByteRTCRoomConfig alloc] init];
   roomConfig.profile = ByteRTCRoomProfileLive;
   [self.rtcRoom joinRoom:@"token" userInfo:userInfo userVisibility:TRUE roomConfig:roomConfig];
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如需瞭解如何獲取 AppID，請參閱<a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid">建立 BytePlus RTC 應用並獲取 AppID</a>。   </div>
   

2. 設定本地預覽畫面與視訊編碼參數。

   ```objectivec
   // Set the local preview view.
   ByteRTCVideoCanvas *canvasView = [[ByteRTCVideoCanvas alloc] init];
   canvasView.view = self.previewView;
   canvasView.renderMode = (ByteRTCRenderMode)renderMode;
   [self.rtcEngine setLocalVideoCanvas:ByteRTCStreamIndexMain withCanvas:canvasView];
   
   // Set video encoding parameters.
   ByteRTCVideoEncoderConfig *vconfig = [[ByteRTCVideoEncoderConfig alloc] init];
   vconfig.width = self.config.encodeSize.width;
   vconfig.height = self.config.encodeSize.height;
   vconfig.frameRate = self.config.encodeFPS;
   vconfig.maxBitrate = self.config.maxBitrate;
   vconfig.minBitrate = self.config.minBitrate;
   vconfig.encoderPreference = ByteRTCVideoEncoderPreferenceMaintainQuality;
   [self.rtcEngine setVideoEncoderConfig:vconfig];
   ```
   

3. 啟動音訊與視訊擷取。

   ```objectivec
   //  Start video capture.
   [self.rtcEngine startVideoCapture];
   
   // Start audio capture.
   [self.rtcEngine startAudioCapture];
   ```
   

4. 開始推流。

   ```objectivec
   // 設置推流配置，包括推流的 URL。
   ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
   pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
   pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
   
   // 設置轉碼用的視訊編碼參數。
   ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
   videoConfig.width = self.config.encodeSize.width;
   videoConfig.height = self.config.encodeSize.height;
   videoConfig.fps = self.config.encodeFPS;
   videoConfig.gop = self.config.encodeGOPSeconds;
   
   // 設置轉碼用的音訊編碼參數。
   ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
   audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
   audioConfig.sampleRate = 48000;
   audioConfig.channels = 2;
   audioConfig.bitrate = 128;
   audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
   
   // Set the push-to-CDN layout.由於房間內僅有主持人，將主持人的版面配置設為全畫布佔滿。
   ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
   region.roomID = [self.rtcRoom getRoomId];
   region.userID = @"zzx123";
   region.streamType = ByteRTCMixedStreamVideoTypeMain;
   region.mediaType = ByteRTCMixedStreamMediaTypeAudioAndVideo;
   region.renderMode = ByteRTCMixedStreamRenderModeFit;
   region.locationX = 0;
   region.locationY = 0;
   region.width = videoConfig.width;
   region.height = videoConfig.height;
   NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
   
   // 將已配置的音訊與視訊參數傳入最終結構。
   ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
   mixedStreamConfig.audioConfig = audioConfig;
   mixedStreamConfig.videoConfig = videoConfig;
   mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
   mixedStreamConfig.userID = @"zzx123";
   mixedStreamConfig.regions = regions;
   
   self.pushTaskId = @""; // 推流至 CDN 任務的唯一 ID，不超過 127 bytes。
   
   // Start pushing the stream.透過 ByteRTCEngineDelegate 接收推流狀態資訊。
   int ret = [self.rtcEngine startPushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   ```
   


<span id="064a1bc3"></span>
### （選用）為主持人啟用美顏 AR

請參閱[視訊特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)，了解如何為主持人啟用美顏 AR 功能的詳細操作。

<span id="de24a5cd"></span>
### 啟動主持人 PK 對戰

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/630a998ba11a46ac9e09eb9934778a15~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)與[回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-startforwardstreamtorooms)

* [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged)

* [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined)

* [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

* [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

* [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)


**程式碼範例**


1. 當主持人 A 成功收到啟動 PK 對戰通知時，呼叫`startForwardStreamToRooms:`，將主持人 A 的串流推送至主持人 B 的房間，並將主持人 B 的串流推送至主持人 A 的房間。

   ```objectivec
   // Push Host A's stream to Host B's room.configDict 包含 主持人 B 房間等資訊。
   NSMutableArray *dest = [NSMutableArray array];
   ByteRTCForwardStreamConfiguration *config = [[ByteRTCForwardStreamConfiguration alloc] initWithDict:configDict];
   [dest addObject:config];
   [self.rtcRoom startForwardStreamToRooms:dest];
   
   // Push Host B's stream to Host A's room.configDict 包含 主持人 A 房間等資訊。
   NSMutableArray *dest = [NSMutableArray array];
   ByteRTCForwardStreamConfiguration *config = [[ByteRTCForwardStreamConfiguration alloc] initWithDict:configDict];
   [dest addObject:config];
   [self.rtcRoom startForwardStreamToRooms:dest];
   ```
   

2. 當主持人收到`rtcRoom:onUserJoined:`回呼時，更新房間設定與推送至 CDN 的佈局。當主持人收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回呼時，更新遠端用戶畫面。

   ```objectivec
   // 對於主持人 A
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 設定房間型態為聯合直播型態，即 ByteRTCRoomProfileLINKMIC。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLINKMIC]
       
       // 設定推流配置，包含混流推送的 URL。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 設定轉碼的視訊編碼參數。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 設定轉碼的音訊編碼參數。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 將推流至 CDN 的版面配置由單人布局更新為雙人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主持人 A 的用戶 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 僅供參考。
       region.locationY        = 0.0; // 僅供參考。
       region.widthProportion    = 0.5; // 僅供參考。
       region.heightProportion   = 0.5; // 僅供參考。
       region.zOrder   = 0;   // 僅供參考。
       region.alpha    = 1.0; // 僅供參考。
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // 主持人 B 的用戶 ID。
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // 僅供參考。
       regionRemote.locationY        = 0.0; // 僅供參考。
       regionRemote.widthProportion    = 0.5; // 僅供參考。
       regionRemote.heightProportion   = 0.5; // 僅供參考。
       regionRemote.zOrder   = 0;   // 僅供參考。
       regionRemote.alpha    = 1.0; // 僅供參考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
       
       // 將已配置的音訊與視訊參數傳入最終結構。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // 更新推流參數。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (isPublish) {
           // 新增遠端用戶視圖。
           ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
           canvas.renderMode = ByteRTCRenderModeHidden;
           canvas.view.backgroundColor = [UIColor clearColor];
           canvas.view = view;
             
           ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
           streamKey.userId = info.uid;
           streamKey.streamIndex = ByteRTCStreamIndexMain;
           streamKey.roomId = info.roomID;
           [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
       }
   }
   // 對於主持人 B
        ...
       // 將推流至 CDN 的版面配置由單人布局更新為雙人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主持人 B 的用戶 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 僅供參考。
       region.locationY        = 0.0; // 僅供參考。
       region.widthProportion    = 0.5; // 僅供參考。
       region.heightProportion   = 0.5; // 僅供參考。
       region.zOrder   = 0;   // 僅供參考。
       region.alpha    = 1.0; // 僅供參考。
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // 主持人 A 的用戶 ID。
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // 僅供參考。
       regionRemote.locationY        = 0.0; // 僅供參考。
       regionRemote.widthProportion    = 0.5; // 僅供參考。
       regionRemote.heightProportion   = 0.5; // 僅供參考。
       regionRemote.zOrder   = 0;   // 僅供參考。
       regionRemote.alpha    = 1.0; // 僅供參考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
   ...
   ```
   


<span id="a0d4626c"></span>
### 結束主持人 PK 對戰

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a96045456f0146459f5f42928014351c~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)與[回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-stopforwardstreamtorooms)

* [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged)

* [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason)

* [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

* [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

* [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)


**程式碼範例**


1. 當主持人 A 成功收到結束 PK 對戰通知時，呼叫`stopForwardStreamToRooms`，停止將主持人 A 的串流推送至主持人 B 的房間，或將主持人 B 的串流推送至主持人 A 的房間。

   ```objectivec
   // Stop pushing Host A's stream to Host B's room.
   [self.rtcRoom stopForwardStreamToRooms];
   
   // Stop pushing Host B's stream to Host A's room.
   [self.rtcRoom stopForwardStreamToRooms];
   ```
   

2. 當主持人收到`rtcRoom:onUserLeave:reason:`回呼時，更新房間設定與推送至 CDN 的佈局。當主持人收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回呼時，移除遠端用戶畫面。

   ```objectivec
   // For Host A
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 設定房間型態為直播型態，即 ByteRTCRoomProfileLIVE。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLIVE]
       
       // 設定推流配置，包含混流推送的 URL。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 設定轉碼的視訊編碼參數。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 設定轉碼的音訊編碼參數。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 將推流至 CDN 的版面配置由雙人布局更新為單人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主持人 A 的用戶 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 僅供參考。
       region.locationY        = 0.0; // 僅供參考。
       region.widthProportion    = 0.5; // 僅供參考。
       region.heightProportion   = 0.5; // 僅供參考。
       region.zOrder   = 0;   // 僅供參考。
       region.alpha    = 1.0; // 僅供參考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
       
       // 將已配置的音訊與視訊參數傳入最終結構體。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // 更新推流參數。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (!isPublish) {
           // 移除遠端用戶畫面。
           ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
           canvas.renderMode = ByteRTCRenderModeHidden;
           canvas.view.backgroundColor = [UIColor clearColor];
           canvas.view = nil;
             
           ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
           streamKey.userId = info.uid;
           streamKey.streamIndex = ByteRTCStreamIndexMain;
           streamKey.roomId = info.roomID;
           [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
       }
   }
   // 對於主播 B
        ...
       // 將推流至 CDN 的版面配置由雙人佈局更新為單人佈局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播 B 的用戶 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 僅供參考。
       region.locationY        = 0.0; // 僅供參考。
       region.widthProportion    = 0.5; // 僅供參考。
       region.heightProportion   = 0.5; // 僅供參考。
       region.zOrder   = 0;   // 僅供參考。
       region.alpha    = 1.0; // 僅供參考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
    ...
   ```
   


<span id="5c1f93b7"></span>
### 結束直播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ba533c490f9482080cb464a8f803d5a~tplv-goo7wpa0wc-image.image) </span>

主要 API 與回呼如下。如需其他 API 與回呼的詳細資訊，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)與[回呼](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopPushMixedStream:withPushTargetType:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stoppushmixedstream-withpushtargettype)

* [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopvideocapture)

* [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopaudiocapture)

* [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

* [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-destroy)

* [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-destroyrtcengine)


**程式碼範例**


1. 停止推流。

   ```objectivec
   [self.rtcEngine stopPushMixedStream:self.pushTaskId withPushTargetType:ByteRTCMixedStreamPushTargetTypeToCDN];
   ```
   

2. 停止視訊與音訊擷取，並移除本地預覽畫面。

   ```objectivec
   // Stop video capture.
   [self.rtcEngine stopVideoCapture];
   
   // Stop audio capture.
   [self.rtcEngine stopAudioCapture];
   
   // Remove the local preview view.
   ByteRTCVideoCanvas *canvasView = [[ByteRTCVideoCanvas alloc] init];
   canvasView.view = nil;
   canvasView.renderMode = ByteRTCRenderModeHidden;
   [self.rtcEngine setLocalVideoCanvas:ByteRTCStreamIndexMain withCanvas:canvasView];
   ```
   

3. 銷毀 RTC 房間與 RTC 引擎。

   ```objectivec
   // Destroy the RTC room.
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Destroy the RTC engine.
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngine = nil;
   ```
   


<span id="ef36bbb0"></span>
## 為觀眾實現功能

本節說明如何為觀眾實現互動式直播功能。

<span id="7e071d75"></span>
### 觀看直播

觀眾使用播放器觀看直播。

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68d69fcb410f4f0c9da91c6147082532~tplv-goo7wpa0wc-image.image) </span>

`主要 API 及回調如下。如需瞭解其他 API 和回調，請參閱`[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)`及`[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)`。`


* [setConfig：](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig)

* [setObserver：](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver)

* [setPlayUrl：](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl)

* [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play)


**範例程式碼**


1. 建立並設置播放器。

   ```objectivec
   // Create a player.
   TVLManager *livePlayer = [[TVLManager alloc]initWithType:VeLivePlayerTypeOwn];
   self.livePlayer = livePlayer;
   
   // Set player callbacks.
   [self.livePlayer setObserver:self];
   
   // Set player parameters.
   VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc]init];
   config.enableStatisticsCallback = YES;
   config.enableLiveDNS = YES;
   config.enableSei = YES;
   [self.livePlayer setConfig:config];
   ```
   

2. 設置播放器視圖與拉流地址，並開始播放。

   ```objectivec
   // Set the player view.
   self.livePlayer.playerView.frame = self.view.bounds;
   [self.view addSubview:self.livePlayer.playerView];
   
   // Set the pull stream address.
   [self.livePlayer setPlayUrl:LIVE_PULL_URL];
   
   // Start playback.
   [self.livePlayer play];
   ```
   


<span id="1b3b748c"></span>
### （可選）為觀眾啟用美顏 AR

請參閱[視訊特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)，瞭解如何為觀眾啟用美顏 AR 功能的詳細說明。

<span id="a790a0eb"></span>
### 成為聯播主播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2102de0eb6a4bc5af75d006afc3da93~tplv-goo7wpa0wc-image.image) </span>

主要 API 及回調如下。


* MediaLive SDK。如需瞭解其他 API 和回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)及[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop)

* RTC SDK。如需瞭解其他 API 和回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)及[回調](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [createRTCEngine:delegate:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-creatertcengine-delegate)

   * [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

   * [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setvideoencoderconfig)

   * [startVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-startvideocapture)

   * [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-startaudiocapture)

   * [createRTCRoom:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-creatertcroom)

   * [joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig)

   * [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

   * [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)

   * [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined)

   * [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

   * [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)


**範例程式碼**


1. 停止播放並移除播放器視圖。

   ```objectivec
   // Stop playback.
   [self.livePlayer stop];
   
   // Remove the player view.
   self.livePlayer.playerView.hidden = YES;
   ```
   

2. 建立 RTC 引擎，設置本地預覽視圖及視訊編碼參數，並開始視訊與音訊採集。

   ```objectivec
   // 初始化 ByteRTCEngine 物件以接收與 RTC 引擎相關的回調。
   ByteRTCEngineConfig* engineConfig = [[ByteRTCEngineConfig alloc] init];
   engineConfig.appID = RTC_APP_ID;
   engineConfig.isGameScene = FALSE;
   engineConfig.parameters = params;
   // 創建 RTC 引擎。
   self.rtcEngine = [ByteRTCEngine createRTCEngine:engineConfig delegate:self];
   
   // 設定本地預覽畫面。
   ByteRTCVideoCanvas *canvasView = [[ByteRTCVideoCanvas alloc] init];
   canvasView.view = self.previewView;
   canvasView.renderMode = (ByteRTCRenderMode)renderMode;
   [self.rtcEngine setLocalVideoCanvas:ByteRTCStreamIndexMain withCanvas:canvasView];
   
   // 設定視訊編碼參數。
   ByteRTCVideoEncoderConfig *vconfig = [[ByteRTCVideoEncoderConfig alloc] init];
   vconfig.width = self.config.encodeSize.width;
   vconfig.height = self.config.encodeSize.height;
   vconfig.frameRate = self.config.encodeFPS;
   vconfig.maxBitrate = self.config.maxBitrate;
   vconfig.minBitrate = self.config.minBitrate;
   vconfig.encoderPreference = ByteRTCVideoEncoderPreferenceMaintainQuality;
   [self.rtcEngine setVideoEncoderConfig:vconfig];
   
   // 開始音視頻採集。
   [self.rtcEngine startVideoCapture];
   [self.rtcEngine startAudioCapture];
   ```
   

3. 建立並加入 RTC 房間，使用與主播相同的 RoomID。

   ```objectivec
   // 創建 RTC 房間。
   self.rtcRoom = [self.rtcEngine createRTCRoom:roomid];
   
   // 加入 RTC 房間。必須將 profile 設為連麥場景，即 ByteRTCRoomProfileLinkMic。
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = @"zzx123";
   ByteRTCRoomConfig *roomConfig = [[ByteRTCRoomConfig alloc] init];
   roomConfig.profile = ByteRTCRoomProfileLinkMic;
   [self.rtcRoom joinRoom:@"token" userInfo:userInfo userVisibility:TRUE roomConfig:roomConfig];
   ```
   

4. 當觀眾收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回調時，調用`setRemoteVideoCanvas:withCanvas:`調整遠端用戶視圖。

   ```objectivec
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish { {
           if (isPublish) {
               // Add the remote user view.
               ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
               canvas.renderMode = ByteRTCRenderModeHidden;
               canvas.view.backgroundColor = [UIColor clearColor];
               canvas.view = view;
                 
               ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
               streamKey.userId = info.uid;
               streamKey.streamIndex = ByteRTCStreamIndexMain;
               streamKey.roomId = info.roomID;
               [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
           } else {
               // Remove the remote user view.
               ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
               canvas.renderMode = ByteRTCRenderModeHidden;
               canvas.view.backgroundColor = [UIColor clearColor];
               canvas.view = null;
                 
               ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
               streamKey.userId = info.uid;
               streamKey.streamIndex = ByteRTCStreamIndexMain;
               streamKey.roomId = info.roomID;
               [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
           }
       }
   };
   ```
   

5. 當主播收到`rtcRoom:onUserJoined:`回調時，更新房間配置及推流至 CDN 的版面配置。當主播收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回調時，更新遠端用戶視圖。

   ```objectivec
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 設定 profile 為連麥場景，即 ByteRTCRoomProfileLINKMIC。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLINKMIC]
       
       // 設定推流配置，包括混流推送的 URL。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 設定轉碼的視訊編碼參數。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 設定轉碼的音訊編碼參數。一般建議與啟動直播時的配置保持一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 將推流至 CDN 的版面配置由單人佈局更新為雙人佈局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播的用戶 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 僅供參考。
       region.locationY        = 0.0; // 僅供參考。
       region.widthProportion    = 0.5; // 僅供參考。
       region.heightProportion   = 0.5; // 僅供參考。
       region.zOrder   = 0;   // 僅供參考。
       region.alpha    = 1.0; // 僅供參考。
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // 連麥者的用戶 ID。
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // 僅供參考。
       regionRemote.locationY        = 0.0; // 僅供參考。
       regionRemote.widthProportion    = 0.5; // 僅供參考。
       regionRemote.heightProportion   = 0.5; // 僅供參考。
       regionRemote.zOrder   = 0;   // 僅供參考。
       regionRemote.alpha    = 1.0; // 僅供參考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
       
       // 將已配置的音訊與視訊參數傳入最終結構體。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // 更新推流參數。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (isPublish) {
           // 新增遠端用戶畫面。
           ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
           canvas.renderMode = ByteRTCRenderModeHidden;
           canvas.view.backgroundColor = [UIColor clearColor];
           canvas.view = view;
             
           ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
           streamKey.userId = info.uid;
           streamKey.streamIndex = ByteRTCStreamIndexMain;
           streamKey.roomId = info.roomID;
           [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
       }
   }
   ```
   


<span id="b7ec9c92"></span>
### 結束聯播

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddafd73883f34341a54674c22021d699~tplv-goo7wpa0wc-image.image) </span>

主要 API 及回調如下。


* MediaLive SDK。如需瞭解其他 API 和回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)及[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)。

   * [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play)

* RTC SDK。如需瞭解其他 API 和回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)及[回調](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [leaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRTSRoom-leaveroom)

   * [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

   * [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)

   * [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason)

   * [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

   * [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

   * [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

   * [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopvideocapture)

   * [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopaudiocapture)


**範例程式碼**


1. 離開 RTC 房間，停止視訊與音訊採集，並移除本地預覽視圖及遠端用戶視圖。

   ```objectivec
   // Leave the RTC room.
   [self.rtcRoom leaveRoom];
   
   // Remove the local preview view.
   ByteRTCVideoCanvas *canvasView = [[ByteRTCVideoCanvas alloc] init];
   canvasView.view = nil; 
   canvasView.renderMode = ByteRTCRenderModeHidden;
   [self.rtcEngine setLocalVideoCanvas:ByteRTCStreamIndexMain withCanvas:canvasView];
   
   // Remove the remote user view.
   ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
   canvas.renderMode = ByteRTCRenderModeHidden;
   canvas.view.backgroundColor = [UIColor clearColor];
   canvas.view = nil;
           
   ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
   streamKey.userId = uid;
   streamKey.streamIndex = ByteRTCStreamIndexMain;
   streamKey.roomId = self.roomId;
   [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
   
   // Stop video capture.
   [self.rtcEngine stopVideoCapture];
   
   // Stop audio capture.
   [self.rtcEngine stopAudioCapture];
   ```
   

2. 設置播放器視圖並開始播放。

   ```objectivec
   // Set the player view.
   self.livePlayer.playerView.hidden = NO;
   
   // Start playback.
   [self.livePlayer play];
   ```
   

3. 當主播收到`rtcRoom:onUserLeave:reason:`回調時，更新房間配置及推流至 CDN 的版面配置。當主播收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回調時，移除遠端用戶視圖。

   ```objectivec
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 設定 profile 為直播場景，即 ByteRTCRoomProfileLIVE。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLIVE]
       
       // 設定推流配置，包括混流推送的 URL。一般而言，請保持配置與啟動直播時所用配置一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 設定視訊編碼參數以進行轉碼。一般而言，請保持配置與啟動直播時所用配置一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 設定音訊編碼參數以進行轉碼。一般而言，請保持配置與啟動 直播時所用配置一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 將推流至 CDN 的版面配置從2人版面變更為1人版面。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主持人的用戶 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 僅供參考。
       region.locationY        = 0.0; // 僅供參考。
       region.widthProportion    = 0.5; // 僅供參考。
       region.heightProportion   = 0.5; // 僅供參考。
       region.zOrder   = 0;   // 僅供參考。
       region.alpha    = 1.0; // 僅供參考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
       
       // 將已配置的音訊與視訊參數傳入最終結構。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // 推流至 CDN 的任務 ID，必須與啟動直播時所配置的相同。
       
       // 更新推流參數。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (!isPublish) {
           // 移除遠端用戶視圖。
           ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
           canvas.renderMode = ByteRTCRenderModeHidden;
           canvas.view.backgroundColor = [UIColor clearColor];
           canvas.view = nil;
             
           ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
           streamKey.userId = info.uid;
           streamKey.streamIndex = ByteRTCStreamIndexMain;
           streamKey.roomId = info.roomID;
           [self.rtcEngine setRemoteVideoCanvas:streamKey withCanvas:canvas];
       }
   }
   ```
   


<span id="7610522f"></span>
### 離開直播間

**時序圖**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6913fad5f1a24afb937dbf66c52e2118~tplv-goo7wpa0wc-image.image) </span>


* MediaLive SDK。如需瞭解其他 API 和回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)及[回調](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop)

   * [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy)

* RTC SDK。如需瞭解其他 API 和回調，請參閱[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)及[回調](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-destroy)

   * [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-destroyrtcengine)


**範例程式碼**


1. 停止播放，移除播放器視圖並銷毀播放器。

   ```objectivec
   // Stop playback.
   [self.livePlayer stop];
   
   // Remove the player view.
   self.livePlayer.playerView.hidden = YES;
   
   // Destroy the player.
   [self.livePlayer destroy];
   self.livePlayer = nil;
   ```
   

2. 銷毀 RTC 房間及 RTC 引擎。

   ```objectivec
   // Destroy the RTC room.
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Destroy the RTC engine.
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngine = nil;
   ```
