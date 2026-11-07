---
title: "Android Player SDK: Initial bitrate selection for M3U8"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/initial-bitrate-selection-android"
---

Initial bitrate selection refers to the intelligent selection of the optimal video resolution to start playback, based on user's network conditions, device information, and business scenario. It optimizes the playback experience with a fast time\-to\-first\-frame and the highest possible initial picture quality. This feature and [Android Player SDK: Playing Master M3U8 with Adaptive Bitrate Streaming (ABR)](https://docs.byteplus.com/docs/byteplus-vod/docs-m3u8-abr-playback-android)both rely on the ABR module within the SDK, but with different application scenarios:


* **Initial bitrate selection:**  It performs a single bitrate selection before starting playback. During playback, the resolution remains unchanged and does not automatically switch based on network fluctuations. It has fine\-grained initial bitrate selection strategies and supports advanced optimizations such as Super\-Resolution Downgrade.

* **ABR playback:**  It begins with an initial bitrate selection, and constantly monitors the network conditions throughout playback. This allows the player to dynamically and seamlessly adapt the resolution.


This document is applicable if your business scenario does not require automatic resolution switching during playback, or if you prioritize the optimal initial bitrate selection. For automatic resolution switching during playback, please use the ABR feature.

This document explains how to implement the initial bitrate selection feature for playing standard HLS Master M3U8 videos.

<span id="c8edc951"></span>
## Prerequisites

Before integrating the startup resolution selection feature, ensure you have completed the following steps:


* **Obtain a valid license**: The initial bitrate selection feature relies on the ABR module. You must have a license with ABR functionality enabled. See [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management) for details.

* **Integrate the Premium SDK and ABR module**: Following [Android Player SDK: Integrating the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-integration-android) to integrate the **Premium SDK, version1.48.200.1 or later**. Make sure to add dependencies for both the `player_premium` and `ttabr` modules in your `build.gradle` file:

   ```Groovy
   // app/build.gradle
   def ttsdk_version = "1.48.200.1" // Use version 1.48.200.1 or higher
   implementation "com.bytedanceapi:ttsdk-player_premium:$ttsdk_version"
   implementation "com.bytedanceapi:ttsdk-ttabr:$ttsdk_version"
   ```
   


<span id="dc9d3bb6"></span>
## Implementing initial bitrate selection

<span id="87cddda6"></span>
### Step 1: Configure global initialization

In the `onCreate` method of your `Application`, initialize the ABR strategy module after the regular SDK initialization. This operation is only required once at app startup.

```Java
public class App extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        initVodSDK();
    }
}

public static void initVodSDK() {
    // 1. Initialize the SDK
    Env.init(/*omitted*/);
    
    // 2. Critical step: Initialize the ABR global configuration, required for initial bitrate selection
    TTVideoABRStrategy.init();
}
```


<span id="2357cb3c"></span>
### Step 2: Enable bitrate selection for the player instance

You must configure and enable the initial bitrate selection feature for the `TTVideoEngine` instance after its creation and before calling `play` for each playback.


1. **Construct the selection configuration:**  Create a `TTVideoABRStartupConfig` object to define the behavior of the bitrate selection algorithm.

   ```Java
   public TTVideoABRStartupConfig createStartupConfig() {
       TTVideoABRStartupConfig startupConfig = new TTVideoABRStartupConfig();
       
       // -- Basic device information --
       startupConfig.screenWidth = UIUtils.getScreenWidth(this.mContext); // Current device screen width
       startupConfig.screenHeight = UIUtils.getScreenHeight(this.mContext); // Current device screen height
       
       // -- Strategy configuration --
       // The default resolution to use when no network speed measurement information is available (for example, when playing the first video after a cold start)
       startupConfig.defaultResolution = Resolution.High; // 480p
       // The maximum allowable resolution for selection on a Wi-Fi network
       startupConfig.wifiMaxResolution = Resolution.ExtremelyHigh; // 1080p
       // The maximum allowable resolution for selection on a cellular network
       startupConfig.mobileMaxResolution = Resolution.SuperHigh; // 720p
       
       // -- Business scenario configuration: Optimize selection based on video display size --
       startupConfig.displayWidth = Math.min(startupConfig.screenWidth, startupConfig.screenHeight);
       startupConfig.displayHeight = (int) (startupConfig.displayWidth / 9f * 16);
       
       return startupConfig;
   }
   ```
   

2. After creating the DirectUrl playback source, apply the configuration and enable the initial bitrate selection.

   ```Java
   // Assume directUrlSource has been created
   if (mVideoEngine == null) {
       mVideoEngine = new TTVideoEngine(context);
       
       // Set the playback source
       mVideoEngine.setStrategySource(directUrlSource);
       
       // Critical step 1: Enable speed prediction optimization
       mVideoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_OPTIMIZED_SPEED_PREDICTION, 1);
       
       // Critical step 2: Apply the initial bitrate selection configuration
       final TTVideoABRStartupConfig startupConfig = createStartupConfig();
       TTVideoABRStrategy.initEngine(mVideoEngine, startupConfig);
       
       // Critical step 3: Set HLS callback
       mVideoEngine.setPlayerHLSChooseStreamCallback(new TTVideoEnginePlayHLSChooseStreamCallback() {
           @Override
           public void streamInfos(TTVideoEngineMasterPlaylist masterPlaylist) {
               // You can retrieve all stream information parsed from the Master M3U8 here
           }
   
           @Override
           public int chooseVariantBandWidth() {
               // Return 0 to delegate the decision to the SDK's internal initial bitrate selection strategy
               return 0;
           }
   
           @Override
           public int chooseRenditionInfoId(int varIndex) {
               return 0;
           }
       });
   }
   // Start playback
   mVideoEngine.play();
   ```
