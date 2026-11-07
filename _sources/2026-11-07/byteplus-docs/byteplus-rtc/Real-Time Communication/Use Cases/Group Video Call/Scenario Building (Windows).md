---
title: "Scenario Building (Windows)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-154438"
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

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/videocall/ce18d3a6-90cd-4a2b-8a42-17a1ff88cc72.png) </span>

<span id="sample-code"></span>
#### Sample code

```cpp
int VideoCallRtcEngineWrap::initAndJoinRTCRoom() {
     // Initialize the RTC Video object
     video_engine_(nullptr,[](bytertc::IRTCVideo* self) {
                             bytetc::destroyRTCVideo(); }),
     video_engine_.reset(bytertc::createRTCVideo(app_id.c_str(), this, ""));
         // Initialize the RTC Room object
      rtcRoom_ = std::shared_ptr<bytertc::IRTCRoom>(
             video_engine_->createRTCRoom(room_id.c_str()),
                 [=](bytertc::IRTCRoom* room) { room->destroy(); });
                
      // Enable/disable camera acquisition and video stream push according to the preview page configuration
     if (DataMgr::instance(). camera_on) {
         video_engine_->startVideoCapture();
         rtcRoom->publishStream(bytertc::MediaStreamType::kMediaStreamTypeVideo);
     }
     else {
         video_engine_->stopVideoCapture();
         rtcRoom_ ->unpublishStream(bytertc::MediaStreamType::kMediaStreamTypeVideo);
     }
   
     // Enable/disable audio capture and stream push according to the preview page configuration
     if (DataMgr::instance().mic_on) {
         video_engine_->startAudioCapture();
         rtcRoom->publishStream(bytertc::MediaStreamType::kMediaStreamTypeAudio);
     }
     else {
         video_engine_->stopAudioCapture();
         rtcRoom_ ->unpublishStream(bytertc::MediaStreamType::kMediaStreamTypeAudio);
     }
    
     // Enable the audio properties report
     bytetc::AudioPropertiesConfig config;
     config.interval = 1000;
     video_engine_->enableAudioPropertiesReport(config);
    
     // Joins the room. Note: An AppId and Token are required.
     auto userName = videocall::DataMgr::instance().user_name();
     auto userId = videocall::DataMgr::instance().user_id()
     QJsonObject extra_info;
     extra_info["user_id"] = QString::fromStdString(userId);
     extra_info["user_name"] = QString::fromStdString(userName);
      
     auto infoStr = QString(QJsonDocument(extra_info).toJson());
     auto infoStdString = std::string(infoStr.toUtf8());
    
     bytetc::UserInfo user = {uid.c_str(), infoStdString.c_str()};
    
     bytetc::RTCRoomConfig config;
     config.room_profile_type = bytetc::RoomProfileType::kRoomProfileTypeCommunication;
        // Enable automatic push (default enabled)
     config.is_auto_publish = true;
     // Enable automatic subscription to audio and video (default enabled)
     config.is_auto_subscribe_audio = true;
     config.is_auto_subscribe_video = true;
     rtcRoom_.joinRoom(token, user, config);
}
```



* Leave room


```cpp
void leaveRTCRoom(){
     VideoCallNotify::offAll();
     if (screen_shared_uid == self. user_id()) {
         // Stop screen and audio capture
         VideoCallRtcVideoWrap::stopScreenAudioCapture();
         VideoCallRtcVideoWrap::stopScreenCapture();
     }
     // leave the room
     rtcRoom_->leaveRoom();
     rtcRoom_->destroy();
}
```


<span id="reconnection-after-disconnection"></span>
### Reconnection after disconnection

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Usecase/350/videocall/11b7aa8b-4d05-4003-b124-886578ed4b57.png) </span>

<span id="code-sample"></span>
#### Code sample


* Short\-term disconnection

   No action is required. The RTC SDK will resend the lost messages during network disconnection.

   For example, a remote user might join the room while the local user's network is switching from Wi\-Fi to 5G. After the local user's network switch is complete, the SDK triggers the onUserJoined callback for that remote user.

* Long\-term disconnection, sample code


```cpp
void IRTCRoomEventHandler::onRoomStateChanged(const char* room_id, const char* uid,
                                        int state, const char* extra_info) {
     auto infoArray = QByteArray(extra_info. data(), static_cast<int>(extra_info. size()));
     auto infoJsonObj = QJsonDocument::fromJson(infoArray).object();
     auto joinType = infoJsonObj["join_type"].toInt();
     // joinType '0' indicates the first time a user joins the room, while '1' indicates a reconnection. state '0' means the join was successful.
     if (state == 0 && joinType == 1) {
     // Execute the application's reconnection logic to update its state.
         userReconnect([=](int code) {

                 });
       }

}
```


<span id="screen-sharing"></span>
### Screen sharing

For Screen sharing, see [PC](https://docs.byteplus.com/en/docs/12/docs-70144)

<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Feature |API |
|---|---|
|Create ByteRTCVideo instance |createRTCVideo |
|Set video publishing parameters |[SetVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideoencoderconfig) |
|Start local audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startaudiocapture) |
|Start local video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startvideocapture) |
|Set local video rendering |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideocanvas) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#joinroom) |
|Set video rendering view |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70095#setremotevideocanvas) |
|Leave room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70095#leaveroom) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#stopaudiocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#stopvideocapture) |
|Destroy the engine instance |[destroy](https://docs.byteplus.com/en/docs/12/docs-70095#destroy) |
|Publish/Stop the local media stream |publishStream |
|Set the audio playback device to speaker or earpiece |[setAudioPlaybackDevice](https://docs.byteplus.com/en/docs/12/docs-70095#setaudioplaybackdevice) |
|Enable audio properties report |[enableAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70095#enableaudiopropertiesreport) |
|Enable mirroring |[setLocalVideoMirrorType](https://docs.byteplus.com/en/docs/12/docs-70095#setlocalvideomirrortype) |
|Set audio profile |[setAudioProfile](https://docs.byteplus.com/en/docs/12/docs-70095#setaudioprofile) |


<span id="callback"></span>
### Callback


|Feature |Callback |
|---|---|
|Local user joins room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onroomstatechanged) |
|A remote user joins the room |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70096#onuserjoined) |
|A remote user publishes a media stream |[onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-70096#onuserjoined) |
|A remote user unpublishes a media stream |[onUserUnpublishStream](https://docs.byteplus.com/en/docs/12/docs-70096#onuserjoined) |
|Reports information about the local audio |[onLocalAudioPropertiesReport](https://docs.byteplus.com/en/docs/12/docs-70096#onuserjoined) |
|Reports events related to the connection status between the SDK and the signaling server |[onConnectionStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#onuserjoined) |
