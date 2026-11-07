---
title: "Initializing the Player SDK for Flutter"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter"
---

Before you can use the features of the Player SDK for Flutter, you must initialize the SDK. This topic provides the necessary sample code and configuration steps to properly initialize the SDK with your app information and license, ensuring it is ready for playback.

<span id="e5519615"></span>
## Prerequisites


* You have integrated the Player SDK for Flutter. For more information, see [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter).

* You have obtained the app ID and other basic information. For more information, see [Getting your SDK license](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management).


<span id="7b6eeb47"></span>
## Importing the header file

```Dart
import 'package:byteplus_live/velive_flutter_sdk.dart';
```


<span id="249e3e10"></span>
## Initializing the SDK

To ensure correct initialization, we recommend initializing the SDK in the `runApp` method of your project's `main.dart`file.

```Java
TTSDKConfiguration config = TTSDKConfiguration(
  appID: 'APP_ID',// Replace APP_ID with the app ID.
  bundleID: 'BUNDLE_ID', // Replace BUNDLE_ID with the bundle identifier of the iOS app.
  appName: 'APP_NAME', // Replace APP_NAME with the app name.
  channel: 'CHANNEL_NAME', // Replace CHANNEL_NAME with the name of the channel through which to download the app, such as App Store.
  licenseFilePath: 'LICENSE_PATH', // Replace LICENSE_PATH with the path to your license file, such as assets/live.lic.
  appVersion: 'APP_VERSION',  // Replace APP_VERSION with the app version. A valid version number must contain at least two separators, such as 1.3.2.
);
VeLivePlayer.startWithConfiguration(config);
```


<span id="d5f62e90"></span>
## Next steps

For more information on how to use the Player SDK for Flutter, such as creating a player, starting playback, and configuring the video scaling mode, see [Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features).
