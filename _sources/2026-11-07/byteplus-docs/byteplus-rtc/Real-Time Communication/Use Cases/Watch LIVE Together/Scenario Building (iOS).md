---
title: "Scenario Building (iOS)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-153588"
---

<span id="sdk-integration"></span>
## SDK Integration

To ensure the best experience, this use case requires the integration of RTC SDK and MediaLive Player (recommended). You need to activate the service in the console of RTC and MediaLive. Activation instructions are as follows:


1. For details of the overall access process of RTC SDK, see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/image.jpg) </span>

2. For details of the access procedure of MediaLive player, see [Getting started with BytePlus MediaLive](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)

> You can do so by using the same third\-party LIVE player. To ensure the best experience, however, you must implement the audio hosting feature. For details, contact our technical support team.


<span id="implementation-flows"></span>
## Implementation Flows


* Overall business flow diagram


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/watchlivetogether/f6877cc6-3604-49f1-8221-326b39b3d98f.png) </span>

<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="join-room"></span>
### Join room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/watchlivejoinroom.jpg) </span>

<span id="sample-code"></span>
#### Sample code

```objectivec
/**
* Joins the RTC room and initializes the parameters
 * @param token: RTC Token
* @param roomID: RTC room ID
* @param uid: RTC user ID
 **/

- (void)joinRTCRoomWithToken:(NSString *)token
                      roomID:(NSString *)roomID
                         uid:(NSString *)uid {
    // Initialize the ByteRTCVideo object
    self.rtcEngineKit = [ByteRTCVideo createRTCVideo:APPID
                                        delegate:self
                                      parameters:@{}];
    
    // Initialize the ByteRTCRoom object
    self.rtcRoom = [self.rtcEngineKit createRTCRoom:roomID];
    self.rtcRoom.delegate = self;
    
    // Set visibility
    [self.rtcRoom setUserVisibility:YES];
    
When joining a room, hosts should enable their microphone and camera, while audience members should keep them disabled.
    [self.rtcEngineKit startVideoCapture];
    [self.rtcEngineKit startAudioCapture];
        
    // Set local rendering and encoded images
    [self.rtcEngineKit setLocalVideoMirrorType:ByteRTCMirrorTypeRenderAndEncoder];
   
    // Bind the local video preview view
    UIView *view = [[UIView alloc] init];
    ByteRTCVideoCanvas *videoCanvas = [[ByteRTCVideoCanvas alloc] init];
    videoCanvas.uid = uid;
    videoCanvas.renderMode = ByteRTCRenderModeHidden;
    videoCanvas.view = view;
    [self.rtcEngineKit setLocalVideoCanvas:ByteRTCStreamIndexMain
                                withCanvas:videoCanvas];
    
    // Set the audio scenario type
    [self.rtcEngineKit setAudioScenario:ByteRTCAudioScenarioCommunication];
 
    // Enable speaker volume monitoring
    ByteRTCAudioPropertiesConfig *audioPropertiesConfig = [[ByteRTCAudioPropertiesConfig alloc] init];
    audioPropertiesConfig.interval = 300;
    [self.rtcEngineKit enableAudioPropertiesReport:audioPropertiesConfig];
    
To join a room and enable audio communication, you must provide an AppId and a Token.
    ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
    userInfo.userId = uid;
    ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
    config.profile = ByteRTCRoomProfileLwtogether;
    config.isAutoPublish = YES;
    config.isAutoSubscribeAudio = YES;
    config.isAutoSubscribeVideo = YES;
    [self.rtcRoom joinRoom:token
                         userInfo:userInfo
                       roomConfig:config];
}
```


```objectivec

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom onRoomStateChanged:(NSString *)roomId
                                                  withUid:(NSString *)uid
                                                    state:(NSInteger)state
                                                extraInfo:(NSString *)extraInfo {
Callback for the result of joining an RTC room.
}

- (void)rtcEngine:(ByteRTCVideo *)engine onLocalAudioPropertiesReport:(NSArray<ByteRTCLocalAudioPropertiesInfo *> *)audioPropertiesInfos {
    // Local user volume callback    
}

- (void)rtcEngine:(ByteRTCVideo *)engine onRemoteAudioPropertiesReport:(NSArray<ByteRTCRemoteAudioPropertiesInfo *> *)audioPropertiesInfos 
                                                     totalRemoteVolume:(NSInteger)totalRemoteVolume {
    // Remote user volume callback
}

- (void)rtcRoom:(ByteRTCRoom *)rtcRoom onUserJoined:(ByteRTCUserInfo *)userInfo elapsed:(NSInteger)elapsed {
Callback for when a remote user joins the room.
}

/**
Callback for when a remote user publishes a new media stream (from a camera or microphone).
 */

- (void)rtcRoom:( ByteRTCRoom *)rtcRoom onUserPublishStream:(NSString *)userId type:(ByteRTCMediaStreamType)type {
    if (type == ByteRTCMediaStreamTypeAudio) {
        return;
    }
    // Bind remote user video view 
    UIView *view = [[UIView alloc] init];
    ByteRTCVideoCanvas *videoCanvas = [[ByteRTCVideoCanvas alloc] init];
    videoCanvas.uid = userId;
    videoCanvas.renderMode = ByteRTCRenderModeHidden;
    videoCanvas.view = view;
    videoCanvas.roomId = self.roomId;
    [self.rtcEngineKit setRemoteVideoCanvas:userId
                                  withIndex:ByteRTCStreamIndexMain
                                 withCanvas:videoCanvas];
}
```


<span id="watch-live-together"></span>
### Watch LIVE together

When the room owner initiates Watch LIVE together, audience members synchronously join the live room. The room owner and audience can watch the same live stream via the LIVE player.

For player integration and detailed instructions, see [Player SDK for iOS](https://docs.byteplus.com/en/byteplus-media-live/docs/implementing-basic-features-3)

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/watchlive.jpg) </span>

<span id="code-sample"></span>
#### Code sample

```objectivec
/** 
 * Enable PCM mix 
* @param mixId Mix ID. Used to identify the mix and ensure the unique mix ID. If this method is called repeatedly with the same ID, the existing mixing task stops and a new one begins.  
 */ 
 
- (void)startAudioMixing:(int)mixId { 
    // Enable local mix playback 
    ByteRTCMediaPlayer *mediaPlayer = [self.rtcEngineKit getMediaPlayer:mixId];
    ByteRTCMediaPlayerCustomSource *customSource = [[ByteRTCMediaPlayerCustomSource alloc] init];
    customSource.provider = nil;
    customSource.mode = ByteRTCMediaPlayerCustomSourceModePush;
    customSource.type = ByteRTCMediaPlayerCustomSourceStreamTypeRaw;
    
    ByteRTCMediaPlayerConfig *playerConfig = [[ByteRTCMediaPlayerConfig alloc] init];
    playerConfig.type = ByteRTCAudioMixingTypePlayout;
    playerConfig.playCount = 0;
    playerConfig.startPos = 0;
    playerConfig.syncProgressToRecordFrame = NO;
    playerConfig.autoPlay = YES;
    
    [mediaPlayer openWithCustomSource:customSource
                               config:playerConfig];
} 
 
/**  
 * Player audio data callback, pushing audio data to RTC 
 */ 
 
- (void)pushAudioMixingFrame:(int)mixId audioFrame:(ByteRTCAudioFrame *)audioFrame { 
    // Send the data from the player callback to RTC for playback 
    ByteRTCMediaPlayer *mediaPlayer = [self.rtcEngineKit getMediaPlayer:mixId];
    [mediaPlayer pushExternalAudioFrame:audioFrame]; 
} 
 
/** 
* Disable PCM mix 
*/ 
 
- (void)stopAudioMixing:(int)mixId { 
    // Disable mix 
    ByteRTCMediaPlayer *mediaPlayer = [self.rtcEngineKit getMediaPlayer:mixId];
    [mediaPlayer stop];
} 
```


<span id="console"></span>
### Console

<span id="code-sample"></span>
#### Code sample

```objectivec
/**  
* Enable/disable the volume ducking feature.
When this feature is enabled, the local media playback volume is automatically reduced when audio from remote users is detected, ensuring their voices are clearly audible. When the remote audio stops, the local media volume returns to its original level.
 * @param enable Whether to enable audio ducking 
 */ 
 
- (void)enablePlaybackDucking:(BOOL)enable { 
    [self.rtcEngineKit enablePlaybackDucking:enable]; 
} 
 
/**  
 * Adjust the mix volume, including audio file mixes and PCM mixes. 
 * @param mixId Mix ID 
* @param volume The mixing volume as a percentage of the original volume. The value ranges from `[0, 400]`, with a recommended range of `[0, 100]`. 
 */ 
 
- (void)setAudioMixingVolume:(int)mixId volume:(int)volume { 
    ByteRTCMediaPlayer *mediaPlayer = [self.rtcEngineKit getMediaPlayer:mixId];
    [mediaPlayer setVolume:volume type:ByteRTCAudioMixingTypePlayout];
} 
 
/**  
Adjusts the local playback volume of all mixed remote audio streams.
You can use this interface to set the playback volume before or during audio playback. * @param volume The ratio of the audio playback volume value to the original volume is in the range [0, 400] and in %, with built-in overflow protection.
 */ 
 
- (void)setPlaybackVolume:(NSInteger)volume { 
    [self.rtcEngineKit setPlaybackVolume:volume]; 
} 
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Creates an RTCVideo object |createRTCVideo:delegate:parameters: |
|Create RTCRoom object |[createRTCRoom:](https://docs.byteplus.com/en/docs/12/docs-70086#creatertcroom) |
|Set user visibility |[setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#setuservisibility) |
|Set local rendering and encoding mirroring |[setLocalVideoMirrorType:](https://docs.byteplus.com/en/docs/12/docs-70086#setlocalvideomirrortype) |
|Set local video rendering view |`setLocalVideoCanvas:withCanvas:` |
|Set audio scenario type |[setAudioScenario:](https://docs.byteplus.com/en/docs/12/docs-70086#setaudioscenario) |
|Enable audio properties report |[enableAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70086#enableaudiopropertiesreport) |
|Create a mixing management interface |[getMediaPlayer:](https://docs.byteplus.com/en/docs/12/docs-70086#getmediaplayer) |
|Start local audio capture |[startAudioCapture:](https://docs.byteplus.com/en/docs/12/docs-70086#startaudiocapture) |
|Start local video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startvideocapture) |
|Join RTC room |`joinRoom` |
|Set the remote user video rendering view |[setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/docs-70086#setremotevideocanvas-withcanvas) |
|Enable PCM audio data mixing |[openWithCustomSource:config:](https://docs.byteplus.com/en/docs/12/docs-70086#openwithcustomsource-config) |
|Push PCM audio frame data for mixing |[pushExternalAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#pushexternalaudioframe) |
|Adjust the volume of mixed audio |`setVolume:type:` |
|Disable audio mixing |[stop](https://docs.byteplus.com/en/docs/12/docs-70086#stop) |
|Adjust the playback volume of remote users |[setPlaybackVolume:](https://docs.byteplus.com/en/docs/12/docs-70086#setplaybackvolume) |
|Enable volume ducking |[enablePlaybackDucking:](https://docs.byteplus.com/en/docs/12/docs-70086#enableplaybackducking) |
|Leave room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) |
|Destroy the RTCRoom object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70086#destroy) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopaudiocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopvideocapture) |
|Destroy the RTCVideo object |destroyRTCVideo |


<span id="callback"></span>
### Callback


|Function |Callback |
|---|---|
|Local user joins RTC room |`rtcRoom:onRoomStateChanged:uid:state:extraInfo` |
|Audio playback route changes |[rtcEngine:onAudioRouteChanged:](https://docs.byteplus.com/en/docs/12/docs-70087#rtcengine-onaudioroutechanged) |
|Local audio's related information |[rtcEngine:onLocalAudioPropertiesReport:](https://docs.byteplus.com/en/docs/12/docs-70087#onlocalaudiopropertiesreport) |
|Audio properties of subscribed remote users |`rtcEngine:onRemoteAudioPropertiesReport:totalRemoteVolume:` |
|Remote user joins RTC room |`rtcRoom:onUserJoined:elapsed:` |
|A new media stream is published by a remote user in the room. |`rtcRoom:onUserPublishStream:type:` |
