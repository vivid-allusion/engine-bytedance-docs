---
title: "Custom Video Processing"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-79888"
---

To use a third\-party beautification SDK or apply custom effects like video trimming, you can process the video captured by the RTC SDK before it is encoded and transmitted.

This functionality is commonly used in the following scenarios:


* Use other beautification SDKs instead of the BytePlus Effects SDK

* Trim the captured video.

> The deep integration of the RTC SDK and the BytePlus Effects SDK provides a powerful, easy\-to\-use RTC\-CV solution. For details, contact our technical support team.


This guide provides the steps and code examples to implement and register a custom video processor, giving you full control over the pre\-encoding video stream.

<span id="prerequisite"></span>
## Prerequisite

Ensure you have integrated the RTC SDK, version 3.45 or later.

<span id="process-video-with-a-custom-processor"></span>
## Process video with a custom processor

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/79888_api_en.png) </span>


1. Call `IVideoProcessor` to create a video processor to meet your business needs.

2. Call `registerLocalVideoProcessor` to use the video processor.


<span id="video-data-transfer"></span>
## Video data transfer

The following diagram shows how video data is transferred when you use a custom video processor:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/79888_79888_en_flow.png) </span>

To disable the video processor, call `registerLocalVideoProcessor` and set the processor to `null`.

> Note:

> To ensure compatibility with the RTC SDK, it's recommended to develop a video processor that supports the video format and pixel format specified in the API reference.


<span id="code-samples"></span>
## Code Samples

To implement the custom video source in your project, see the following code samples.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `public RTCVideoFrame processFrame(RTCVideoFrame rtcVideoFrame) {
                    int cameraTextureId = rtcVideoFrame.getGlTextureId();
                    int width = rtcVideoFrame.getWidth();
                    int height = rtcVideoFrame.getHeight();
                    int textureId = FuRender.drawFrameSingleInput(cameraTextureId, width, height);
                    if (textureId < 0) {
                        return null;
                    }
                    RTCVideoFrame textureFrame = RTCVideoFrame.createTextureFrame(RTCVideoFrame.PixelFormat.TEXTURE_2D,
                            textureId, width, height, rtcVideoFrame.getRotation(),
                            rtcVideoFrame.getTimestamp(), rtcVideoFrame.getTransform(), null);
                    return textureFrame;
                }`, 
  },
  {
    "lang": "cpp",
    "text": `# pragma mark -- ByteRTCVideoProcessorDelegate

- (ByteRTCVideoFrame *)processFrame:(ByteRTCVideoFrame *)src_frame{
    CVPixelBufferRef pixelBuffer = src_frame.textureBuf;
    CVPixelBufferLockBaseAddress(pixelBuffer, 0);
    int width = (int)CVPixelBufferGetWidth(pixelBuffer);
    int height = (int)CVPixelBufferGetHeight(pixelBuffer);
    // y
    uint8_t* src_y = CVPixelBufferGetBaseAddressOfPlane(pixelBuffer, 0);
    const size_t src_ystride = CVPixelBufferGetBytesPerRowOfPlane(pixelBuffer, 0);
    // u
    uint8_t* src_u = CVPixelBufferGetBaseAddressOfPlane(pixelBuffer, 1);
    const size_t src_ustride = CVPixelBufferGetBytesPerRowOfPlane(pixelBuffer, 1);
    // v
    uint8_t* src_v = CVPixelBufferGetBaseAddressOfPlane(pixelBuffer, 2);
    const size_t src_vstride = CVPixelBufferGetBytesPerRowOfPlane(pixelBuffer, 2);
    [[LPFaceUnityManager sharedManager] processFrame:src_y
                                                   u:src_u
                                                   v:src_v
                                             ystride:(int)src_ystride
                                             ustride:(int)src_ustride
                                             vstride:(int)src_vstride
                                               width:width
                                              height:height];
    CVPixelBufferUnlockBaseAddress(pixelBuffer, 0);
    return src_frame;
}`, 
  },
]
return (<PreCodeTabs list={list} />);
```


<span id="api-reference"></span>
## API Reference

View API details and parameters here.


* Android:

   [IVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#ivideoprocessor)

   [registerLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70080#registerlocalvideoprocessor)

* iOS:

   [ByteRTCVideoProcessorDelegate](https://docs.byteplus.com/en/docs/12/docs-70087#bytertcvideoprocessordelegate)

   [registerLocalVideoProcessor:withConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#registerlocalvideoprocessor-withconfig)

* Windows:

   [IVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#ivideoprocessor)

   [RegisterLocalVideoProcessor](https://docs.byteplus.com/en/docs/12/docs-70095#registerlocalvideoprocessor)
