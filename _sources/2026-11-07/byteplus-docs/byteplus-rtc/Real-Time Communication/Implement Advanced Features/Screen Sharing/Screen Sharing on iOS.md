---
title: "Screen Sharing on iOS"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-124177"
---

<span id="introduction"></span>
## Introduction

RTC supports the following two ways to share screens on iOS:


* Cross\-application screen sharing: Based on the iOS\-side native Replaykit screen recording framework, to share the screen content of the entire system, you need to add Extension extension components outside the current main App.

* In\-app screen sharing: Only share the screen of the current app. No need to configure the Extension component, you can enable screen capture by calling RTC APIs.


This document will explain how to implement cross\-app screen sharing on iOS platforms.

<span id="prerequisites"></span>
## Prerequisites


1. You have integrated the RTC SDK and implemented real\-time communication.

2. You have a good understanding of [Broadcast Extensions](https://developer.apple.com/app-extensions/), [AppGroupIDs](https://developer.apple.com/documentation/bundleresources/entitlements/com_apple_security_application-groups?language=objc), and [ReplayKit](https://developer.apple.com/documentation/replaykit).

3. Use iOS 12+.

> For devices with iOS 12 to 12.2, RTC SDK v3.52 or later version is required.


<span id="to-share-screens-on-ios"></span>
## To share screens on iOS

<span>![图片](https://files.readme.io/7e70685-ios_screen_sharing_en.drawio.png) </span>

On iOS, screen recording is achieved using Apple's [ReplayKit](https://developer.apple.com/documentation/replaykit) framework, allowing for sharing of the entire system's screen content. However, data cannot be shared between different apps due to Apple's privacy settings. Hence, the current app (main app process) needs to provide an Extension component (Extension process), and both the App and Extension should be configured under the same App Group. This allows the screen recording process in the Extension to communicate cross\-process with the main app process, enabling screen content sharing.

<span id="step-1-create-an-app-group"></span>
## Step 1: Create an App Group

Refer to [How to create and configure an App Group](https://docs.byteplus.com/en/docs/12/docs-125721)

<span id="step-2-create-an-extension"></span>
## Step 2: Create an Extension

Create a **Broadcast Upload Extension** component and perform the necessary configuration.


1. In your app project, click **File** \-\> **New** \-\> **Target...** , select **Broadcast Upload Extension** in the iOS tab, and click **Next**.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_3f6854ce3992fbbe2447cb860224454c) </span>

2. Fill in the relevant information, including **Product name** and **Language**, deselect the **include UI Extension**, and click **Finish**.

3. Select the newly created target for configuration:

   * Click **Build Settings** \-\> **Build Options** \-\> **Setting** and set the value of **Enable Bitcode** setting to **No**. Repeat this step for your main app target if you haven't already done so.

   * Ensure that the Bundle Identifier of the newly created target has the main App target's Bundle Identifier as its prefix.

4. Import the screen sharing plugin of the RTC SDK into the project. You can download the [iOS SDK](https://docs.byteplus.com/en/docs/12/docs-75707#download-sdk) and drag the `BytePlusRTCScreenCapturer.framework` file into your project. Alternatively, you can add the following code to your project's Podfile:

   ```Ruby
   target 'ScreenShareExtension' do
   use_frameworks!
   pod 'BytePlusRTC', '3.xx.xx', :subspecs => ['ScreenCapture']
   end
   ```
   


<span id="step-3-implement-screen-capture-logic-within-the-extension-component"></span>
## Step 3: Implement screen capture logic within the Extension component

Refer to the following code to implement the screen capture logic in the `SampleHandler.m` file. In the newly created target, Xcode will automatically create the `SampleHandler.h` file.

```objc
#import "SampleHandler.h"
#import <BytePlusRTCScreenCapturer/ByteRTCScreenCapturerExt.h>

@interface SampleHandler () <ByteRtcScreenCapturerExtDelegate>
@end

@implementation SampleHandler

- (void)broadcastStartedWithSetupInfo:(NSDictionary<NSString *,NSObject *> *)setupInfo {
    // Fill in the App Group ID 
    // NSString *groupId = @"xxxxxxxxx";
    // Start screen capture
    [[ByteRtcScreenCapturerExt shared] startWithDelegate:self groupId:groupId];
}

- (void)broadcastPaused {
    // User has requested to pause the broadcast. Samples will stop being delivered.
}

- (void)broadcastResumed {
    // User has requested to resume the broadcast. Samples delivery will resume.
}

- (void)broadcastFinished {
    // User has requested to finish the broadcast. End screen capture
    [[ByteRtcScreenCapturerExt shared] stop];
}

- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType {
    switch (sampleBufferType) {
        // Captured screen video stream
        case RPSampleBufferTypeVideo:
        // Acquired device audio stream
        case RPSampleBufferTypeAudioApp:
            [[ByteRtcScreenCapturerExt shared] processSampleBuffer:sampleBuffer withType:sampleBufferType];
            break;
        case RPSampleBufferTypeAudioMic:
            // Acquired microphone audio stream
        break;

        default:
            break;
    }
}
#pragma mark - ByteRtcScreenCapturerExtDelegate
// Notify the Broadcast Upload Extension to stop capturing the screen.

- (void)onQuitFromApp {
    NSDictionary *dic = @{
        NSLocalizedFailureReasonErrorKey: @"You stopped screen sharing"};
    NSError *error = [
    NSError *errorWithDomain:RPRecordingErrorDomain
                        code:RPRecordingErrorUserDeclined
                    userInfo:dic];
    [self finishBroadcastWithError:error];
}
@end
```


<span id="step-4-set-the-app-group-id-for-rtcengine"></span>
## Step 4: Set the App Group ID for RTCEngine

After creating the RTC engine instance, call the [setExtensionConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setextensionconfig) method and provide the App Group ID created in step 1. This allows your app to respond to screen sharing requests initiated from the system's Control Center.

```objc
(void)initEngineAndJoinRoom{
    // Create an engine.
    self.rtcEngine = [ByteRTCEngine createRTCEngine:APPID delegate:self parameters:@{}];
    // Fill in the App Group ID created in the above step.
    [self.rtcEngine setExtensionConfig:APP_GROUP];
}
```


<span id="step-5-call-the-rtc-apis-to-share-your-screen"></span>
## Step 5: Call the RTC APIs to share your screen.

<span id="internal-capture"></span>
### Internal capture


1. [Optional] Set encoding parameters

   If the default encoding parameters do not meet your requirements, you can set encoding parameters through the [setVideoEncoderConfig](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setvideoencoderconfig) method before starting screen capture.

   * When RTC scales the screen source, it does not change the original aspect ratio. When the width and height are inconsistent with the source resolution:

      * If the source resolution is greater than the target resolution, the recorded video will be proportionally scaled down.

      * If the source resolution is smaller than the target resolution, the recording resolution remains unchanged.

   * When both width and height are the default value `0`, the recording resolution remains unchanged. However, if the longer side of the screen's physical resolution exceeds `1920` px, the video is proportionally scaled down so that its longer side is `1920` px.

2. Start screen capture

   Option 1: Start the capture by adding the following code sample.

   ```objc
   (void)startScreenShare {
   // Set screen streaming video parameters (optional)
   ByteRTCScreenVideoEncoderConfig * config = [[ByteRTCScreenVideoEncoderConfig alloc] init];
       config.width = 360;
       config.height = 640;
       config.frameRate = 15;
       config.maxBitrate = 500000;
       config.minBitrate = 0;
       [self.rtcEngine setVideoEncoderConfig:config];
   // Start screen sharing, choose to capture audio and video at the same time, or only capture audio/video, bundleId is the Bundle Identifier
       [self.rtcEngine startScreenCapture:ByteRTCScreenMediaTypeVideoAndAudio bundleId:EXTENSION_BUNDLE_ID];
   }
   ```
   

   Option 2: Initiate from the system control center.

   1. While your application is running, navigate to the **Control Center** of your iOS device, long press the **Screen Recording** button.

   2. Select your application, and tap the **Start Recording** option to start broadcasting your screen.

      <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/advancedFeatures/ScreenSharing/61a73d1b-57d0-4870-913d-c61bdd571144.png) </span>


<span id="for-custom-video-sources"></span>
### For custom video sources

We recommend using the RTC SDK to capture audio and video. To use custom audio and video sources in screen\-sharing:


1. Capture audio and video from custom sources.

2. Switch the screen\-sharing source to a custom screen recorder.

   * Call [setScreenAudioSourceType:](https://docs.byteplus.com/en/docs/12/docs-70086#setscreenaudiosourcetype) to set the screen\-sharing audio source.

   * Call [setVideoSourceType:WithStreamIndex:](https://docs.byteplus.com/en/docs/12/docs-70086#setvideosourcetype-withstreamindex) to set the screen\-sharing video source.

3. Call [pushScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#pushscreenaudioframe) and [pushScreenVideoFrame:time:rotation:](https://docs.byteplus.com/en/docs/12/docs-70086#pushscreenvideoframe-time-rotation) to push the captured audio and video frames to the RTC SDK for encoding and transmission.


<span id="publishing-screen-stream"></span>
### Publishing screen stream

[Optional] On the local client, implement the `onVideoDeviceStateChanged` callback method. This step does not require calling APIs related to screen capture, only updating the relevant UI.

```objc

- (void)rtcEngine:(ByteRTCVideo *)engine onVideoDeviceStateChanged:(NSString *)device_id device_type:(ByteRTCVideoDeviceType)device_type device_state:(ByteRTCMediaDeviceState)device_state device_error:(ByteRTCMediaDeviceError)device_error {
    if (device_type == ByteRTCVideoDeviceTypeScreenCaptureDevice && self.preJoinSetting.isScreenShare) {
        if (device_state == ByteRTCMediaDeviceStateStarted) {
            // Publish screen-sharing stream
            [_rtcRoom publishScreen:ByteRTCMediaStreamTypeBoth];dispatch_async(dispatch_get_main_queue(), ^{
                self.localView.uid = @"Sharing screen";
                self.screenShareBtn.selected = YES;
                self.screenShareBtn.imageView.backgroundColor = UIColor.clearColor;
            });
        } else if (device_state == ByteRTCMediaDeviceStateStopped ||
                   device_state == ByteRTCMediaDeviceStateRuntimeError) {
            // Stop publish screen-sharing stream
            [_rtcRoom unpublishScreen:ByteRTCMediaStreamTypeBoth];
            
            dispatch_async(dispatch_get_main_queue(), ^{
                self.localView.uid = @"Loading sharing screen.";
                self.screenShareBtn.selected = NO;
                self.screenShareBtn.imageView.backgroundColor = UIColor.lightGrayColor;
            });
}
```


<span id="rendering-screen-streams"></span>
### Rendering screen streams

You can use the `onUserPublishStreamVideo` and `onFirstRemoteVideoFrameDecoded` callbacks on the remote end to monitor video streams and screen sharing streams. It is recommended to set up video rendering in the `onFirstRemoteVideoFrameDecoded` callback to ensure video rendering occurs after video decoding is complete, avoiding stuttering.

```objectivec
- (void)rtcEngine:(ByteRTCEngine * _Nonnull)engine onFirstRemoteVideoFrameDecoded:(NSString * _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info withFrameInfo:(ByteRTCVideoFrameInfo * _Nonnull)frameInfo {
    self.userIdStreamInfoMap[info.userId] = info; // Save stream-related information
    dispatch_async(dispatch_get_main_queue(), ^{
        UIView *view = [[UIView alloc] init];
        ByteRTCVideoCanvas *canvas = [[ByteRTCVideoCanvas alloc] init];
        canvas.view = view;
        canvas.renderMode = ByteRTCRenderModeHidden;
        [self.rtcEngine setRemoteVideoCanvas:streamId withCanvas:canvas];
        UserLiveView *liveView = [[UserLiveView alloc] init];
        liveView.uid = info.userId;
        liveView.view = view;
        [self.containerView.subviews append:liveView];
    });
}
- (void)rtcRoom:(ByteRTCRoom* _Nonnull)rtcRoom onUserPublishStreamVideo:(NSString* _Nonnull)streamId info:(ByteRTCStreamInfo* _Nonnull)info isPublish:(BOOL)isPublish {
    if (!isPublish) {
        [self.userIdStreamInfoMap[info.userId] removeObjectForKey:info.userId]; // Remove stream-related information
        dispatch_async(dispatch_get_main_queue(), ^{
            for (UserLiveView *liveView in self.containerView.subviews) {
                if ([userId isEqualToString:liveView.uid]) {
                    liveView.uid = @"";
                }
            }
        });
    }
}
```


<span id="stopping-screen-sharing"></span>
### Stopping screen sharing

```objectivec
- (void)stopScreenShare {
    // Stop using RTC SDK internal capture method to capture screen audio and video
    [self.rtcEngine stopScreenCapture];
}
```


<span id="faq"></span>
## FAQ

Q1: How can I prevent screen sharing from being interrupted when the app enters the background?

A1: Screen sharing relies on the main target process to publish media streams to the RTC server. We recommend playing a silent audio file in the background to keep the app process active.

Q2: How to import the RTC SDK as a package?

A2:

```ruby
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
target 'your target' do
  pod 'BytePlusRTC', '3.xx.x.xxx'
end

// Screen-sharing extension
target 'ScreenShareExtension' do
  use_frameworks!
  pod 'BytePlusRTC', '3.xx.x.xxx', :subspecs => ['ScreenCapture']
end
```


In the code above, "3.xx.x.xxx" is the version of the RTC SDK which you intend to integrate.

For details, see [Access the SDK through the package management tool](https://docs.byteplus.com/en/docs/12/docs-75707#ios).

<span id="api-reference"></span>
## API Reference


* [setExtensionConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setextensionconfig)

* [setVideoEncoderConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setvideoencoderconfig)

* [startScreenCapture:bundleId:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-startscreencapture-bundleid)

* [updateScreenCapture:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-updatescreencapture)

* [stopScreenCapture](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-stopscreencapture)

* [publishStreamVideo:](https://docs.byteplus.com/en/docs/12/docs-70086#publishstreamvideo)

* [publishStreamAudio:](https://docs.byteplus.com/en/docs/12/docs-70086#publishstreamaudio)

* [setScreenAudioSourceType:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-setscreenaudiosourcetype)

* [pushScreenAudioFrame:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-pushscreenaudioframe)


<span id="changelog"></span>
## Changelog

The SDK version at the time of this update is 3.50.1. If you are using a previous version of the SDK, please be aware of the following changes and adapt your code accordingly:


* V 3.60:

* The `createRTCVideo` method has been changed to `createRTCEngine`.

* The `publishScreen` and `unpublishScreen` interfaces have been removed. Use `publishStreamVideo` and `publishStreamAudio` to control audio and video publishing. After calling `startScreenCapture`, call `publishStreamVideo(true)` to start screen stream publishing.

* After the screen is ready, you will receive the `onVideoDeviceStateChanged` callback.

* The `onUserUnpublishScreen` callback has been removed. Use the `onUserPublishStreamVideo` callback instead. Check `streamInfo.isScreen` to identify screen streams.

* Version 3.50.3

   * The encoding parameter type name for screen sharing streams has been changed to `ByteRTCScreenVideoEncoderConfig`.

   * The interface names and behaviors related to custom screen streams have changed.

* Version 3.43.1

   * The publishScreen and unpublishScreen methods were moved from the `ByteRTCEngineKit` class to the `RTCRoom` class. Other specified methods were moved to the `RTCVideo` class.

   * The callback interface changed from `ByteRTCEngineDelegate` to `RTCVideoDelegate`.

* Version 3.36.1

   * The method for setting the encoding parameters for shared streams has been changed from `setVideoEncoderConfig:` to `SetScreenVideoEncoderConfig:`.

   * Parameters of the `PublishScreen:` API and others have changed.
