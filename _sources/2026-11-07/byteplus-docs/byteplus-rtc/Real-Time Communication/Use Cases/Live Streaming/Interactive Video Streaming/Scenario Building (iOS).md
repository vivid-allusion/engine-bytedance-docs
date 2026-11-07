---
title: "Scenario Building (iOS)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113692"
---

<span id="sdk-integration"></span>
## SDK integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/intergration.png) </span>

<span id="implementation-flowchart"></span>
## Implementation flowchart


* **Host\-vs\-Host Interaction Across Rooms**

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/pkbet.png) </span>

* **Interaction Between Host and Co\-host**

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/intbet.png) </span>


<span id="core-feature-implementation"></span>
## Core feature implementation

<span id="host-goes-live-and-audience-members-join-room"></span>
### Host Goes Live and Audience Members Join Room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/1c615f8f-6c2d-416f-b394-53d885756557.png) </span>

<span id="sample-code"></span>
#### Sample Code

```objectivec
/**
  * Join the RTC room and initialize parameters
  * @param token: RTC Token
  * @param roomID: RTC room id
  * @param uid: RTC user id
  * @param isHost: YES business host; NO business audience
  **/

- (void)joinRTCRoomWithToken:(NSString *)token
                       roomID: (NSString *) roomID
                          uid:(NSString *)uid
                       isHost:(BOOL)isHost {
     // Initialize the ByteRTCVideo object
     self.rtcEngineKit = [ByteRTCVideo createRTCVideo:APPID
                                         delegate:self
                                       parameters:@{}];
    
     // Initialize the ByteRTCRoom object
     self.rtcRoom = [self.rtcEngineKit createRTCRoom:roomID];
     self.rtcRoom.delegate = self;
    
     // Set the host as visible and the viewer as invisible
     [self.rtcRoom setUserVisibility:isHost? YES : NO];
    
When joining the room, the host needs to turn on the microphone and camera, and audience members need to turn them off
     if (isHost) {
         [self.rtcEngineKit startVideoCapture];
         [self.rtcEngineKit startAudioCapture];
        
         // Set up local rendering and encoding mirroring
         [self.rtcEngineKit setLocalVideoMirrorType:ByteRTCMirrorTypeRenderAndEncoder];
     } else {
         [self.rtcEngineKit stopVideoCapture];
         [self.rtcEngineKit stopAudioCapture];
     }
 
     // Set audio routing mode
     [self.rtcEngineKit setDefaultAudioRoute:ByteRTCAudioRouteSpeakerphone];
 
     // Enable speaker volume monitoring
     ByteRTCAudioPropertiesConfig *audioPropertiesConfig = [[ByteRTCAudioPropertiesConfig alloc] init];
     audioPropertiesConfig.interval = 300;
     [self.rtcEngineKit enableAudioPropertiesReport:audioPropertiesConfig];
    
     // Join the room and start connecting to the host, you need to apply for AppId and Token
     ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
     userInfo. userId = uid;
     ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
     config.profile = ByteRTCRoomProfileInteractivePodcast;
     config.isAutoPublish = YES;
     config.isAutoSubscribeAudio = YES;
     config.isAutoSubscribeVideo = YES;
     [self.rtcRoom joinRoom:token userInfo:userInfo roomConfig:config];
}
```


```objectivec

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom onRoomStateChanged:(NSString *)roomId
                                                   withUid:(NSString *)uid
                                                     state: (NSInteger) state
                                                 extraInfo:(NSString *)extraInfo {
     // Receive RTC join room result
}

- (void)rtcEngine:(ByteRTCVideo *)engine onLocalAudioPropertiesReport:(NSArray<ByteRTCLocalAudioPropertiesInfo *> *)audioPropertiesInfos {
     // local user volume callback
}

- (void)rtcEngine:(ByteRTCVideo *)engine onRemoteAudioPropertiesReport:(NSArray<ByteRTCRemoteAudioPropertiesInfo *> *)audioPropertiesInfos
                                                      totalRemoteVolume:(NSInteger) totalRemoteVolume {
     // Remote user volume callback
}
```


<span id="implementing-cross-room-host-interaction"></span>
### Implementing Cross\-Room Host Interaction

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/614b98aa-f865-4698-b36f-8d8841118d78.png) </span>

<span id="sample-code"></span>
#### Sample Code

```objectivec
/**
* Starts forwarding media streams to other rooms.
* @param roomID The ID of the destination room.
* @param token The token required to join the room is issued by your application server
 **/

- (void)startForwardStream:(NSString *)roomId token:(NSString *)token {
    ForwardStreamConfiguration *configuration = [[ForwardStreamConfiguration alloc] init];
    configuration.roomId = roomId;
    configuration.token = token;
    int res = [self.rtcRoom startForwardStreamToRooms:@[configuration]];
    if (res != 0) {
        NSLog(@"failed tostart forward code code:%d", res);
    }
}

/**
* Callback for when a remote user publishes a media stream in the room.
 * @param rtcRoom ByteRTCRoom object
 * @param userId User ID of the user
 * @param type the type of remote media stream
 **/

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom onUserPublishStream:(NSString *)userId
           type:(ByteRTCMediaStreamType)type {
    if (type == ByteRTCMediaStreamTypeVideo ||
        type == ByteRTCMediaStreamTypeBoth) {
// Get the rendering view from the application layer.
        UIView *renderView = [self getRenderView];
       
        ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
        canvas.renderMode = ByteRTCRenderModeHidden;
        canvas.view.backgroundColor = [UIColor clearColor];
        canvas. view = renderView;
               
        ByteRTCRemoteStreamKey *streamKey = [[ByteRTCRemoteStreamKey alloc] init];
        streamKey. userId = userId;
        streamKey.roomId = self.rtcRoom.getRoomId;
        streamKey.streamIndex = ByteRTCStreamIndexMain;
        [self.rtcEngineKit setRemoteVideoCanvas:streamKey withCanvas:canvas];
    }
}

/**
* Stops forwarding media streams to other rooms.
 **/

- (void)stopForwardStream {
    [self.rtcRoom stopForwardStreamToRooms];
}
```


<span id="co-host-between-host-and-audience"></span>
### Co\-host between Host and Audience

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/b07bf292-de6d-4059-983c-085b6643ca46.png) </span>

**Sample Code**

```objectivec
 /**
* Promotes an audience member to a co-host.
* @param userID The user ID of the audience member becoming a co-host.
 **/

- (void)receivedJoinInteractWithUser:(NSString *)userID {
// TODO: Replace with the logged-in user's ID
    NSString *LoginUserID = @"";
    // The co-host is the logged in user
    if ([userID isEqualToString:LoginUserID]) {
        // Update the RTC encoding resolution, frame rate, and bit rate. Contact technical support for specific values.
        // Refer to :https://docs.byteplus.com/byteplus-rtc/docs/70122
        ByteRTCVideoEncoderConfig *videoEncoderConfig = [[ByteRTCVideoEncoderConfig alloc] init];
        videoEncoderConfig.width = width;
        videoEncoderConfig.height = height;
        videoEncoderConfig.frameRate = frameRate;
        videoEncoderConfig.maxBitrate = maxBitrate;
        [self.rtcEngineKit setMaxVideoEncoderConfig:videoEncoderConfig];
        
// The audience member turns on their camera and microphone.
        [self.rtcEngineKit startAudioCapture];
        [self.rtcEngineKit startVideoCapture];
        
// The audience member starts audio and video streaming.
        [self.rtcRoom publishStream:ByteRTCMediaStreamTypeBoth];
        
// The audience member is set to visible.
        [self.rtcRoom setUserVisibility:YES];
    }
}

/**
* Handles the notification for a co-host being demoted to an audience member.
* @param userID The user ID of the co-host being demoted to an audience member.
 **/

- (void)receivedLeaveInteractWithUser:(NSString *)userID {
// Replace with the logged-in user's ID
    NSString *LoginUserID = @"";
    // The co-host is the logged in user
    if ([userID isEqualToString:LoginUserID]) {
// The audience member turns off their camera and microphone.
        [self.rtcEngineKit stopAudioCapture];
        [self.rtcEngineKit stopVideoCapture];
        
// The audience member stops publishing their audio and video stream.
        [self.rtcRoom unpublishStream:ByteRTCMediaStreamTypeBoth];
        
// The audience member is set to invisible.
        [self.rtcRoom setUserVisibility:NO];
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
|Set User Visibility |[setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#setuservisibility) |
|Enable internal video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture) |
|Disable internal video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture) |
|Enable internal audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startaudiocapture) |
|Disable internal audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopaudiocapture) |
|Set the video encoding configuration |[SetVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideoencoderconfig) |
|Enable mirroring for the captured video stream |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70086#setlocalvideomirrortype) |
|Set the current audio playback route |[setDefaultAudioRoute:](https://docs.byteplus.com/en/docs/12/docs-70086#setdefaultaudioroute) |
|Enable volume level reporting |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#enableaudiopropertiesreport) |
|Join RTC room |joinRoom:userInfo:roomConfig: |
|Leave the RTC room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) |
|Destroy the room object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70086#destroy) |
|Publish the media stream in the current room |publishStream: |
|Start forwarding media streams across rooms |[startForwardStreamToRooms:](https://docs.byteplus.com/en/docs/12/docs-70086#startforwardstreamtorooms) |
|Stop forwarding media streams across rooms |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70086#stopforwardstreamtorooms) |
|Set local video rendering |setLocalVideoCanvas:withCanvas: |
|Set remote video rendering |setRemoteVideoCanvas:withIndex:withCanvas: |


<span id="callback"></span>
### callback


|Function |Callback |
|---|---|
|Callback for when the local user joins the room |rtcRoom:onRoomStateChanged:uid:state:extraInfo |
|Callback for when a remote user joins the room |rtcRoom:onUserJoined:elapsed: |
|Local user volume callback |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onlocalaudiopropertiesreport) |
|Remote user volume callback |[rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onremotaudiopropertiesreport-totalremotevolume) |
|Callback for when a remote user publishes a media stream |rtcRoom:onUserPublishStream:type: |
|Callback for cross\-room media stream forwarding status and errors |[rtcRoom:onForwardStreamStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#onforwardstreamstatechanged) |
