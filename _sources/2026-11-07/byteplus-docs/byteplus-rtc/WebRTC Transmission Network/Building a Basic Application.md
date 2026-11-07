---
title: "Building a Basic Application"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132450"
---

This article uses the Web platform as an example to introduce how to implement audio and video publishing and subscribing streams using WTN in a project.

<span id="demo-project"></span>
## Demo Project

Refer to the [Demo Project](https://github.com/byteplus-sdk/BytePlusWTN/tree/main/Demo/Web).

<span id="prerequisites"></span>
## Prerequisites


* Create a WTN application in the [Console](https://console.byteplus.com/rtc/listRTC) and obtain the AppID and AppKey.

* A computer that meets the following conditions:

   * Equipped with an Intel 2nd generation Core processor or better;

   * Equipped with physical audio and video capture devices, such as a built\-in camera and microphone;

   * The latest version of the Chrome browser, set as the default browser.

   * An internet connection.


<span id="implementing-the-app"></span>
## Implementing the App

The flowchart for a simple audio and video call is as follows:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_58117c2f16f65471cdf52b6994d0e278.png) </span>

To implement a simple audio\-video call, follow these steps:

<span id="step-1-get-the-publishing-and-subscribing-addresses"></span>
### Step 1: Obtain the Publishing and Subscribing Addresses


1. Call the API to create the publishing resource, and get the publishing address `location` from the response. See [Create Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132482).

2. Call the API to create the subscribing resource, and get the subscribing address from the `location` field in the response. See [Create Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132484).


<span id="step-2-publishing-side-creating-and-initializing-the-client-object"></span>
### Step 2: Publisher: Create and Initialize the Client Object

Invoke the browser's native getUserMedia to create a local audio\-video stream and obtain the audio and video tracks.

```typescript
// See https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints.
const stream:MediaStream=  await navigator.mediaDevices.getUserMedia(options as MediaStreamConstraints)
const videoTrack = mediaStream.getVideoTracks()[0];
const audioTrack = mediaStream.getAudioTracks()[0];
```


<span id="step-3-publishing-side-creating-peerconnection-and-sdp-offer"></span>
### Step 3: Publishing Side: Creating `PeerConnection` and SDP offer

```typescript
const peer = new RTCPeerConnection({})

const ms = new MediaStream()
// Add video and audio tracks
if (audioTrack) ms.addTrack(audioTrack);
if (videoTrack) ms.addTrack(videoTrack);

peer.addTransceiver(audioTrack || "audio",{
    streams:[ms],
    direction:"sendonly"
})

peer.addTransceiver(videoTrack || "video",{
    streams:[ms],
    direction:"sendonly"
})

// Create P2P offer
const offer = await peer.createOffer();

// Set local offer
// See https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/setLocalDescription
peer.setLocalDescription(offer);
```


<span id="step-4-subscription-side-creating-peerconnection-and-sdp-offer"></span>
### Step 4: Subscription Side: Creating `PeerConnection` and SDP offer

```typescript
const peer = new RTCPeerConnection({})

peer.addTransceiver("audio",{
    direction:"recvonly"
})

peer.addTransceiver("video",{
    direction:"recvonly"
})

// Create P2P offer
const offer = await peer.createOffer();

// Set local offer
// See https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/setLocalDescription
peer.setLocalDescription(offer);
```


<span id="step-5-publishing-side-and-subscription-side-exchange-sdp-offer-via-wtn"></span>
### Step 5: Publishing Side and Subscription Side: Exchange SDP Offer via WTN

```typescript
// Exchange SDP offer via WTN
const res = await fetch(YOUR_PUSH_URL||YOUR_PULL_URL, { method: 'POST', body: offer.sdp, headers });

if (!res.ok) {
  return res;
}

// Get the URL for disconnecting in the headers
const resourceURL = new URL(res.headers.get('location') || '', url);

const sdp = await res.text();
const answer = new RTCSessionDescription({ type: 'answer', sdp });
await peerConn.setRemoteDescription(answer);
```


<span id="step-6-subscription-side-subscribing-to-and-rendering-the-media-stream"></span>
### Step 6: Subscription Side: Subscribing to and Rendering the media stream

After the publisher and subscriber exchange SDP, the PeerConnection has successfully established a connection. At this point, the subscriber's PeerConnection can receive the publisher's audio and video stream in the `ontrack` callback.

```typescript
peer.ontrack = function (event) {
  if (event && event.streams) {
    if (event.track.kind === 'video') {
      const player =  document.querySelector("#video");
      player.onloadeddata = () =>{
        player.play();
      }
      // Set srcObject to the received stream 
      player.current.srcObject = event.streams[0];
    }
  }
};
```


<span id="step-7-publishing-side-and-subscription-side-terminate-peerconnection"></span>
### Step 7: Publishing Side and Subscription Side: Terminate PeerConnection

Once the PeerConnection is terminated, the media stream is no longer published or subscribed to.

```typescript
peer.close();
peer = undefined;

fetch(resourceURL.href, { method: 'DELETE' });
```


At this point, we have implemented a basic audio\-video call using WTN.
