---
title: "React Native Player SDK: Picture-in-picture"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-pip"
---

Picture\-in\-Picture (PiP) is a multi\-window mode that allows users to watch videos in a small window in one corner of the screen while continuing to interact with other apps or content on the main screen. The Player SDK supports the following two PiP implementation modes to accommodate different business scenarios:


* **Manual mode**: Triggered explicitly by the user. Typically, the player UI provides a “Picture\-in\-Picture” or “Mini Player” button. After the user taps the button, the video window shrinks and floats on the screen. Developers need to call the SDK API to start PiP when the user taps the button.

* **Automatic mode**: Triggered by system events. In this mode, the app can enter PiP automatically when it moves to the background. This is not a built\-in automatic behavior of the SDK. Instead, developers need to listen for app lifecycle events, such as the app entering the background, and explicitly call the API to start PiP.


<span id="897d8db7"></span>
## Compatibility and prerequisites

Before integrating PiP, make sure your project meets the prerequisites for the target platform.

<span id="9bd92c5a"></span>
### Android


* **Floating PiP (** **`type: 'floating'`**  **)** :

   * **Minimum OS version**: Android 6.0 (API 23) or later.

   * **Permission requirement**: The app must have the **Display over other apps** permission.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If <code>startPictureInPicture</code> is called before the app has been granted permission, the SDK automatically redirects the user to the system authorization page.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You can also call <code>requestOverlayPermission</code> to proactively guide the user through authorization. For details, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-pip#41c04eac">Request permissions (Android only)</a>.      </div>
      

* **System PiP (** **`type: 'system'`**  **)** :

   * **Minimum OS version**: Android 8.0 (API 26) or later.

   * **Permission requirement**: Declare PiP support in `AndroidManifest.xml`:

      ```XML
      <activity
          android:name=".MainActivity"
          android:supportsPictureInPicture="true"
          android:configChanges="screenSize|smallestScreenSize|screenLayout|orientation"
          ... />
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">It is recommended to configure <code>configChanges</code> to prevent the Activity from being recreated when entering or exiting PiP.      </div>
      

   * **Automatic system entry** (via `enableAutoStartPictureInPicture()`): To enter system PiP automatically in supported scenarios, Android 12 (API 31) or later is required.


<span id="acf053ad"></span>
### iOS


* **OS version**: iOS 15 or later.

* **Project configuration**: In your Xcode project, you must enable the **Audio, AirPlay, and Picture in Picture** background mode. Follow these steps:

   1. Select the app target in Xcode.

   2. Click the **Signing & Capabilities** tab.

   3. Click  **+ Capability** to add **Background Modes**. Select **Audio, AirPlay, and Picture in Picture**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09881e13481b426ba8bb939d65c27ca5~tplv-goo7wpa0wc-image.image) </span>


**System PiP setting**: Make sure the user has toggled on **Start PiP Automatically** on the device at **Settings** \> **General** \> **Picture in Picture**.

<span id="41c04eac"></span>
## Request permissions (Android only)

For a better user experience, it is recommended that you proactively request overlay permission before the user taps the PiP button, rather than triggering the permission flow after the user action.

```TypeScript
import { requestOverlayPermission } from '@byteplus/react-native-vod-player';

// Redirects the user to the system settings page for manual authorization
requestOverlayPermission();
```


<span id="5555b19a"></span>
## Configure PiP

It is recommended to configure PiP as early as possible after player initialization.

```TypeScript
import { configurePictureInPicture } from '@byteplus/react-native-vod-player';

configurePictureInPicture({
  type: 'floating',            // Android: 'floating' | 'system', default is 'floating'
  syncPlayerViewConfig: false, // Whether to sync the player view configuration
});
```


**Parameter description**:


* `type`: The PiP type on Android. Valid values are `'floating'` for Floating PiP and `'system'` for System PiP. The default value is `'floating'`. For the difference between the two modes, see [PiP types on Android](https://docs.byteplus.com/docs/byteplus-vod/docs-rn-player-pip#6fa66e8b). This parameter is ignored on iOS.

* `syncPlayerViewConfig`: Whether to sync the player view configuration. When set to `true`, the PiP window keeps the same aspect ratio and content scaling mode as the player view as much as possible.


<span id="952c6ddb"></span>
## Start PiP manually

<span id="18053796"></span>
### Step 1: Set the global listener callback

It is recommended to register the listener during app initialization or when the playback page is mounted, so that the app UI state can stay in sync.

```TypeScript
import { setPictureInPictureListener } from '@byteplus/react-native-vod-player';

setPictureInPictureListener({
  onStartPictureInPicture() {
    console.log('PiP started');
  },
  onStopPictureInPicture() {
    console.log('PiP stopped');
  },
  onError(code, extraData) {
    // Error codes: 0 = success, 1 = not supported, 2 = invalid parameter, 3 = already started
    console.log(`Failed to start PiP: ${code}, ${extraData}`);
  },
  onClickPictureInPictureRestoreBtn() {
    // Triggered when the user taps the restore button in the top-right corner of the PiP window
    console.log('Restoring from PiP to the app');
  },
});
```


<span id="0f07c8e8"></span>
### Step 2: Call the start API

During video playback, call the player instance method.

```TypeScript
// 1. Check whether the current environment supports PiP
import { isPictureInPictureSupported } from '@byteplus/react-native-vod-player';
const isSupport = isPictureInPictureSupported();

if (isSupport) {
  // 2. Start PiP (available only during playback)
  player.startPictureInPicture();
}

// 3. Stop PiP (or return to the original page)
player.stopPictureInPicture();
// Or call stopPictureInPictureGlobal to stop PiP without relying on a player instance
// stopPictureInPictureGlobal();
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning"><code>startPictureInPicture</code> can be called only during playback. PiP cannot be started when playback is inactive.</div>


* <div data-tips="true" data-tips-type="warning">PiP is a global singleton. Multiple PiP windows cannot be started at the same time.</div>


* <div data-tips="true" data-tips-type="warning">After the user taps the close button on the PiP window, the SDK pauses the current video by default.</div>


* <div data-tips="true" data-tips-type="warning">You can call <code>isPictureInPictureStarted()</code> at any time to check whether PiP is currently active.</div>


* <div data-tips="true" data-tips-type="warning">The first time Floating PiP is started on Android, the Overlay permission dialog may appear. You can call <code>requestOverlayPermission</code> in advance to prompt the user to grant the required permission.</div>


* <div data-tips="true" data-tips-type="warning">Android System PiP cannot be forced to exit immediately through <code>stopPictureInPicture</code>. In most cases, PiP stops automatically when the user returns to the app.</div>



<span id="b3a71b65"></span>
## Start PiP automatically

This section describes how to start PiP automatically when the app moves from the foreground to the background. This feature requires app lifecycle handling in your integration.

<span id="e5420da0"></span>
### Step 1: Enable the SDK auto PiP configuration

After the player is created, call the following API to allow the app to trigger PiP logic in the background.

```TypeScript
// Allow the app to start PiP automatically after moving to the background
player.enableAutoStartPictureInPicture();
```


<span id="9ff2ca26"></span>
### Step 2: Listen to app lifecycle events and trigger PiP manually

If `configurePictureInPicture` is not called to switch the Android PiP type, Floating PiP is used by default. Due to system limitations, the SDK cannot directly detect when the app moves to the background. Therefore, the key to automatic PiP is to listen to app state changes through React Native `AppState` and explicitly call the PiP API when the app enters the background.

```JavaScript
import { AppState } from 'react-native';

useEffect(() => {
  const subscription = AppState.addEventListener('change', nextAppState => {
    if (nextAppState === 'background') {
      // The app enters the background and PiP is triggered explicitly
      player.startPictureInPicture();
    } else if (nextAppState === 'active') {
      // The app returns to the foreground and PiP is usually stopped to restore full-screen playback
      player.stopPictureInPicture();
    }
  });

  return () => {
    subscription.remove();
  };
}, []);
```


<span id="db0ae47b"></span>
## Enable PiP in feed scenarios

In feed scenarios, where users swipe vertically to switch between videos, you can implement seamless playback switching inside the PiP window by following these steps:


1. **Destroy the previous player instance**: When calling `close`, pass `{stopPip: false}` so that the player instance is destroyed while the current PiP window remains open.

2. **Create the next player instance**: After switching to the next video, immediately call `startPictureInPicture` on the new player instance to take over the existing PiP window.


```TypeScript
// 1. Stop and destroy the current player instance while keeping the PiP window open
lastPlayer.close({ stopPip: false });

// 2. Let the new player instance take over the PiP window and continue playback
nextPlayer.startPictureInPicture();
nextPlayer.play();
```


<span id="7b409abc"></span>
## Appendix

<span id="6fa66e8b"></span>
### PiP types on Android

On Android, the SDK provides two PiP implementations:


* **Floating PiP**: This mode is implemented using an overlay window. This is the default mode and requires the user to grant overlay permission.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/df641c03f9f7486683c5ad217171207a" width="250px" />   </div>
   

* **System PiP**: This mode is implemented using the [Android Activity system PiP mode](https://developer.android.com/develop/ui/views/picture-in-picture). This mode provides smoother system transition animations, and the app moves to the background after PiP starts.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/51c4be77be824810afb2b4471e3dd4c3" width="250px" />   </div>
