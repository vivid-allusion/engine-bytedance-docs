---
title: "Forward Media Stream across Rooms"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-104398"
---

With forwarding across rooms, media streams of visible users can be simultaneously forwarded to multiple RTC rooms. There is no limit on the number of rooms that can be forwarded to on the RTC side.

The use of forwarding media streaming function does not incur additional fees. It follows the same billing principles as other audio and video calls. Please refer to the [Billing Rules](https://docs.byteplus.com/en/docs/12/docs-69871) for details.

<span id="use-cases"></span>
## Use cases

This feature is useful in scenarios where viewers in their original room need to receive media streams from hosts in other rooms.


* Host PK through microphone connection: After accepting the microphone connection invitation, host A's audio and video stream can be forwarded to the host B's room, and at the same time, host B's audio and video stream can also be forwarded to room A. Both viewers and hosts do not need to leave their original room to watch the audio and video content from the hosts in PK.

* Parent and child live streaming rooms: The audio and video from the parent room, often produced centrally, can be forwarded to multiple child live streaming rooms simultaneously. The hosts of the child live streaming rooms can directly live\-stream the content of the parent live streaming room while interacting with users. They can also incorporate their own personalized content into the live streaming.


<span id="glossary"></span>
## Glossary

**Push stream**: The media stream forwarded across rooms.

**Target room**: The room to which the stream is forwarded.

<span id="prerequisite"></span>
## Prerequisite

You have already integrated RTC SDK and are able to implement basic audio and video calls.

For details about which SDKs support this feature, see API and Callback.

<span id="to-forward-media-streams-across-rooms"></span>
## To forward media streams across rooms

> The API sequence chart below uses the API names in the Android SDK as examples. API and callback names may differ on other platforms. For the definitive names, refer to the API and Callback reference.


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/104398_api_en.png) </span>

<span id="_1-join-a-room"></span>
#### 1. Join a room

Create an engine instance and join a room. Local users are visible to others by default.

```mixin-react
const list = [
 {
    "lang": "typescript",
    "text": `import VERTC, { ForwardStreamState } from '@byteplus/rtc';
const engine = VERTC.createEngine('appid');
await engine.joinRoom('roomId_token', 'roomId', { userId: 'userid' });`,
    "selected": true,
  },
  {
    "lang": "java",
    "text": `// Create engine
    EngineConfig config = new EngineConfig();
    config.appID = appId;
    config.context = applicationContext;
    rtcEngine = RTCEngine.createRTCEngine(config, engineEventHandler);`, 


    // Join room
    private void joinRoom(String roomId) {
        rtcRoom = rtcEngine.createRTCRoom(roomId);
        rtcRoom.setRTCRoomEventHandler(roomEventHandler);
        String token = requestRoomToken(roomId);
        // User info
        UserInfo userInfo = new UserInfo(localUid, "");
        // Set room configuration
        boolean isAutoPublishAudio = true;
        boolean isAutoPublishVideo = true;
        boolean isAutoSubscribeAudio = true;
        boolean isAutoSubscribeVideo = true;
        RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_LIVE, isAutoPublishAudio, isAutoPublishVideo, isAutoSubscribeAudio, isAutoSubscribeVideo);
        rtcRoom.joinRoom(token, userInfo, true, roomConfig);
    }`, 
  },
  {
    "lang": "swift",
    "text": `//Create engine
    let engineCfg = ByteRTCEngineConfig.init()
    engineCfg.appId = appId
    //Private parameters, can be left empty
    engineCfg.advancedConfig = ""
    //delegate: Interface instance for receiving ByteRTCEngine callbacks
    self.rtcEngine = ByteRTCEngine.createRTCEngine(engineCfg, delegate: self)
    
    //Create room
    self.rtcRoom = self.rtcEngine?.createRTCRoom(roomId)
    self.rtcRoom?.delegate = self
    
    //Join room
    let userInfo = ByteRTCUserInfo.init()
    userInfo.userId = userId
    
    let roomCfg = ByteRTCRoomConfig.init()
    roomCfg.isPublishAudio = true
    roomCfg.isPublishVideo = true
    roomCfg.isAutoSubscribeAudio = true
    roomCfg.isAutoSubscribeVideo = true
    self.rtcRoom1?.joinRoom(token, userInfo: userInfo, userVisibility: true, roomConfig: roomCfg)`, 
  },
  {
    "lang": "cpp",
    "text": `//Create engine
    bytertc::EngineConfig conf;
    conf.app_id = g_appid.c_str();
    engine = bytertc::IRTCEngine::createRTCEngine(conf, handler.get());
engine->startAudioCapture();
engine->startVideoCapture();

//Create room
bytertc::IRTCRoom *room = engine->createRTCRoom(roomid);
room->setRTCRoomEventHandler(room_handler);

bytertc::UserInfo info;
bytertc::RTCRoomConfig config;
info.uid = str_uid.c_str();
config.is_publish_audio = true;
config.is_publish_video = true;
config.is_auto_subscribe_audio = true;
config.is_auto_subscribe_video = true;
int ret = room->joinRoom(token, userinfo, true, config);`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_2-enable-forwarding-across-rooms"></span>
### 2. Enable forwarding across rooms


* The token passed into `startForwardStreamToRooms` corresponds to the token of the target room, not the token of the room that the user is currently in.

* `startForwardStreamToRooms` can be called only once before calling `stopForwardStreamToRooms`.

* If the media stream is forwarded to a room with [audio routing](https://docs.byteplus.com/en/docs/12/docs-113547) enabled, the media stream may not be played.


```mixin-react
const list = [
{
    "lang": "typescript",
    "text": `// Create a list of target rooms
const targetRoomList: string[] = [];

// Start forwarding streams across rooms.
const startResult = await engine.startForwardStreamToRooms([
  { roomId: 'targetRoomIdA', token: 'targetRoomIdA_token' },
  // You can specify multiple target rooms.
  { roomId: 'targetRoomIdB', token: 'targetRoomIdB_token' }
]);

// Handle the result of the call.
startResult.forEach(item => {
  if (item.state === ForwardStreamState.FORWARD_STREAM_STATE_SUCCESS) {
    // Save the ID of the room where the stream has been forwarded.
    targetRoomList.push(item.roomId);
  } else {
    // Handle the error.
    console.error(item.error);
  }
});`,
    "selected": true,
  },
  {
    "lang": "java",
    "text": `
private void startForwardStreamToRooms(String roomId) {
    ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(roomId, requestRoomToken(roomId));
    if (rtcRoom != null) {
        rtcRoom.startForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
    }
}`, 
  },
  {
    "lang": "swift",
    "text": `
let config = ForwardStreamConfiguration.init()
config.roomId = roomId

let token = generatorToken(roomId: roomId, userId: userId)
config.token = token

self.rtcRoom?.startForwardStreamToRooms([config])`, 
  },
  {
    "lang": "cpp",
    "text": `// List stores each roomid and corresponding token
for (int i=0; i<list.size(); i++) {
        bytertc::ForwardStreamInfo one;
        one.room_id = roomids[i].c_str();
        one.token = tokens[i].c_str();
        forward_stream_dests.push_back(one);
}
// Start cross-room media stream forwarding
bytertc::ForwardStreamConfiguration configuration;
configuration.dest_count = forward_stream_dests.size();
configuration.forward_stream_dests = forward_stream_dests.data();
int ret = m_room1->startForwardStreamToRooms(configuration);`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_3-update-forwarding-configuration"></span>
### 3. Update forwarding configuration

Update the request to forward media streams across rooms.

If no parameter or a null value is passed when calling `updateForwardStreamToRooms`, all streams being forwarded to target rooms will be stopped. In this case, you must still call `stopForwardStreamToRooms` before you can call `startForwardStreamToRooms` again.

```mixin-react
const list = [
{
    "lang": "typescript",
    "text": `// Update the list of the target rooms.
const updateResult = await engine.updateForwardStreamToRooms([
// targetRoomIdA is not in the update list, so the stream will stop forwarding to this room.
  // Token for targetRoomIdB will be updated.
// Note that the token cannot be validated until stream forwarding resumes.
  { roomId: 'targetRoomIdB', token: 'targetRoomIdB_new_token' },
  // targetRoomIdC is not in the previous list, and the stream will start forwarding to this room immediately.
  { roomId: 'targetRoomIdC', token: 'targetRoomIdC_token' }
]);

// Handle the result of the call.
// The result will include the room where the stream had been stopped forwarding due to this update.
updateResult.forEach(item => {
  if (item.state === ForwardStreamState.FORWARD_STREAM_STATE_SUCCESS) {
    if (!['targetRoomIdB', 'targetRoomIdC'].includes(item.roomId)) {
      // Remove the room from the target room list.
      targetRoomList.splice(targetRoomList.indexOf(item.roomId), 1);
    } else if (!targetRoomList.includes(item.roomId)) {
      // Add the new target room to the target room list.
      targetRoomList.push(item.roomId);
    }
  } else {
// Handle the error.
    console.error(item.error);
  }
});`,
    "selected": true,
  },
  {
    "lang": "java",
    "text": `ForwardStreamInfo forwardStreamInfo = new ForwardStreamInfo(roomId, requestRoomToken(roomId));
if (rtcRoom != null) {
    rtcRoom.updateForwardStreamToRooms(Collections.singletonList(forwardStreamInfo));
}`, 
  },
  {
    "lang": "swift",
    "text": `let config = ForwardStreamConfiguration.init()
config.roomId = roomId

let token = generatorToken(roomId: roomId, userId: userId)
config.token = token

self.rtcRoom?.updateForwardStreamToRooms([config])`, 
  },
  {
    "lang": "cpp",
    "text": `// Create list to store each room roomid and corresponding token
for (int i=0; i<list.size(); i++) {
        bytertc::ForwardStreamInfo one;
        one.room_id = roomids[i].c_str();
        one.token = tokens[i].c_str();
        forward_stream_dests.push_back(one);
}
bytertc::ForwardStreamConfiguration configuration;
configuration.dest_count = forward_stream_dests.size();
configuration.forward_stream_dests = forward_stream_dests.data();
int ret = m_room1->updateForwardStreamToRooms(configuration);`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_4-pause-and-resume-forwarding"></span>
### 4. Pause and resume forwarding

Pause and resume forwarding media streams to all target rooms.

`pauseForwardStreamToAllRooms` can be called only once before calling `resumeForwardStreamToAllRooms` to resume media stream forwarding.

```mixin-react
const list = [
   {
    "lang": "typescript",
    "text": `// Pause
await engine.pauseForwardStreamToAllRooms();

// Resume
const result = await engine.resumeForwardStreamToAllRooms();

// Handle the result of the call.
result.forEach(item => {
  if (item.state !== ForwardStreamState.FORWARD_STREAM_STATE_SUCCESS) {
    // Handle the error.
    console.error(item.error);
  }
});`,
    "selected": true,
  },
  {
    "lang": "java",
    "text": `
// Pause
rtcRoom.pauseForwardStreamToAllRooms();

// Resume
rtcRoom.resumeForwardStreamToAllRooms();`, 
  },
  {
    "lang": "swift",
    "text": `
// Pause
self.rtcRoom?.pauseForwardStreamToAllRooms()

// Resume
self.rtcRoom?.resumeForwardStreamToAllRooms()`, 
  },
  {
    "lang": "cpp",
    "text": `// Pause
int ret = room->pauseForwardStreamToAllRooms();
// Resume
int ret = room->resumeForwardStreamToAllRooms();`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_5-stop-forwarding"></span>
### 5. Stop forwarding

Stop forwarding media streams to all target rooms.

```mixin-react
const list = [
  {
    "lang": "typescript",
    "text": `await engine.stopForwardStreamToRooms();`,
    "selected": true,
  },
  {
    "lang": "java",
    "text": `
rtcRoom.stopForwardStreamToRooms();`, 
  },
  {
    "lang": "swift",
    "text": `
self.rtcRoom?.stopForwardStreamToRooms()`, 
  },
  {
    "lang": "cpp",
    "text": `int ret = room->stopForwardStreamToRooms();`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="_6-callbacks"></span>
### 6. Callbacks

Monitor `onForwardStreamStateChanged` to get the status of media stream forwarding across rooms.


* When a stream is forwarded to a target room, it behaves like a user joining that room. This triggers user\-related callbacks such as `onUserJoin`, `onUserLeave`, `onUserPublishStream`, and `onUserUnpublishStream`.

* If the user switches to invisible during the media stream forwarding, the media stream forwarding will stop.


```mixin-react
const list = [
  {
    "lang": "typescript",
    "text": `function onForwardError(info) {
  console.error(info);
}

engine.on(EngineEventsTypes.onForwardStreamError, onForwardError);`,
    "selected": true,
  },
  {
    "lang": "java",
    "text": `
@Override
public void onForwardStreamEvent(ForwardStreamEventInfo[] eventInfos) {

}

@Override
public void onForwardStreamStateChanged(ForwardStreamStateInfo[] stateInfos) {

}`, 
  },
  {
    "lang": "swift",
    "text": `
func rtcRoom(_ rtcRoom: ByteRTCRoom, onForwardStreamStateChanged infos: [ForwardStreamStateInfo]) {

}

func rtcRoom(_ rtcRoom: ByteRTCRoom, onForwardStreamEvent infos: [ForwardStreamEventInfo]) {
}`, 
  },
  {
    "lang": "cpp",
    "text": `void ByteRTCRoomHandler::onForwardStreamStateChanged(bytertc::ForwardStreamStateInfo* infos, int info_count) {
// Callback for cross-room media stream forwarding status and errors.
}

void ByteRTCRoomHandler::onForwardStreamEvent(bytertc::ForwardStreamEventInfo* infos, int info_count)
{
//Cross-room media stream forwarding event callback
}`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="sample-project"></span>
## Sample project


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/room/CrossRoomPKActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/AudioVideoTransmission/CrossRoomPK/CrossRoomPKViewController.swift)


<span id="change-log"></span>
## Change log


1. This function is available in the Native SDK starting from v3.34.

2. From Web SDK v4.54, this function is available on the Web side.
