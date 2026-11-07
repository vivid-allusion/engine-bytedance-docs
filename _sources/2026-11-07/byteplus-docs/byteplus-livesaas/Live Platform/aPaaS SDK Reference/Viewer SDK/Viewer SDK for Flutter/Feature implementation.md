---
title: "Feature implementation"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation"
---

To integrate a full\-featured live room into your Flutter application, you can use the Viewer SDK. This guide provides detailed instructions and code examples for core operations such as joining and leaving a room, and setting status callbacks. It covers two primary implementation methods: using the default native page for a quick setup, or using Flutter widgets for a more customized user interface.


* To use the native page, refer to [Creating a default full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#a3d73eee).

* To display custom Flutter widgets, such as a shopping cart icon, refer to [Creating live room for displaying Flutter widgets](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#2cfaa0a8).


<span id="04caa314"></span>
## Prerequisites

You have integrated the Viewer SDK for Flutter. For more information, see [Integrating the Viewer SDK for Flutter](https://docs.byteplus.com/docs/byteplus-livesaas/integrating-the-viewer-sdk-for-flutter).

<span id="36efe78e"></span>
## Notes

Since errors may occur when using the simulator, we recommend that you use a real device for debugging.

<span id="dcbaa372"></span>
## Demo

Click [here](https://sf3-ttcdn-tos.pstatp.com/obj/bytelive-sdk/release/flutter/1.65.0/bdlive-flutter-viewer.zip) to download and view the sample code.

<span id="d301acbd"></span>
## Using the SDK

<span id="83a8d814"></span>
### Importing the header file

```Dart
import 'package:bdlive_flutter_viewer/bdlive_flutter_viewer.dart';
```


<span id="a4ab4a00"></span>
### Initializing the SDK

To ensure the SDK initializes in the correct sequence, we recommend initializing it using the `runApp` method in your project's `main.dart` file.

```Dart
TTSDKConfiguration config = TTSDKConfiguration(
  appID: 'APP_ID',// Replace APP_ID with the app ID you receive after successfully applying for a license. Contact BytePlus Live technical support to get the app ID. 
  bundleID: 'BUNDLE_ID', // Replace BUNDLE_ID with your iOS app's bundle identifier.
  appName: 'APP_NAME', // Replace APP_NAME with the app name you used to apply for the license. Contact BytePlus Live technical support to get the app name.
  channel: 'CHANNEL_NAME', // Replace CHANNEL_NAME with the channel where users download the app (e.g., App Store).
  vodLicenseFilePath: 'VOD_LICENSE_PATH', // Replace VOD_LICENSE_PATH with the path to your VOD license file (e.g., assets/vod.lic).
  liveLicenseFilePath: 'LIVE_LICENSE_PATH', // Replace LIVE_LICENSE_PATH with the path to your live streaming license file (e.g., assets/live.lic).
  appVersion: 'APP_VERSION',  // Replace APP_VERSION with your app's version. A valid version number must include at least two separators (e.g., 1.3.2).
);
BdliveViewerApi.startWithConfiguration(config);
```


<span id="a3d73eee"></span>
## Creating a default full\-featured live room

To use the native page, follow the instructions below to create the default full\-featured live room.

<span id="091832f4"></span>
### Joining a live room

The following sample code allows viewers to join a full\-featured live room and displays the full\-featured live room page in the app.

```Dart
/**
 * @param activity: The configuration required to join a live room.
 */
Future<bool> enterLiveRoom(BdlActivityConfig activity);
```


For more information, see [BdlActivityConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#5ed875e7).

<span id="eef486da"></span>
### Leaving a live room

Use the following sample code to leave the full\-featured live room when viewers exit your viewing page. If a floating player is displayed, it will also be destroyed.

```Dart
Future<void> leaveLiveRoom();
```


Use the following sample code to leave the full\-featured live room when viewers exit your viewing page. If a video is playing, the floating player will be displayed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For Android devices, the floating player will only be displayed if the viewer has granted overlay permissions to your app.</div>


```Dart
Future<void> manualClickLiveRoomExitBtn();
```


<span id="d7efb698"></span>
### Setting callbacks for live room status

Set callbacks for the live room status to listen for events on the full\-featured live room page.

```Dart
Future<void> setLiveRoomStatusListener(BdlLiveRoomStatusListener listener);
```


The callbacks for this implementation are as follows.

```Dart
class BdlLiveRoomStatusListener {
  /**
   * Callback triggered when the live room switches to the foreground.
   * @param activity: The information required to join a live room.
   */
  void Function(BdlActivityConfig activity)? onLiveRoomActivityResume;

  /**
   * Callback triggered when the live room switches to the background.
   * @param activity: The information required to join a live room.
   */
  void Function(BdlActivityConfig activity)? onLiveRoomActivityPause;

  /**
   * Callback triggered when the floating player is about to appear.
   * @param activity: The information required to join a live room.
   */
  void Function(BdlActivityConfig activity)? onFloatViewWillAppear;

  /**
   * Callback triggered when the floating player is about to disappear.
   * @param activity: The information required to join a live room.
   */
  void Function(BdlActivityConfig activity)? onFloatViewWillClose;
  
    /**
   * Callback triggered when both the live room page and floating player are destroyed.
   * @param activity: The information required to join a live room.
   */
  void Function(BdlActivityConfig activity)? onLiveRoomFullDestroyed;

    /**
     * Triggered when viewers tap product cards displayed under the menu, floating product cards, header ads, in-page ads, or floating ads that contain linked content.
     * @param url             The URL associated with the product card or ad.
     * @param type            The content type of the linked URL. See BdlViewerOpenUrlType.
     * @param enableFloating  A setting returned from the BytePlus Live server that indicates whether the content should be displayed as floating layer on the viewing page.
     *                        true  — Display as a floating layer.
     *                        false — Open in a new page.
     */
  void Function(String url, BdlViewerOpenUrlType type, bool enableFloating)? onOpenUrlCallback;
}
```


For more information, see [BdlActivityConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#5ed875e7), [BdlViewerOpenUrlType](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#0c2adc1a), and [Loading embedded links in product cards and ads](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#0257277a).

<span id="2cfaa0a8"></span>
## Creating live room for displaying Flutter widgets

To display custom Flutter widgets, such as a shopping cart icon in the full\-featured live room, refer to the steps below to build the live room using Flutter pages.

<span id="3e0c63ef"></span>
### Overall workflow

The following is the overall workflow for displaying a Flutter\-based live room when a user joins a full\-featured live room.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62a33c0d1ce2497182361d2613b5a27b~tplv-goo7wpa0wc-image.image) </span>

<span id="af9e0646"></span>
### Sample code

The overall implementation code is as follows.

```Dart
  /**
   * Implement the BdlLiveRoomStatusListener. For details, refer to the following section.
   */
class BdlLiveRoomStatusListenerExampleImpl implements BdlLiveRoomStatusListener {

  /**
   * Triggered when a logical entry into the live room is completed 
   * or when the user taps the PiP.
   *
   * Implement this callback to display the LivePullView.
   */
  void Function(BdlActivityConfig activity)? showLivePullView;

  /**
   * Triggered when the close button inside the live room is clicked.
   *
   * Implement this callback to hide the LivePullView.
   */
  void Function(BdlActivityConfig activity)? hideLivePullView;

  /**
   * Triggered when an ad or product card inside the live room is clicked.
   *
   * Implement this callback to perform custom redirection logic.
   */
  void Function(String url, BdlViewerOpenUrlType type, bool enableFloating)?
      onOpenUrlCallback;
}


// Create BdlActivityConfig
BdlActivityConfig activity = BdlActivityConfig(
  activityId: activityId,
  token: token,
  authMode: _authMode,
  isPortrait: _isPortrait,
);

// Create the BdlLiveRoomStatusListener
BdlLiveRoomStatusListenerExampleImpl bdlistener = BdlLiveRoomStatusListenerExampleImpl();

// Set the Listener
BdliveViewerApi.instance.setLiveRoomStatusListener(bdlistener);

// Logically enter the live room
BdliveViewerApi.instance.enterLiveRoomLogically(activity);

// If logical entry is successful
if (isPreLoadSuccess) {
  // showLivePullView of BdlLiveRoomStatusListener will be triggered.
  // Navigate to the live room page in showLivePullView.
} else {
  // Notify user of entry failure
  Fluttertoast.showToast(
    msg: "Join room failed",
  );
}
```


<span id="52b1fc4d"></span>
### Reference

<span id="3fa58b5b"></span>
#### Joining a live room logically

Use the following sample code to join a full\-featured live room logically without showing the live room page. For more information about `BdlActivityConfig`, see [BdlActivityConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#5ed875e7).

```Dart
/**
 * Enter the full-featured live room logically without showing the live room page.
 * @param activity: The information required to join a live room.
 */
Future<bool> enterLiveRoomLogically(BdlActivityConfig activity);
```


After viewers successfully join the live room, the SDK triggers `showLivePullView`. You must set this callback to display the live room page.

<span id="5a670dd9"></span>
#### Leaving a live room logically

Use the following sample code to leave the full\-featured live room logically when viewers exit your viewing page. If a floating player is displayed, it will also be destroyed. This method only performs a logical exit.

```Dart
/**
 * Leave the full-featured live room. If the floating player is currently displayed, it is also destroyed.
 */
Future<void> leaveLiveRoomLogically();
```


After viewers successfully leave the live room, the SDK triggers `hideLivePullView`. You must set this callback to hide the live room page.

<span id="328e5faf"></span>
#### Setting callbacks for live room status

Set callbacks for the live room to listen for events on the full\-featured live room page.

```Dart
Future<void> setLiveRoomStatusListener(BdlLiveRoomStatusListener listener);
```


For this implementation, use the following callbacks.

```Dart
/**
 * Triggered when a logical join to the live room is successful or when the viewer taps the PiP window.
 * Implement this callback to show the live pull view.
 *
 * @param activity  The configuration used when entering the live room.
 */
void Function(BdlActivityConfig activity)? showLivePullView;

/**
 * Triggered when the close button in the live room is clicked.
 * Implement this callback to hide the live pull view.
 *
 * @param activity  The configuration used when entering the live room.
 */
void Function(BdlActivityConfig activity)? hideLivePullView;

/**
 * Triggered when viewers tap product cards displayed under the menu, floating product cards, header ads, in-page ads, or floating ads that contain linked content.
 *
 * @param url             The URL associated with the product card or ad.
 * @param type            The content type of the linked URL. See BdlViewerOpenUrlType.
 * @param enableFloating  A setting returned from the BytePlus Live server that indicates whether the content should be displayed as a floating layer on the viewing page.
 *                        true  — Display as a floating layer.
 *                        false — Open in a new page.
 */
void Function(String url, BdlViewerOpenUrlType type, bool enableFloating)?
    onOpenUrlCallback;
```


For more information, see [BdlActivityConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#5ed875e7) and [BdlViewerOpenUrlType](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#0c2adc1a).

<span id="cb42f54a"></span>
#### Displaying the live room page

The SDK triggers showLivePullView callback when enterLiveRoomLogically succeeds or when the user taps the PiP image. When this callback is triggered, you must display the live room page.

Meanwhile, to prevent launching the live room page multiple times, first check whether the current live room page already exists in the navigation back stack by using `isLiveRoomRouteInStack`. For details on `isLiveRoomRouteInStack`, see [isLiveRoomRouteInStack()](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#0e6a994e).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3e4b68149134a07b02d9f3bde0b33a0~tplv-goo7wpa0wc-image.image) </span>

The example code for displaying the live room page is as follows:

```Dart
// Check whether the live room page exists in the back stack
if (isLiveRoomRouteInStack()) {
    // If the live room page is in the back stack, directly popUntil the live room page
    navigatorKey.currentState!.popUntil((route) {
        return route.settings.name == 'LiveRoomPage';
    });
    return;
}


// If the live room page is not in the back stack, create the live room page
// Initialize the full live room page
_livePullRoute = MaterialPageRoute(
    builder: (context) {
        // Initialize the BuildContext of the full live room page
        _liveRouteContext = context;
        return const LiveRoomPage();
    },
    settings: const RouteSettings(name: 'LiveRoomPage'),
);


// Push the live room page onto the navigation stack
navigatorKey.currentState!.push(_livePullRoute!);
```


The following example shows how to display a `MaterialPageRoute` containing a `BdlLivePullView` and a leave button in the `showLivePullView` callback.

```Dart
showLivePullView: (activity) {
  debugPrint('showLivePullView...$activity');
  _livePullRoute = MaterialPageRoute(
    builder: (context) {
      MediaQueryData mediaQueryData = MediaQuery.of(context);
      return SizedBox(
        width: mediaQueryData.size.width,
        height: mediaQueryData.size.height,
        child: Stack(
          children: [
            BdlLivePullView(
              onPlatformViewCreated: () {
              },
            ),
            // Floating window button - blue background, black text, with the content "Leave"
            Positioned(
              bottom: 200,
              left: 20,
              child: ElevatedButton(
                style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.blue,
                  padding: const EdgeInsets.symmetric(horizontal: 20, vertical: 10),
                  shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(20),
                  ),
                ),
                onPressed: () {
                  BdliveViewerApi.instance.leaveLiveRoomLogically();
                },
                child: const Text(
                  'Exit',
                  style: TextStyle(
                    color: Colors.black,
                    fontSize: 16,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
            ),
          ],
        ),
      );
    },
  );
  Navigator.of(context).push(_livePullRoute);
}
```


<span id="727aae89"></span>
#### Hiding the live room page

The SDK triggers `hideLivePullView` callback when the user leaves the current live room page. When this callback is triggered, you must hide the live room page. Refer to the following workflow and sample code to hide the live room page. For details, see [isLiveRoomRouteInStack()](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#0e6a994e) and [isLiveRoomRouteAtTop()](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-feature-implementation#b1402c5d).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/decdcb7d60a642eca90c2a5a43acf4eb~tplv-goo7wpa0wc-image.image) </span>

```Dart
// Check if the current live room page exists
if (_livePullRoute != null) {
  try {
    // If the current live room is at the top (currently displayed page)
    if (isLiveRoomRouteAtTop()) {
      // Pop directly to exit the live room page
      navigatorKey.currentState!.pop();

    // If the live room page exists in the navigation stack
    } else if (isLiveRoomRouteInStack()) {
      // Remove the live room page from the stack
      navigatorKey.currentState!.removeRoute(_livePullRoute!);
    }

    // Reset the BuildContext of the current live room page
    _liveRouteContext = null;

    // Reset the current live room page route
    _livePullRoute = null;

  } catch (e) {
    debugPrint('Failed to remove LiveRoom route: $e');

    // Ensure references are reset even on error
    _liveRouteContext = null;
    _livePullRoute = null;
  }
}
```


The following example shows how to remove the `BdlLivePullView` from the `Navigator` in the `hideLivePullView` callback.

```Dart
hideLivePullView: (activity) {
  debugPrint('hideLivePullView...$activity');
  Navigator.of(context).removeRoute(_livePullRoute);
},
```


<span id="0e6a994e"></span>
#### `isLiveRoomRouteInStack()`

This function checks if the LiveRoom route is in the navigation stack.

```Dart
  // Check if the LiveRoom route is in the navigation stack
  bool isLiveRoomRouteInStack() {
    try {
      // Use ModalRoute.of to get the route associated with the context
      final modalRoute = ModalRoute.of(_liveRouteContext!);
      // If modalRoute is not null and isActive is true, the route is in the stack
      return modalRoute != null && modalRoute.isActive;
    } catch (e) {
      // Catch possible exceptions, such as context being invalid
      debugPrint('Error checking if LiveRoom route is in stack: $e');
      return false;
    }
  }
```


<span id="b1402c5d"></span>
#### `isLiveRoomRouteAtTop()`

This function checks if the LiveRoom route is at the top of the navigation stack.

```Dart
 // Check if LiveRoom route is at the top of navigation stack
  bool isLiveRoomRouteAtTop() {
    try {
      // Use ModalRoute.of to get the route associated with the context
      final modalRoute = ModalRoute.of(_liveRouteContext!);
      // If modalRoute is not null and isCurrent is true, the route is at the top
      return modalRoute != null && modalRoute.isCurrent;
    } catch (e) {
      // Catch possible exceptions, such as context being invalid
      debugPrint('Error checking if LiveRoom route is at top: $e');
      return false;
    }
  }
```


<span id="035741d0"></span>
## Custom configuration

<span id="2519a643"></span>
### Autoplay

By default, the player will automatically play a video when viewers join the full\-featured live room if the live room is in the **Live**, **Preview**, or **Playback** status.

Use the following sample code to disable the autoplay feature.

```Dart
BdLiveViewerConfig config = BdliveViewerApi.instance.getLiveRoomConfig();
// Do not play the live video automatically if the live room is in the Live status.
config.playerConfig.liveAutoPlay = false;
// Do not play the preview automatically if the live room is in the Preview status and a preview is available.
config.playerConfig.previewAutoPlay = false;
// Do not play the playback automatically if the live room is in the Playback status.
config.playerConfig.replayAutoPlay = false;
BdliveViewerApi.instance.setLiveRoomConfig(config);
```


For more information, see [BdLiveViewerConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#4b59aa3f).

<span id="5d59daf1"></span>
### PiP

By default, a video will be displayed in picture\-in\-picture (PiP) mode when viewers leave the live room, open a new page by tapping a URL (including URLs embedded in product cards and ads), or move the app to the background.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Viewers must enable the floating window permission on their Android devices to use the PiP feature.</div>


Use the following sample code to configure the PiP feature. You can disable it only when a viewer leaves the room, or disable it in all scenarios (leaving the room, opening a new page, or moving the app to the background).

```Dart
BdLiveViewerConfig config = BdliveViewerApi.instance.getLiveRoomConfig();
// Disable the PiP feature when viewers leave the live room, open a new page by tapping a URL (including URLs embedded in product cards and ads), or move the app to the background.
config.playerConfig.enablePIP = false;
// Only disable the PiP feature when viewers leave the live room.
config.playerConfig.enablePIPWhenExit = false;
BdliveViewerApi.instance.setLiveRoomConfig(config);
```


For more information, see [BdLiveViewerConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#4b59aa3f).

<span id="0257277a"></span>
### Loading embedded links in product cards and ads

The SDK triggers `onOpenUrlCallback` when viewers tap product cards displayed under the menu, floating product cards, header ads, in\-page ads, or floating ads that have embedded links. To load these links, refer to the steps and code below.


1. Use the `onOpenUrlCallback` to listen for viewer taps.

2. Implement custom redirection logic or call the SDK's `openUrl` API to execute the default redirection behavior. For more information, see [BdlViewerOpenUrlType](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#0c2adc1a).


```Dart
// Use the onOpenUrlCallback to listen to viewer taps
onOpenUrlCallback = (url, type, enableFloating) {
  // Implement custom redirection logic
  if (usingCustomPage) {
    // Navigate to the custom product detail page
    navigator.push(
      ProductDetailPage(
        url: url,
        type: type,
        enableFloating: enableFloating,
      ),
    );
  } else {
    // Use the SDK built-in API to open the URL
    BdliveViewerApi.instance.openUrl(url, type, enableFloating);
  }
};
```


The description of `onOpenUrlCallback` is as follows:

```Dart
/**
 * Triggered when viewers tap product cards displayed under the menu, floating product cards, header ads, in-page ads, or floating ads that contain linked content.
 * @param url             The URL associated with the product card or ad.
 * @param type            The content type of the linked URL. See BdlViewerOpenUrlType.
 * @param enableFloating  A setting returned from the BytePlus Live server that indicates whether the content should be displayed as floating layer on the viewing page.
 *                        true  — Display as a floating layer.
 *                        false — Open in a new page.
 */
void Function(String url, BdlViewerOpenUrlType type, bool enableFloating)?
    onOpenUrlCallback;
```


The description of `openUrl` is as follows:

```Dart
/**
 * Opens the content associated with the embedded link configured for a product card or ad.
 *
 * @param url             The embedded URL configured for the product card or ad.
 * @param type            The content type of the embedded URL. See BdlViewerOpenUrlType.
 * @param enableFloating  Whether the content should be displayed as a floating layer on the viewing page.
 *                        true  — Display the content as a floating layer, i.e., open a WebView window within the full-featured live room page to show the linked content.
 *                        false — Open the content in a new page using the app’s DeepLink mechanism to navigate to the appropriate page.
 */
Future<void> openUrl(String url, BdlViewerOpenUrlType type, bool enableFloating);
```
