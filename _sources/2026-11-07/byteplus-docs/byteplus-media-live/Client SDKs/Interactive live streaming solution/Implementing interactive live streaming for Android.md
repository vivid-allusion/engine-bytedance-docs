---
title: "Implementing interactive live streaming for Android"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-implementing-interactive-live-for-android"
---

This topic provides comprehensive, step\-by\-step instructions for building the interactive live streaming feature into your Android app. You will find detailed code examples for implementing core features for both the host and audience, including starting a live stream, enabling host PK battles, and allowing audience members to become co\-hosts.

<span id="d0660c19"></span>
## Prerequisites


* A valid [BytePlus account](http://console.byteplus.com/) with [BytePlus MediaLive](https://console.byteplus.com/live) and [BytePlus RTC](https://console.byteplus.com/rtc/workplaceRTC) activated. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account), [Activating the MediaLive service](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#da5a6a63), and [Activating the RTC service](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865).

* You have integrated the required SDKs:

   * BytePlus RTC SDK version 3.60.104 or later. For more information, see [Integrating the RTC SDK for Android](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70134).

   * BytePlus MediaLive SDK with no specific version required. For more information, see [Integrating the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android) and [Initializing the Player SDK for Android](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android).


<span id="86abfd57"></span>
## Implementing the feature for the host

This section provides instructions on implementing the interactive live streaming feature for the host.

<span id="33f82960"></span>
### Starting a live stream

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2347c01157542d89c81f6a4ec544765~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


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


**Sample code**


1. Create an RTC engine and an RTC room, and join the RTC room.

   ```Java
   // Create an RTC engine. Set rtcEngineHandler to receive callbacks related to the RTC engine.
   EngineConfig config = new EngineConfig();
   config.parameters = new JSONObject();
   config.context = mContext;
   config.appID = RTC_APP_ID; // Replace the RTC_APP_ID with the AppID you get after you create a BytePlus RTC app.
   mRTCEngine = RTCEngine.createRTCEngine(config, rtcEngineHandler);
   
   // Create an RTC room. Set rtcRoomHandler to receive callbacks related to the RTC room.
   mRTCRoom = mRTCEngine.createRTCRoom(roomid);
   mRTCRoom.setRTCRoomEventHandler(rtcRoomHandler);
   
   // Join the RTC room. The profile must be set to the live streaming profile, that is, ROOM_PROFILE_LIVE. 
   mUserId = userId;
   mRoomId = roomId;
   UserInfo userInfo = new UserInfo(userId, null);
   RTCRoomConfig roomConfig = new RTCRoomConfig(ROOM_PROFILE_LIVE,
           true, true, true);
   mRTCRoom.joinRoom(token, userInfo, true, roomConfig);
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on how to get the AppID, see <a href="https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865#step-3-create-a-byteplus-rtc-app-and-get-the-appid">Create a BytePlus RTC app and get the AppID</a>.   </div>
   

2. Set the local preview view and video encoding parameters.

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
   

3. Start audio and video capture.

   ```Java
   // Start video capture.
   mRTCEngine.startVideoCapture();
   
   // Start audio capture.
   mRTCEngine.startAudioCapture();
   ```
   

4. Start pushing the stream.

   ```Java
   // Set the stream push configuration, including the URL for the stream to be pushed to.
   MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
   pushTargetConfig.pushCDNURL = mTargetUrl;
   pushTargetConfig.pushTargetType = PUSH_TO_CDN;
   
   // Set video encoding parameters for transcoding.
   MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
   videoconfig.fps = mConfig.mmVideoEncoderFps;
   videoconfig.height = mConfig.mVideoEncoderHeight;;
   videoconfig.width = mConfig.mVideoEncoderWidth;;
   videoconfig.bitrate = mVideoEncoderKBitrate;
   videoconfig.gop = mConfig.mVideoGopVal;
   
   // Set audio encoding parameters for transcoding.
   MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
   audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
   audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
   audioConfig.bitrate = 128;
   audioConfig.channels = 2;
   audioConfig.sampleRate = 48000;
   
   // Set the push-to-CDN layout. Since only the host is in the room, set the host's layout to occupy the entire canvas.
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
   
   // Pass the configured audio and video parameters into the final structure.
   MixedStreamConfig streamConfig = MixedStreamConfig.defaultMixedStreamConfig();
   streamConfig.audioConfig = audioConfig;
   streamConfig.videoConfig = videoconfig;
   streamConfig.roomID = mRTCRoom.getRoomId();
   streamConfig.userID = localUid;
   streamConfig.regions = regions;
   
   String taskId = ""; // A  unique ID for the push-to-CDN task, which does not exceed 127 bytes.
   
   // Start pushing the stream. Receive stream push status information through the rtcEngineHandler set when creating the RTC engine.
   mRTCEngine.startPushMixedStream(taskId, pushTargetConfig, streamConfig);
   ```
   


<span id="fb003e2e"></span>
### (Optional) Enabling beauty AR for the host

Refer to [Video Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717) for detailed instructions on how to enable the beauty AR feature for the host.

<span id="91ff8ccd"></span>
### Starting a host PK battle

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ee305921cc46feabe545fa0af2131c~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


* [startForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#startforwardstreamtorooms)

* [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged)

* [onUserJoined](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserjoined)

* [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

* [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

* [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

* [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)


**Sample code**


1. Call `startForwardStreamToRooms` to push Host A's stream to Host B's room and Host B's stream to Host A's room when Host A receives the notification of starting the PK battle successfully.

   ```Java
   // Push Host A's stream to Host B's room.
   mRTCRoom1.startForwardStreamToRooms(room2ID, token);
   
   // Push Host B's stream to Host A's room.
   mRTCRoom2.startForwardStreamToRooms(room1ID, token);
   ```
   

2. Update the profile and push\-to\-CDN layout when the host receives the `onUserJoined` callback. Update the remote user view when the host receives the `onUserPublishStreamVideo` callback.

   ```Java
   // For Host A
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserJoined(UserInfo userInfo) {
           // Set the profile to the co-hosting profile, that is, ROOM_PROFILE_LINKMIC.
           mRTCRoom1.setRoomProfile(ROOM_PROFILE_LINKMIC);
           
           // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mConfig.mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // Update the push-to-CDN layout from a 1-person layout to a 2-person layout.
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // Host A's user ID.
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // For reference only.
           region.setLocationY(0.0); // For reference only.
           region.setWidthProportion(0.5); // For reference only.
           region.setHeightProportion(0.5); // For reference only.
           region.setAlpha(1.0); // For reference only.
           region.setZOrder(0); // For reference only.
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // Host B's user ID.
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // For reference only.
           regionRemote.setLocationY(0.0); // For reference only.
           regionRemote.setWidthProportion(0.5); // For reference only.
           regionRemote.setHeightProportion(0.5); // For reference only.
           regionRemote.setAlpha(1.0); // For reference only.
           regionRemote.setZOrder(0); // For reference only.
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
           
           // Update the stream push parameters.
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // Add the remote user view.
               TextureView renderView = new TextureView(Env.getApplicationContext());
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = renderView;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   // For Host B
           ...
           // Update the push-to-CDN layout from a 1-person layout to a 2-person layout.
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // Host B's user ID.
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // For reference only.
           region.setLocationY(0.0); // For reference only.
           region.setWidthProportion(0.5); // For reference only.
           region.setHeightProportion(0.5); // For reference only.
           region.setAlpha(1.0); // For reference only.
           region.setZOrder(0); // For reference only.
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // Host A's user ID.
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // For reference only.
           regionRemote.setLocationY(0.0); // For reference only.
           regionRemote.setWidthProportion(0.5); // For reference only.
           regionRemote.setHeightProportion(0.5); // For reference only.
           regionRemote.setAlpha(1.0); // For reference only.
           regionRemote.setZOrder(0); // For reference only.
           regionRemote.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[1] = regionRemote;
           ...
   ```
   


<span id="91a69d1c"></span>
### Ending the host PK battle

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b655a753b164cda9efbd7239b2eb908~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


* [stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-stopforwardstreamtorooms)

* [onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onforwardstreamstatechanged)

* [onUserLeave](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserleave)

* [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

* [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

* [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

* [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)


**Sample code**


1. Call `stopForwardStreamToRooms` to stop pushing Host A's stream to Host B's room or Host B's stream to Host A's room when Host A receives the notification of ending the PK battle successfully.

   ```Java
   // Stop pushing Host A's stream to Host B's room.
   mRTCRoom1.stopForwardStreamToRooms();
   
   // Stop pushing Host B's stream to Host A's room.
   mRTCRoom2.stopForwardStreamToRooms();
   ```
   

2. Update the profile and push\-to\-CDN layout when the host receives the `onUserLeave` callback. Remove the remote user view when the host receives the `onUserPublishStreamVideo` callback.

   ```Java
   // For Host A
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserLeave(String uid, int reason) {
           // Set the profile to the live streaming profile, that is, ROOM_PROFILE_LIVE.
           mRTCRoom1.setRoomProfile(ROOM_PROFILE_LIVE);
           
           // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // Update the push-to-CDN layout from a 2-person layout to a 1-person layout.
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // Host A's user ID.
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // For reference only.
           region.setLocationY(0.0); // For reference only.
           region.setWidthProportion(0.5); // For reference only.
           region.setHeightProportion(0.5); // For reference only.
           region.setAlpha(1.0); // For reference only.
           region.setZOrder(0); // For reference only.
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
           
           // Update the stream push parameters.
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // Remove the remote user view.
               VideoCanvas canvas = new VideoCanvas();
               canvas.renderView = null;
               canvas.renderMode = RENDER_MODE_HIDDEN;
               RemoteStreamKey key = new RemoteStreamKey(mRoomId, uid, StreamIndex.STREAM_INDEX_MAIN);
               mRTCEngine.setRemoteVideoCanvas(key, canvas);
           }
       }
   }
   // For Host B
            ...
           // Update the push-to-CDN layout from a 2-person layout to a 1-person layout.
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // Host B's user ID.
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // For reference only.
           region.setLocationY(0.0); // For reference only.
           region.setWidthProportion(0.5); // For reference only.
           region.setHeightProportion(0.5); // For reference only.
           region.setAlpha(1.0); // For reference only.
           region.setZOrder(0); // For reference only.
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           ...
   ```
   


<span id="33d6c35f"></span>
### Ending the live stream

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e525b9e474634955a1b1859dc16d0a69~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).


* [stopPushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stoppushmixedstream)

* [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopvideocapture)

* [startAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-startaudiocapture)

* [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

* [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-destroy)

* [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-destroyrtcengine)


**Sample code**


1. Stop pushing the stream.

   ```Java
   mRTCEngine.stopPushMixedStream(taskId, PUSH_TO_CDN);
   ```
   

2. Stop video and audio capture, and remove the local preview view.

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
   

3. Destroy the RTC room and RTC engine.

   ```Java
   // Destroy the RTC room.
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine.
   mRTCEngine.destroyRTCEngine();
   mRTCEngine = null;
   ```
   


<span id="ec36bcae"></span>
## Implementing the feature for the audience

This section provides instructions on implementing the interactive live streaming feature for the audience.

<span id="935dd891"></span>
### Watching the live stream

The audience uses the player to watch the live stream.

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c1f1f3e252648aaa05fda30502ad6f3~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback).


* [setConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setconfig)

* [setObserver](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setobserver)

* [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)

* [setPlayUrl](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setplayurl)

* [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play)


**Sample code**


1. Create and set the player.

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
   

2. Set the player view and pull stream address, and start playback.

   ```Java
   // Set the player view.
   mLivePlayer.setSurfaceHolder(holder);
   
   // Set the pull stream address.
   mLivePlayer.setPlayUrl(mPullUrl);
   
   // Start playback.
   mLivePlayer.play();
   ```
   


<span id="148f2373"></span>
### (Optional) Enabling beauty AR for the audience

Refer to [Video Effects](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-114717) for detailed instructions on how to enable the beauty AR feature for the audience.

<span id="c6e434d1"></span>
### Becoming a co\-host

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f085b77054334c1585a68383690539b7~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows.


* MediaLive SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback).

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop)

* RTC SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).

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


**Sample code**


1. Stop playback and remove the player view.

   ```Java
   // Stop playback.
   mLivePlayer.stop();
   ```
   

2. Create an RTC engine, set the local preview view and video encoding parameters, and start video and audio capture.

   ```Java
   // Create an RTC engine. Set rtcEngineHandler to receive callbacks related to the RTC engine.
   EngineConfig config = new EngineConfig();
   config.parameters = new JSONObject();
   config.context = mContext;
   config.appID = RTC_APP_ID;
   mRTCEngine = RTCEngine.createRTCEngine(config, rtcEngineHandler);
   
   // Set the local preview view.
   VideoCanvas videoCanvas = new VideoCanvas();
   videoCanvas.renderView = renderView;
   videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   mRTCEngine.setLocalVideoCanvas(StreamIndex.STREAM_INDEX_MAIN, videoCanvas);
   
   // Set video encoding parameters.
   VideoEncoderConfig config = new VideoEncoderConfig(
           mConfig.mVideoEncoderWidth, mConfig.mVideoEncoderHeight, mConfig.mVideoEncoderFps, mConfig.mVideoEncoderKBitrate * 1000);
   mRTCEngine.setVideoEncoderConfig(config);
   
   // Start video and audio capture.
   mRTCEngine.startVideoCapture();
   mRTCEngine.startAudioCapture();
   ```
   

3. Create and join the RTC room, using the same RoomID as the host.

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
   

4. Call `setRemoteVideoCanvas` to adjust the remote user view when the audience receives the `onUserPublishStreamVideo` callback.

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
   

5. Update the profile and push\-to\-CDN layout when the host receives the `onUserJoined` callback. Update the remote user view when the host receives the `onUserPublishStreamVideo` callback.

   ```Java
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserJoined(UserInfo userInfo) {
           // Set the profile to the co-hosting profile, that is, ROOM_PROFILE_LINKMIC.
           mRTCRoom.setRoomProfile(ROOM_PROFILE_LINKMIC)
       
           // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // Update the push-to-CDN layout from a 1-person layout to a 2-person layout.
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[2];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // Host's user ID.
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // For reference only.
           region.setLocationY(0.0); // For reference only.
           region.setWidthProportion(0.5); // For reference only.
           region.setHeightProportion(0.5); // For reference only.
           region.setAlpha(1.0); // For reference only.
           region.setZOrder(0); // For reference only.
           region.setRenderMode(MixedStreamConfig.MixedStreamRenderMode.MIXED_STREAM_RENDER_MODE_HIDDEN);
           regions[0] = region;
           MixedStreamConfig.MixedStreamLayoutRegionConfig regionRemote = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           regionRemote.setUserID(uid); // Co-host's user ID.
           regionRemote.setRoomID(mRoomId);
           regionRemote.setIsLocalUser(false);
           regionRemote.setLocationX(0.0); // For reference only.
           regionRemote.setLocationY(0.0); // For reference only.
           regionRemote.setWidthProportion(0.5); // For reference only.
           regionRemote.setHeightProportion(0.5); // For reference only.
           regionRemote.setAlpha(1.0); // For reference only.
           regionRemote.setZOrder(0); // For reference only.
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
           
           // Update the stream push parameters.
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (isPublish) {
               // Add the remote user view.
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
### Stopping co\-hosting

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65e0b0f83f7d4812bc0a798855b637e0~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows.


* MediaLive SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback).

   * [setSurfaceHolder](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-setsurfaceholder)

   * [play](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-play)

* RTC SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).

   * [leaveRoom](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTSRoom-leaveroom)

   * [onUserPublishStreamVideo](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserpublishstreamvideo)

   * [setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setremotevideocanvas)

   * [onUserLeave](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081#IRTCRoomEventHandler-onuserleave)

   * [setRoomProfile](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080?_vtm_=a78999.b69280.0_0.0_0.0.94_undefined#RTCRoom-setroomprofile)

   * [updatePushMixedStream](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-updatepushmixedstream)

   * [setLocalVideoCanvas](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-setlocalvideocanvas)

   * [stopVideoCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopvideocapture)

   * [stopAudioCapture](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-stopaudiocapture)


**Sample code**


1. Leave the RTC room, stop video and audio capture, and remove the local preview view and remote user view.

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
   

2. Set the player view and start playback.

   ```Java
   // Set the player view.
   mLivePlayer.setSurfaceHolder(holder);
   // Start playback.
   mLivePlayer.play();
   ```
   

3. Update the profile and push\-to\-CDN layout when the host receives the `onUserLeave` callback. Remove the remote user view when the host receives the `onUserPublishStreamVideo` callback.

   ```Java
   private IRTCRoomEventHandler mIRtcRoomEventHandler = new IRTCRoomEventHandler() {
       public void onUserLeave(String uid, int reason) {
           // Set the profile to the live streaming profile, that is, ROOM_PROFILE_LIVE.
           mRTCRoom.setRoomProfile(ROOM_PROFILE_LIVE)
           
           // Set the stream push configuration, including the URL for the mixed stream to be pushed to. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamPushTargetConfig pushTargetConfig = new MixedStreamPushTargetConfig();
           pushTargetConfig.pushCDNURL = mTargetUrl;
           pushTargetConfig.pushTargetType = PUSH_TO_CDN;
           
           // Set video encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamVideoConfig videoconfig = new MixedStreamVideoConfig();
           videoconfig.fps = mConfig.mmVideoEncoderFps;
           videoconfig.height = mConfig.mVideoEncoderHeight;;
           videoconfig.width = mConfig.mVideoEncoderWidth;;
           videoconfig.bitrate = mVideoEncoderKBitrate;
           videoconfig.gop = mConfig.mVideoGopVal;
           
           // Set audio encoding parameters for transcoding. Generally, keep the configuration consistent with that used when starting the live stream.
           MixedStreamAudioConfig audioConfig = new MixedStreamAudioConfig();
           audioConfig.audioCodec = MIXED_STREAM_AUDIO_CODEC_TYPE_AAC;
           audioConfig.audioProfile = MIXED_STREAM_AUDIO_PROFILE_HEV1;
           audioConfig.bitrate = 128;
           audioConfig.channels = 2;
           audioConfig.sampleRate = 48000;
           
           // Update the push-to-CDN layout from a 2-person layout to a 1-person layout.
           MixedStreamConfig.MixedStreamLayoutRegionConfig[] regions = new MixedStreamConfig.MixedStreamLayoutRegionConfig[1];
           MixedStreamLayoutRegionConfig region = new MixedStreamConfig.MixedStreamLayoutRegionConfig();
           region.setUserID(mUserId); // Host's user ID.
           region.setRoomID(mRoomId);
           region.setIsLocalUser(true);
           region.setLocationX(0.0); // For reference only.
           region.setLocationY(0.0); // For reference only.
           region.setWidthProportion(0.5); // For reference only.
           region.setHeightProportion(0.5); // For reference only.
           region.setAlpha(1.0); // For reference only.
           region.setZOrder(0); // For reference only.
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
           
           // Update the stream push parameters.
           mRTCEngine.updatePushMixedStream(taskId, pushTargetConfig, streamConfig);
       }
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               // Remove the remote user view.
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
### Leaving the live room

**Sequence diagram**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c877eaadfb9e4304995c4d6a787ef6df~tplv-goo7wpa0wc-image.image) </span>

Key APIs and callbacks are as follows.


* MediaLive SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-reference) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-player-android-api-callback).

   * [stop](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-stop)

   * [destroy](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-reference#VeLivePlayer-destroy)

* RTC SDK. For more information on other APIs and callbacks, see [APIs](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080) and [Callbacks](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70081).

   * [destroy](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCRoom-destroy)

   * [destroyRTCEngine](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70080#RTCEngine-destroyrtcengine)


**Sample code**


1. Stop playback, remove the player view, and destroy the player.

   ```Java
   // Stop playback.
   mLivePlayer.stop();
   
   // Destroy the player.
   mLivePlayer.destroy();
   mLivePlayer = null;
   ```
   

2. Destroy the RTC room and RTC engine.

   ```Java
   // Destroy the RTC room.
   mRTCRoom.destroy();
   mRTCRoom = null;
   
   // Destroy the RTC engine.
   RTCEngine.destroyRTCEngine();
   RTCEngine = null;
   ```
