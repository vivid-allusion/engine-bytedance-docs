---
title: "Custom Video Capturing (Native)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70138"
---

You can use the built\-in modules for video capturing and rendering when using the RTC service. However, you might want to use your own module to do so in some scenarios such as the followings:


* Your app has its own video capturing and rendering modules.

* You want to use the video source captured by other devices, such as screen recording videos.

* You want to perform some pre\-transmission processing on the captured audio and video, such as image enhancement.

* the video capture equipment is in use


This guide provides step\-by\-step instructions on how to push external video frames to the RTC SDK, which then handles the encoding and transmission for you.

<span id="prerequisite"></span>
## Prerequisite

You have a functioning video communication app that is integrated with RTC SDK v3.45 or later.

<span id="feature-details"></span>
## Feature details

Call the `setVideoSourceType` method to specify the custom video source. After capturing video using the custom device, call the `pushExternalVideoFrame` to send the captured video frames to the SDK.

The following diagram shows the video data flow.

<span>![图片](https://files.readme.io/8213938-.jpg) </span>

<span id="api-call-sequence"></span>
### API call sequence

Refer to the API call sequence to implement custom video capture:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/custom_cap_and_render/custom-capture.drawio.png) </span>

<span id="operation-steps"></span>
### Operation steps

<span id="_1-specify-the-video-source"></span>
#### 1. Specify the video source

Call the `setVideoSourceType` to specify the custom video source.


* iOS

   ```objectivec
   [self.rtcEngine setVideoSourceType:ByteRTCVideoSourceTypeExternal];
   ```
   

* Android

   ```java
   mRTCEngine.setVideoSourceType(VIDEO_SOURCE_TYPE_EXTERNAL);
   ```
   


<span id="_2-build-your-video-capture-module"></span>
#### 2. Build your video capture module

Build a video capture module that is independent of the RTC SDK, and use it to start capturing video. The following sample project demonstrates how to build a video capture module.

<span id="_3-build-the-videoframe-struct"></span>
#### 3. Build the VideoFrame struct

You can set the `VideoFrame` in the `pushExternalVideoFrame` to process the captured video frames before encoding. For example, set the `rotation` in the `VideoFrame` as `180` to rotate the video frames by 180 degrees clockwise. You can also add other pre\-encoding processing here.

> Set VideoFrame according to the encoding format of your video data.


<span id="_4-push-the-video-frames"></span>
#### 4. Push the video frames

Call pushExternalVideoFrame to send the captured video frames to the RTC SDK, which then proceeds with the data encoding and transmission.

<span id="ios"></span>
##### iOS

The specific pushExternalVideoFrame API to call depends on the additional settings you require for the video frames. Refer to for details.

The following sample code uses pushExternalVideoFrame:time: as an example.

```objectivec
#pragma mark - AVCaptureVideoDataOutputSampleBufferDelegate
// Call pushExternalVideoFrame to send video frames to SDK as soon as you receive the callback with camera video frames

- (void)captureOutput:(AVCaptureOutput *)output didOutputSampleBuffer:(CMSampleBufferRef)sampleBuffer fromConnection:(AVCaptureConnection *)connection {
        CVPixelBufferRef buffer = CMSampleBufferGetImageBuffer(sampleBuffer);
        CMTime timestamp = CMSampleBufferGetPresentationTimeStamp(sampleBuffer);
        ByteRTCVideoFrameData *frame = [[ByteRTCVideoFrameData alloc] init];
        frame.timestamp = timestamp;
        frame.width = (int32_t)CVPixelBufferGetWidth(buffer);
        frame.height = (int32_t)CVPixelBufferGetHeight(buffer);
        frame.cvpixelbuffer = buffer;
        frame.rotation = ByteRTCVideoRotation0;
        frame.seiData = nil;
        [self.rtcEngine pushExternalVideoFrame:frame];
    }
```


<span id="android"></span>
##### Android

Methods and formats to encode the videos vary by capture device. You need to set the parameters according to the format of the video frames.

The sample code below shows how to set the parameters for the video frames that use Texture\-compression and encoding with RGBA color space respectively.


* Texture


```java
   public void frameAvailable(SurfaceTexture texture) {
        VideoFrameData frame = new VideoFrameData();
        frame.bufferType = VideoBufferType.GL_TEXTURE;   
        frame.pixelFormat = VideoPixelFormat.TEXTURE_2D;
        frame.eglContext = sharedEglContext;
        frame.textureId = textureId;
        frame.textureMatrix = transformMatrix;
        frame.width = width;
        frame.height = height;
        frame.rotation = VideoRotation.VIDEO_ROTATION_0;
        frame.timestampUs = (long)System.currentTimeMillis() * TimeUnit.MILLISECONDS.toNanos(1);
        ...
        mRTCEngine.pushExternalVideoFrame(frame);
    }
```



* RGBA


```java
public void createRGBAFrame(byte[] RGBABuffer, ColorSpace colorSpace) {
    VideoFrameData frame = new VideoFrameData();
    frame.bufferType = VideoBufferType.RAW_MEMORY;
    frame.pixelFormat = VideoPixelFormat.RGBA;
    frame.width = width;
    frame.height = height;
    frame.rotation = VideoRotation.VIDEO_ROTATION_0;
    frame.timestampUs = System.currentTimeMillis() * TimeUnit.MILLISECONDS.toNanos(1);
    frame.planeData = buffers;
    frame.numberOfPlanes = 1;
    frame.planeStride = width * 4;
    mRTCEngine.pushExternalVideoFrame(frame);
}
```


<span id="apireference"></span>
## API Reference

The API references for different platforms are as follows:


* Android：

   * [setVideoSourceType](doc s\-70080#setvideosourcetype)

   * [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70080#pushexternalvideoframe)

* iOS：

   * [setVideoSourceType:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideosourcetype)

   * [pushExternalByteVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#pushexternalvideoframe)

* macOS：

   * [setVideoSourceType:](https://docs.byteplus.com/en/docs/12/docs-70092#setvideosourcetype)

   * [pushExternalByteVideoFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#pushexternalvideoframe)

* Windows：

   * [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#setvideosourcetype)

   * [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-70095#pushexternalvideoframe)

* Linux：

   * [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideosourcetype)

   * [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-pushexternalvideoframe)


<span id="see-also"></span>
## See Also


* [Custom Video Rendering](https://docs.byteplus.com/en/docs/12/docs-81201)

* [Switch between SDK and custom video capture modules](https://docs.byteplus.com/en/docs/12/docs-100448)

* [Custom Audio and Video Capturing (Web)](https://docs.byteplus.com/en/docs/12/docs-128914)


```Plain


```
