---
title: "iOS Player SDK: Initial bitrate selection"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/initial-bitrate-selection-ios"
---

Initial bitrate selection is a feature that intelligently selects the most suitable initial bitrate to begin video playback, based on the user's network conditions, device information, and business scenario. This feature optimizes the startup experience by ensuring a fast time to first frame (TTFF) while delivering the highest possible initial video quality.

Unlike [ABR streaming](https://docs.byteplus.com/en/docs/byteplus-vod/docs-m3u8-abr-playback-ios), which dynamically switches bitrates during playback, initial bitrate selection makes a one\-time decision *before* playback begins. The quality remains fixed throughout the playback session and does not automatically change with network fluctuations.

The iOS Player SDK supports initial bitrate selection for playing standard HLS Master M3U8 video sources.

<span id="d4b29555"></span>
## **Prerequisites**

Before implementing this feature, ensure you have met all the following conditions:


* Integrate and initialize the SDK: Integrate the SDK and complete the basic initialization by following [iOS Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk). Use 1.48.100.4 or later versions.


<span id="faa6ff56"></span>
## **Implementing** initial bitrate selection

<span id="d1d70048"></span>
### Step 1: Global initialization

After initializing the Player SDK, call the following code to configure the selection module globally. This operation only needs to be performed once.

```objectivec
// Call this after [TTSDKManager startWithConfiguration:configuration]

// 1. Initialize the selection module with the default configuration.
// This is the same default configuration used by Douyin, optimized for an ideal balance
// between user experience and cost by matching target bitrates with network speeds.
[TTVideoEngineStrategyAutoSelectConfig globalInitWithSDKDefaultConfig];

// 2. (Recommended) Enable log reporting for selection results to facilitate debugging and data analysis.
[TTVideoEngine setGlobalForKey:VEGSKeyEngineSelectResultReport_BOOL value:@(YES)];

// 3. (Recommended) Apply the same selection strategy to preloading tasks to improve efficiency and hit rates.
// This switch affects all preloading tasks within the app.
[TTVideoEngine ls_localServerConfigure].isEnablePreloadAutoSelect = YES;
```


<span id="cf183f0b"></span>
### Step 2: Enable initial bitrate selection for a player instance

For each playback session, you need to enable the feature for the `TTVideoEngine` instance after creating it but **before** setting its `videoSource`. When initial bitrate selection is enabled, you should **not** call `configResolution` to manually set a resolution, as the SDK will handle it automatically.

```objectivec
// Call this after creating the TTVideoEngine instance but before setting its videoSource.
if (AutoSelectSwitchOn) { // 'AutoSelectSwitchOn' is your business logic switch.
    
    // 1. (Optional but recommended) Set the delegate to receive callbacks, such as the selection result.
    self.videoEngine.autoSelectDelegate = self;
    
    // 2. Enable the initial bitrate selection feature for the current player instance.
    [self.videoEngine setOptionForKey:VEKKeyPlayerEnableAutoSelectBitrate_BOOL value:@YES];
    
    // 3. (Conditional) If you are playing a standard Master M3U8 source,
    //    you must also enable this specific switch.
    //    This line is not needed for proprietary protocol sources (Vid/VideoModel).
    [self.videoEngine setOptionForKey:VEKKeyStrategyEnableMasterM3u8ABR_BOOL value:@(YES)];

} else {
    // If initial bitrate selection is disabled, fall back to your original logic
    // for manually setting the resolution.
    [self.videoEngine configResolution:YourDefaultResolution];
}

// Then, set the videoSource and start playback.
// [self.videoEngine setVideoEngineVideoSource:vidSource];
// [self.videoEngine play];
```
