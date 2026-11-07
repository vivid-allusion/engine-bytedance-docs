---
title: "Flutter Player SDK: Playing DRM encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-playing-drm-encrypted-videos"
---

To play DRM (Digital Rights Management) encryption videos in your Flutter application for copyright protection, you can use the BytePlus Player SDK. This guide provides the prerequisites and a step\-by\-step implementation, including code examples, for playing HLS DRM\-encrypted videos in Vid mode.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Flutter SDK only supports playing HLS DRM\-encrypted videos in Vid mode.</div>


<span id="333bf642"></span>
## Prerequisites


* Configure the DRM licenses and encrypt your content in the BytePlus VOD console. For details, see [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption).

* To play DRM\-encrypted videos in Vid mode, your application server must generate a temporary playback token and a DRM license auth token and provide them to the client before playback. You can use the BytePlus VOD Server SDKs to generate these tokens. For more information, see the following documentation:

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

* To play DRM encrypted video on iOS, you need to get a FairPlay streaming certificate from Apple. For details, see [Getting a FairPlay certificate from Apple](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-fairplay-certificate). You can download your FairPlay certificate to your local device and save it in your project's sandbox directory.

* Integrate Player SDK version 1.44.3\-3 or later.


<span id="03b71671"></span>
## Implementation


1. (Android only) Check if the device supports DRM:

   ```Dart
   bool? isDeviceSupportDrm = await FlutterTTSDKManager.isDeviceSupportDrm();
   ```
   

2. (Android only) When creating `TTVideoPlayerView` on Android, use `NativeViewType.SurfaceView` and `RenderType.HybridComposition`:

   ```Dart
   TTVideoPlayerView playerView = TTVideoPlayerView(
     nativeViewType: NativeViewType.SurfaceView,
     renderType: RenderType.HybridComposition,
     onPlatformViewCreated: (int viewId) {
       // After the NativeView is created, bind the player and viewId
       player.setPlayerContainerView(viewId);
     },
   );
   ```
   

3. Set the `useDrm` option to `true` during player creation:

   ```Dart
   player.createPlayer(useDrm: true);
   ```
   

4. Specify the playback source and start playing:

   ```Dart
   TTVideoEngineVidSource source = TTVideoEngineVidSource.init(
           vid: <vid>,
           // Set the temporary playback token
           playAuthToken: <playAuthToken>,
           resolution: <TTVideoEngineResolutionType>,
           // Set the DRM auth token
           drmLicenseAuthToken: <drmLicenseAuthToken>,
           // Set the FairPlay certificate
           certData: <certData>);
   player.setMediaSource(source);
   player.play();
   ```
