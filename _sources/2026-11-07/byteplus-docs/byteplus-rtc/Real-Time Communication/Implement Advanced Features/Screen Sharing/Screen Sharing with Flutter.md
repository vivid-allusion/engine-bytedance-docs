---
title: "Screen Sharing with Flutter"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1177503"
---

<span id="introduction"></span>
# Introduction

In real\-time communication, if you want your app users to be able to share the screen content and audio playing on their local devices, you can use the built\-in screen capture feature of RTC to capture the screen, and share the captured content with remote users through the screen sharing functionality.

> Notes:

> 1. Only visible users can publish screen streams. See setUserVisibility for details.

> 2. The RTC Flutter SDK only supports sharing screen content captured internally. For custom capture, you need to follow the integration and usage guidelines of the Native SDK.



|**Scenarios** |**Description** |
|---|---|
|**Online Education** |Instructors share their screens with their students. |
|**Video Game Livestreaming** |Hosts share their gameplay screens with viewers. |
|**Interactive Livestreaming** |Hosts share their screens to interact with their audience. |
|**Video Conferencing** |Speakers share their slides or documents with other participants. |


<span id="prerequisites"></span>
# Prerequisites


* You have integrated the RTC SDK, and implemented [real-time communications](https://docs.byteplus.com/en/docs/12/docs-132236).

* Supported operating systems:

   * Android 5 (API level 21) or later. Android 10 (API level 29) or later is recommended because Android 5\-10 only supports capturing **video** from the screen (not audio).

   * iOS 12 or later. For devices with iOS 12 to 12.2, RTC SDK v3.52 or later is required.


<span id="implementation-ios"></span>
# Implementation (iOS)

On iOS, screen recording is achieved using Apple's [Replaykit](https://developer.apple.com/documentation/replaykit) framework, allowing for sharing of the entire system's screen content. However, data cannot be shared between different apps due to Apple's privacy settings. Hence, the current app (main app process) needs to provide an Extension component (Extension process), and both the App and Extension should be configured under the same App Group. This allows the screen recording process in the Extension to communicate cross\-process with the main app process, enabling screen content sharing.

<span id="step-1-create-and-configure-the-extension-component"></span>
## Step 1: Create and configure the Extension component

Refer to steps 1 to 3 in the [Implementation](https://docs.byteplus.com/en/docs/12/docs-124177) of screen sharing on iOS to create the App Group and Extension, and implement the screen capture logic.

> Note:

> When importing the screen sharing plug\-in for the RTC iOS SDK into your project, ensure that the version of BytePlus RTC is consistent with the version that the Flutter SDK depends on, which can be found in the `SDK root/ios/byteplus_rtc.podspec` file.


<span id="step-2-set-the-app-group-id-for-rtc-video"></span>
## Step 2: Set the App Group ID for RTC Video

After creating the RTC engine instance, call `setExtensionConfig` to pass in the App Group ID and Bundle ID of the Extension. This allows the RTC engine to respond to screen sharing requests initiated from the system Control Center.

```objectivec
#if __has_include(<byteplus_rtc/ByteRTCVideoManager.h>)
#import <byteplus_rtc/ByteRTCVideoManager.h>
#else
@import byteplus_rtc;
#endif

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [GeneratedPluginRegistrant registerWithRegistry:self];
// Before using the built-in capture module of the SDK to capture the screen, set the Extension configuration by providing the App Group ID shared by your app and the Extension, and the Bundle Identifier of the Extension.
    [ByteRTCVideoManager setExtensionConfig:APPGroupId bundleId:ExtensionBundleId];
    return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

@end
```


<span id="implementation-android"></span>
# Implementation (Android)

On Android, screen sharing uses both the [android.media.projection](https://developer.android.com/reference/android/media/projection/package-summary) API introduced in Android 5 (API level 21) and the RTC SDK API.

> Note:

> By default, the SDK has added the `android.permission.FOREGROUND_SERVICE` permission required for screen sharing. No additional declaration is needed.


<span id="step-1-create-screencapturerequestactivity"></span>
## Step 1: Create ScreenCaptureRequestActivity

In the Android project, create a file named `ScreenCaptureRequestActivity.java`, and implement it by extending the BaseScreenCaptureRequestActivity class provided in the SDK.

```Java
import android.app.Activity;

import com.ss.bytertc.engine.flutter.screencapture.BaseScreenCaptureRequestActivity;

public class ScreenCaptureRequestActivity extends BaseScreenCaptureRequestActivity {
    /**
     * For Android 10 or later
     * Specify the large icon to be displayed on the screen recording notification.
     */
    @Override
    public int getLargeIcon() {
        return R.mipmap.ic_launcher;
    }

    /**
     * For Android 10 or later
     * Specify the small icon to be displayed on the screen recording notification.
     */
    @Override
    public int getSmallIcon() {
        return R.mipmap.ic_launcher;
    }

    /**
     * For Android 10 or later
     * Specify the Activity to launch when the user taps the screen recording notification.
     */
    @Override
    public Class<? extends Activity> getLaunchActivity() {
        return MainActivity.class;
    }

    /**
     * For Android 10 or later
     * Specify the prompt text on the screen recording notification.
     */
    @Override
    public String getContextText() {
        return "Recording/Casting your screen";
    }
}
```


<span id="step-2-bind-screencapturerequestactivity"></span>
## Step 2: Bind ScreenCaptureRequestActivity

Add the following code to the `AndroidManifest.xml` file in the root directory of the Android project.

```XML
<application
    ...
    <activity
        android:name=".ScreenCaptureRequestActivity"
        android:exported="false"
        android:theme="@android:style/Theme.Translucent.NoTitleBar.Fullscreen">
        <intent-filter>
            <action android:name="${applicationId}.action.REQUEST_SCREEN_CAPTURE" />
            <category android:name="android.intent.category.DEFAULT" />
        </intent-filter>
    </activity>
</application>
```


<span id="call-the-rtc-apis"></span>
# Call the RTC APIs

<span id="sequence-diagram"></span>
## Sequence diagram

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/flutterscreensharing.jpg) </span>

<span id="optional-set-encoding-parameters"></span>
## [Optional] Set encoding parameters

You can call `setScreenVideoEncoderConfig` to set the encoding parameters through `ScreenVideoEncoderConfig` before starting screen capture if the default setting does not meet your requirements. See the example below.

```Dart
ScreenVideoEncoderConfig screenStream = ScreenVideoEncoderConfig(
    width: 1280,
    height: 720,
    frameRate: 15,
    maxBitrate: 600,
    minBitrate: 100,
    encoderPreference: ScreenVideoEncoderPreference.maintainFrameRate);
    
rtcVideo.setScreenVideoEncoderConfig(screenStream);
```



* When the width and height are both set to the default value of 0, the SDK will not scale the captured screen video frames.

   * If the physical resolution of the screen has a longer side with a pixel count less than 1920px, the recorded video resolution will be the same as the screen's physical resolution.

   * If the physical resolution of the screen has a longer side with a pixel count greater than 1920px, the recorded video will be scaled to about 1920px on the longer side.

* If the resolution is set to a non\-zero value, the SDK will scale the screen video frames captured by the system proportionally.

   * If the source resolution is greater than the target resolution, the recorded video will be scaled down proportionally.

   * If the source resolution is less than the target resolution, the recording resolution remains unchanged.


<span id="start-screen-capture"></span>
## Start screen capture

<span id="internal-capture"></span>
### Internal capture

You can call startScreenCapture to start screen capture. You can specify the type of media to be captured, including audio only, video only, and audio and video. After enabling capture, you can adjust the type of captured media through updateScreenCapture.

```Dart
// Start capturing screen audio and video streams.
rtcVideo.startScreenCapture(ScreenMediaType.videoAndAudio);
// Update the screen capture media type to video only to achieve a mute effect.
rtcVideo.updateScreenCapture(ScreenMediaType.videoOnly);
```


> Note: On iOS, screen sharing can also be initiated from the System Control Center:

> 1. Open the Control Center of the iOS system and long\-press the Screen Recording button;

> 2. Select your app in the pop\-up window and tap the **Start Recording** option to start recording the screen.

   > <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/61a73d1b-57d0-4870-913d-c61bdd571144.png) </span>


<span id="custom-capture"></span>
### Custom capture

It is highly recommended that you use RTC internal capture. If you still want to use custom capture, refer to [Advanced Feature Usage Instructions for RTC Flutter SDK](https://docs.byteplus.com/en/docs/12/docs-1177504) to use related interfaces on the Native layer.

<span id="stop-screen-capture"></span>
## Stop Screen Capture

```Dart
rtcVideo.stopScreenCapture();
```


<span id="publish-unpublish-screen-stream"></span>
## Publish/Unpublish Screen Stream

```Dart
// Publish/unpublish screen streams in RTCVideoEventHandler.
engineHandler.onVideoDeviceStateChanged = (String deviceId,
    VideoDeviceType deviceType,
    MediaDeviceState deviceState,
    MediaDeviceError deviceError) {
    if (deviceType == VideoDeviceType.screenCaptureDevice) {
        if (deviceState == MediaDeviceState.started) {
            // Publish screen streams.
            rtcRoom.publishScreen(MediaStreamType.both);
        } else if (deviceState == MediaDeviceState.stopped ||
            deviceState == MediaDeviceState.runtimeError) {
            // Unpublish screen streams.
            rtcRoom.unpublishScreen(MediaStreamType.both);
        }
    }
};
```


<span id="render-remote-screen-stream"></span>
## Render Remote Screen Stream

```Dart
// In RTCRoomEventHandler, refresh the UI when receiving the callback of the remote user publishing the screen stream.
roomEventHandler.onUserPublishScreen = (String uid, MediaStreamType type) {
    // After obtaining the uid, create RTCViewContext.remoteContext by refreshing the UI. 
    // Use RTCSurfaceView to render the remote video.
}
```


<span id="stop-rendering-remote-screen-stream"></span>
## Stop Rendering Remote Screen Stream

```Dart
// In RTCRoomEventHandler, refresh the UI when receiving the callback of the remote user unpublishing the screen stream.
roomEventHandler.onUserUnpublishScreen =
    (String uid, MediaStreamType type, StreamRemoveReason reason) {
    // Cancel the setting of the remote video canvas.
    rtcVideo.removeRemoteVideo(
        roomId: roomId,
        uid: uid,
        streamType: StreamIndex.screen);
    // Refresh the UI to remove the video rendering view.
};
```
