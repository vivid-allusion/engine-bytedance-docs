---
title: "Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-106914"
---

This page provides information on how to build a video call App with Web RTC SDK.

<span id="prerequisites"></span>
## Prerequisites


* Follow instructions in [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) to obtain the AppID and Token.

* Your PC must meet the following requirements:

   * A browser. The latest version of Chrome is recommended.

   * Physical audio and video capture devices.

   * An Intel 2.2GHz Core processor (2nd generation) or equivalent

   * Access to the Internet

> See [Supported Browsers of WebRTC SDK](https://docs.byteplus.com/en/docs/12/docs-111854).


<span id="integrate-sdk"></span>
## Integrate SDK


1. Install the [RTC Web SDK](https://docs.byteplus.com/en/docs/12/docs-75707) package.

2. Move the SDK to your project folder.


```Plain
.
├── index.html
├── package.json
├── index.js
├── lib
    └── index.min.js
```



3. Import the RTC SDK into your code. The import method varies depending on how you installed the SDK.

   1. Installing via package manager: add `import BytePlusRTC from '@byteplus/rtc';` into your JS code.

   2. Downloading from our [website](https://docs.byteplus.com/en/docs/12/docs-75707).


<span id="implement-a-video-call"></span>
## Implement a Video Call

The following chart provides the API call sequence of a basic video call.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B/%E6%9E%84%E5%BB%BA%E5%9F%BA%E7%A1%80%E5%BA%94%E7%94%A8/webflow.png) </span>

Refer to the following procedure to implement a video call.

<span id="_1-create-an-engine-instance"></span>
### 1. Create an Engine Instance

Call [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine) to create a local Engine instance.

```typescript
import BytePlusRTC from '@byteplus/rtc';

// To create an RTC engine instance
const engine:IRTCEngine = BytePlusRTC.createEngine(appId);
```


<span id="_2-join-an-rtc-room"></span>
### 2. Join an RTC Room

Call [joinRoom](https://docs.byteplus.com/en/docs/12/docs-104478#joinroom) to join an RTC room. You can enable auto\-publishing and auto\-subscribing for media streams. And you can update publish and subscribe related settings after the user joins the room.

```typescript
import { RoomProfileType } from '@byteplus/rtc';

const config = {
  appId: 'your appId',
  roomId: 'your roomId',
  uid:'your uid',
  token: 'your token',
};
const join = async () => {
  try {
    await engine
      .joinRoom(
        config.token,
        config.roomId,
        {
          userId: config.uid,
        },
        {
          isAutoPublish: true, // To enable auto-publish
          isAutoSubscribeAudio: true, // To enable auto-subscribe to audio streams
          isAutoSubscribeVideo: true, // To enable auto-subscribe to video streams
          roomProfileType:RoomProfileType.communication // [Deprecated since V4.51] To change the room profile for your scenario.
        }
      )
  } catch(e) {
    console.error('Failed to join the room:', (e as {
      code: typeof BytePlusRTC.ErrorCode;
      message: string;
    }).message);
  }
};
```


<span id="_3-create-and-play-local-medias"></span>
### 3. Create and Play Local Media

Call [startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startaudiocapture) and/or [startVideoCapture](https://docs.byteplus.com/en/docs/12/docs-104478#startvideocapture) to start audio and video capture, and then set the local media player.

```typescript
import { StreamIndex,MediaType } from '@byteplus/rtc';

async function createLocalStream(){
    await engine.startAudioCapture();
    await engine.startVideoCapture();
    engine.setLocalVideoPlayer(StreamIndex.STREAM_INDEX_MAIN, {
      // The `renderDom` property accepts the ID of an empty div element, for example, 'local-player'.
      renderDom: 'local-player'
    });
    // You do not need to call this API if auto-publish is enabled.
    await engine.publishStream(MediaType.AUDIO_AND_VIDEO)
}
createLocalStream()
```


<span id="_4-receive-and-play-media-streams"></span>
### 4. Receive and Play Media Streams


1. Listen to [onUserPublishStream](https://docs.byteplus.com/en/docs/12/docs-104479#onuserpublishstream) event.

   * You will receive this event when you join a room where other users are already publishing streams.

   * You will also receive this event when another participant starts publishing streams after you have joined the room.

2. When this event is triggered, the media information is passed to the `handleUserPublishStream` handler.

3. Call [setRemoteVideoPlayer](https://docs.byteplus.com/en/docs/12/docs-104478#setremotevideoplayer) to set the media player for the remote streams.


```typescript
import { MediaType, StreamIndex } from '@byteplus/rtc';

engine.on(BytePlusRTC.events.onUserPublishStream, handleUserPublishStream); // Listen for the `onUserPublishStream` event to handle new remote streams.

async function handleUserPublishStream(e: {
    userId: string;
    mediaType: MediaType;
}){
    const player = document.querySelector('#video-container');
    
    await engine.setRemoteVideoPlayer(BytePlusRTC.StreamIndex.STREAM_INDEX_MAIN, {
      userId: e.userId,
      renderDom: player,
    });
}
```


<span id="_5-leave-the-room"></span>
### 5. Leave the Room

After a user leaves the room, their local client will no longer receive media streams or notifications from that room.

```typescript
await engine.leaveRoom();
```


<span id="related-information"></span>
## Related information


* API Documentation

   * [Overview](https://docs.byteplus.com/en/docs/12/docs-104477)

   * [API Reference](https://docs.byteplus.com/en/docs/12/docs-104478)

   * [Event](https://docs.byteplus.com/en/docs/12/docs-104479)

   * [Error Code](https://docs.byteplus.com/en/docs/12/docs-104480)

   * [Key Type](https://docs.byteplus.com/en/docs/12/docs-104481)
