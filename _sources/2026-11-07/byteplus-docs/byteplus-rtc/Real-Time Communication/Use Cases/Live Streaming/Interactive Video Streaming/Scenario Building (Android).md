---
title: "Scenario Building (Android)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-154499"
---

<span id="sdk-integration"></span>
## SDK integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/intergration.png) </span>

<span id="implementation-flowchart"></span>
## Implementation flowchart


* **Cross\-Room Host Competition**

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/pkbet.png) </span>

* **Interact between host and co\-host**

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/interactivevideostreaming/intbet.png) </span>


<span id="core-feature-implementation"></span>
## Core feature implementation

<span id="host-starts-live-stream-and-audience-enters-room"></span>
### Host Starts Live Stream and Audience Enters Room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/b6b15375-88d8-4eee-b36c-329a108c0bc5.png) </span>

<span id="sample-code"></span>
#### Sample Code

```Java
/**
  * Join the RTC room and initialize parameters
  * @param token the token to join the RTC room
  * @param roomId The ID of the RTC room to join
  * @param userId join the userId of the RTC room
  * @param isHost Specifies the user role. Set to `true` for a host or `false` for an audience member.
  */
public void joinRTCRoom(String token, String roomId, String userId, boolean isHost) {
     // Initialize the RTCVideo object
     mRTCVideo = RTCVideo.createRTCVideo(applicationContext, appId, mRTCVideoEventHandler, null, null);
     // Initialize the RTCRoom object
     mRTCRoom = mRTCVideo.createRTCRoom(roomId);
     mRTCRoom.setRTCRoomEventHandler(mRTCRoomEventHandler);
     // Set the host as visible and the viewer as invisible
     mRTCRoom.setUserVisibility(isHost);
// When joining the room, the host needs to enable their microphone and camera, and the audience needs to turn off the microphone and camera
     if (isHost) {
         mRTCVideo.startVideoCapture();
         mRTCVideo.startAudioCapture();
         // Set up local rendering and encoding mirroring
         mRTCVideo.setLocalVideoMirrorType(MirrorType.MIRROR_TYPE_RENDER_AND_ENCODER);
     } else {
         mRTCVideo. stopVideoCapture();
         mRTCVideo. stopAudioCapture();
     }
     // Set audio routing mode
     mRTCVideo.setDefaultAudioRoute(AudioRoute.AUDIO_ROUTE_SPEAKERPHONE);
     // Enable speaker volume monitoring
     AudioPropertiesConfig audioPropertiesConfig = new AudioPropertiesConfig(300);
     mRTCVideo.enableAudioPropertiesReport(audioPropertiesConfig);
     // Join the room and start connecting to the host, you need to apply for AppId and Token
     UserInfo userInfo = new UserInfo(userId, null);
     RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_INTERACTIVE_PODCAST,
             true, true, true);
     mRTCRoom.joinRoom(token, userInfo, roomConfig);
}
```


```Java
private final IRTCVideoEventHandler mRTCVideoEventHandler = new IRTCVideoEventHandler(){
     @Override
     public void onLocalAudioPropertiesReport(LocalAudioPropertiesInfo[] audioPropertiesInfos) {
         super.onLocalAudioPropertiesReport(audioPropertiesInfos);
         // local user volume callback
     }
     @Override
     public void onRemoteAudioPropertiesReport(RemoteAudioPropertiesInfo[] audioPropertiesInfos, int totalRemoteVolume) {
         super.onRemoteAudioPropertiesReport(audioPropertiesInfos, totalRemoteVolume);
         // Remote user volume callback
     }
};
private final IRTCRoomEventHandler mRTCRoomEventHandler = new IRTCRoomEventHandler() {
     @Override
     public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
         // Receive RTC join room result
     }
}
```


<span id="cross-room-co-hosting"></span>
### Cross\-Room Co\-hosting

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/ed44b70b-518b-46a7-bfbf-7e3c9d74097a.png) </span>

<span id="sample-code"></span>
#### Sample Code

```Java
/**
* start forward across rooms
* @param roomId The ID of the destination room
* @param token  The token required to join the room is issued by the business server
**/
public void startForwardStream(String roomId, String token) {
   ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(roomId, token);
   mRTCRoom.startForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
}

private final IRTCRoomEventHandler mRTCRoomEventHandler = new IRTCRoomEventHandler() {

   /**
    * Added callback for remote media stream in the room
    * @param rtcRoom The ByteRTCRoom object
    * @param type Type of remote media stream
    */
   @Override
   public void onUserPublishStream(String uid, MediaStreamType type) {
       if (type == MediaStreamType.RTC_MEDIA_STREAM_TYPE_AUDIO) {
           return;
       }
       TextureView textureView = new TextureView(applicationContext);
       VideoCanvas videoCanvas = new VideoCanvas(textureView,VideoCanvas.RENDER_MODE_HIDDEN);
       RemoteStreamKey streamKey = new RemoteStreamKey(roomId,uid,StreamIndex.STREAM_INDEX_MAIN);
       mRTCVideo.setRemoteVideoCanvas(streamKey,videoCanvas);
   }
};

/**
* stop forward across rooms
*/
public void stopForwardStream() {
   mRTCRoom.stopForwardStreamToRooms();
}
```


<span id="co-host-between-host-and-audience"></span>
### Co\-host between Host and Audience

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/6dc954a7-9ed5-4e49-b226-db3d0300b7e0.png) </span>

**Sample Code**

```Java
/**
 * Handles an audience member being promoted to a co-host
 * @param User ID of audiences becoming co-host
 */
public void onReceivedJoinInteract(String userId) {
// The ID of the locally logged-in user in your application.
    if (!TextUtils.equals(userId, loginUserId)) {
        return;
    }
    // Update the RTC encoding resolution, frame rate, and bit rate. Contact technical support for specific values.
        // Refer to: https://docs.byteplus.com/byteplus-rtc/docs/70122
    VideoEncoderConfig videoEncoderConfig = new VideoEncoderConfig();
    videoEncoderConfig.width = width;
    videoEncoderConfig.height = height;
    videoEncoderConfig.frameRate = frameRate;
    videoEncoderConfig.maxBitrate = maxBitrate;
    videoEncoderConfig.minBitrate = minBitrate;
    mRTCVideo.setVideoEncoderConfig(videoEncoderConfig);
// The audience member enables their camera and microphone
    mRTCVideo.startVideoCapture();
    mRTCVideo.startAudioCapture();
    // Audience is set to visible
    mRTCRoom.setUserVisibility(true);
// The audience member enables their camera and microphone
    mRTCRoom.publishStream(MediaStreamType.RTC_MEDIA_STREAM_TYPE_BOTH);
}
/**
 * Receive a notification of a co-host becoming audience
 * @param userId userI User ID of a co-host becoming audience
 */
public void onReceivedLeaveInteract(String userId) {
// The ID of the locally logged-in user in your application.
    if (!TextUtils.equals(userId, loginUserId)) {
        return;
    }
// The co-host (now an audience member) disables their camera and microphone
    mRTCVideo.stopVideoCapture();
    mRTCVideo.stopAudioCapture();
// The audience member is set to invisible
    mRTCRoom.setUserVisibility(false);
// The audience member stops publishing their audio and video stream
    mRTCRoom.unpublishStream(MediaStreamType.RTC_MEDIA_STREAM_TYPE_BOTH);
}
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create ByteRTCVideo instance |createRTCVideo |
|Create ByteRTCRoom instance |[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcroom) |
|Set User Visibility |[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#setuservisibility) |
|Enable internal video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture) |
|Disable internal video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startvideocapture) |
|Enable internal audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startaudiocapture) |
|Disable internal audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopaudiocapture) |
|Set video encoding parameters (e.g., resolution, frame rate, and bitrate) |[SetVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setvideoencoderconfig) |
|Enable mirroring for the captured video stream |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideomirrortype) |
|Set the current audio playback route |[setDefaultAudioRoute](https://docs.byteplus.com/en/docs/12/docs-70080#setdefaultaudioroute) |
|Enable volume level reporting |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70080#enableaudiopropertiesreport) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |
|Leave the RTC room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#leaveroom) |
|Destroy the room object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#destroy) |
|Publish/Stop a media stream in the current room |publishStream |
|Start forwarding media streams across rooms |[startForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#startforwardstreamtorooms) |
|Stop forwarding media streams across rooms |[stopForwardStreamToRooms](https://docs.byteplus.com/en/docs/12/docs-70080#stopforwardstreamtorooms) |
|Set local video rendering |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideocanvas) |
|Set remote video rendering |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setremotevideocanvas) |


<span id="callback"></span>
### callback


|Function |Callback |
|---|---|
|Callback for the local user joining a room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onroomstatechanged) |
|Remote user joins RTC callback |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
|Local user volume callback |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onlocalaudiopropertiesreport) |
|Remote user volume callback |[onRemoteAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70081#onremoteaudiopropertiesreport) |
|Added remote media stream callback in the room |onuserpublishstream |
|Cross\-room media stream forwarding status and error callback |[onForwardStreamStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onforwardstreamstatechanged) |
