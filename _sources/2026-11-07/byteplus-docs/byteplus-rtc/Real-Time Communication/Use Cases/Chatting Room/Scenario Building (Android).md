---
title: "Scenario Building (Android)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-152874"
---

<span id="sdk-integration"></span>
## SDK Integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/image.jpg) </span>

<span id="implementation-flows"></span>
## Implementation Flows


* Overall business flow diagram


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/flowdia.png) </span>


* The room owner can invite audiences to become guests, remove guests from guest seats, and lock guest seats.

* The room owner can play background music and adjust the music and voice volumes.

* The room owner can enable or disable audience requests to co\-host. When this feature is disabled, an audience member's request to become a co\-host requires the owner's approval.

* Audience members can apply to become a guest or request to be removed from a guest spot.


<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="join-room"></span>
### Join room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/5c361f34-83b2-4af0-8690-1b3ab3c66c5d.png) </span>

<span id="sample-code"></span>
#### Sample code

```java
public void joinRoom(String roomId, String token, String userId, boolean isHost) {
     // Initialize the RTCVideo object
     mRTCVideo = RTCVideo.createRTCVideo(applicationContext, appId,
             mRTCVideoEventHandler, null, null);

     // Initialize the RTCRoom object
     mRTCRoom = mRTCVideo.createRTCRoom(roomId);
     mRTCRoom.setRTCRoomEventHandler(mRTCRoomEventHandler);

     // The host enables microphone capture, while the audience member disables it
     if (isHost) {
         mRTCVideo.startAudioCapture();
     } else {
         mRTCVideo. stopAudioCapture();
     }

     // Set audio routing mode
     mRTCVideo.setDefaultAudioRoute(AudioRoute.AUDIO_ROUTE_SPEAKERPHONE);

     // Enable speaker volume monitoring
     AudioPropertiesConfig config = new AudioPropertiesConfig(300);
     mRTCVideo.enableAudioPropertiesReport(config);

     // Set the host as visible and viewer as invisible
     mRTCRoom.setUserVisibility(isHost);

     // To join the room, you need a valid AppId and Token to enable co-hosting
     UserInfo userInfo = new UserInfo(userId, null);
     RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_INTERACTIVE_PODCAST,
             true, true, false);
     mRTCRoom.joinRoom(token, userInfo, roomConfig);
}
```


```java
private final IRTCRoomEventHandler mRTCRoomEventHandler = new IRTCRoomEventHandler() {

     /**
      * Receive RTC join room result
      */
     @Override
     public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
         super.onRoomStateChanged(roomId, uid, state, extraInfo);
     }

};

private final IRTCVideoEventHandler mRTCVideoEventHandler = new IRTCVideoEventHandler() {
    
     /**
      * Local user volume callback
      *
      * @param audioPropertiesInfos local audio information
      */
     @Override
     public void onLocalAudioPropertiesReport(LocalAudioPropertiesInfo[] audioPropertiesInfos) {
         super.onLocalAudioPropertiesReport(audioPropertiesInfos);
     }

     /**
      * Remote user volume callback
      *
      * @param audioPropertiesInfos remote audio information, including audio stream properties, room ID, user ID
      * @param totalRemoteVolume The total volume of all subscribed remote audio streams after mixing.
      */
     @Override
     public void onRemoteAudioPropertiesReport(RemoteAudioPropertiesInfo[] audioPropertiesInfos, int totalRemoteVolume) {
         super.onRemoteAudioPropertiesReport(audioPropertiesInfos, totalRemoteVolume);
     }
}
```


<span id="co-host"></span>
### Co\-host

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/e53d7123-6221-415e-86ff-f746a6c81110.png) </span>

<span id="code-sample"></span>
#### Code sample

```java
// An audience member becomes a co-host, or a co-host reverts to being an audience member
public void makeCoHost(boolean isCoHost) {
    if (isCoHost) {
        mRTCVideo.startAudioCapture();
        mRTCRoom.setUserVisibility(true);
        mRTCRoom.publishStream(MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO);
    } else {
        mRTCVideo.stopAudioCapture();
        mRTCRoom.setUserVisibility(false);
        mRTCRoom.unpublishStream(MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO);
    }
}
```


<span id="background-music"></span>
### Background music

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/image5.jpg.jpg) </span>

<span id="code-sample"></span>
#### Code sample

```java
/** 
 * Set background music 
 * @param filePath mix file path 
 */ 
public void startBackgroundMusic(String filePath) {
    // Get the IAudioEffectPlayer object
    IAudioEffectPlayer audioEffectPlayer = mRTCVideo.getAudioEffectPlayer();
    // start mixing playback
    audioEffectPlayer.preload(audioMixingId, filePath);
    AudioMixingConfig config = new AudioMixingConfig(AUDIO_MIXING_TYPE_PLAYOUT_AND_PUBLISH, -1);
    audioEffectPlayer.start(audioMixingId, filePath, config);
}
 
/** 
 * Set audio capture volume 
 * @param volume The ratio of the captured volume to the original volume. The range is `[0, 400]`, the recommended range is `[0, 100]`. 
 */ 
public void setRecordingVolume(int volume) { 
    // Set the microphone acquisition volume 
    mRTCVideo.setCaptureVolume(StreamIndex.STREAM_INDEX_MAIN, volume); 
} 
 
/** 
 * Set the mix volume 
 * @param volume The ratio of the mixing volume to the original volume. The range is `[0, 400]`, the recommended range is `[0, 100]`. 
 */ 
public void setMusicVolume(int volume) {
    // Get the IAudioEffectPlayer object
    IAudioEffectPlayer audioEffectPlayer = mRTCVideo.getAudioEffectPlayer();
    audioEffectPlayer.setVolume(audioMixingId, volume);
}
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create ByteRTCVideo instance |[createRTCEngine](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcengine) |
|Create ByteRTCRoom instance |[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcroom) |
|Start microphone capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startaudiocapture) |
|Disable microphone capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopaudiocapture) |
|Set audio routing mode |[setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#setdefaultaudioroute) |
|Enable speaker volume monitoring |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#enableaudiopropertiesreport) |
|Set User Visibility |[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#setuservisibility) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |
|Leave the RTC room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#leaveroom) |
|Destroy the room object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#destroy) |
|Create a mixing management interface |[getAudioEffectPlayer](https://docs.byteplus.com/en/docs/12/docs-70080#getaudioeffectplayer) |
|Start mixing playback |[start](https://docs.byteplus.com/en/docs/12/docs-70080#start) |
|Turn off mixing playback |[stop](https://docs.byteplus.com/en/docs/12/docs-70080#stop) |
|Pause mixing playback |[pause](https://docs.byteplus.com/en/docs/12/docs-70080#pause) |
|Resume mixing playback |[resume](https://docs.byteplus.com/en/docs/12/docs-70080#resume) |
|Set the mixing volume |[setVolume()](https://docs.byteplus.com/en/docs/12/docs-70080#setvolume) |
|Set the microphone capture volume |[setCaptureVolume](https://docs.byteplus.com/en/docs/12/docs-70080#setcapturevolume) |


<span id="callback"></span>
### Callback


|Function |CallBack |
|---|---|
|Local user joins RTC callback |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) |
|Remote user joins RTC callback |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined) |
|Local user volume callback |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalaudiopropertiesreport) |
|Remote user volume callback |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onremoteaudiopropertiesreport) |
