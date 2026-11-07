---
title: "Screen Sharing on PC"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70144"
---

Screen sharing allows you to share your entire screen, specific areas, a designated tab, and a whiteboard with remote users. Use this function for various industry solutions to accommodate your needs.

> Only visible users can publish screen streams.

|**Scenarios** |**Description** |
|---|---|
|**Online Education** |Instructors share their screens with their students. |
|**Video Game Livestreaming** |Hosts share their gameplay with viewers. |
|**Interactive Livestreaming** |Hosts share their screens for interactive communications. |
|**Video Conferencing** |Speakers share their slides or documents with other participants. |

## Prerequisites

* Use the following operating system:

   * Windows 7+

   * MacOS 10.8+

   * Linux with Wayland or X11 protocol

* You have integrated the RTC SDK and implemented real\-time communication features.

## Share the screen recorded by the RTC SDK

To use the RTC SDK to capture your screen, follow these steps:

### Step 1: Get a list of shared objects

Before you start sharing your screen, call the following APIs to specify the screen/window you want to share.

1. Call `getScreenCaptureSourceList` to get a list of shared objects:

   * The app window: `kScreenCaptureSourceTypeWindow`

   * The entire screen: `kScreenCaptureSourceTypeScreen`. The `source_id` of the virtual desktop on Windows is `-1`.

2. Call `getThumbnail` to get the thumbnails of shared objects and set the parameters including width, height, and resolution.

3. (Optional) Call `getWindowAppIcon` to get the app icon.

   * Thumbnail size: maximize the thumbnail within the specified space while keeping its aspect ratio.

   * App icon size: the square icon will be scaled proportionally to a specified size.

```cpp
void AppBusiLogic::SDKGetAppIconAndShow(bool show, int width, int height) {
    if (!show && mAppIconView) {
        mAppIconView->hide();
    } else if (show) {
        bytertc::ScreenCaptureSourceInfo info = mCurScreenSourceInfo;
        bytertc::IVideoFrame* videoFrame = mByteEngineWrapper->GetWindowAppIcon(info.source_id, width, height);
        if (info.type != bytertc::kScreenCaptureSourceTypeWindow || !videoFrame) {
            ToastForm::toast(TEXT("Failed to get the app icon"), 2000, ToastForm::TipsToast,
                             WindowMgr::GetInstance().Find(WindowMgr::RTC_CALL_SETTTING));
            return;
        }

        QImage image;
        if (videoFrame->pixelFormat() == bytertc::kVideoPixelFormatRGBA) {
            image = QImage(videoFrame->getPlaneData(0), videoFrame->width(),
                videoFrame->height(), QImage::Format_RGBA8888);
        } else if (videoFrame->pixelFormat() == bytertc::kVideoPixelFormatARGB) {
            image = QImage(videoFrame->getPlaneData(0), videoFrame->width(),
                videoFrame->height(), QImage::Format_ARGB32);
        }

        if (!mAppIconView) {
            mAppIconView = new PixmapButton();
            auto settingWdg = WindowMgr::GetInstance().Find(WindowMgr::RTC_CALL_SETTTING);
            mAppIconView->move(settingWdg->x(), 0);
        }
        QString title = QString::number(videoFrame->width()) + "x" + QString::number(videoFrame->height());
        mAppIconView->setWindowTitle(title);
        mAppIconView->makePixmapBtn(QPixmap::fromImage(image));
        mAppIconView->setMinimumSize(200, 200);
        mAppIconView->show();

        videoFrame->release();
    }
}
```

### Step 2: Enable screen capture

1. (Optional) Call `setScreenVideoEncoderConfig` to set the encoding configuration of the screen\-sharing stream.

> * When the shared object's original resolution is greater than the resolution you specify, the frame will be scaled down to match your chosen resolution, while maintaining the original aspect ratio.

> * When the resolution you set is higher than that of the shared object, the object's size and aspect ratio will remain unaltered.

2. Call `startScreenVideoCapture` to enable screen capture. If you previously set `is_auto_publish_video = true`, calling this API will directly start publishing the screen stream. Otherwise, you need to call the `publishStreamVideo` method to start screen sharing.

   * For Linux systems using the Wayland protocol, when enabling screen capture, the system automatically displays a popup with relevant information for users to select the screen or window to share. Border highlighting and window exclusion features are not available.

   * For Windows and Linux systems using the X11 protocol, the `HighlightConfig` parameter in the `ScreenCaptureParameters` object adds border markers to the shared screen/window to indicate to users that this window is being shared. RTC recommends excluding the application's own window during screen sharing. You can exclude specified windows by setting the `ScreenFilterConfig` parameter.

The following Electron example assumes that `rtcEngine` has been initialized and `rtcRoom` has joined the room.

```typescript
const sources = rtcEngine.getScreenCaptureSourceList();
const source = sources.find(item => item.type === 2); // Desktop source
if (!source) {
  throw new Error("No screen capture source is available.");
}

rtcEngine.setVideoEncoderConfig({
  width: 1920,
  height: 1080,
  frame_rate: 15,
  max_bitrate: -1,
});

const captureRet = rtcEngine.startScreenVideoCapture(source, {
  region_rect: source.region_rect,
  capture_mouse_cursor: 0, // kMouseCursorCaptureStateOn
  filter_config: [],
  highlight_config: { enable_highlight: true },
});
if (captureRet !== 0) {
  throw new Error(`Failed to start screen capture: ${captureRet}`);
}

const publishRet = rtcRoom.publishStreamVideo(true);
if (publishRet !== 0) {
  throw new Error(`Failed to publish the screen stream: ${publishRet}`);
}
```

To stop screen sharing, stop publishing before stopping screen capture.

```typescript
rtcRoom.publishStreamVideo(false);
rtcEngine.stopScreenVideoCapture();
```

### Step 3: Enable audio capture

* **Windows**: Call `startScreenAudioCapture` to start screen audio capture. The `device_id` parameter is used to set the capture of audio from a specified local audio process. For example, you can set this parameter to the filename of an application's executable file (such as `QQMusic.exe`), and the SDK will only capture audio from that application. If you pass nullptr or an empty string, the SDK captures audio from all applications on the system except for the current process. Currently, screen audio capture only supports QQ Music, NetEase Cloud Music, and Kugou Music. Capturing other processes may lead to unknown behavior.

* **macOS**

> SDK v3.43.1 or later is required.

   1. Install the virtual sound card (VSC). It is recommended to install [VeRTCVirtualSoundCard](https://docs.byteplus.com/en/docs/12/docs-125703).

   2. Call `getDevice` to obtain the VSC ID.

   3. Call `startScreenAudioCapture` to pass the VSC ID and capture the device audio.

### Step 4: Update the screen sharing configuration

After starting to publish the screen stream, you can update the screen capture settings through the following interfaces. The following interfaces can be used on Windows and various Linux systems:

* Call `updateScreenCaptureRegion` to update the capture region. If you want to update the shared screen/window, you need to restart sharing.

* Call `updateScreenCaptureMouseCursor` to update the mouse cursor capture setting.

   The following interfaces can only be used on Windows and Linux with X11 systems:

* Call `updateScreenCaptureHighlightConfig` to update border highlighting settings.

* Call `updateScreenCaptureFilterConfig` to update windows that need to be filtered.

## Share the screen recorded by the external recorder

RTC strongly recommends that you use internal capture. If you still want to use custom capture, refer to the following steps:

1. Capture audio and videos from custom sources.

2. Call `setScreenAudioSourceType` and `setVideoSourceType` to set the audio and video source for the screen\-sharing.

3. Call `pushScreenAudioFrame` to use the RTC SDK to encode and transmit externally captured audio and video streams.

## Receive screen audio and videos

When a remote user publishes screen streams, the SDK notifies your application via the `onUserPublishStreamVideo` callback. To receive the streams, subscribe to them using `subscribeStreamVideo` and `subscribeStreamAudio`.

> If automatic subscription has been enabled when joining the room, manual subscription is not required.

> After the screen video stream is decoded normally, you will receive the `onFirstRemoteVideoFrameDecoded` first frame decoding callback. You can render the screen video through `setRemoteVideoSink` or `setRemoteVideoCanvas` in this callback or the `onUserPublishStreamVideo` callback. It is recommended that you set video rendering in the `onFirstRemoteVideoFrameDecoded` callback to ensure that video rendering occurs after video decoding is completed, to avoid stuttering.

## Known issues

During screen sharing on some Windows 7 devices, if you use a media player to play a video file, for example, Windows native player or QuickTime, the remote user cannot see the video in the player.

## API Reference

| |Windows |macOS |Linux with X11 |Linux with Wayland |Electron |
|---|---|---|---|---|---|
|Get shared objects |[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-70095#getscreencapturesourcelist) |[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-getscreencapturesourcelist) |[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getscreencapturesourcelist) |X |[getScreenCaptureSourceList](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getscreencapturesourcelist) |
|Get shared object thumbnails |[getThumbnail](https://docs.byteplus.com/en/docs/12/docs-70095#getthumbnail) |[getThumbnail:sourceId:maxWidth:maxHeight:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-getthumbnail-sourceid-maxwidth-maxheight) |[getThumbnail](https://docs.byteplus.com/en/docs/12/docs-70095#getthumbnail) |X |[getThumbnail](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getthumbnail) |
|Get the window icon |[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-70095#getwindowappicon) |[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-getwindowappicon-width-height) |[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-getwindowappicon) |X |[getWindowAppIcon](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-getwindowappicon) |
|Set the encoder configuration |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70095#setvideoencoderconfig) |[setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setvideoencoderconfig) |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-setvideoencoderconfig) |Same as left |[setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideoencoderconfig) |
|Start screen capture |[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startscreenvideocapture) |[startScreenVideoCapture:captureParameters:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-startscreenvideocapture-captureparameters) |[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-startscreenvideocapture) |Same as left |[startScreenVideoCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenvideocapture) |
|Start device audio capture |[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70095#startscreenaudiocapture) |[startScreenAudioCapture:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-startscreenaudiocapture) |X |X |[startScreenAudioCapture](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-startscreenaudiocapture) |
|Update capture region |[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-70095#updatescreencaptureregion) |[updateScreenCaptureRegion:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-updatescreencaptureregion) |[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatescreencaptureregion) |Same as left |[updateScreenCaptureRegion](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencaptureregion) |
|Update highlight control |[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-70095#updatescreencapturehighlightconfig) |[updateScreenCaptureHighlightConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-updatescreencapturehighlightconfig) |[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatescreencapturehighlightconfig) |X |[updateScreenCaptureHighlightConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencapturehighlightconfig) |
|Update filter options |[updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/docs-70095#updatescreencapturefilterconfig) |[updateScreenCaptureFilterConfig:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-updatescreencapturefilterconfig) |X |X |[updateScreenCaptureFilterConfig](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencapturefilterconfig) |
|Update mouse capture options |[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-70095#updatescreencapturemousecursor) |[updateScreenCaptureMouseCursor:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-updatescreencapturemousecursor) |[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCEngine-updatescreencapturemousecursor) |Same as left |[updateScreenCaptureMouseCursor](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-updatescreencapturemousecursor) |
|Publish screen stream |[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-publishstreamaudio) |[publishStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70092#publishstreamaudio) |[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-publishstreamaudio) |Same as left |[publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamvideo) / [publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamaudio), with `true` |
|Stop publishing screen stream |[unpublishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-publishstreamaudio) |[publishStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70092#publishstreamaudio) |[publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85516#IRTCRoom-publishstreamaudio) |Same as left |[publishStreamVideo](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamvideo) / [publishStreamAudio](https://docs.byteplus.com/en/docs/12/docs-85532#rtcroom-publishstreamaudio), with `false` |
|Switch external screen capture |[setScreenAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-70095#setscreenaudiosourcetype) |[setScreenAudioSourceType:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setscreenaudiosourcetype) |X |X |[setAudioSourceType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setaudiosourcetype) / [setVideoSourceType](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-setvideosourcetype) |
|Push custom device audio capture data |[pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70095#pushscreenaudioframe) |[pushScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-pushscreenaudioframe) |X |X |[pushExternalAudioFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalaudioframe) / [pushExternalVideoFrame](https://docs.byteplus.com/en/docs/12/docs-85532#rtcengine-pushexternalvideoframe) |

## Known issues

During screen sharing on some Windows 7 devices, if you use a media player to play a video file, for example, Windows native player or QuickTime, the remote user cannot see the video in the player.

## Changelog

This document was last updated with SDK version 3.50.1. If you are using a previous version of the SDK, please review the following changes and make the corresponding adaptations:

* Version 3.60 (single\-stream) includes the following changes:

   * The `createRTCVideo` interface has been changed to `createRTCEngine`.

   * The `publishScreen` and `unpublishScreen` interfaces have been removed. Use `publishStreamVideo` and `publishStreamAudio` to control audio and video publishing. After calling `startScreenVideoCapture`, call `publishStreamVideo(true)` to start screen stream publishing.

   * After the screen is ready, you will receive the `onVideoDeviceStateChanged` callback.

   * The `onUserUnPublishScreen` callback has been removed. Use the `onUserPublishStreamVideo` callback instead. Check `streamInfo.isScreen` to identify screen streams.

* Version 3.50.3

   * The encoding parameter type name for shared streams has been changed to `ScreenVideoEncoderConfig`.

   * The interface names and behaviors related to custom screen streams have changed.

   * The interface name for obtaining a thumbnail of a shared object on Mac has been changed from `getScreenCaptureSourceThumbnail:sourceId:maxWidth:maxHeight:` to `getThumbnail:sourceId:maxWidth:maxHeight:`.

   * The interface name for starting screen capture on Mac has been changed from `startScreenCaptureSourceInfo:captureParameters:` to `startScreenVideoCapture:captureParameters:`.

* Version 3.43.1

   |Platform |macOS |Windows |Linux (available since V3.58) |
   |---|---|---|---|
   |API |The class of `publishScreen:` and `unpublishScreen:` changed from `ByteRTCEngineKit` to `RTCRoom`. The class of the other methods changed to `RTCVideo`. |The class of `publishScreen` and `unpublishScreen` changed from `IRtcEngine` to `IRTCRoom`. The class of the other methods changed to `IRTCVideo`. |The class of `publishScreen` and `unpublishScreen` changed from `IRtcEngine` to `IRTCRoom`. The class of the other methods changed to `IRTCVideo`. |
   |Callback |The callback interface changed from `ByteRTCEngineDelegate` to `RTCVideoDelegate`. |The callback interface changed from `IRtcEngineEventHandler` to `IRTCVideoEventHandler`. |The callback interface changed from `IRtcEngineEventHandler` to `IRTCVideoEventHandler`. |

* Since version 3.42.1, all API and callback naming styles have been changed from PascalCase to camelCase.

* Version 3.36.1

   * The method for setting the encoding parameters for shared streams has been changed from `SetVideoEncoderConfig` to `SetScreenVideoEncoderConfig`.

   * Parameters of the `publishScreen` API and others have changed.
