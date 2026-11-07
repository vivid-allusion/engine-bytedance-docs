---
title: "Scenario Building (Android)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-154379"
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

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/356demo/androidjoinroom.jpg) </span>

<span id="sample-code"></span>
#### Sample code

```Java
/** 
   * Initialize and join the room 
   * @param appId The ID of the application 
   * @param roomId the RTC room to join 
   * @param userId The user ID 
   * @param userName The user name 
   * @param token The token for joining the RTC room 
   */ 
public void initAndJoinRoom(String appId, String roomId, String userId, String userName, 
                             String token) { 
     // create RTC engine object 
     mRTCVideo = RTCVideo.createRTCVideo(Utilities.getApplicationContext(), appId, 
             mIRTCEngineEventHandler, null, null); 
     // Create RTC Room object 
     mRTCRoom = mRTCVideo.createRTCRoom(roomId); 
     mRTCRoom.setRTCRoomEventHandler(mRTCRoomEventHandler); 
     // start audio capture 
     mRTCVideo.startAudioCapture(); 
     // Turn on/off video capture according to settings 
     if (mIsCameraOn) { 
         mRTCVideo.startVideoCapture(); 
     } else { 
         mRTCVideo. stopVideoCapture(); 
     } 
     // Enable/disable audio push according to settings 
     if (mIsAudioMute) { 
         mRTCRoom.unpublishStream(MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO); 
     } else { 
         mRTCRoom.publishStream(MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO); 
     } 
// Selects the audio route (speaker or earpiece) based on the settings 
     mRTCVideo.setDefaultAudioRoute(mIsSpeakerphone 
             ? AudioRoute.AUDIO_ROUTE_SPEAKERPHONE 
             : AudioRoute.AUDIO_ROUTE_EARPIECE); 
// Enables audio property reports with a callback interval of 1000 ms 
     mRTCVideo.enableAudioPropertiesReport( 
             new AudioPropertiesConfig( 
                     1000, 
                     true, 
                     false)); 
     // Join the RTC room, enable automatic publishing and subscription 
     RTCRoomConfig roomConfig = new RTCRoomConfig(roomProfile.room_PROFILE_COMMUNICATION, 
             true, true, true); 
     mRTCRoom.joinRoom(token, userIdNameToUserInfo(userId, userName), roomConfig); 
} 
 
/** 
   * Assemble userInfo of RTC 
   * User nicknames are stored in `extraInfo` in JSON format and can be parsed by other users in the onUserJoined callback 
   * 
   * @param userId user id 
   * @param userName user nickname 
   * @return userinfo 
   */ 
private UserInfo userIdNameToUserInfo(String userId, String userName) { 
     VideoCallUserInfo userInfo = new VideoCallUserInfo(); 
     userInfo. userId = userId; 
     userInfo. userName = userName; 
     String extra = GsonUtils.gson().toJson(userInfo); 
     return new UserInfo(userId, extra); 
} 
 
/** 
   * User data model 
   */ 
public class VideoCallUserInfo { 
 
     // User's Nickname 
     @SerializedName("user_name") 
     public String userName; 
     // userid 
     @SerializedName("user_id") 
     public String userId; 
     
      … 
} 
```



* Leave room


```Java
public void leaveRoom() {
    if (mRTCVideo != null) {
        // Stop audio capture
        mRTCVideo.stopAudioCapture();
    }
    if (mRTCRoom != null) {
        // Leave the room
        mRTCRoom.leaveRoom();
        mRTCRoom.destroy();
        mRTCRoom = null;
    }
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

   For example, if the local user's network switches from Wi\-Fi to 5G, they will receive the onUserJoined callback for any user who joined during the switch after the network reconnection is successful.

* Handling long\-term disconnections


```Java
/**
   * Callback for room state changes, triggered when a user joins or leaves a room, or when a room-related warning or error occurs 
   * @param roomId room id
   * @param uid user id
   * @param state room status code
   * @param extraInfo extra information
   */
@Override
public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
     super.onRoomStateChanged(roomId, uid, state, extraInfo);
     int joinType = getJoinType(extraInfo);
     if (joinType == 1 && state == 0) {
                 SolutionDemoEventManager. post(new NetworkTypeChangedEvent(true));
         }

}

/**
   * Get join room type
   * @param extraInfo extra information
   * @return The room join type 
   */
private int getJoinType(String extraInfo) {
     int joinType = -1;
     try {
// `joinType` indicates the room entry type: 0 for joining for the first time, and 1 for reconnecting 
         JSONObject json = new JSONObject(extraInfo);
                 joinType = json. getInt("join_type");
         } catch (Exception e) {
                 e.printStackTrace();
         }
     return joinType;
}
```


<span id="screen-sharing"></span>
### Screen sharing

For Screen sharing, see [Android](https://docs.byteplus.com/en/docs/12/docs-124176)

<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create ByteRTCVideo instance |createRTCVideo |
|Set the video encoder configuration |[SetVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setvideoencoderconfig) |
|Start local audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startaudiocapture) |
|Start local video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture) |
|Set local video rendering |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideocanvas) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |
|Set the canvas for a remote video stream |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setremotevideocanvas) |
|Leave Room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#leaveroom) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopaudiocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopvideocapture) |
|Destroy engine instance object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#destroy) |
|Publish/Stop the local media stream captured by the camera/microphone |publishStream |
|Set the audio playback device as speaker or earpiece |setAudioRoute |
|Enable audio properties report |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#enableaudiopropertiesreport) |
|Enable mirroring |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideomirrortype) |
|Set audio profile |[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70080#setaudioprofile) |
|Switch between front and rear cameras |[switchCamera](https://docs.byteplus.com/en/docs/12/docs-70080#switchcamera) |


<span id="callback"></span>
### Callback


|Function |Callback |
|---|---|
|Local user joins room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onroomstatechanged) |
|A remote user becomes visible in the room |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onuserjoined) |
|A remote user publishes a media stream |[onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
|A remote user unpublishes a media stream |onuserpublishStream |
|Callback that reports local audio properties |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
|Callback for events related to the connection status between the SDK and the signaling server |[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
