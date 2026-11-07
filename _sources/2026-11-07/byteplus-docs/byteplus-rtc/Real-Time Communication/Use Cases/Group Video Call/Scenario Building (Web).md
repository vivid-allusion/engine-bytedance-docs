---
title: "Scenario Building (Web)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-184311"
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

<span id="joining-and-leaving-a-room"></span>
### Joining and Leaving a Room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/352usecase/joinroomweb.jpg) </span>

<span id="sample-code"></span>
#### Sample code

```typescript
const app_id = "";
const rtc_token="";

interface EngineOptions {
  appId: string;
  uid: string;
  rtsUid: string;
  roomId: string;
  rtmToken: string;
  serverUrl: string;
  serverSignature: string;
  bid: string;
}

// Instance of RTC
class RtcClient {

  createEngine = async (props: EngineOptions) => {
    this.config = props;
    this.engine = VERTC.createEngine(this.config.appId);
  };
  
  joinWithRTS = async () => {
    await this.engine.login(this.config.rtmToken, this.config.rtsUid);
    await this.engine.setServerParams(this.config.serverSignature, this.config.serverUrl);
  };
  
  joinRoom = (token: string | null, username: string): Promise<void> => {
    // Enable audio property reports with a 2000 ms interval
    this.engine.enableAudioPropertiesReport({ interval: 2000 });
    return this.engine.joinRoom(
      token,
      `${this.config.roomId !}`,
      {
        userId: this.config.uid !,
        extraInfo: JSON.stringify({
          user_name: username,
          user_id: this.config.uid,
        }),
      },
      {
        isAutoPublish: true,
        isAutoSubscribeAudio: true,
        isAutoSubscribeVideo: true,
        roomProfileType: RoomProfileType.meeting,
      }
    );
  };
  
  leaveRoom = () => {
    this.engine.leaveRoom();
    VERTC.destroyEngine(this.engine);
    this._videoCaptureDevice = undefined;
    this._audioCaptureDevice = undefined;
    this._audioPlaybackDevice = undefined;
    this._captureConfig = DefaultCaptureConfig;
    this._encoderConfig = DefaultEncoderConfig;
  };
  
  // ...

}

// Business logic layer
const handleStart = async (formValues: FormProps) => {
  
  // Create RTC engine object
  await RtcClient.createEngine({
    appId: app_id,
  });
  
  await RtcClient.joinWithRTS();

  const joinRes: any = await RtcClient.sendServerMessage('videocallJoinRoom');

  await RtcClient.joinRoom(rtc_token, formValues.username);
  
  const mediaDevices = await RtcClient.getDevices();


  // Start or stop video capture based on device permissions and enablement 
  if (devicePermissions.video && formValues.publishVideo) {
     await RtcClient.startVideoCapture();
     RtcClient.setMirrorType(MirrorType.MIRROR_TYPE_RENDER);
  }
  // Start audio capture if device permissions are granted 
  if (devicePermissions.audio) {
     await RtcClient.startAudioCapture();
  }
  
  // Unpublish the audio stream if disabled by the user 
  if (!formValues.publishAudio) {
     RtcClient.unpublishStream(MediaType.AUDIO);
  }
};
```



* Leave room


```typescript
  const handleStop = async () => {
    await RtcClient.stopAudioCapture();
    await RtcClient.stopVideoCapture();
    await RtcClient.stopScreenCapture();
    await RtcClient.leaveRoom();
  };
```


<span id="handling-disconnections"></span>
### Handling Disconnections

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/352usecase/connectionweb.jpg) </span>

<span id="code-sample"></span>
#### Code sample

```typescript
const handleConnectionStateChange = (state) => {
  if (state === ConnectionState.CONNECTION_STATE_DISCONNECTED) {
    message.error("Network connection lost");
  }
}

const handleUserPublishStream = (e: { userId: string; mediaType: MediaType }) => {
  // Update UI
};

const handleUserUnpublishStream = (e: {
  userId: string;
  mediaType: MediaType;
  reason: StreamRemoveReason;
}) => {
  // Update UI
};
```


<span id="screen-sharing"></span>
### Screen sharing

For Screen sharing, see [Web](https://docs.byteplus.com/en/docs/12/docs-80226)

<span id="api-and-callbacks"></span>
## API and Callbacks

<span id="api"></span>
### API


|Feature |API |
|---|---|
|Create ByteRTCVideo instance |[createEngine()](https://docs.byteplus.com/en/docs/12/docs-104478#createengine) |
|Set video publishing parameters |[SetVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-104478#setvideoencoderconfig) |
|Start local audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture) |
|Start local video capture |[startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture) |
|Set local video rendering |[setLocalVideoPlayer()](https://docs.byteplus.com/en/docs/12/docs-104478#setvideoplayer) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#joinroom) |
|Set video rendering view |[setRemoteVideoPlayer()](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer) |
|Leave room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-104478#leaveroom) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopaudiocapture) |
|Stop video capture |[stopVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#stopvideocapture) |
|Destroy the engine instance |[destroyEngine()](https://docs.byteplus.com/en/docs/12/docs-104478#destroyengine) |
|Publish a local media stream |[publishStream](https://docs.byteplus.com/en/docs/12/docs-104478#publishstream) |
|Unpublish a local media stream |[unpublishStream](https://docs.byteplus.com/en/docs/12/docs-104478#unpublishstream) |
|Enable audio property reports |[enableAudioPropertiesReport()](https://docs.byteplus.com/en/docs/12/docs-104478#enableaudiopropertiesreport) |
|Enable mirroring |[setLocalVideoMirrorType()](https://docs.byteplus.com/en/docs/12/docs-104478#setlocalvideomirrortype) |
|Set audio profile |[setAudioProfile()](https://docs.byteplus.com/en/docs/12/docs-104478#setaudioprofile) |


<span id="callback"></span>
### Callback


|Function point |Callback |
|---|---|
|Local user joins room |onRoomStateChanged |
|A remote user joins the room |[onUserJoined()](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) |
|A remote user publishes a media stream |[onUserPublishStream()](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) |
|A remote media stream is removed |[onUserUnpublishStream()](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) |
|Callback for local audio property reports |[onLocalAudioPropertiesReport()](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) |
|Callback for connection state changes |[onConnectionStateChanged()](https://docs.byteplus.com/en/docs/12/docs-104479#onuserjoined) |
