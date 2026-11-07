---
title: "Flutter Player SDK: Picture-in-picture"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-picture-in-picture"
---

The Player SDK includes a picture\-in\-picture (PiP) feature, allowing users to watch video in a floating window while using other apps. This guide explains how to implement the two available modes:


* **Manual mode:**  This mode is **user\-initiated**. Typically, you provide a PiP button in the player UI. When the user taps this button, the video window shrinks and floats on the screen. To implement this, you must call the SDK's API to start PiP in response to the user's action.

* **Automatic mode:**  This mode is **system event\-driven**. When a video is playing and the user moves the app to the background (such as by pressing the Home button), the video automatically transitions into PiP mode without interrupting playback. To implement this, you must first enable the automatic mode via the SDK's API and then handle app lifecycle events.


<span id="8d55d220"></span>
## Prerequisites

Before integrating the PiP feature, ensure your project meets the requirements for each platform.

<span id="82b9b6fd"></span>
### Android

**System permissions**: PiP requires the "**Display over other apps**" (`SYSTEM_ALERT_WINDOW`) permission.


* If you call the `startPictureInPicture` method without this permission, the SDK will automatically redirect the user to the system's authorization page. After the user grants permission and returns to the app, the SDK attempts to enable PiP again.

* Alternatively, you can proactively guide the user to grant this permission by calling the `requestOverlayPermission` method.


<span id="2241690d"></span>
### iOS


* **Project configuration:**  In your Xcode project, you must enable the **Audio, AirPlay, and Picture in Picture** background mode. Follow these steps:

   1. In Xcode, select your app's Target.

   2. Click the **Signing & Capabilities** tab.

   3. Click the  **+ Capability** button, add the **Background Modes** capability, and check the box for **Audio, AirPlay, and Picture in Picture**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09881e13481b426ba8bb939d65c27ca5~tplv-goo7wpa0wc-image.image) </span>

* **System requirements:** 

   * Device OS version: iOS 15 or later.

   * System PiP setting: Ensure the user has enabled the **Start PiP Automatically** switch in the device's **Settings \> General \> Picture in Picture** menu.


<span id="8d80f760"></span>
## (Android only) Requesting permission

For a better user experience, it is recommended to proactively guide the user to grant the "**Display over other apps**" permission before the user starts PiP, rather than relying on the passive, automatic redirection.

```Dart
// This call redirects the user to the system settings page for manual authorization.
await VodPlayerFlutter.requestOverlayPermission();
```


<span id="95042915"></span>
## Enabling PiP manually

This mode is typically triggered by a button in the player UI.

```Dart
// 1. Check if the device supports PiP
bool isSupported = await player.isPictureInPictureSupported();
if (!isSupported) {
  // PiP is not supported; you can show an alert or disable the button.
  print("PiP is not supported on this device.");
  return;
}

// 2. Start PiP (can be called in a button's onTap handler)
// PiP can only be started successfully during video playback.
bool success = await player.startPictureInPicture();
if (!success) {
  print("Failed to start PiP.");
}

// 3. Stop PiP (can be called when returning to the app or through other interactions)
await player.stopPictureInPicture();
```


<span id="ec8d5078"></span>
## Enabling automatic PiP

Automatic PiP allows the video to continue playing in a floating window when the app transitions from the foreground to the background.

<span id="75a42a4a"></span>
### Step 1: Enable automatic PiP mode in the SDK (Android and iOS)

You need to listen for the player's `playbackStateDidChange` event. After playback begins, call `enableAutoBackgroundPictureInPicture` to enable the automatic PiP mode.

```Dart
player.playbackStateDidChange = (TTVideoEnginePlaybackState playbackState) {
  switch (playbackState) {
    case TTVideoEnginePlaybackState.playing:
      // Assuming `enablePIPBackgroundAuto` is a global flag in your app to control this feature
      if (enablePIPBackgroundAuto) {
        // Call this after playback starts to notify the SDK to enable automatic PiP mode
        player.enableAutoBackgroundPictureInPicture(true);
      }
      break;
    default:
      break;
  }
};
```


<span id="97e0f80a"></span>
### Step 2: Listen for app lifecycle and trigger PiP (Android Only)

Unlike on iOS, on Android you must manually call `startPictureInPicture` when the app enters the background.

```Dart
@override
void didChangeAppLifecycleState(AppLifecycleState state) {
  super.didChangeAppLifecycleState(state);
  if (!mounted) return;
  
  if (state == AppLifecycleState.resumed) {
    // When the app is resumed (returns to the foreground)
    if (GlobalConfiguration.enablePIPBackgroundAuto) {
      _player.stopPictureInPicture();
    }
  } else if (state == AppLifecycleState.paused) {
    // When the app is paused (enters the background)
    if (GlobalConfiguration.enablePIPBackgroundAuto && Platform.isAndroid) {
      // Manually call startPictureInPicture
      _player.startPictureInPicture();
    }
  }
}
```
