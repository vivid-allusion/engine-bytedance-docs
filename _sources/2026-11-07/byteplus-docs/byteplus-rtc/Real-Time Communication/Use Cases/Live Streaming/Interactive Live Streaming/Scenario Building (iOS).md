---
title: "Scenario Building (iOS)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-152575"
---

<span id="sdk-integration"></span>
## SDK Integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/intergration.png) </span>

<span id="implementation-flowchart"></span>
## Implementation flowchart


* Battle between host and co\-host

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/livestreaming/image.jpg) </span>

* Co\-hosting between a host and a guest

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/livestreaming/b6c60d1c-511b-4bb6-b15e-cf4ffdd89cd3.png) </span>


<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="host-goes-live-and-audience-members-join-the-room"></span>
### Host goes live and audience members join the room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/352usecase/91aceb13-c63f-4f0b-845b-54303f98b493.png) </span>

<span id="sample-code"></span>
#### Sample Code

```objectivec
// Start mixing and republishing the stream to the specified push URL, RTC UID, and RTC room ID
- (void)startMixStreamRetweetWithPushUrl:(NSString )pushUrl
                                  rtcUid:(NSString )rtcUid
                               rtcRoomId:(NSString *)rtcRoomId {
    if (NOEmptyStr(pushUrl)) {
        // Initialize the ByteRTCVideo object
        self.rtcEngineKit = [ByteRTCVideo createRTCVideo:appID
                                            delegate:self
                                          parameters:@{}];

        // Initialize the ByteRTCRoom object
        self.rtcRoom = [self.rtcEngineKit createRTCRoom:rtcRoomID];
        self.rtcRoom.delegate = self;

        // Join the RTC room
        ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
        userInfo.userId = userID;
        ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
        config.profile = ByteRTCRoomProfileLiveBroadcasting;
        config.isAutoPublish = YES;
        config.isAutoSubscribeAudio = YES;
        config.isAutoSubscribeVideo = YES;
        [self.rtcRoom joinRoom:token
                      userInfo:userInfo
                    roomConfig:config];

        // Set the video capture config
        ByteRTCVideoCaptureConfig *captureConfig = [[ByteRTCVideoCaptureConfig alloc] init];
        captureConfig.videoSize = CGSizeMake(720, 1280);
        captureConfig.frameRate = 15;
        [self.rtcEngineKit setVideoCaptureConfig:captureConfig];

        // Set the video encoder config
        ByteRTCVideoEncoderConfig *encoderConfig = [[ByteRTCVideoEncoderConfig alloc] init];
        encoderConfig.videoSize = videoSize;
        encoderConfig.frameRate = frameRate;
        encoderConfig.maxKbps = maxKbps;
        [self.rtcEngineKit setMaxVideoEncoderConfig:encoderConfig];

        // Start video and audio capture
        [self.rtcEngineKit startVideoCapture];
        [self.rtcEngineKit startAudioCapture];
    }
}

// Delegate for successful joining of RTC room
- (void)rtcRoom:(ByteRTCRoom )rtcRoom onRoomStateChanged:(NSString )roomId withUid:(NSString )uid state:(NSInteger)state extraInfo:(NSString )extraInfo {
    if (state == 0) {
// After receiving the callback for successfully joining the RTC room, start stream mixing and republishing
        [self startLiveTranscoding];
    }
}

- (void)startLiveTranscoding {
    // Get the layout of pushing mixed-stream to CDN
    NSArray *regions = [self getRegionWithUserId:rtcUid
                                       rtcRoomId:rtcRoomId];
    // Set the parameters of pushing mixed-stream to CDN
    self.mixedStreamConfig = [ByteRTCMixedStreamConfig defaultMixedStreamConfig];
    self.mixedStreamConfig.layoutConfig.regions = regions;
    self.mixedStreamConfig.roomID = rtcRoomId;
    self.mixedStreamConfig.userID = [LocalUserComponents userModel].uid;
    self.mixedStreamConfig.pushURL = pushUrl;
    self.mixedStreamConfig.expectedMixingType = ByteRTCMixedStreamByServer;
    self.mixedStreamConfig.audioConfig.sampleRate = 44100;
    self.mixedStreamConfig.audioConfig.channels = 2;
    self.mixedStreamConfig.videoConfig.fps = frameRate;
    self.mixedStreamConfig.videoConfig.bitrate = maxKbps;
    self.mixedStreamConfig.videoConfig.width = videoSize.width;
    self.mixedStreamConfig.videoConfig.height = videoSize.height;

    // Set SEI of pushing mixed-stream to CDN
    self.mixedStreamConfig.layoutConfig.userConfigExtraInfo = @"json";

    // Start pushing mixed-stream to CDN
    [self.rtcEngineKit startPushMixedStreamToCDN:@""
                                     mixedConfig:self.mixedStreamConfig
                                        observer:self];
}

- (NSArray )getRegionWithUserId:(NSString )userId
                       rtcRoomId:(NSString *)rtcRoomId {
    NSInteger audienceIndex = 0;
    NSMutableArray *list = [[NSMutableArray alloc] init];
    ByteRTCMixedStreamLayoutRegionConfig *region = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init];
    region.userID = userId;
    region.roomID = rtcRoomId;
    region.isLocalUser = [userModel.uid isEqualToString:[LocalUserComponents userModel].uid] ? YES : NO;
    region.renderMode = ByteRTCMixedStreamRenderModeHidden;
    region.locationX = 0.0;
    region.locationY = 0.0;
    region.width = videoSize.width;
    region.height = videoSize.height;
    region.zOrder = 1;
    region.alpha = 1.0;
    [list addObject:region];

    return [list copy];
}

```


<span id="host-interacts-with-the-audience"></span>
### Host interacts with the audience

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/cohost.jpg) </span>

<span id="sample-code"></span>
#### Sample Code


* Audience becomes guest


```objectivec

- (void)audienceOnMic {
   // Initialize the ByteRTCVideo object
   self.rtcEngineKit = [ByteRTCVideo createRTCVideo:appID
                                           delegate:self
                                         parameters:@{}];
                                       
   // Initialize the ByteRTCRoom object
   self.rtcRoom = [self.rtcEngineKit createRTCRoom:rtcRoomID];
   self.rtcRoom.delegate = self;
           
   // Set the video encoder config
   ByteRTCVideoEncoderConfig *encoderConfig = [[ByteRTCVideoEncoderConfig alloc] init];
   encoderConfig.videoSize = videoSize;
   encoderConfig.frameRate = frameRate;
   encoderConfig.maxKbps = maxKbps;
   [self.rtcEngineKit setMaxVideoEncoderConfig:encoderConfig];
   
// Join the RTC room
   ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
   userInfo.userId = userID;
   ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
   config.profile = ByteRTCRoomProfileLiveBroadcasting;
   config.isAutoPublish = YES;
   config.isAutoSubscribeAudio = YES;
   config.isAutoSubscribeVideo = YES;
   [self.rtcRoom joinRoomByToken:token
                        userInfo:userInfo
                      roomConfig:config];
   
   // Start video and audio capture
   [self.rtcEngineKit startVideoCapture];
   [self.rtcEngineKit startAudioCapture];
}
```



* Removing a guest


```objectivec

- (void)audienceLeaveMic {
   // Leave the RTC room
   [self.rtcRoom leaveRoom];
   
   // destroy the rtcRoom object
   [self.rtcRoom destroy];
   self.rtcRoom = nil;
   
   // Stop video and audio capture
   [self.rtcEngineKit stopVideoCapture];
   [self.rtcEngineKit stopAudioCapture];
}
```


<span id="battle-between-host-and-co-host"></span>
### Battle between host and co\-host

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/352usecase/cfce207b-e48a-4458-933c-c77d356f2529.png) </span>

<span id="sample-code"></span>
#### Sample Code

```objectivec
 
- (void)startCoHost { 
    // Enable cross-room relaying 
    ForwardStreamConfiguration *configuration = [[ForwardStreamConfiguration alloc] init]; 
    configuration.roomId = roomId; 
    configuration.token = token; 
    [self.rtcEngineKit startForwardStreamToRooms:@[configuration]]; 
} 
 
- (void)rtcEngine:(ByteRTCEngineKit *)engine onUserPublishStream:(NSString *)userId type:(ByteRTCMediaStreamType)type { 
    // Receive video stream callback from Host B 
    if (type == ByteRTCMediaStreamTypeBoth || 
        type == ByteRTCMediaStreamTypeVideo) { 
         
        // Encoder config 
        ByteRTCVideoSolution *pushRTCVideoConfig = [[ByteRTCVideoSolution alloc] init]; 
        pushRTCVideoConfig.videoSize = videoSize; 
        pushRTCVideoConfig.frameRate = frameRate; 
        pushRTCVideoConfig.maxKbps = maxKbps; 
        [self.rtcEngineKit setMaxVideoEncoderConfig:@[pushRTCVideoConfig]]; 
     
        // Current host's layout of mixed-streams 
        ByteRTCMixedStreamLayoutRegionConfig *localRegion = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init]; 
        // The User ID of the currently logged in host 
        localRegion.uid = localUserId; 
        localRegion.roomId = rtcRoomId; 
        localRegion.localUser = YES; 
        localRegion.renderMode = ByteRTCMixedStreamRenderModeHidden; 
        localRegion.locationX = 0.0; 
        localRegion.locationY = 0.25 * videoSize.height; 
        localRegion.width = 0.5 * videoSize.width; 
        localRegion.height = 0.5 * videoSize.height; 
        localRegion.zOrder = 0; 
        localRegion.alpha = 1.0; 
    
        // Mixed-stream layout of remote host 
        ByteRTCMixedStreamLayoutRegionConfig *remoteRegion = [[ByteRTCMixedStreamLayoutRegionConfig alloc] init]; 
        // User ID of remote host 
        remoteRegion.uid = userId; 
        remoteRegion.roomId = rtcRoomId; 
        remoteRegion.localUser = NO; 
        remoteRegion.renderMode = ByteRTCMixedStreamRenderModeHidden; 
        remoteRegion.locationX = 0.5 * videoSize.width; 
        remoteRegion.locationY = 0.25 * videoSize.height;  
        remoteRegion.width = 0.5 * videoSize.width; 
        remoteRegion.height = 0.5 * videoSize.height; 
        remoteRegion.zOrder = 0; 
        remoteRegion.alpha = 1.0; 
// Update the SEI of the mixed stream
        self.mixedStreamConfig.layoutConfig.userConfigExtraInfo = @"json"; 
        // Update mixed-stream layout 
        self.mixedStreamConfig.layoutConfig.regions = @[localRegion, remoteRegion]; 
        [self.rtcEngineKit updatePushMixedStreamToCDN:@"" 
                                          mixedConfig:self.mixedStreamConfig]; 
    } 
} 
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create ByteRTCVideo instance |createRTCVideo:delegate:parameters: |
|Create ByteRTCRoom instance |[createRTCRoom:](https://docs.byteplus.com/en/docs/12/docs-70086#creatertcroom) |
|Set camera capture parameters |[setVideoCaptureConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideocaptureconfig) |
|Set video publishing parameters |setMaxVideoEncoderConfig: |
|Set mirroring |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70086#setlocalvideomirrortype) |
|Join RTC room |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#joinroom-userinfo-uservisibility-roomconfig) |
|Leave RTC room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) |
|Destroy room object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70086#destroy) |
|Get default parameters for pushing a mixed stream to the CDN |defaultMixedStreamConfig |
|Start pushing mixed\-stream to CDN |startPushMixedStreamToCDN |
|Update parameters of pushing mixed\-stream to CDN |updatePushMixedStreamToCDN |
|Stop Pushing mixed\-stream to CDN |stopPushStreamToCDN |
|Start forwarding stream to rooms |[startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/docs-70086#startforwardstreamtorooms) |
|Stop forwarding stream to rooms |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70086#stopforwardstreamtorooms) |
|Start video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopvideocapture) |
|Start audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startaudiocapture) |
|stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopaudiocapture) |
|Switch camera |[switchCamera:](https://docs.byteplus.com/en/docs/12/docs-70086#switchcamera) |
|pause all subscribed stream |pauseAllSubscribedStream: |
|Resume all subscribed streams |resumeAllSubscribedStream: |


<span id="callback"></span>
### Callback


|Function |Callback |
|---|---|
|Local user joins RTC room |[rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#onroomstatechanged-withuid-state-extrainfo) |
|Remote user joins RTC room |[rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#onuserjoined) |
|Receive a remote user's audio and video stream |onUserPublishStream |
|Local stream statistics and network quality |onLocalStreamStats |
|Remote stream statistics and network quality |onRemoteStreamStats |
