---
title: "Custom Video Encoding and Decoding"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-82921"
---

The RTC SDK uses built\-in codecs by default. If your application already has a video codec module, the SDK's re\-encoding process may introduce unwanted latency and video quality degradation. You can use custom encoding and decoding solutions to avoid this issue:


* **Custom encoding**: Push your own encoded video frames to the RTC SDK for transmission.

* **Custom decoding**: Pull the remote encoded video stream from the RTC SDK for custom decoding and rendering.


<span id="custom-video-encoding"></span>
## Custom video encoding


1. Before joining a room, specify a custom encoded video source by calling `setVideoSourceType`.

2. Call `setVideoEncoderConfig` to set the parameters of each video stream if you need to push multiple encoded video streams.

3. You need to implement the video encoding logic yourself.

4. After encoding, call `pushExternalEncodedVideoFrame` within the `onStart` callback to push the encoded video frame to the RTC SDK for transmission. Ensure that the `IEncodedVideoFrame` parameters match those used for the encoding.


<span id="custom-video-decoding"></span>
## Custom video decoding


1. Before joining a room, register the remote encoded video frame callback by calling `registerRemoteEncodedVideoFrameObserver`.

2. After joining the room and receiving a remote stream, call `setVideoDecoderConfig` to enable custom decoding for that stream.

3. After you subscribe to a remote stream, the SDK triggers the `OnRemoteEncodedVideoFrame` callback when it receives encoded video data. You need to implement the video decoding logic yourself.

4. When custom decoding fails, you need to call `requestRemoteVideoKeyFrame` to request keyframes from the remote user.


<span id="api-reference"></span>
## API reference


|Function/Platform |Android |iOS |Windows |macOS |
|---|---|---|---|---|
|Set custom encoded frame push event callback |[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70080#setexternalvideoencodereventhandler) |[setExternalVideoEncoderEventHandler:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setexternalvideoencodereventhandler) |[setExternalVideoEncoderEventHandler](https://docs.byteplus.com/en/docs/12/docs-70095#setexternalvideoencodereventhandler) |[setExternalVideoEncoderEventHandler:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setexternalvideoencodereventhandler) |
|Set video input |[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70080#setvideosourcetype) |[setVideoSourceType:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setvideosourcetype) |[setVideoSourceType:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideosourcetype) |[setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#setvideosourcetype) |
|Set multi\-stream parameters |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setvideoencoderconfig) |[setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setvideoencoderconfig) |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideoencoderconfig) |[setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideoencoderconfig) |
|Push encoded video frames |[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#pushexternalencodedvideoframe) |[pushExternalEncodedVideoFrame:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-pushexternalencodedvideoframe-withencodedvideoframe) |[pushExternalEncodedVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#pushexternalencodedvideoframe) |[pushExternalEncodedVideoFrame:withEncodedVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-pushexternalencodedvideoframe-withencodedvideoframe) |
|Callback for changes in the video sender's transmission state |[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/docs-70081#IExternalVideoEncoderEventHandler-onactivevideolayer) |[onActiveVideoLayer:info:withVideoIndex:withActive:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCExternalVideoEncoderEventHandler-onactivevideolayer-info-withvideoindex-withactive) |[onActiveVideoLayer](https://docs.byteplus.com/en/docs/12/docs-70096#IExternalVideoEncoderEventHandler-onactivevideolayer) |[onActiveVideoLayer:info:withVideoIndex:withActive:](https://docs.byteplus.com/en/docs/12/docs-70093#ByteRTCExternalVideoEncoderEventHandler-onactivevideolayer-info-withvideoindex-withactive) |
|Register remote encoded video data callback |[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70080#registerremoteencodedvideoframeobserver) |[registerRemoteEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-registerremoteencodedvideoframeobserver) |[registerRemoteEncodedVideoFrameObserver](https://docs.byteplus.com/en/docs/12/docs-70095#registerremoteencodedvideoframeobserver) |[registerRemoteEncodedVideoFrameObserver:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-registerremoteencodedvideoframeobserver) |
|Set remote video decoding method |[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70080#setvideodecoderconfig) |[setVideoDecoderConfig:withVideoDecoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setvideodecoderconfig-withvideodecoderconfig) |[setVideoDecoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideodecoderconfig) |[setVideoDecoderConfig:withVideoDecoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideodecoderconfig-withvideodecoderconfig) |
|Request remote key frame |[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70080#requestremotevideokeyframe) |[requestRemoteVideoKeyFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-requestremotevideokeyframe) |[requestRemoteVideoKeyFrame](https://docs.byteplus.com/en/docs/12/docs-70095#requestremotevideokeyframe) |[requestRemoteVideoKeyFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-requestremotevideokeyframe) |


<span id="see-also"></span>
## See also

[Switching between Default and Custom Video Capturing and Encoding Methods](https://docs.byteplus.com/en/docs/12/docs-100448)
