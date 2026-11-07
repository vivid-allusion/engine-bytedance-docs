---
title: "Screen Sharing on Android"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-124176"
---

Screen sharing allows you to present your entire screen, specific areas, a designated tab, and a whiteboard with remote users. Use this function for various industry solutions to accommodate your needs.


|**Scenarios** |**Description** |
|---|---|
|**Online Education** |Instructors share their screens with their students. |
|**Video Game Livestreaming** |Hosts share their gameplay with viewers. |
|**Interactive Livestreaming** |Hosts share their screens to interact with their audience. |
|**Video Conferencing** |Speakers share their slides or documents with other participants. |


<span id="prerequisites"></span>
## Prerequisites


* Integrate the Android SDK and implement [real-time communications](https://docs.byteplus.com/en/docs/12/docs-70134).

* Use Android 5.0 (SDK/API level 21) or later. Android 10 (SDK/API level 29) or later is recommended.

> Android 5\-10 only supports screen video capture.


<span id="to-share-screens-on-android"></span>
## To share screens on Android

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/124176_api_en.png) </span>

<span id="step-1-configure-your-project"></span>
### Step 1: Configure your project

For Android 10 (API level 29) or later, the foreground service is required for screen capture. Add the following foreground service declaration to the app's `AndroidManifest.xml` file.

```xml
<manifest>
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <!-- If your app targets Android 14 (API level 34) or higher, make sure you also apply for the FOREGROUND_SERVICE_MEDIA_PROJECTION permission to avoid security exception. Add the following line:  -->
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE_MEDIA_PROJECTION" />
    
    <application>
        <!-- ... -->
        <!-- RTC ScreenCaptureService -->
        <service android:name="com.bytedance.realx.video.RXScreenCaptureService"android:exported="false"android:enabled="true"android:foregroundServiceType="mediaProjection" />
    </application>
</manifest>
```


<span id="step-2-request-permission-to-share-your-screen"></span>
### Step 2: Request permission to share your screen

```java
public static final int REQUEST_CODE_OF_SCREEN_SHARING = 101;
// Initiate a permission request for screen sharing
public void requestForScreenSharing() {
    if (Build.VERSION.SDK_INT < Build.VERSION_CODES.LOLLIPOP) {
Log.e ("ShareScreen", "The current system version is too low to support screen sharing");
        return;
    }
    MediaProjectionManager projectionManager = (MediaProjectionManager) getSystemService(Context.MEDIA_PROJECTION_SERVICE);
    if (projectionManager != null) {
        startActivityForResult(projectionManager.createScreenCaptureIntent(), REQUEST_CODE_OF_SCREEN_SHARING);
    } else {
Log.e ("ShareScreen", "The current system version is too low to support screen sharing");
    }
}
```


Start screen sharing in the response to the permission request.

```java
public static final int REQUEST_CODE_OF_SCREEN_SHARING = 101;
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    if (requestCode == REQUEST_CODE_OF_SCREEN_SHARING && resultCode == Activity.RESULT_OK) {
        startScreenShare(data)
    } else {
        super.onActivityResult(requestCode, resultCode, data);
    }
}
```


<span id="step-3-calling-apis"></span>
### Step 3: Calling APIs


1. Enable screen capture


```java
private void startScreenShare(Intent data) {
    startRXScreenCaptureService(data);
//encoding parameters
    ScreenVideoEncoderConfig config = new ScreenVideoEncoderConfig();
    config.width = 720;
    config.height = 1280;
    config.frameRate = 15;
    config.maxBitrate = 1600;
    mRTCEngine.setScreenVideoEncoderConfig(config);
    // Enable screen video data capture
    mRTCEngine.startScreenCapture(ScreenMediaType.SCREEN_MEDIA_TYPE_VIDEO_AND_AUDIO, data);
}
private void startRXScreenCaptureService(@NonNull Intent data) {
    Context context = Utilities.getApplicationContext();
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.Q) {
        Intent intent = new Intent();
        intent.putExtra(RXScreenCaptureService.KEY_LARGE_ICON, R.drawable.launcher_quick_start);
        intent.putExtra(RXScreenCaptureService.KEY_SMALL_ICON, R.drawable.launcher_quick_start);
        intent.putExtra(RXScreenCaptureService.KEY_LAUNCH_ACTIVITY, mHostActivity.getClass().getCanonicalName());
intent.putExtra (RXScreenCaptureService.KEY _CONTENT_TEXT, "Recording/projecting your screen");
        intent.putExtra(RXScreenCaptureService.KEY_RESULT_DATA, data);
        context.startForegroundService(RXScreenCaptureService.getServiceIntent(context, RXScreenCaptureService.COMMAND_LAUNCH, intent));
    }
}
```



2. (Optional) Implement the callback method [onVideoDeviceStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onvideodevicestatechanged) in the `IRTCEngineEventHandler` implementation class on the local end. This step does not require calling APIs related to screen capture, only updating the relevant UI.


```java
@Override
public void onVideoDeviceStateChanged(String deviceId, VideoDeviceType deviceType, int deviceState, int deviceError) {
    Log.i(TAG, "onVideoDeviceStateChanged, type: " + deviceType + " state:" + deviceState);
}
```



3. On the remote client, use the `onUserPublishStreamVideo` and `onFirstRemoteVideoFrameDecoded` callbacks to monitor video and screen sharing streams. To prevent stuttering, we recommend setting up video rendering within the `onFirstRemoteVideoFrameDecoded` callback. This ensures rendering begins only after the video frame is decoded.


```java
// Callback for when a remote screen sharing stream is unpublished.
@Override
public void onFirstRemoteVideoFrameDecoded(String streamId, StreamInfo streamInfo, VideoFrameInfo frameInfo) {
    Log.i(TAG, "onUserPublishStreamVideo, streamId: " + streamId);
    runOnUiThread(() -> {
        // Set up remote video rendering view
        setRemoteRenderView(streamId);
    });
}
@Override
public void onUserPublishStreamVideo(String streamId, StreamInfo streamInfo, boolean isPublish) {
    if (!isPublish) {
      Log.i(TAG, "onUserUnpublishStreamVideo, uid: " + streamId);
        runOnUiThread(() -> {
            // Unbind remote video rendering view
            removeRemoteView(streamId);
        });
   }

4. Render remote screen share stream
   

```java
private void setRemoteRenderView(String streamId, String roomID, String userID, FrameLayout container) {
    TextureView renderView = new TextureView(this);
    FrameLayout.LayoutParams params = new FrameLayout.LayoutParams(
            ViewGroup.LayoutParams.MATCH_PARENT,
            ViewGroup.LayoutParams.MATCH_PARENT);
    container.removeAllViews();
    container.addView(renderView, params);
    VideoCanvas videoCanvas = new VideoCanvas();
    videoCanvas.renderView = renderView;
    videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
    
    // Set up remote user video rendering view
   mRTCEngine.setRemoteVideoCanvas(streamId, videoCanvas);
}
getStreamIndex(), videoCanvas);
}
```



5. Stop screen sharing


```java
private void stopScreenShare() {
    // Stop screen data capture and screen sharing
   mRTCEngine.stopScreenCapture();
```



6. Monitor the callback for removal of audio and video streams from remote screen sharing.


```java
// Callback for the removal of audio and video streams from remote screen sharing in the room.
@Override
public void onUserUnPublishScreen(String uid, MediaStreamType type, StreamRemoveReason reason) {
    super.onUserUnPublishScreen(uid, type, reason);
    runOnUiThread(() -> removeRemoteView(getScreenShareUserId(uid)));
}
```


<span id="capturing-a-custom-screen-video-stream"></span>
## Capturing a custom screen video stream

To use custom audio and video sources for screen sharing:


1. Develop your own screen recorder to capture screen video and device audio.

2. To specify an external input source, call `setVideoSourceType` to set up custom screen video capture.

3. Call [pushScreenAudioFrame](https://docs.byteplus.com/en/docs/12/docs-70080#pushscreenaudioframe) to push the captured audio frames to the RTC SDK for encoding and transmission.


<span id="faq"></span>
## FAQ


1. **Why can’t the other party hear audio after I share my screen?** 

* You might be using a version lower than Android 10. The system does not support screen audio capture for these versions.

* Check if other apps have exclusive access to screen audio capture. If so, disable exclusive settings in other apps.

* Ensure that your app has requested and received recording permission from the system.

2. **What should I do if I receive the error message`Media projections require a foreground service of type ServiceInfo.FOREGROUND_SERVICE_TYPE_MEDIA_PROJECTION`** **?** 

* Configure the `android.permission.FOREGROUND_SERVICE` permission and `org.webrtc.RXScreenCaptureService` in `AndroidManifest.xml`.

* Check whether the full class name is passed with `RXScreenCaptureService.KEY_LAUNCH_ACTIVITY` when launching RXScreenCaptureService.

3. **Why is the feature not working even though I do not see any error messages?** 

* Pass `RXScreenCaptureService.KEY_RESULT_DATA` when you start `RXScreenCaptureService`.

* Add a foreground service declaration in the Android manifest file.

* Start foreground service in your code.

* Pass the result of requesting recording permission as a parameter to the foreground service in your code.

4. Unexpected interruption during screen sharing on devices with Android 5.0–10

   As certain Android models with these system versions may have compatibility issues. We recommend users upgrade their system versions to avoid these issues.


<span id="changelog"></span>
## Changelog

The SDK version at the time of this update is 3.50.1. If you are using a previous version of the SDK, please be aware of the following changes and make necessary adaptations:


* V3.60:

   * The `createRTCVideo` method has been changed to `createRTCEngine`.

   * The `publishScreen` and `unpublishScreen` interfaces have been removed. Use `publishStreamVideo` and `publishStreamAudio` to control audio and video publishing. After calling `startScreenCapture`, call `publishStreamVideo(true)` to start screen stream publishing.

   * After the screen is ready, you will receive the `onVideoDeviceStateChanged` callback.

   * The `onUserUnPublishScreen` callback has been removed. Use the `onUserPublishStreamVideo` callback instead. Check `streamInfo.isScreen` to identify screen streams.

* Version 3.50.3

   * The encoding parameter type name for shared streams has been changed to `ScreenVideoEncoderConfig`.

   * The interface names and behaviors related to custom screen streams have changed.

* Version 3.43.1

   * The `publishScreen` and `unpublishScreen` methods were moved from the `RTCEngine` class to the `RTCRoom` class. The class of the other methods changed from RTCEngine to RTCVideo.

   * The callback interface changed from `IRTCEngineEventHandler` to `IRTCVideoEventHandler`.

* Version 3.36.1

   * The method for setting the encoding parameters for shared streams has been changed from `setVideoEncoderConfig` to `setScreenVideoEncoderConfig`.

   * Parameters of the `publishScreen` API and others have changed.
