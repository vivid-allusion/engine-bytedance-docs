---
title: "Scenario Building (iOS)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-117921"
---

<span id="sdk-integration"></span>
## SDK Integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865).

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/image.jpg) </span>

<span id="implementation-flows"></span>
## Implementation Flows


* Overall business flow diagram


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/flowdia.png) </span>


* The room owner can invite audience members to become guests, remove guests, and lock guest seats.

* The room owner can play background music and adjust the music and voice volume.

* The room owner can enable or disable requests from audience members to become guests. When this feature is disabled, the room owner must approve all such requests.

* Audience members can apply to become a guest or to leave their guest role.


<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="join-room"></span>
### Join room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/65c21852-042e-4c0f-a2ba-adfcd915bf1a.png) </span>

<span id="sample-code"></span>
#### Sample code

```objectivec
/**
  * Join the RTC room and initialize parameters
  * @param token: RTC Token
  * @param roomID: RTC room ID
  * @param uid: RTC user ID
  * @param isHost: Set to YES if the user is a host; set to NO if the user is an audience member.
  **/

- (void)joinRTCRoomWithToken:(NSString *)token
                       roomID: (NSString *) roomID
                          uid:(NSString *)uid
                       isHost:(NSString *)isHost {
     // Initialize the ByteRTCVideo object
     self.rtcEngineKit = [ByteRTCVideo createRTCVideo:appID
                                             delegate:self
                                           parameters:@{}];
    
     // Initialize the ByteRTCRoom object
     self.rtcRoom = [self.rtcEngineKit createRTCRoom:roomID];
     self.rtcRoom.delegate = self;
    
     // The host turns on the microphone capture, and the audience member disables it
     if (isHost) {
         [self.rtcEngineKit startAudioCapture];
     } else {
         [self.rtcEngineKit stopAudioCapture];
     }
 
     // Set audio routing mode
     [self.rtcEngineKit setDefaultAudioRoute:ByteRTCAudioRouteSpeakerphone];
 
     // Turn on speaker volume monitoring (for displaying sound wave effects)
     ByteRTCAudioPropertiesConfig *audioPropertiesConfig = [[ByteRTCAudioPropertiesConfig alloc] init];
     audioPropertiesConfig.interval = 300;
     [self.rtcEngineKit enableAudioPropertiesReport:audioPropertiesConfig];
    
     // Set the host as visible and viewer as invisible
     [self.rtcRoom setUserVisibility:isHost? YES : NO];
 
     // To join the room and enable co-hosting, you must provide a valid AppId and Token.
     ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
     userInfo. userId = uid;
     ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
     config.profile = ByteRTCRoomProfileInteractivePodcast;
     config.isAutoPublish = YES;
     config.isAutoSubscribeAudio = YES;
     [self.rtcRoom joinRoom:token userInfo:userInfo roomConfig:config];
}
```


```objectivec

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom onRoomStateChanged:(NSString *)roomId
                                                   withUid:(NSString *)uid
                                                     state: (NSInteger) state
                                                 extraInfo:(NSString *)extraInfo {
     // Handles the callback for the result of joining an RTC room.
}

- (void)rtcEngine:(ByteRTCVideo *)engine onLocalAudioPropertiesReport:(NSArray<ByteRTCLocalAudioPropertiesInfo *> *)audioPropertiesInfos {
     // local user volume callback
}

- (void)rtcEngine:(ByteRTCVideo *)engine onRemoteAudioPropertiesReport:(NSArray<ByteRTCRemoteAudioPropertiesInfo *> *)audioPropertiesInfos
                                                      totalRemoteVolume:(NSInteger) totalRemoteVolume {
     // Remote user volume callback
}
```


<span id="co-host"></span>
### Co\-host

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/ec7a1a26-abff-43e9-98d7-f18e82029b3a.png) </span>

<span id="code-sample"></span>
#### Code sample

```objectivec
// An audience member becomes a co-host, or a co-host reverts to being an audience member.

- (void)makeCoHost:(BOOL)isCoHost {
    if (isCoHost) {
        [self.rtcEngineKit startAudioCapture];
        [self.rtcRoom setUserVisibility:YES];
        [self.rtcRoom publishStream:ByteRTCMediaStreamTypeAudio];
    } else {
        [self.rtcEngineKit stopAudioCapture];
        [self.rtcRoom setUserVisibility:NO];
        [self.rtcRoom unpublishStream:ByteRTCMediaStreamTypeAudio];
    }
}
```


<span id="background-music"></span>
### Background music

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/image5.jpg) </span>

<span id="code-sample"></span>
#### Code sample

```objectivec
 
- (void)startBackgroundMusic:(NSString *)filePath { 
    // Get ByteRTCAudioMixingManager object 
    ByteRTCAudioEffectPlayer *audioPlayer = [self.rtcEngineKit getAudioEffectPlayer];
     
    // Mixes and publishes the audio stream.
    ByteRTCAudioEffectPlayerConfig *config = [[ByteRTCAudioEffectPlayerConfig alloc] init];
    config.type = ByteRTCAudioMixingTypePlayoutAndPublish;
    config.playCount = -1;
    [audioPlayer start:_audioMixingID filePath:filePath config:config];
} 
 
- (void)setRecordingVolume:(NSInteger)volume { 
    // Sets the volume of the microphone capture.
    [self.rtcEngineKit setCaptureVolume:ByteRTCStreamIndexMain volume:(int)volume];
} 
  
- (void)setMusicVolume:(NSInteger)volume { 
    // Sets the volume of the mixed audio.
    ByteRTCAudioEffectPlayer *audioPlayer = [self.rtcEngineKit getAudioEffectPlayer];
    [audioPlayer setVolume:_audioMixingID volume:(int)volume];
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
|Start microphone capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startaudiocapture) |
|Turn off video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopaudiocapture) |
|Set the audio route mode |[setDefaultAudioRoute:](https://docs.byteplus.com/en/docs/12/docs-70086#setdefaultaudioroute) |
|Enable speaker volume monitoring |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#enableaudiopropertiesreport) |
|Set user visibility |[setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#setuservisibility) |
|Join RTC room |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#joinroom-userinfo-uservisibility-roomconfig) |
|Leave RTC room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) |
|Destroy the room object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70086#destroy) |
|Get audio mixing manager |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70086#getaudioeffectplayer) |
|Start audio mixing |[start:filePath:config:](https://docs.byteplus.com/en/docs/12/docs-70086#start-filePath-config) |
|Turn off audio mixing |[stop:](https://docs.byteplus.com/en/docs/12/docs-70086#stop) |
|Pause audio mix playback |[pause:](https://docs.byteplus.com/en/docs/12/docs-70086#pause) |
|Resume audio mixing |[resumeAudioMixing:](https://docs.byteplus.com/en/docs/12/docs-70086#resume) |
|Set the mixing volume |[setAudioMixingVolume:volume:type:](https://docs.byteplus.com/en/docs/12/docs-70086#setVolume-volume) |
|Set the microphone capture volume |[setCaptureVolume:](https://docs.byteplus.com/en/docs/12/docs-70086#setcapturevolume) |


<span id="callback"></span>
### Callback


|Function |Callback |
|---|---|
|Callback for the local user joining a room |[rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/6uofwzl3/14067) |
|Callback for a remote user joining the room |[rtcRoom:onUserJoined:](https://docs.byteplus.com/en/docs/12/docs-70087#onuserjoined) |
|Local user volume callback |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onlocalaudiopropertiesreport) |
|Remote user volume callback |[rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onremoteaudiopropertiesreport-totalremotevolume) |
