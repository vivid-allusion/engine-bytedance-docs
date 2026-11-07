---
title: "iOS Player SDK: Picture-in-picture"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-picture-in-picture"
---

Picture\-in\-picture (PiP) allows users to continue watching a video in a small floating window while using other apps. BytePlus VOD Player SDK provides native PiP APIs for this purpose.

<span id="prerequisites"></span>
## Prerequisites


* **System version**: iOS 15.0 or later.

* **SDK version**: Player SDK 1.51.200.4 or later.


<span id="project-configuration"></span>
## Project configuration

Enable the background mode required for PiP in Xcode:


1. Select your app's target.

2. Click the **Signing & Capabilities** tab.

3. Click  **+ Capability** and add **Background Modes**.

4. Select **Audio, AirPlay, and Picture in Picture**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09881e13481b426ba8bb939d65c27ca5~tplv-goo7wpa0wc-image.image) </span>

<span id="device-configuration"></span>
## Device configuration

To automatically start PiP when the app enters the background, instruct users to go to **Settings \> General \> Picture in Picture** on their device and enable **Start PiP Automatically**.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260723100816-861663214037.png) </span>

<span id="implementation"></span>
## Implementation

<span id="step-1-check-whether-the-device-supports-pip"></span>
### Step 1: Check whether the device supports PiP

Call `isPictureInPictureSupported` to check whether the current device supports PiP.

```objectivec
if ([TTVideoEngine isPictureInPictureSupported]) {
    // The current device supports PiP.
}
```


<span id="step-2-enable-pip"></span>
### Step 2: Enable PiP

PiP is disabled by default. After creating a `TTVideoEngine` instance, set `enablePictureInPicture` to `YES`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">PiP is supported only for instances created with the SDK's proprietary player and is not supported for the system player. Set <code>initWithOwnPlayer:</code> to <code>YES</code>.</div>


```objectivec
TTVideoEngine *player = [[TTVideoEngine alloc] initWithOwnPlayer:YES];
player.enablePictureInPicture = YES;
```


<span id="step-3-configure-pip-behavior-when-the-app-enters-the-background"></span>
### Step 3: Configure PiP behavior when the app enters the background

The SDK allows PiP to start automatically when the app enters the background by default. The user must also enable **Start PiP Automatically** on the device. If you do not want PiP to start automatically when the app enters the background, set `canStartPictureInPictureAutomaticallyFromInline` to `NO`. This setting does not change the system PiP setting on the device.

```objectivec
player.canStartPictureInPictureAutomaticallyFromInline = NO;
```


<span id="step-4-manually-start-or-stop-pip"></span>
### Step 4: Manually start or stop PiP

```objectivec
// Manually start PiP.
[player startPictureInPicture];

// Manually stop PiP.
[player stopPictureInPicture];
```


<span id="step-5-query-the-pip-status"></span>
### Step 5: Query the PiP status

Call `isPictureInPictureStarted` to check whether PiP is active.

```objectivec
BOOL isPictureInPictureStarted = [TTVideoEngine isPictureInPictureStarted];
```


<span id="optional-configuration"></span>
### Optional configuration

<span id="set-custom-pip-delegates"></span>
#### Set custom PiP delegates

To listen for events such as PiP starting and stopping, implement the following delegates. The SDK already handles the required PiP delegate methods, so you do not need to implement them in most scenarios.

```objectivec
@property (nonatomic, weak, nullable) id<AVPictureInPictureControllerDelegate> pictureInPictureDelegate;
@property (nonatomic, weak, nullable) id<AVPictureInPictureSampleBufferPlaybackDelegate> pictureInPicturePlaybackDelegate;
```


<span id="update-the-pip-playback-progress"></span>
#### Update the PiP playback progress

To actively update the playback progress in the PiP window, call `invalidatePictureInPicturePlaybackState`. The SDK already handles the required progress updates, so you do not need to call this method in most scenarios.

```objectivec
[player invalidatePictureInPicturePlaybackState];
```
