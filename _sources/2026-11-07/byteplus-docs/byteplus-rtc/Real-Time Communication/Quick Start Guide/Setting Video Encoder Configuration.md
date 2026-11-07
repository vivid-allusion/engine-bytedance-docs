---
title: "Setting Video Encoder Configuration"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70122"
---

In different video call scenarios, the video image size, requirements for video resolution and smoothness, and network bandwidth are often different. You need to configure appropriate video configuration parameters based on the actual situation.

<span id="glossary"></span>
## Glossary

When using the RTC SDK to capture video for local preview or remote rendering, you can set the parameters as shown below.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/70122_70122_en_video_properties.png) </span>

<span id="resolution"></span>
### Resolution

It refers to the `width (px) × height (px)` of the video. The width corresponds to the horizontal edge of the video display interface, and the height corresponds to the vertical edge of the video display interface. For the orientation mode of the video display interface, refer to [Video Rotation](https://docs.byteplus.com/6uofwzl3/14130). High\-resolution videos are clearer, but it also increases the demand for bandwidth, which may cause stalling.

> Since the video image is displayed vertically by default on mobile devices and horizontally on PCs, the concepts of width and height on mobile devices are opposite to those on PCs. For example, 720P represents `720 x 1280` for mobile devices and `1280 x 720` for PCs.


* Capture resolution: Refers to the image resolution provided by capture devices such as cameras.

* Encoding resolution: The resolution of the encoded image. The encoding resolution is less than or equal to the capture resolution. When the encoding resolution is less than the capture resolution, the aspect ratios of the encoding and capture resolutions should be consistent in order to avoid image distortion. For example, if the capture resolution is `1920 × 1080`, and the encoding resolution can be proportionally scaled down to `640 × 360`.


<span id="frame-rate"></span>
### Frame rate

Generally, the higher the frame rate, the smoother the image. `15 fps` is generally used. For images with resolutions less than `200 × 200`, `10 fps` can be used. The frame rate usually does not exceed `30 fps`.


* Video capture frame rate (fps) is the number of frames captured per second.

* Video encoding frame rate (fps), which is the number of frames to be encoded per second. The encoding frame rate is less than or equal to the capture frame rate.


<span id="bitrate"></span>
### Bitrate

Data transfer rate (Kbps), which is the amount of data transferred per second. The higher the resolution and frame rate of the video image, the higher the quality, and the higher the bitrate required. Under the same real\-time performance requirements, the higher the bitrate, the higher the bandwidth required.

<span id="set-video-capture-parameters"></span>
## Set video capture parameters

This API can be called after the engine is created. We recommend that you call `setVideoCaptureConfig` to set the video capture parameters before calling `startVideoCapture`. Different engines on the same device use the same video capture parameters.

```Java
private void setVideoCaptureConfig() {
    String width = captureWidth.getText().toString();
    String height = captureHeight.getText().toString();
    String frameRate = captureFrameRate.getText().toString();
    VideoCaptureConfig config = new VideoCaptureConfig();
    
    config.capturePreference = VideoCaptureConfig.CapturePreference.MANUAL;
        
        config.width = width.isEmpty() ? 1920 : Integer.parseInt(width);
        config.height = height.isEmpty() ? 1080 : Integer.parseInt(height);
        config.frameRate = frameRate.isEmpty() ? 30 : Integer.parseInt(frameRate);
    rtcEngine.setVideoCaptureConfig(config);
}
```


```Swift
let config = ByteRTCVideoCaptureConfig.init()
    config.preference = .manual
    config.videoSize =  CGSize(width:  480, height:  640) 
    config.frameRate =  15 
    self.rtcEngine?.setVideoCaptureConfig(config)
```


```C++
bytertc::VideoCaptureConfig config;
config.width = 1280;
config.height = 720;
config.frameRate = 15;
config.capturePreference = bytertc::VideoCaptureConfig::CapturePreference::kManual; 
    
int ret = m_engine->setVideoCaptureConfig(config);
```


The three capture parameter modes are described as follows:


* `Auto`: (Default) Automatically sets capture parameters. The SDK will apply the capture parameters based on the distributed configuration and device performance. In this mode, the resolution and frame rate passed in by calling this API will not take effect.

* `Manual`: Manually set the capture parameters, including capture resolution and frame rate. If the device does not support the resolution set for capture, the closest resolution will be selected first, and then scaled to the target resolution after capture. We recommend that you use the same capture and encoding resolutions, and the resolution should be configured to a common value to avoid multiple scaling of video frames.

* `AutoPerformance`: The capture parameters are the same as the encoding parameters, that is, the parameters set in `setVideoEncoderConfig` will be used for capture. In this mode, the resolution and frame rate passed in by calling this API will not take effect.

> Note: When the video capture parameters, such as resolution, are set, or the video rotation angle (setVideoCaptureRotation) changes, the `onLocalVideoSizeChanged` callback will be received.


<span id="set-video-encoding-parameters"></span>
## Set video encoding parameters

You can call `setVideoEncoderConfig` to set video encoding parameters before and after entering the RTC room. We recommend setting the video encoding parameters before starting the live stream to speed up the rendering of the first video frame.

```mixin-react
const list = [
  {
    "lang": "java",
    "text": `private void setVideoEncoderConfig() {
    VideoEncoderConfig config = new VideoEncoderConfig();
    config.width = 480;
    config.height = 640;
    config.frameRate = 10;
    config.maxBitrate = 1000;
  
    rtcVideo.setVideoEncoderConfig(config);
}`,
    "selected": true,
  },
  {
    "lang": "swift",
    "text": `let encoderCfg = ByteRTCVideoEncoderConfig.init()
encoderCfg.width = 480
encoderCfg.height = 640
encoderCfg.frameRate = 15
encoderCfg.maxBitrate = 1000

self.rtcVideo?.setMaxVideoEncoderConfig(encoderCfg)`, 
  },
  {
    "lang": "cpp",
    "text": `bytertc::VideoEncoderConfig config;
config.width = 1280;
config.height = 720;
config.frameRate = 15;
config.encoderPreference = bytertc::kVideoEncodePreferenceFramerate;
config.minBitrate = 500;
config.maxBitrate = 1000;
int ret = m_video->setVideoEncoderConfig(config);`, 
  }
]
return (<PreCodeTabs list={list} />);
```


When setting the bitrate of video encoding, it is recommended to set it to `-1` to use the bitrate automatically set by the SDK. Set the above parameters to their ideal maximum values. When the video cannot reach the maximum value set for resolution, frame rate, or bitrate due to network environment and other reasons, the SDK will take the value closest to the maximum value.

For video, the encoding resolution and frame rate are subject to the capture resolution and frame rate, and higher resolution and frame rate are not always better. First of all, higher resolution and frame rate than those of the captured image will not make the image clearer or smoother. At the same time, high resolution and frame rate require higher bandwidth. Using [high-resolution video](https://docs.byteplus.com/en/docs/12/docs-69871) during a call will also incur higher costs. If the bitrate is constant, an excessively high frame rate will reduce the video's resolution.

For example, in a one\-on\-one teaching scenario with large video windows and high real\-time performance requirements, a higher resolution and frame rate are necessary. In contrast, for a one\-on\-four scenario with smaller windows, you can reduce the resolution and bitrate for each stream to conserve resources and reduce pressure on the receiver's bandwidth.

You should choose appropriate video launch parameters according to the needs of the scenario. The following are recommended parameters for mobile devices in some common scenarios.

> For PCs, you can swap the recommended width and height values from the table below. For example, swap 720 x 1280 to 1280 x 720 for use on PCs.


<span id="solo"></span>
### Solo


|Resolution |Height (px) |Width (px) |Frame Rate (fps) |Default Bitrate (kbps) |Recommended Highest Bitrate (kbps) |Recommended Lowest Bitrate (kbps) |
|---|---|---|---|---|---|---|
|Blu\-ray (1080P) |1080 |1920 |20 |2500 |3800 |1000 |
|UHD (720P) |720 |1280 |15 |1200 |1900 |800 |
|HD (540P) |540 |960 |15 |1000 |1520 |500 |
|SD (480P) |480 |864 |15 |800 |1260 |320 |


<span id="duel"></span>
### Duel

Video encoding profile for each host:


|Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|
|540 |960 |15 |1200 |
|360 |640 |15 |800 |
|270 |480 |15 |600 |
|248 |432 |15 |400 |


<span id="_1v2-or-1v3"></span>
### 1V2 or 1V3


|Window |Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|---|
|Big window |360 |640 |15 |800 |
|Small window |320 |360 |15 |400 |


<span id="guest-interview"></span>
### Guest interview


|Window |Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|---|
|Host window |540 |960 |15 |1200 |
|Viewer window |240 |240 |15 |360 |


<span id="video-chat-room"></span>
### Video chat room


|Layout type |Window |Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|---|---|
|1V6 |Host window |540 |960 |15 |1200 |
| |Co\-host window |256 |256 |15 |300 |
|1V1 |Cell window |360 |360 |15 |800 |
|1V2 |Big window |360 |640 |15 |800 |
| |Small window |320 |360 |15 |500 |
|Four\-grid |Cell window |320 |360 |15 |500 |
|Six\-grid |Small window |240 |320 |15 |400 |
|Nine\-grid |Small window |240 |240 |15 |280 |


<span id="video-karaoke-meetup"></span>
### Video Karaoke meetup


|Window |Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|---|
|Big window |540 |960 |15 |1200 |
|Small window |256 |256 |15 |300 |


<span id="audio-only-karaoke-meetup"></span>
### Audio\-only Karaoke meetup


|Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|
|540 |720 |15 |1000 |


<span id="watch-live-together"></span>
### Watch LIVE Together


|Height (px) |Width (px) |Frame Rate (fps) |Bitrate (kbps) |
|---|---|---|---|
|368 |640 |15 |800 |


<span id="encoding-parameter-reference"></span>
### Encoding parameter reference

For the best viewing experience, use a higher video resolution, bitrate, and frame rate. However, in practice, you must choose appropriate video encoding parameters by considering your application's requirements, device performance, network conditions, and traffic costs. Generally speaking, a higher resolution requires a higher bitrate; if the bitrate is constant, an excessively high frame rate will reduce the video's resolution. We recommend that you use the SDK's default video encoding bitrate.

Refer to the table below to select an appropriate frame rate and bitrate for your chosen video resolution:


|Resolution (W × H) |Frame rate (fps) |Recommended bitrate when prioritizing smoothness (kbps) |Recommended bitrate when prioritizing image quality (kbps) |Recommended bitrate in game scenarios (kbps) |
|---|---|---|---|---|
|160 × 120 |15 |65 |130 |/ |
|120 × 120 |15 |50 |100 |/ |
|320 × 180 |15 |140 |280 |/ |
|180 × 180 |15 |100 |200 |/ |
|240 × 180 |15 |120 |240 |/ |
|320 × 240 |15 |200 |400 |/ |
|240 × 240 |15 |140 |280 |/ |
|424 × 240 |15 |220 |440 |/ |
|640 × 360 |15 |400 |800 |/ |
|360 × 360 |15 |260 |520 |/ |
|640 × 360 |30 |600 |1200 |/ |
|360 × 360 |30 |400 |800 |/ |
|480 × 360 |15 |320 |640 |/ |
|480 × 360 |30 |490 |980 |/ |
|640 × 480 |15 |500 |1000 |/ |
|480 × 480 |15 |400 |800 |/ |
|640 × 480 |30 |750 |1500 |/ |
|480 × 480 |30 |600 |1200 |/ |
|848 × 480 |15 |610 |1220 |/ |
|848 × 480 |30 |930 |1860 |/ |
|640 × 480 |10 |400 |800 |/ |
|1280 × 720 |15 |1130 |2260 |/ |
|1280 × 720 |30 |1710 |3420 |/ |
|960 × 720 |15 |910 |1820 |/ |
|960 × 720 |30 |1380 |2760 |/ |
|1920 × 1080 |15 |2080 |4160 |/ |
|1920 × 1080 |30 |3150 |6300 |/ |
|1920 × 1080 |60 |4780 |6500 |/ |
|2048 × 1080 |60 |/ |/ |8000 |
|4096 × 2160 |60 |/ |/ |20000 |


<span id="set-the-video-rendering-mode"></span>
## Set the video rendering mode

Call `setLocalVideoCanvas` and `setRemoteVideoCanvas` to set the rendering modes for the local and remote video streams.

Three video rendering fill modes are supported. The SDK will render the video image according to the selected fill mode based on the resolutions of the captured image and the canvas. See `VideoCanvas`.

<span id="default-rendermodehidden"></span>
### (Default) RenderModeHidden

The window will be filled up with the video. If the video's aspect ratio does not match the window's, the video is scaled proportionally and cropped to fit the window.

For example:


* Ratio of the sender: 9:16

* Ratio of the receiver: 16:9


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/70122_70122_en_hidden.png) </span>

<span id="rendermodefit"></span>
### RenderModeFit

The video will be fully displayed in the window. If the video's dimensions do not align with those of the window, the video will be scaled proportionally. And the blank area will be filled with the background color.

For example:


* Ratio of the sender: 9:16

* Ratio of the receiver: 16:9


<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/70122_70122_en_fit.png) </span>

<span id="rendermodefill"></span>
### RenderModeFill

The video is stretched or shrunk to fill the entire window. If the video's aspect ratio does not match the window's, the video is stretched non\-proportionally to fill the space.

<span id="sample-project"></span>
## Sample project


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/video/VideoCommonConfigActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/VideoManager/CommonConfig/CommonVideoConfigViewController.swift)
