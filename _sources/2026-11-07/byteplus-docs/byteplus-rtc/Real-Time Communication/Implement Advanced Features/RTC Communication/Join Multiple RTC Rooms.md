---
title: "Join Multiple RTC Rooms"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-196844"
---

Users can join multiple rooms, respectively subscribe and receive audio and video streams of these rooms, and post audios and videos in one of them.

<span id="use-cases"></span>
## Use cases


* Breakout classes: Teachers give lessons in a main classroom that all students attend. Meanwhile, students are allowed to communicate and raise questions in group rooms and obtain answers from teaching assistants.

* Online games: Players can use voice chat with teammates in their team rooms while listening to broadcast audio messages in the world room.

* Online meetings: During cloud meetings, hosts are allowed to initiate group discussions. Attendees can have audio and video interactions with each other without leaving the previous meetings, and discussion groups are independent.


<span id="prerequisites"></span>
## Prerequisites

You have already integrated RTC SDK v3.43 or later versions and are able to implement basic audio and video calls.

Please refer to API and Callback for details about multi\-room\-supporting SDKs.

<span id="to-allow-users-to-join-multiple-rooms"></span>
## To allow users to join multiple rooms

During the process of integrating the RTC SDK and completing the business logic code, we believe that you have already recognized that there are apparent functional differences between the audio and video engine and the room class, the two commonly\-used main call classes:


* By using the method of the audio and video engine, you can enable audio and video capture and configure related settings (e.g., switching cameras);

* By using the method of the room class, you can publish/subscribe to streams in rooms and configure related settings (e.g., configuring user visibility in a room).


To allow a single user to enter multiple rooms, you can use an audio and video engine instance, create multiple room instances and set different room IDs for these instances. The same user who joins multiple rooms is allowed to subscribe audio and video streams posted in the rooms.

You can repeat the example step to allow users to join more rooms.

> The API call sequence diagram below uses the API names in the Android SDK as examples. API or callback names may vary across SDKs for different platforms. The names in the API and Callback reference are definitive.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/196844_api_en.png) </span>

<span id="_1-create-an-engine-class"></span>
### 1. Create an engine class

Create and initialize an audio and video engine.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `
    EngineConfig config = new EngineConfig();
    config.appID = appId;
    config.context = applicationContext;
    rtcEngine = RTCEngine.createRTCEngine(config, engineEventHandler);`, 
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `
    let engineCfg = ByteRTCEngineConfig.init()
    engineCfg.appID = appId
    engineCfg.parameters = [:]
    self.rtcEngine = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)`,  
  },
  {
    "lang": "cpp",
    "text": `
    bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    engine = bytertc::IRTCEngine::createRTCEngine(conf, handler.get());`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_2-enable-audio-and-video-capture"></span>
### 2. Enable audio and video capture

After creating the audio and video engine, you can enable audio and video capture and configure rendering views.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `
    rtcEngine.startAudioCapture();
    rtcEngine.startVideoCapture();

    private void setLocalRenderView() {
        VideoCanvas videoCanvas = new VideoCanvas();
        videoCanvas.renderView = localView;
        videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
        rtcEngine.setLocalVideoCanvas(videoCanvas);
    }`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `
    self.rtcEngine?.startVideoCapture()
    self.rtcEngine?.startAudioCapture()

    let canvas = ByteRTCVideoCanvas.init()
    canvas.view = self.localView.videoView
    canvas.renderMode = .hidden
    self.rtcEngine?.setLocalVideoCanvas(withCanvas: canvas);`, 
      },
  {
    "lang": "cpp",
    "text": `
   engine->startAudioCapture();
   engine->startVideoCapture();
   
   bytertc::VideoCanvas cas;
   cas.view = view;
   engine->setLocalVideoCanvas(cas);`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_3-create-a-room-instance"></span>
### 3. Create a room instance

You can join a room and publish and subscribe to audio and video streams once you have created the room instance. We recommend configuring the room callback interface to monitor status callbacks for the room and its streams.

Continue calling createRTCRoom and import different room IDs to create room instances and join the rooms.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `
    rtcRoom1 = rtcEngine.createRTCRoom(roomID);
    rtcRoom1.setRTCRoomEventHandler(firstRoomEventHandler);
    rtcRoom2 = rtcEngine.createRTCRoom(roomID);
    rtcRoom2.setRTCRoomEventHandler(secondRoomEventHandler);`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `
    self.rtcRoom1 = self.rtcEngine?.createRTCRoom(roomId1)
    self.rtcRoom1?.delegate = self
    self.rtcRoom2 = self.rtcEngine?.createRTCRoom(roomId2)
    self.rtcRoom2?.delegate = self`, 
  },
  {
    "lang": "cpp",
    "text": `
bytertc::IRTCRoom *room1 = engine->createRTCRoom("roomid1");
room1->setRTCRoomEventHandler(room_handler); 

bytertc::IRTCRoom *room2 = engine->createRTCRoom("roomid2");
room2->setRTCRoomEventHandler(room_handler);`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_4-join-an-rtc-room"></span>
### 4. Join an RTC room

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/196844_joinroom_en.png) </span>


1. When a user joins a room, auto subscription of the audio and video streams of the room will be enabled by default.

   ```mixin-react
   const list = [
   {
      "lang": "java",
      "text": `
      UserInfo userInfo = new UserInfo(localUid, "");
   
      RTCRoomConfig room1Config = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_LIVE, true, true, true, true);
   
      rtcRoom1.joinRoom(room1token, userInfo, true, room1Config);
   
   
      RTCRoomConfig room2Config = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_LIVE, false, false, true, true);
   
      rtcRoom2.joinRoom(room2token, userInfo, true, room2Config);`,
      "selected": true,
   },
   {
      "lang": "swift",
      "text": `
      let token1 = generatorToken(roomId: roomId1, userId: userId1)
      
      let userInfo = ByteRTCUserInfo.init()
      userInfo.userId = userId
   
      let room1Cfg = ByteRTCRoomConfig.init()
      room1Cfg.isPublishAudio = true
      room1Cfg.isPublishVideo = true
      room1Cfg.isAutoSubscribeAudio = true
      room1Cfg.isAutoSubscribeVideo = true
      self.rtcRoom1?.joinRoom(token, userInfo: userInfo, userVisibility: true, roomConfig: room1Cfg)
   
   
      let token2 = generatorToken(roomId: roomId2, userId: userId2)
      let room2Cfg = ByteRTCRoomConfig.init()
      room2Cfg.isPublishAudio = false
      room2Cfg.isPublishVideo = false
      room2Cfg.isAutoSubscribeAudio = true
      room2Cfg.isAutoSubscribeVideo = true
      self.rtcRoom2?.joinRoom(token2, userInfo: userInfo,  userVisibility: true, roomConfig: room2Cfg)`, 
   },
   {
      "lang": "cpp",
      "text": `
         bytertc::UserInfo user;
         bytertc::RTCRoomConfig config;
         config.is_publish_audio = true;
         config.is_publish_video = true; 
         config.is_auto_subscribe_audio = true;
         config.is_auto_subscribe_video = true;
         config.room_profile_type = bytertc::kRoomProfileTypeCommunication;
         user.uid = uid1.c_str();
         int ret = m_room1->joinRoom(token.c_str(), user, true, config);
   
         bytertc::UserInfo user;
         bytertc::RTCRoomConfig config;
         config.is_publish_audio = false; 
         config.is_publish_video = false;
         config.is_auto_subscribe_audio = true;
         config.is_auto_subscribe_video = true;
         config.room_profile_type = bytertc::kRoomProfileTypeCommunication;
         user.uid = uid2.c_str();
         int ret = m_room2->joinRoom(token.c_str(), user, true, config);`, 
   },
   ]
   return (<PreCodeTabs list={list} />);
   ```
   

2. Monitor the room entry status and handle entry failures.

   ```mixin-react
   const list = [
     {
       "lang": "java",
       "text": `public void onRoomStateChanged(String roomId, String uid, int state, String extraInfo) {
       if (state == 0) { 
       } else if (state == -1000) { 
       } else {
       }
   }`,
       "selected": true,
     },
     {
       "lang": "swift",
       "text": `func rtcRoom(_ rtcRoom: ByteRTCRoom, onRoomStateChanged roomId: String, withUid uid: String, state: Int, extraInfo: String) {
       if (state == 0) { 
       } else if (state == -1000) { 
       } else {
       }
   }`, 
     },
     {
       "lang": "cpp",
       "text": `void RoomHandler::onRoomStateChanged(const char* room_id, const char* uid, int state, const char* extra_info) {
       if (state == 0) {
       } else if (state == -1000) {
       } else {
       }
   }`, 
     },
   ]
   return (<PreCodeTabs list={list} />);
   ```
   

3. Set rendering views when subscription\-side receives post/cancel callback of audio or video streams by another user.

   After receiving the onUserPublishVideoStream or onFirstRemoteVideoFrameDecoded callback from a remote user, you need to call setRemoteVideoCanvas to set up the remote view to display remote video during the call. It is recommended to set up video rendering in the onFirstRemoteVideoFrameDecoded callback to ensure that video rendering occurs after video decoding is complete, preventing stuttering.

   ```mixin-react
   const list = [
     {
       "lang": "java",
       "text": `
       @Override
       public void onFirstRemoteVideoFrameDecoded(String streamId, StreamInfo streamInfo, VideoFrameInfo frameInfo) {
           runOnUiThread(() -> {
               VideoCanvas videoCanvas = new VideoCanvas();
               videoCanvas.renderView = firstRoomRemoteView;
               videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
               rtcEngine.setRemoteVideoCanvas(streamId, videoCanvas);
           });
       }
   
       @Override
       public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
           if (!isPublish) {
               runOnUiThread(() -> {
                  
                   rtcEngine.setRemoteVideoCanvas(streamId, null);
               });
           }
       }`,
       "selected": true,
     },
     {
       "lang": "swift",
       "text": `
       func rtcEngine(_ rtcEngine: ByteRTCEngine, onFirstRemoteVideoFrameDecoded streamId: String, info: ByteRTCStreamInfo, withFrameInfo: ByteRTCVideoFrameInfo) { 
   
           DispatchQueue.main.async {
               
               let canvas = ByteRTCVideoCanvas.init()
               canvas.view = view.videoView
               canvas.renderMode = .hidden
               self.rtcEngine?.setRemoteVideoCanvas(streamId, withCanvas: canvas);
           }
       }
   
       func rtcRoom(_ rtcRoom: ByteRTCRoom, onUserPublishStreamVideo streamId: String, info: ByteRTCStreamInfo, isPublish: Bool) {
           if !isPublish  {
               DispatchQueue.main.async {
                   let canvas = ByteRTCVideoCanvas.init()
                   canvas.view = nil 
                   canvas.renderMode = .hidden
                   self.rtcEngine?.setRemoteVideoCanvas(streamId, withCanvas: canvas)
               }
           }
       }`, 
     },
     {
       "lang": "cpp",
       "text": `
   void EngineHandler::onFirstRemoteVideoFrameDecoded(std::string streamId, bytertc::StreamInfo info, bytertc::VideoFrameInfo frameInfo) {
       bytertc::VideoCanvas canvas;
       canvas.view = (void*)ui->widget->winId();
       engine->setRemoteVideoCanvas(streamId.c_str(), canvas);
   }
   
   void RoomHandler::onUserPublishStreamVideo(std::string streamId, bytertc::StreamInfo info, bool publish)
       if (!publish) { 
         bytertc::VideoCanvas cas;
         cas.view = nullptr;
         engine->setRemoteVideoCanvas(streamId.c_str(), cas);
       }`, 
   }
   ]
   return (<PreCodeTabs list={list} />);
   ```
   


<span id="_5-leave-an-rtc-room"></span>
#### 5. Leave an RTC room

When users end calls, they leave the rooms, and you should destroy the local room instances.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `rtcRoom.leaveRoom();
    rtcRoom.destroy();
    rtcRoom = null;`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `self?.rtcRoom?.leave()
    self?.rtcRoom?.destroy()
    self?.rtcRoom = nil`, 
  },
  {
    "lang": "cpp",
    "text": `room->leaveRoom();
room->destroy();`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_6-destroy-the-engine-class"></span>
#### 6. Destroy the engine class

After all room instances are destroyed, the audio and video engine can also be destroyed.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `RTCEngine.destroyRTCEngine();`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `
    ByteRTCEngine.destroyRTCEngine()
    self.rtcEngine = nil`, 
  },
  {
    "lang": "cpp",
    "text": `bytertc::IRTCEngine::destroyRTCEngine();`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="sample-project"></span>
## Sample project


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/room/MultiRoomActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/RoomManager/MutiRoom/MutiRoomViewController.swift)


<span id="faq"></span>
## FAQ

<span id="q1-how-can-a-user-post-audio-and-video-streams-in-multiple-rooms-at-the-same-time"></span>
### Q1: How can a user post audio and video streams in multiple rooms at the same time?

**A**: In case of a single audio and video engine instance, users can only publish audio and video streams in one room even though they've joined multiple rooms. To publish audio and video streams in multiple rooms simultaneously, refer to [Forward Across Rooms](https://docs.byteplus.com/en/docs/12/docs-104398).

<span id="q2-how-can-i-handle-token-related-errors"></span>
### Q2: How can I handle token\-related errors?

**A**: You must make sure that the token of each room is generated with the corresponding roomId. For more information about token, please refer to [FAQ About Token Usage](https://docs.byteplus.com/en/docs/12/docs-1157360).
