---
title: "在 iOS 上实现互动直播"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-interactive-live-for-ios-zh-CN"
---

本主题为你提供全面的分步说明，指导如何将互动直播功能集成到你的 iOS 应用中。你将获得详细的代码示例，帮助实现主播和观众的核心功能，包括开启直播流、启用连麦 PK，以及允许观众成为连麦（主播与主播）。

<span id="bac8e2f8"></span>
## 前提条件


* 已激活 [BytePlus 账号](http://console.byteplus.com/)、[BytePlus MediaLive](https://console.byteplus.com/live) 和 [火山引擎实时音视频](https://console.byteplus.com/rtc/workplaceRTC)。更多信息，请参见 [注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)、[激活 MediaLive 服务](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-zh-CN#da5a6a63)，以及 [激活实时音视频服务](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865)。

* 你已集成所需的 SDK：

   * 火山引擎实时音视频 SDK 版本 3.60.104 或更高。更多信息，请参见 [iOS 集成实时音视频 SDK](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133)。

   * BytePlus MediaLive SDK，无特定版本要求。更多信息，请参见 [集成 iOS 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios-zh-CN) 和 [初始化 iOS 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios-zh-CN)。


<span id="fd484c24"></span>
## 为主播实现功能

本节为你提供主播端实现互动直播功能的说明。

<span id="56ca198e"></span>
### 开启直播流

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0d89fd738774914b44489e419af1509~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


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


**示例代码**


1. 创建 RTC 引擎和 RTC 房间，并加入 RTC 房间。

   ```objectivec
   // 设置 ByteRTCEngineDelegate 和 ByteRTCRoomDelegate，以接收与 RTC 引擎和 RTC 房间相关的回调。
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
   
   // 创建 RTC 房间。
   self.rtcRoom = [self.rtcEngine createRTCRoom:roomid];
   
   // 加入 RTC 房间。必须将房间配置设置为直播流配置，即ByteRTCRoomProfileLive。
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = @"zzx123";
   ByteRTCRoomConfig *roomConfig = [[ByteRTCRoomConfig alloc] init];
   roomConfig.profile = ByteRTCRoomProfileLive;
   [self.rtcRoom joinRoom:@"token" userInfo:userInfo userVisibility:TRUE roomConfig:roomConfig];
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">关于如何获取 AppID 的更多信息，请参见<a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid">创建火山引擎实时音视频应用并获取 AppID</a>。   </div>
   

2. 设置本地预告视图和视频编码参数。

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
   

3. 开始音视频采集。

   ```objectivec
   //  Start video capture.
   [self.rtcEngine startVideoCapture];
   
   // Start audio capture.
   [self.rtcEngine startAudioCapture];
   ```
   

4. 开始推流。

   ```objectivec
   // 设置流推送配置，包括要推送流的 URL。
   ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
   pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
   pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
   
   // 设置转码的视频编码参数。
   ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
   videoConfig.width = self.config.encodeSize.width;
   videoConfig.height = self.config.encodeSize.height;
   videoConfig.fps = self.config.encodeFPS;
   videoConfig.gop = self.config.encodeGOPSeconds;
   
   // 设置转码的音频编码参数。
   ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
   audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
   audioConfig.sampleRate = 48000;
   audioConfig.channels = 2;
   audioConfig.bitrate = 128;
   audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
   
   // Set the push-to-CDN layout.由于房间内只有主播，将主播的布局设置为占满整个画布。
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
   
   // 将配置好的音频和视频参数传入最终结构。
   ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
   mixedStreamConfig.audioConfig = audioConfig;
   mixedStreamConfig.videoConfig = videoConfig;
   mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
   mixedStreamConfig.userID = @"zzx123";
   mixedStreamConfig.regions = regions;
   
   self.pushTaskId = @""; // 推流到 CDN 任务的唯一 ID，不超过 127 字节。
   
   // Start pushing the stream.通过 ByteRTCEngineDelegate 接收流推送状态信息。
   int ret = [self.rtcEngine startPushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   ```
   


<span id="064a1bc3"></span>
### （可选）为主播启用美颜

请参见 [视频特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)，获取主播端启用美颜功能的详细说明。

<span id="de24a5cd"></span>
### 开启连麦 PK

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/630a998ba11a46ac9e09eb9934778a15~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-startforwardstreamtorooms)

* [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged)

* [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined)

* [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

* [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

* [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)


**示例代码**


1. 当主播 A 收到连麦 PK 成功通知时，调用 `startForwardStreamToRooms:`，将主播 A 的流推送到主播 B 的房间，将主播 B 的流推送到主播 A 的房间。

   ```objectivec
   // Push Host A's stream to Host B's room.configDict 包含 主播 B 房间等信息。
   NSMutableArray *dest = [NSMutableArray array];
   ByteRTCForwardStreamConfiguration *config = [[ByteRTCForwardStreamConfiguration alloc] initWithDict:configDict];
   [dest addObject:config];
   [self.rtcRoom startForwardStreamToRooms:dest];
   
   // Push Host B's stream to Host A's room.configDict 包含 主播 A 房间等信息。
   NSMutableArray *dest = [NSMutableArray array];
   ByteRTCForwardStreamConfiguration *config = [[ByteRTCForwardStreamConfiguration alloc] initWithDict:configDict];
   [dest addObject:config];
   [self.rtcRoom startForwardStreamToRooms:dest];
   ```
   

2. 当主播收到 `rtcRoom:onUserJoined:` 回调时，更新房间配置和推流到 CDN 的布局。当主播收到 `rtcRoom:onUserPublishStreamVideo:info:isPublish:` 回调时，更新远端用户视图。

   ```objectivec
   // 针对主播 A
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 设置房间配置为连麦（主播与主播）配置，即 ByteRTCRoomProfileLINKMIC。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLINKMIC]
       
       // 设置流推送配置，包括要推送混流的 URL。一般保持与启动 直播流 时使用的配置一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 设置转码的视频编码参数。一般保持与启动直播流时使用的配置一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 设置转码的音频编码参数。一般保持与启动直播流时使用的配置一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 将推流到 CDN 的布局从单人布局更新为双人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播 A 的用户 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 仅供参考。
       region.locationY        = 0.0; // 仅供参考。
       region.widthProportion    = 0.5; // 仅供参考。
       region.heightProportion   = 0.5; // 仅供参考。
       region.zOrder   = 0;   // 仅供参考。
       region.alpha    = 1.0; // 仅供参考。
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // 主播 B 的用户 ID。
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // 仅供参考。
       regionRemote.locationY        = 0.0; // 仅供参考。
       regionRemote.widthProportion    = 0.5; // 仅供参考。
       regionRemote.heightProportion   = 0.5; // 仅供参考。
       regionRemote.zOrder   = 0;   // 仅供参考。
       regionRemote.alpha    = 1.0; // 仅供参考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
       
       // 将配置好的音频和视频参数传入最终结构。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // 更新流推送参数。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (isPublish) {
           // 添加远端用户视图。
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
   // 针对主播 B
        ...
       // 将推流到 CDN 的布局从单人布局更新为双人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播 B 的用户 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 仅供参考。
       region.locationY        = 0.0; // 仅供参考。
       region.widthProportion    = 0.5; // 仅供参考。
       region.heightProportion   = 0.5; // 仅供参考。
       region.zOrder   = 0;   // 仅供参考。
       region.alpha    = 1.0; // 仅供参考。
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // 主播 A 的用户 ID。
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // 仅供参考。
       regionRemote.locationY        = 0.0; // 仅供参考。
       regionRemote.widthProportion    = 0.5; // 仅供参考。
       regionRemote.heightProportion   = 0.5; // 仅供参考。
       regionRemote.zOrder   = 0;   // 仅供参考。
       regionRemote.alpha    = 1.0; // 仅供参考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
   ...
   ```
   


<span id="a0d4626c"></span>
### 结束连麦 PK

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a96045456f0146459f5f42928014351c~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-stopforwardstreamtorooms)

* [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged)

* [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason)

* [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

* [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

* [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)


**示例代码**


1. 当主播 A 收到结束连麦 PK 成功通知时，调用 `stopForwardStreamToRooms`，停止将主播 A 的流推送到主播 B 的房间或主播 B 的流推送到主播 A 的房间。

   ```objectivec
   // Stop pushing Host A's stream to Host B's room.
   [self.rtcRoom stopForwardStreamToRooms];
   
   // Stop pushing Host B's stream to Host A's room.
   [self.rtcRoom stopForwardStreamToRooms];
   ```
   

2. 当主播收到 `rtcRoom:onUserLeave:reason:` 回调时，更新房间配置和推流到 CDN 的布局。当主播收到 `rtcRoom:onUserPublishStreamVideo:info:isPublish:` 回调时，移除远端用户视图。

   ```objectivec
   // For Host A
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 设置房间配置为直播流配置，即 ByteRTCRoomProfileLIVE。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLIVE]
       
       // 设置流推送配置，包括要推送混流的 URL。一般保持与启动 直播流 时使用的配置一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 设置转码的视频编码参数。一般保持与启动 直播流 时使用的配置一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 设置转码的音频编码参数。一般保持与启动 直播流 时使用的配置一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 将推流到 CDN 的布局从双人布局更新为单人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播 A 的用户 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 仅供参考.
       region.locationY        = 0.0; // 仅供参考.
       region.widthProportion    = 0.5; // 仅供参考.
       region.heightProportion   = 0.5; // 仅供参考.
       region.zOrder   = 0;   // 仅供参考.
       region.alpha    = 1.0; // 仅供参考.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
       
       // 将已配置的音频和视频参数传入最终结构体。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // 更新流推送参数。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (!isPublish) {
           // 移除远端用户视图。
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
   // 对于主播 B
        ...
       // 将推流到 CDN 的布局从双人布局更新为单人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播 B 的用户 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 仅供参考.
       region.locationY        = 0.0; // 仅供参考.
       region.widthProportion    = 0.5; // 仅供参考.
       region.heightProportion   = 0.5; // 仅供参考.
       region.zOrder   = 0;   // 仅供参考.
       region.alpha    = 1.0; // 仅供参考.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
    ...
   ```
   


<span id="5c1f93b7"></span>
### 结束直播流

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ba533c490f9482080cb464a8f803d5a~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见 [API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) 和 [回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。


* [stopPushMixedStream:withPushTargetType:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stoppushmixedstream-withpushtargettype)

* [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopvideocapture)

* [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopaudiocapture)

* [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

* [销毁](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-destroy)

* [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-destroyrtcengine)


**示例代码**


1. 停止推流。

   ```objectivec
   [self.rtcEngine stopPushMixedStream:self.pushTaskId withPushTargetType:ByteRTCMixedStreamPushTargetTypeToCDN];
   ```
   

2. 停止音视频采集，并移除本地预告视图。

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
   

3. 销毁 RTC 房间和 RTC 引擎。

   ```objectivec
   // Destroy the RTC room.
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Destroy the RTC engine.
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngine = nil;
   ```
   


<span id="ef36bbb0"></span>
## 为观众实现功能

本节为你提供观众端实现互动直播功能的说明。

<span id="7e071d75"></span>
### 观看直播流

观众使用播放器观看直播流。

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68d69fcb410f4f0c9da91c6147082532~tplv-goo7wpa0wc-image.image) </span>

`主要 API 和回调如下。关于其他 API 和回调的更多信息，请参见`[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)`和`[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)`。`


* [setConfig：](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig)

* [setObserver：](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver)

* [setPlayUrl：](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl)

* [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play)


**示例代码**


1. 创建并设置播放器。

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
   

2. 设置播放器视图和拉流地址，并开始回放。

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
### （可选）为观众开启美颜

有关为观众开启美颜功能的详细操作，请参见[视频特效](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717)。

<span id="a790a0eb"></span>
### 成为连麦（主播与主播）

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2102de0eb6a4bc5af75d006afc3da93~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。


* MediaLive SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop)

* RTC SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)和[回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

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


**示例代码**


1. 停止回放并移除播放器视图。

   ```objectivec
   // Stop playback.
   [self.livePlayer stop];
   
   // Remove the player view.
   self.livePlayer.playerView.hidden = YES;
   ```
   

2. 创建 RTC 引擎，设置本地预览视图和视频编码参数，并启动视频和音频采集。

   ```objectivec
   // 初始化 ByteRTCEngine 对象以接收与 RTC 引擎相关的回调。
   ByteRTCEngineConfig* engineConfig = [[ByteRTCEngineConfig alloc] init];
   engineConfig.appID = RTC_APP_ID;
   engineConfig.isGameScene = FALSE;
   engineConfig.parameters = params;
   // 创建 RTC 引擎。
   self.rtcEngine = [ByteRTCEngine createRTCEngine:engineConfig delegate:self];
   
   // 设置本地预览视图。
   ByteRTCVideoCanvas *canvasView = [[ByteRTCVideoCanvas alloc] init];
   canvasView.view = self.previewView;
   canvasView.renderMode = (ByteRTCRenderMode)renderMode;
   [self.rtcEngine setLocalVideoCanvas:ByteRTCStreamIndexMain withCanvas:canvasView];
   
   // 设置视频编码参数。
   ByteRTCVideoEncoderConfig *vconfig = [[ByteRTCVideoEncoderConfig alloc] init];
   vconfig.width = self.config.encodeSize.width;
   vconfig.height = self.config.encodeSize.height;
   vconfig.frameRate = self.config.encodeFPS;
   vconfig.maxBitrate = self.config.maxBitrate;
   vconfig.minBitrate = self.config.minBitrate;
   vconfig.encoderPreference = ByteRTCVideoEncoderPreferenceMaintainQuality;
   [self.rtcEngine setVideoEncoderConfig:vconfig];
   
   // 启动视频和音频采集。
   [self.rtcEngine startVideoCapture];
   [self.rtcEngine startAudioCapture];
   ```
   

3. 创建并加入 RTC 房间，使用与主播相同的 RoomID。

   ```objectivec
   // 创建 RTC 房间。
   self.rtcRoom = [self.rtcEngine createRTCRoom:roomid];
   
   // 加入 RTC 房间。必须将 profile 设置为连麦（主播与主播）profile，即 ByteRTCRoomProfileLinkMic。
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = @"zzx123";
   ByteRTCRoomConfig *roomConfig = [[ByteRTCRoomConfig alloc] init];
   roomConfig.profile = ByteRTCRoomProfileLinkMic;
   [self.rtcRoom joinRoom:@"token" userInfo:userInfo userVisibility:TRUE roomConfig:roomConfig];
   ```
   

4. 当观众收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回调时，调用`setRemoteVideoCanvas:withCanvas:`调整远端用户视图。

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
   

5. 当主播收到`rtcRoom:onUserJoined:`回调时，更新房间配置和推流到 CDN 的布局。当主播收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回调时，更新远端用户视图。

   ```objectivec
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 将 profile 设置为连麦（主播与主播）profile，即 ByteRTCRoomProfileLINKMIC。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLINKMIC]
       
       // 设置流推送配置，包括要推送混流的 URL。通常保持与启动直播流时一致的配置。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 设置转码的视频编码参数。通常保持与启动直播流时一致的配置。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 设置转码的音频编码参数。通常保持与启动直播流时一致的配置。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 将推流到 CDN 的布局从单人布局更新为双人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播的用户 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 仅供参考.
       region.locationY        = 0.0; // 仅供参考.
       region.widthProportion    = 0.5; // 仅供参考.
       region.heightProportion   = 0.5; // 仅供参考.
       region.zOrder   = 0;   // 仅供参考.
       region.alpha    = 1.0; // 仅供参考.
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // 连麦（主播与主播）用户 ID。
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // 仅供参考.
       regionRemote.locationY        = 0.0; // 仅供参考.
       regionRemote.widthProportion    = 0.5; // 仅供参考.
       regionRemote.heightProportion   = 0.5; // 仅供参考.
       regionRemote.zOrder   = 0;   // 仅供参考.
       regionRemote.alpha    = 1.0; // 仅供参考.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
       
       // 将已配置的音频和视频参数传入最终结构体。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // 更新流推送参数。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (isPublish) {
           // 添加远端用户视图。
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
### 停止连麦（主播与主播）

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddafd73883f34341a54674c22021d699~tplv-goo7wpa0wc-image.image) </span>

主要 API 和回调如下。


* MediaLive SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)。

   * [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play)

* RTC SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)和[回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [leaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRTSRoom-leaveroom)

   * [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

   * [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)

   * [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason)

   * [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

   * [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

   * [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

   * [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopvideocapture)

   * [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopaudiocapture)


**示例代码**


1. 离开 RTC 房间，停止视频和音频采集，并移除本地预览视图和远端用户视图。

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
   

2. 设置播放器视图并开始回放。

   ```objectivec
   // Set the player view.
   self.livePlayer.playerView.hidden = NO;
   
   // Start playback.
   [self.livePlayer play];
   ```
   

3. 当主播收到`rtcRoom:onUserLeave:reason:`回调时，更新房间配置和推流到 CDN 的布局。当主播收到`rtcRoom:onUserPublishStreamVideo:info:isPublish:`回调时，移除远端用户视图。

   ```objectivec
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // 将 profile 设置为直播流 profile，即 ByteRTCRoomProfileLIVE。
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLIVE]
       
       // 设置流推送配置，包括要推送混流的 URL。通常，保持配置与启动直播流时一致。
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // 设置视频编码参数用于转码。通常，保持配置与启动直播流时一致。
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // 设置音频编码参数用于转码。通常，保持配置与启动 直播流时一致。
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // 将推送到 CDN 的布局从2人布局更新为1人布局。
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // 主播的用户 ID。
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // 仅供参考。
       region.locationY        = 0.0; // 仅供参考。
       region.widthProportion    = 0.5; // 仅供参考。
       region.heightProportion   = 0.5; // 仅供参考。
       region.zOrder   = 0;   // 仅供参考。
       region.alpha    = 1.0; // 仅供参考。
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
       
       // 将已配置的音频和视频参数传入最终结构。
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // 推送到 CDN 的任务 ID，必须与启动直播流时配置的 ID 相同。
       
       // 更新流推送参数。
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (!isPublish) {
           // 移除远端用户视图。
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
### 离开直播间

**时序图**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6913fad5f1a24afb937dbf66c52e2118~tplv-goo7wpa0wc-image.image) </span>


* MediaLive SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)和[回调](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)。

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop)

   * [销毁](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy)

* RTC SDK。关于其他 API 和回调的更多信息，请参见[API](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086)和[回调](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081)。

   * [销毁](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-destroy)

   * [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-destroyrtcengine)


**示例代码**


1. 停止回放，移除播放器视图，并销毁播放器。

   ```objectivec
   // Stop playback.
   [self.livePlayer stop];
   
   // Remove the player view.
   self.livePlayer.playerView.hidden = YES;
   
   // Destroy the player.
   [self.livePlayer destroy];
   self.livePlayer = nil;
   ```
   

2. 销毁 RTC 房间和 RTC 引擎。

   ```objectivec
   // Destroy the RTC room.
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Destroy the RTC engine.
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngine = nil;
   ```
