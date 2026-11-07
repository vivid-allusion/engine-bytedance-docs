---
title: "Flutter Player SDK: Initial bitrate selection for M3U8"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-initial-bitrate-selection"
---

Initial bitrate selection refers to the intelligent selection of optimal video resolution to start playback, based on user's network conditions, device information, and business scenario. It optimizes the playback experience with a fast time\-to\-first\-frame and the highest possible initial picture quality. Different from playing with ABR, it performs a single bitrate selection before starting playback. During playback, the resolution remains unchanged and does not automatically switch based on network fluctuations.

This article applies to initial bitrate selection for M3U8 playback using Vid or VideoModel sources.

<span id="a9825b5f"></span>
## Configure bitrate selection strategy

After initializing the SDK with `FlutterTTSDKManager.startWithConfiguration`, call `FlutterTTSDKManager.initStartupAutoSelectStrategy` to initialize the strategy module. We recommend initializing the SDK before the `runApp` method in your project's `main.dart` file to ensure all functional modules are correctly initialized.

```Dart
Future<void> initTTSDK() async {
     // Enable logging for debugging.
    FlutterTTSDKManager.openAllLog();
    
    // Register plugin logs. You can choose to output to the console or a local file for troubleshooting
    TTFLogger.onLog = (logLevel, msg) {
      print(msg);
    };

    // Provide the path to your license file. Pass a valid license file path, such as 'assets/VEVod.lic'
    String licPath = 'your license file path'; 
    // For Android, pass a valid channel name for analytics; for iOS, this is optional and defaults to App Store
    String channel = Platform.isAndroid ? 'your channel' : 'App Store';
    // Initialize configuration
    TTSDKVodConfiguration vodConfig = TTSDKVodConfiguration();
    // Set the maximum cache size (default: 100 MB). Adjust as needed for your business requirements. When the cache exceeds the set size, it will be cleared following the LRU rule
    vodConfig.cacheMaxSize = 300 * 1024 * 1024;
    
    // Enter the AppID obtained from VOD console > SDK management > Applications
    TTSDKConfiguration sdkConfig =
        TTSDKConfiguration.defaultConfigurationWithAppIDAndLicPath(
            appID: 'your AppID', licenseFilePath: licPath, channel: channel);
    sdkConfig.vodConfiguration = vodConfig;
    await FlutterTTSDKManager.startWithConfiguration(sdkConfig);
    // Initialize the playback selection strategy module.
    await FlutterTTSDKManager.initStartupAutoSelectStrategy();
  }
```


<span id="c5d9af5a"></span>
## Configure initial bitrate selection

Due to platform differences, the configuration methods differ between Android and iOS.

<span id="ae109ef8"></span>
### Android initial bitrate selection

On Android, you can configure fine\-grained selection control by creating a detailed configuration object.

<span id="9fa8eb6d"></span>
#### Core implementations


1. Build the configuration object `TTVideoABRStartupConfig` to select initial bitrate. The `displayWidth` and `displayHeight` are key parameters. Set them to the actual rendering dimensions of the video player widget to ensure accuracy.

   ```Dart
   import 'dart:math' as math;
   
   // Obtain the screen size
   final screenWidth = MediaQuery.of(context).size.width.toInt();
   final screenHeight = MediaQuery.of(context).size.height.toInt();
   final int minSide = math.min(screenWidth, screenHeight);
   
   // Create an initial bitrate selection configuration instance
   TTVideoABRStartupConfig sharedAbrConfig = await TTVideoABRStartupConfig.create(
     screenWidth: screenWidth, // The screen width of the current device
     screenHeight: screenHeight, // The screen height of the current device 
     displayWidth: minSide, // Actual display width of the video. Key parameter
     displayHeight: (minSide / 9 * 16).toInt(), // Actual display height of the video. Key parameter
     
     // ----- Optional configuration -----
     // Set a default initial resolution as a fallback in case of poor network or insufficient information
     defaultResolution: TTVideoEngineResolutionType.TTVideoEngineResolutionTypeHD,
     // The maximum resolution selectable on Wi-Fi networks
     wifiMaxResolution: TTVideoEngineResolutionType.TTVideoEngineResolutionTypeFullHD,
     // The maximum resolution selectable on mobile networks
     mobileMaxResolution: TTVideoEngineResolutionType.TTVideoEngineResolutionTypeHD_H,
     // The resolution manually selected by the user. If it is set, the selection strategy will prioritize this value, usually used to implement the "remember user's resolution choice" feature
     userSelectedResolution: TTVideoEngineResolutionType.TTVideoEngineResolutionTypeFullHD,
     // Set a listener to receive the result callback after selection is complete
     listener: TTVideoABRStartupResolutionListener(
       onResolutionSelected: (videoModel, resolution) {
          debugPrint('Selection complete. The final resolution: $resolution');
       },
     ),
   );
   ```
   

2. Enable the initial bitrate selection feature on the player, and bind the configuration instance created in the previous step to the player.

   ```Dart
   // Enable initial bitrate selection feature
   await player.enableStartupAutoSelectBitrate(true);
   // Bind the configuration instance to the player engine
   await TTVideoABRStrategy.initEngine(player: player, config: sharedAbrConfig);
   ```
   

3. Set `VideoModel` or `Vid` playback sources and start playback. The SDK will automatically execute the selection logic internally.

   ```Dart
   final TTVideoPlayerView _playerView = TTVideoPlayerView(
     nativeViewType: NativeViewType.TextureView,
     onPlatformViewCreated: (viewId) async {
       await player.setPlayerContainerView(viewId);
       await player.setMediaSource(source); // The source should be VidSource or VideoModelSource
       player.play();
     },
   );
   ```
   


<span id="5f512aba"></span>
#### Monitor selection results

You can pass a listener when creating `TTVideoABRStartupConfig` to obtain the final resolution after the selection process is complete.

```Dart
TTVideoABRStartupConfig sharedAbrConfig = await TTVideoABRStartupConfig.create(
  // ... Other configurations
  // Set a callback listener for when bitrate selection is complete
  listener: TTVideoABRStartupResolutionListener(
    onResolutionSelected: (videoModel, resolution) {
      // The resolution parameter represents the final selected resolution
      debugPrint('Selection complete. The final resolution: $resolution');
    },
  ),
);
```


<span id="43f70f1f"></span>
#### Combine with preloading strategy (recommended)

For the best experience when scrolling through short video feeds, we recommend combining initial bitrate selection with the preloading strategy to select the optimal resolution.


1. First, enable the preloading strategy:

   ```Dart
   // We recommend enabling this when the user enters the short video page
   TTVideoEngineStrategy.enableEngineStrategy(
             strategyType: TTVideoEngineStrategyType.preload, scene: TTVideoEngineStrategyScene.smallVideo);
   ```
   

2. Set the playback sources list to preload:

   ```Dart
   // Build the list of playback sources to preload
   final List<TTVideoEngineMediaSource> sources = [];
   // ... Add your VidSource or VideoModelSource to the sources list
   await TTVideoEngineStrategy.setStrategyVideoSources(videoSources: sources);
   ```
   

3. Create the initial bitrate selection configuration. You can reuse the same `sharedAbrConfig` instance for playback.

   ```Dart
   TTVideoABRStartupConfig sharedAbrConfig = await TTVideoABRStartupConfig.create(...);
   ```
   

4. Configure the bitrate selection strategy for preloading tasks. This step injects the selection logic into the preloading process. When a preload task executes, it determines which resolution to load based on the selection configuration, and then caches it.

   ```Dart
   // Enable the preload task factory
   await TTVideoEngineStrategy.setPreloadTaskFactory();
   // Update (set) initial bitrate selection configuration for preload tasks
   await TTVideoEngineStrategy.updatePreloadABRConfig(config: sharedAbrConfig!);
   ```
   


<span id="53c75dbe"></span>
#### Combine with custom preloading


<Tabs>
<Tab zoneid="u8SJ6d2MeE" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

```Dart
// Build initial bitrate selection configuration
TTVideoEngineABRStartupConfig sharedAbrConfig = await TTVideoABRStartupConfig.create(...);

// Create Vid playback source
final TTVideoEngineVidSource vidSource = TTVideoEngineVidSource.init(
           vid: <vid>,
           playAuthToken: <playAuthToken>,
           resolution: <TTVideoEngineResolutionType>); // The resolution can be set to the default value here

// Build custom preload items for Vid
final TTVideoEnginePreloaderVidItem item =
 TTVideoEnginePreloaderVidItem.vidItemWithVideoSource(
  vidSource, // Preloaded VidSource
  800 * 1024, // Preload size, default is 800KB
  abrStartupConfig: sharedAbrConfig, // Pass in initial playback profile configuration
);

// Add preload task
await TTVideoEnginePreload.addTaskWithVidItem(item);
```



</Tab>
<Tab zoneid="ekaM8cCwVn" title="VideoModel mode">
<TabTitle>VideoModel mode</TabTitle>

When building `TTVideoEnginePreloaderVideoModelItem`, pass the startup profile selection configuration through the `abrStartupConfig` parameter.

```Dart
// Build initial playback profile configuration; can reuse the instance used during playback
TTVideoABRStartupConfig sharedAbrConfig = await TTVideoABRStartupConfig.create(...);

// Build custom preload items for VideoModel
final TTVideoEnginePreloaderVideoModelItem item =
 TTVideoEnginePreloaderVideoModelItem.videoModelItemWithSource(
  videoModelSource, // Preloaded VideoModelSource
  800 * 1024, // Preload size, unit: bytes. Default: 800KB
  abrStartupConfig: sharedAbrConfig, // Pass in initial playback selection configuration
);

// Add preload task
await TTVideoEnginePreload.addTaskWithVideoModelItem(item);
```



</Tab>
</Tabs>


<span id="171c66f6"></span>
### iOS initial bitrate selection

The configuration is simpler. You only need to enable an option before setting the playback source. This setting automatically applies to playback, preloading strategy and custom preloading scenarios.

<span id="502f4a7e"></span>
#### Configure initial bitrate selection


<Tabs>
<Tab zoneid="YG9ZeQR4W4" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

```Dart
// Create Vid playback source
TTVideoEngineVidSource source = TTVideoEngineVidSource.init(
        vid: <vid>,
        playAuthToken: <playAuthToken>,
        resolution: <TTVideoEngineResolutionType>); // Here, resolution can be set to the default value
        
// Key: turn on the initial playback selection option before setting the playback source
await player.enableStartupAutoSelectBitrate(true);

// Set playback source
player.setMediaSource(source);
```



</Tab>
<Tab zoneid="UM0IyGeK1E" title="VideoModel mode">
<TabTitle>VideoModel mode</TabTitle>

```Dart
// Create VideoModel playback source
TTVideoEngineVideoModelSource videoModelSource = TTVideoEngineVideoModelSource.init(
  vid: 'v1234567890',
  resolution: TTVideoEngineResolutionType.TTVideoEngineResolutionType1080P, // Here, resolution can be set to the default value
  playInfoList: items,
  duration: 123.45,
);

// Key: Turn on the playback selection switch before setting the playback source
await player.enableStartupAutoSelectBitrate(true);

// Set playback source
player.setMediaSource(videoModelSource);
```



</Tab>
</Tabs>


<span id="9b6d9d03"></span>
#### Monitor selection results

Set the `onVideoEngineAutoSelectResolution` callback function for the player instance. This function is triggered after the bitrate selection is complete and returns the final resolution.

```Dart
player.onVideoEngineAutoSelectResolution = (TTVideoEngineResolutionType resolution) {
  // The resolution is the result of the bitrate selection
  debugPrint('Selection complete. The final resolution: $resolution');
};
```
