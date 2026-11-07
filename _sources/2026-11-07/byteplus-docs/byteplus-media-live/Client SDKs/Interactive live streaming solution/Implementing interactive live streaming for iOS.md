---
title: "Implementing interactive live streaming for iOS"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-interactive-live-for-ios"
---

This topic provides comprehensive, step\-by\-step instructions for building the interactive live streaming feature into your iOS app. You will find detailed code examples for implementing core features for both the host and audience, including starting a live stream, enabling host PK battles, and allowing audience members to become co\-hosts.

<span id="bac8e2f8"></span>
## Prerequisites


* A valid [BytePlus account](http://console.byteplus.com/) with [BytePlus MediaLive](https://console.byteplus.com/live) and [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC) activated. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account), [Activating the MediaLive service](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#da5a6a63), and [Activating the RTC service](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865).

* You have integrated the required SDKs:

   * BytePlus RTC SDK version 3.60.104 or later. For more information, see [Integrating the RTC SDK for iOS](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133).

   * BytePlus MediaLive SDK with no specific version required. For more information, see [Integrating the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios) and [Initializing the Player SDK for iOS](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios).


<span id="fd484c24"></span>
## Implementing the feature for the host

This section provides instructions on implementing the interactive live streaming feature for the host.

<span id="56ca198e"></span>
### Starting a live stream

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0d89fd738774914b44489e419af1509~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


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


**Sample code**


1. Create an RTC engine and an RTC room, and join the RTC room.

   ```objectivec
   // Set ByteRTCEngineDelegate and ByteRTCRoomDelegate to receive callbacks related to the RTC engine and the RTC room.
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
   
   // Create an RTC room.
   self.rtcRoom = [self.rtcEngine createRTCRoom:roomid];
   
   // Join the RTC room. The profile must be set to the live streaming profile, that is, ByteRTCRoomProfileLive. 
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = @"zzx123";
   ByteRTCRoomConfig *roomConfig = [[ByteRTCRoomConfig alloc] init];
   roomConfig.profile = ByteRTCRoomProfileLive;
   [self.rtcRoom joinRoom:@"token" userInfo:userInfo userVisibility:TRUE roomConfig:roomConfig];
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on how to get the AppID, see <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid">Create a BytePlus RTC app and get the AppID</a>.   </div>
   

2. Set the local preview view and video encoding parameters.

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
   

3. Start audio and video capture.

   ```objectivec
   //  Start video capture.
   [self.rtcEngine startVideoCapture];
   
   // Start audio capture.
   [self.rtcEngine startAudioCapture];
   ```
   

4. Start pushing the stream.

   ```objectivec
   // Set the stream push configuration, including the URL for the stream to be pushed to.
   ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
   pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
   pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
   
   // Set video encoding parameters for transcoding.
   ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
   videoConfig.width = self.config.encodeSize.width;
   videoConfig.height = self.config.encodeSize.height;
   videoConfig.fps = self.config.encodeFPS;
   videoConfig.gop = self.config.encodeGOPSeconds;
   
   // Set audio encoding parameters for transcoding.
   ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
   audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
   audioConfig.sampleRate = 48000;
   audioConfig.channels = 2;
   audioConfig.bitrate = 128;
   audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
   
   // Set the push-to-CDN layout. Since only the host is in the room, set the host's layout to occupy the entire canvas.
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
   
   // Pass the configured audio and video parameters into the final structure.
   ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
   mixedStreamConfig.audioConfig = audioConfig;
   mixedStreamConfig.videoConfig = videoConfig;
   mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
   mixedStreamConfig.userID = @"zzx123";
   mixedStreamConfig.regions = regions;
   
   self.pushTaskId = @""; // A  unique ID for the push-to-CDN task, which does not exceed 127 bytes.
   
   // Start pushing the stream. Receive stream push status information through ByteRTCEngineDelegate.
   int ret = [self.rtcEngine startPushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   ```
   


<span id="064a1bc3"></span>
### (Optional) Enabling beauty AR for the host

Refer to [Video Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717) for detailed instructions on how to enable the beauty AR feature for the host.

<span id="de24a5cd"></span>
### Starting a host PK battle

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/630a998ba11a46ac9e09eb9934778a15~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


* [startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-startforwardstreamtorooms)

* [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged)

* [rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserjoined)

* [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

* [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

* [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)


**Sample code**


1. Call `startForwardStreamToRooms:` to push Host A's stream to Host B's room and Host B's stream to Host A's room when Host A receives the notification of starting the PK battle successfully.

   ```objectivec
   // Push Host A's stream to Host B's room. configDict contains information such as the roomid of Host B's room.
   NSMutableArray *dest = [NSMutableArray array];
   ByteRTCForwardStreamConfiguration *config = [[ByteRTCForwardStreamConfiguration alloc] initWithDict:configDict];
   [dest addObject:config];
   [self.rtcRoom startForwardStreamToRooms:dest];
   
   // Push Host B's stream to Host A's room. configDict contains information such as the roomid of Host A's room.
   NSMutableArray *dest = [NSMutableArray array];
   ByteRTCForwardStreamConfiguration *config = [[ByteRTCForwardStreamConfiguration alloc] initWithDict:configDict];
   [dest addObject:config];
   [self.rtcRoom startForwardStreamToRooms:dest];
   ```
   

2. Update the profile and push\-to\-CDN layout when the host receives the `rtcRoom:onUserJoined:` callback. Update the remote user view when the host receives the `rtcRoom:onUserPublishStreamVideo:info:isPublish:` callback.

   ```objectivec
   // For Host A
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // Set the profile to the co-hosting profile, that is, ByteRTCRoomProfileLINKMIC.
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLINKMIC]
       
       // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // Update the push-to-CDN layout from a 1-person layout to a 2-person layout.
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // Host A's user ID.
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // For reference only.
       region.locationY        = 0.0; // For reference only.
       region.widthProportion    = 0.5; // For reference only.
       region.heightProportion   = 0.5; // For reference only.
       region.zOrder   = 0;   // For reference only.
       region.alpha    = 1.0; // For reference only.
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // Host B's user ID.
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // For reference only.
       regionRemote.locationY        = 0.0; // For reference only.
       regionRemote.widthProportion    = 0.5; // For reference only.
       regionRemote.heightProportion   = 0.5; // For reference only.
       regionRemote.zOrder   = 0;   // For reference only.
       regionRemote.alpha    = 1.0; // For reference only.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
       
       // Pass the configured audio and video parameters into the final structure.
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // Update the stream push parameters.
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
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
       }
   }
   // For Host B
        ...
       // Update the push-to-CDN layout from a 1-person layout to a 2-person layout.
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // Host B's user ID.
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // For reference only.
       region.locationY        = 0.0; // For reference only.
       region.widthProportion    = 0.5; // For reference only.
       region.heightProportion   = 0.5; // For reference only.
       region.zOrder   = 0;   // For reference only.
       region.alpha    = 1.0; // For reference only.
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // Host A's user ID.
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // For reference only.
       regionRemote.locationY        = 0.0; // For reference only.
       regionRemote.widthProportion    = 0.5; // For reference only.
       regionRemote.heightProportion   = 0.5; // For reference only.
       regionRemote.zOrder   = 0;   // For reference only.
       regionRemote.alpha    = 1.0; // For reference only.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
   ...
   ```
   


<span id="a0d4626c"></span>
### Ending the host PK battle

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a96045456f0146459f5f42928014351c~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


* [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-stopforwardstreamtorooms)

* [rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onforwardstreamstatechanged)

* [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason)

* [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

* [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

* [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

* [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)


**Sample code**


1. Call `stopForwardStreamToRooms` to stop pushing Host A's stream to Host B's room or Host B's stream to Host A's room when Host A receives the notification of ending the PK battle successfully.

   ```objectivec
   // Stop pushing Host A's stream to Host B's room.
   [self.rtcRoom stopForwardStreamToRooms];
   
   // Stop pushing Host B's stream to Host A's room.
   [self.rtcRoom stopForwardStreamToRooms];
   ```
   

2. Update the profile and push\-to\-CDN layout when the host receives the `rtcRoom:onUserLeave:reason:` callback. Remove the remote user view when the host receives the `rtcRoom:onUserPublishStreamVideo:info:isPublish:` callback.

   ```objectivec
   // For Host A
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // Set the profile to the live streaming profile, that is, ByteRTCRoomProfileLIVE.
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLIVE]
       
       // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // Update the push-to-CDN layout from a 2-person layout to a 1-person layout.
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // Host A's user ID.
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // For reference only.
       region.locationY        = 0.0; // For reference only.
       region.widthProportion    = 0.5; // For reference only.
       region.heightProportion   = 0.5; // For reference only.
       region.zOrder   = 0;   // For reference only.
       region.alpha    = 1.0; // For reference only.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
       
       // Pass the configured audio and video parameters into the final structure.
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // Update the stream push parameters.
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (!isPublish) {
           // Remove the remote user view.
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
   // For Host B
        ...
       // Update the push-to-CDN layout from a 2-person layout to a 1-person layout.
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // Host B's user ID.
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // For reference only.
       region.locationY        = 0.0; // For reference only.
       region.widthProportion    = 0.5; // For reference only.
       region.heightProportion   = 0.5; // For reference only.
       region.zOrder   = 0;   // For reference only.
       region.alpha    = 1.0; // For reference only.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
    ...
   ```
   


<span id="5c1f93b7"></span>
### Ending the live stream

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ba533c490f9482080cb464a8f803d5a~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


* [stopPushMixedStream:withPushTargetType:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stoppushmixedstream-withpushtargettype)

* [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopvideocapture)

* [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopaudiocapture)

* [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

* [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-destroy)

* [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-destroyrtcengine)


**Sample code**


1. Stop pushing the stream.

   ```objectivec
   [self.rtcEngine stopPushMixedStream:self.pushTaskId withPushTargetType:ByteRTCMixedStreamPushTargetTypeToCDN];
   ```
   

2. Stop video and audio capture, and remove the local preview view.

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
   

3. Destroy the RTC room and RTC engine.

   ```objectivec
   // Destroy the RTC room.
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Destroy the RTC engine.
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngine = nil;
   ```
   


<span id="ef36bbb0"></span>
## Implementing the feature for the audience

This section provides instructions on implementing the interactive live streaming feature for the audience.

<span id="7e071d75"></span>
### Watching the live stream

The audience uses the player to watch the live stream.

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68d69fcb410f4f0c9da91c6147082532~tplv-goo7wpa0wc-image.image) </span>

`Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see`[APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api)`and`[Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback)`.`


* [setConfig:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setconfig)

* [setObserver:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setobserver)

* [setPlayUrl:](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-setplayurl)

* [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play)


**Sample code**


1. Create and set the player.

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
   

2. Set the player view and pull stream address, and start playback.

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
### (Optional) Enabling beauty AR for the audience

Refer to [Video Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717) for detailed instructions on how to enable the beauty AR feature for the audience.

<span id="a790a0eb"></span>
### Becoming a co\-host

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2102de0eb6a4bc5af75d006afc3da93~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows.


* MediaLive SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback).

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop)

* RTC SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).

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


**Sample code**


1. Stop playback and remove the player view.

   ```objectivec
   // Stop playback.
   [self.livePlayer stop];
   
   // Remove the player view.
   self.livePlayer.playerView.hidden = YES;
   ```
   

2. Create an RTC engine, set the local preview view and video encoding parameters, and start video and audio capture.

   ```objectivec
   // Initialize the ByteRTCEngine object to receive callbacks related to the RTC engine.
   ByteRTCEngineConfig* engineConfig = [[ByteRTCEngineConfig alloc] init];
   engineConfig.appID = RTC_APP_ID;
   engineConfig.isGameScene = FALSE;
   engineConfig.parameters = params;
   // Create an RTC engine.
   self.rtcEngine = [ByteRTCEngine createRTCEngine:engineConfig delegate:self];
   
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
   
   // Start video and audio capture.
   [self.rtcEngine startVideoCapture];
   [self.rtcEngine startAudioCapture];
   ```
   

3. Create and join the RTC room, using the same RoomID as the host.

   ```objectivec
   // Create an RTC room.
   self.rtcRoom = [self.rtcEngine createRTCRoom:roomid];
   
   // Join the RTC room. The profile must be set to the co-hosting profile, that is, ByteRTCRoomProfileLinkMic. 
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = @"zzx123";
   ByteRTCRoomConfig *roomConfig = [[ByteRTCRoomConfig alloc] init];
   roomConfig.profile = ByteRTCRoomProfileLinkMic;
   [self.rtcRoom joinRoom:@"token" userInfo:userInfo userVisibility:TRUE roomConfig:roomConfig];
   ```
   

4. Call `setRemoteVideoCanvas:withCanvas:` to adjust the remote user view when the audience receives the `rtcRoom:onUserPublishStreamVideo:info:isPublish:` callback.

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
   

5. Update the profile and push\-to\-CDN layout when the host receives the `rtcRoom:onUserJoined:` callback. Update the remote user view when the host receives the `rtcRoom:onUserPublishStreamVideo:info:isPublish:` callback.

   ```objectivec
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // Set the profile to the co-hosting profile, that is, ByteRTCRoomProfileLINKMIC.
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLINKMIC]
       
       // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // Update the push-to-CDN layout from a 1-person layout to a 2-person layout.
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // Host's user ID.
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // For reference only.
       region.locationY        = 0.0; // For reference only.
       region.widthProportion    = 0.5; // For reference only.
       region.heightProportion   = 0.5; // For reference only.
       region.zOrder   = 0;   // For reference only.
       region.alpha    = 1.0; // For reference only.
       ByteRTCMixedStreamLayoutRegionConfig *regionRemote = [[ByteRTCMixedStreamLayoutRegionConfig alloc]init];
       regionRemote.roomID = self.roomID;
       regionRemote.userID = userId; // Co-host's user ID.
       regionRemote.isLocalUser    = NO;
       regionRemote.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       regionRemote.locationX        = 0.5; // For reference only.
       regionRemote.locationY        = 0.0; // For reference only.
       regionRemote.widthProportion    = 0.5; // For reference only.
       regionRemote.heightProportion   = 0.5; // For reference only.
       regionRemote.zOrder   = 0;   // For reference only.
       regionRemote.alpha    = 1.0; // For reference only.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region, regionRemote];
       
       // Pass the configured audio and video parameters into the final structure.
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // Update the stream push parameters.
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
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
       }
   }
   ```
   


<span id="b7ec9c92"></span>
### Stopping co\-hosting

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddafd73883f34341a54674c22021d699~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows.


* MediaLive SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback).

   * [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-play)

* RTC SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).

   * [leaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRTSRoom-leaveroom)

   * [rtcRoom:onUserPublishStreamVideo:info:isPublish:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserpublishstreamvideo-info-ispublish)

   * [setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setremotevideocanvas-withcanvas)

   * [rtcRoom:onUserLeave:reason:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70087#ByteRTCRoomDelegate-rtcroom-onuserleave-reason)

   * [setRoomProfile:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-setroomprofile)

   * [updatePushMixedStream:withPushTargetConfig:withMixedConfig:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-updatepushmixedstream-withpushtargetconfig-withmixedconfig)

   * [setLocalVideoCanvas:](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-setlocalvideocanvas)

   * [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopvideocapture)

   * [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-stopaudiocapture)


**Sample code**


1. Leave the RTC room, stop video and audio capture, and remove the local preview view and remote user view.

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
   

2. Set the player view and start playback.

   ```objectivec
   // Set the player view.
   self.livePlayer.playerView.hidden = NO;
   
   // Start playback.
   [self.livePlayer play];
   ```
   

3. Update the profile and push\-to\-CDN layout when the host receives the `rtcRoom:onUserLeave:reason:` callback. Remove the remote user view when the host receives the `rtcRoom:onUserPublishStreamVideo:info:isPublish:` callback.

   ```objectivec
   - (void)rtcRoom:( ByteRTCRoom*_Nonnull)rtcRoom onUserJoined:(ByteRTCUserInfo*_Nonnull)userInfo {
       // Set the profile to the live streaming profile, that is, ByteRTCRoomProfileLIVE.
       [self.rtcRoom setRoomProfile:ByteRTCRoomProfileLIVE]
       
       // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamPushTargetConfig* pushTargetConfig = [[ByteRTCMixedStreamPushTargetConfig alloc] init];
       pushTargetConfig.pushCDNURL = self.config.urls.firstObject;
       pushTargetConfig.pushTargetType = ByteRTCMixedStreamPushTargetTypeToCDN;
       
       // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamVideoConfig* videoConfig = [[ByteRTCMixedStreamVideoConfig alloc] init];
       videoConfig.width = self.config.encodeSize.width;
       videoConfig.height = self.config.encodeSize.height;
       videoConfig.fps = self.config.encodeFPS;
       videoConfig.gop = self.config.encodeGOPSeconds;
       
       // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
       ByteRTCMixedStreamAudioConfig* audioConfig = [[ByteRTCMixedStreamAudioConfig alloc] init];
       audioConfig.audioCodec = ByteRTCMixedStreamAudioCodecTypeAAC;
       audioConfig.sampleRate = 48000;
       audioConfig.channels = 2;
       audioConfig.bitrate = 128;
       audioConfig.audioProfile = ByteRTCMixedStreamAudioProfileHEv1;
       
       // Update the push-to-CDN layout from a 2-person layout to a 1-person layout.
       ByteRTCMixedStreamLayoutRegionConfig* region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
       region.roomID = self.roomID;
       region.userID = self.userId; // Host's user ID.
       region.isLocalUser    = YES;
       region.renderMode   = ByteRTCMixedStreamRenderModeHidden;
       region.locationX        = 0.0; // For reference only.
       region.locationY        = 0.0; // For reference only.
       region.widthProportion    = 0.5; // For reference only.
       region.heightProportion   = 0.5; // For reference only.
       region.zOrder   = 0;   // For reference only.
       region.alpha    = 1.0; // For reference only.
       NSArray<ByteRTCMixedStreamLayoutRegionConfig*>* regions = @[region];
       
       // Pass the configured audio and video parameters into the final structure.
       ByteRTCMixedStreamConfig* mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
       mixedStreamConfig.audioConfig = audioConfig;
       mixedStreamConfig.videoConfig = videoConfig;
       mixedStreamConfig.roomID = [self.rtcRoom getRoomId];
       mixedStreamConfig.userID = @"zzx123";
       mixedStreamConfig.regions = regions;
       
       self.pushTaskId = @""; // The push-to-CDN task ID, which must be the same as the one configured when starting the live stream.
       
       // Update the stream push parameters.
       int ret = [self.rtcEngine updatePushMixedStream:self.pushTaskId withPushTargetConfig:pushTargetConfig withMixedConfig:mixedStreamConfig];
   }
   
   - (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom 
       onUserPublishStreamVideo:(NSString* _Nonnull)streamId 
       info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
       if (!isPublish) {
           // Remove the remote user view.
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
### Leaving the live room

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6913fad5f1a24afb937dbf66c52e2118~tplv-goo7wpa0wc-image.image) </span>


* MediaLive SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-api) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-sdk-for-ios-callback).

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-stop)

   * [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api#TVLManager(VeLivePlayer)-destroy)

* RTC SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).

   * [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCRoom-destroy)

   * [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70086#ByteRTCEngine-destroyrtcengine)


**Sample code**


1. Stop playback, remove the player view, and destroy the player.

   ```objectivec
   // Stop playback.
   [self.livePlayer stop];
   
   // Remove the player view.
   self.livePlayer.playerView.hidden = YES;
   
   // Destroy the player.
   [self.livePlayer destroy];
   self.livePlayer = nil;
   ```
   

2. Destroy the RTC room and RTC engine.

   ```objectivec
   // Destroy the RTC room.
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Destroy the RTC engine.
   [ByteRTCEngine destroyRTCEngine];
   self.rtcEngine = nil;
   ```
