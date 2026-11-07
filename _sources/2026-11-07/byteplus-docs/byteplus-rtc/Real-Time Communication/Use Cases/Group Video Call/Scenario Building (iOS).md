---
title: "Scenario Building (iOS)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-154378"
---

<span id="sdk-integration"></span>
## SDK Integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/intergration.png) </span>

<span id="implementation-flows"></span>
## Implementation Flows

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/videocall/dc462788-5261-4add-ad3c-ea4f5add5e4a.png) </span>

<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="join-room-and-leave-room"></span>
### Join room and leave room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/imagejoinroomvideocall.jpg) </span>

<span id="sample-code"></span>
#### Sample code

```objectivec

- (void)joinRTCRoomWithModel:(VideoCallRoomUserModel *)localUserModel
                     rtcToken:(NSString *)rtcToken {
     // Initialize the RTC Video object
     self.rtcRTCVideo = [ByteRTCVideo createRTCVideo:appID
                                            delegate:self
                                          parameters:@{}];
     // Initialize the RTC Room object
     self.rtcRoom = [self.rtcRTCVideo createRTCRoom:roomId];
     self.rtcRoom.delegate = self;
// Start microphone capture
     [self.rtcRTCVideo startAudioCapture];
     // Enable/disable camera capture according to the preview page configuration
     if (preSetting. isEnableVideo) {
         [self.rtcRTCVideo startVideoCapture];
     } else {
         [self.rtcRTCVideo stopVideoCapture];
     }
     // Enable/disable audio push according to the preview page configuration
     if (preSetting.isEnableAudio) {
         [self.rtcRoom publishStream:ByteRTCMediaStreamTypeAudio];
     } else {
         [self.rtcRoom unpublishStream:ByteRTCMediaStreamTypeAudio];
     }
     //Set the audio routing mode, speaker/earpiece
     [self.rtcRTCVideo setAudioPlaybackDevice:preSetting.playback];
// Enable the audio properties report
     ByteRTCAudioPropertiesConfig *audioPropertiesConfig = [[ByteRTCAudioPropertiesConfig alloc] init];
     audioPropertiesConfig.interval = 1000;
     [self.rtcRTCVideo enableAudioPropertiesReport:audioPropertiesConfig];
// Join the room. You must have an AppID and a token.
     ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
     userInfo.userId = localUserModel.uid;
     NSDictionary *extraInfo = @{
         @"user_name": localUserModel.name,
         @"user_id": localUserModel.uid
     };
     userInfo.extraInfo = [extraInfo yy_modelToJSONString];
     ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
     config.profile = ByteRTCRoomProfileCommunication;
// Enable automatic publishing
     config.isAutoPublish = YES;
     // Enable automatic subscription of audio and video
     config.isAutoSubscribeAudio = YES;
     config.isAutoSubscribeVideo = YES;
     [self.rtcRoom joinRoom:rtcToken userInfo:userInfo roomConfig:config];
}
```



* Leave room


```objectivec
- (void)leaveRTCRoom {
    [self.rtcEngineKit stopAudioCapture];
    [self.rtcRoom leaveRoom];
    [self.rtcRoom destroy];
    self.rtcRoom = nil;
}
```


<span id="reconnection-after-disconnection"></span>
### Reconnection after disconnection

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/videocall/e4840a13-8215-475a-ac15-9187b11bf78c.png) </span>

<span id="code-sample"></span>
#### Code sample


* Short\-term disconnection

   No action is required. The RTC SDK will resend the lost messages during network disconnection.

   For example: the local user network is switched from WIFI to 5G, and a remote user joins the room during the network switch. After the local user successfully switches networks, the SDK receives the onUserJoined callback.

* Handling long\-term disconnections


```objectivec

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom onRoomStateChanged:(NSString *)roomId withUid:(NSString *)uid state:(NSInteger)state extraInfo:(NSString *)extraInfo {
     NSDictionary *dic = [self dictionaryWithJsonString:extraInfo];
     NSInteger joinType = -1;
     if ([dic isKindOfClass:[NSDictionary class]]) {
         NSString *joinTypeStr = [NSString stringWithFormat:@"%@", dic[@"join_type"]];
         joinType = joinTypeStr. integerValue;
     }
     // joinType '0' means entering the room for the first time, '1' means joining the room again; state '0' means joining the room successfully
     // joinType '0' is the first time entering the room, '1' is the reconnection entering the room; state '0' means join the room successfully
     if (state == 0 && joinType == 1) {
// Call the application's reconnection API to update the application state.
         // Execute business re-API, update business status
         [Networking reconnectBlock:^(RTMACKModel * _Nonnull model) {
         }];
     }
}
```


<span id="screen-sharing"></span>
### Screen sharing

For Screen sharing, see [iOS](https://docs.byteplus.com/en/docs/12/docs-124177)

<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Feature |API |
|---|---|
|Create ByteRTCVideo instance |`createRTCVideo:delegate:parameters:` |
|Set video publishing parameters |[setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideoencoderconfig) |
|Start local audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startaudiocapture) |
|Start local video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture) |
|Set local video rendering |`setLocalVideoCanvas:withCanvas:` |
|Join RTC room |`joinRoom:userInfo:roomConfig:` |
|Set video rendering view |[setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/docs-70086#setremotevideocanvas-withcanvas) |
|Leave room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopaudiocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopvideocapture) |
|Destroy the engine instance |[destroy](https://docs.byteplus.com/en/docs/12/docs-70086#destroy) |
|Publish the local media stream |publishStream |
|Set the audio playback device to speaker or earpiece |[setAudioRoute:](https://docs.byteplus.com/en/docs/12/docs-70086#setaudioroute) |
|Enable audioProperties report |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#enableaudiopropertiesreport) |
|Enable mirroring |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70086#setlocalvideomirrortype) |
|Set audio profile |[setAudioProfile:](https://docs.byteplus.com/en/docs/12/docs-70086#setaudioprofile) |
|Switch the front/rear camera |[switchCamera:](https://docs.byteplus.com/en/docs/12/docs-70086#switchcamera) |


<span id="callback"></span>
### Callback


|Function point |Callback |
|---|---|
|Local user joins room |`rtcRoom:onRoomStateChanged:withUid:state:extraInfo:` |
|A remote user joins the room |`rtcRoom:onUserJoined:elapsed:` |
|A remote user publishes a media stream |`rtcRoom:onUserPublishStream:type:` |
|A remote media stream is removed |[rtcRoom:onUserUnpublishStream:type:reason:](https://docs.byteplus.com/en/docs/12/docs-70081#onuserunpublishstream-type-reason) |
|Callback for local audio properties |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalaudiopropertiesreport) |
|Reports connection status changes |[rtcEngine:onConnectionStateChanged:](https://docs.byteplus.com/en/docs/12/docs-70081#onconnectionstatechanged) |
