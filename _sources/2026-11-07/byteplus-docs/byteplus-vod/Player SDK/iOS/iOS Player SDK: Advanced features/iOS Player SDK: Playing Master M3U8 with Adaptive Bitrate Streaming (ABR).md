---
title: "iOS Player SDK: Playing Master M3U8 with Adaptive Bitrate Streaming (ABR)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-m3u8-abr-playback-ios"
---

Adaptive Bitrate Streaming (ABR) playback refers to the process of dynamically and seamlessly switching to the most suitable video resolution based on the user's network conditions. This ensures smooth video playback while providing the best possible viewing experience. This document guides you on how to play standard HLS Master M3U8 videos in **DirectUrl mode**.

<span id="6d12f82e"></span>
## Prerequisites

Before integrating the ABR playback feature, ensure that you have completed the following steps:


* **Obtain a license**: ABR playback is only supported by Premium Edition. Make sure your license includes the ABR playback functionality. For details, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).

* **Integrate the Premium SDK**: Refer to [Android Player SDK: Integrating the SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-integration-android) to integrate the 1.47.200.2 or later versions of the Premium SDK.

* **Complete basic SDK initialization**: Refer to [Android Player SDK: Quickstart](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-android-player-sdk) to complete the basic configuration and initialization of your project.

* **Verify the Master M3U8 File**: Ensure that in your Master M3U8 file, every `#EXT-X-STREAM-INF` tag includes the `"AVERAGE-BANDWIDTH"` and `"RESOLUTION"` attributes. The ABR strategy relies heavily on these attributes to assess the match between network conditions and bitrate for automatic switching. For example:

   ```Plain
   #EXT-X-STREAM-INF:BANDWIDTH=2628000,AVERAGE-BANDWIDTH=2500000,RESOLUTION=...
   /path/to/1080p.m3u8
   ```
   


<span id="88e8c888"></span>
## **Implementing ABR playback**

<span id="4bf8ff22"></span>
### Step 1: Initialize ABR globally

In your application's startup logic, before initializing the SDK, you need to globally enable the modules required for ABR. This operation only needs to be performed once.

```objectivec
/// 1. Before SDK initialization, globally enable the bandwidth detection module, which is the foundation for ABR.
[TTVideoEngine setGlobalForKey:VEGSKeyAlgoOptionEnableModuleBandwidth value:@(YES)];

/// 2. (Optional) Set a default ABR resolution.
/// This will be used as the default resolution for the first video played on a cold start when no network speed data is available.
[TTVideoEngineStrategyABRAlgoConfig shareInstance].defaultResolution = TTVideoEngineResolutionTypeHD;

/// 3. Initialize the SDK.
// The `configuration` object should be created as described in the "Quick Start" guide.
[TTSDKManager startWithConfiguration:configuration];
```


<span id="316eb6f5"></span>
### Step 2: Configure ABR for the player instance

For each player instance where you want to enable ABR, apply the following configurations before setting the playback URL.

```objectivec
// 1. Enable the ABR switch for Master M3U8 to allow the SDK to parse and apply ABR strategies.
[self.videoEngine setOptionForKey:VEKKeyStrategyEnableMasterM3u8ABR_BOOL value:@(YES)];

// 2. (Recommended) Enable seamless switching for a better user experience.
[self.videoEngine setOptionForKey:VEKKeyPlayerHLSSeamlessSwitchEnable_BOOL value:@(YES)];

// 3. Set the resolution map.
// Provide a mapping between the resolution strings in your Master M3U8 file and the SDK's resolution enums.
// You must configure this based on the actual resolution strings in your M3U8 file. The following is an example.
NSDictionary<NSString *, NSNumber *> *resolutionMap = @{
    @"640x360": @(TTVideoEngineResolutionTypeSD),
    @"854x480": @(TTVideoEngineResolutionTypeHD),
    @"1280x720": @(TTVideoEngineResolutionTypeFullHD),
    @"1920x1080": @(TTVideoEngineResolutionType1080P)
};
self.videoEngine.resolutionMap = resolutionMap;

// 4. Enable ABR mode.
// Set the resolution type to TTVideoEngineResolutionTypeABRAuto to activate ABR.
[self.videoEngine configResolution:TTVideoEngineResolutionTypeABRAuto];

// 5. Set the playback URL and start playing.
// [self.videoEngine setDirectUrl:...];
// [self.videoEngine play];
```


<span id="633efa66"></span>
### Step 3: (Optional) Listen for ABR events and configure parameters

You can implement the `TTVideoEngineABRDelegate` protocol to listen for ABR switching events or to dynamically provide more fine\-grained configurations to the ABR algorithm.

<span id="afe053c4"></span>
#### Listening for switch events

Implement the event callback methods in the protocol to receive notifications at key moments during the resolution switching process.

```objectivec
// Set the delegate
self.videoEngine.abrDelegate = self;

#pragma mark - TTVideoEngineABRDelegate

// ABR is about to switch resolution
- (void)videoEngineAbrWillSelectResolution:(TTVideoEngine *)videoEngine resolution:(TTVideoEngineResolutionType)resolution {
    NSLog(@"[ABR] Resolution will switch to: %@", @(resolution));
}

// ABR has finished switching resolution
- (void)videoEngineAbrEndSelectResolution:(TTVideoEngine *)videoEngine resolution:(TTVideoEngineResolutionType)resolution {
    NSLog(@"[ABR] Resolution has switched to: %@", @(resolution));
}
```


<span id="1452540d"></span>
#### Configuring parameters dynamically

By implementing the `videoEngineAbrConfig:` method, you can provide runtime parameters to the ABR algorithm, such as limiting the maximum available resolution for different network conditions.

```objectivec
#pragma mark -- TTVideoEngineABRDelegate (Parameter Configuration)

- (TTVideoEngineStrategyABRConfig *)videoEngineAbrConfig:(TTVideoEngine *)videoEngine {
    TTVideoEngineStrategyABRConfig *abrConfig = [[TTVideoEngineStrategyABRConfig alloc] init];

    // Example: Limit max resolution to 1080P on WiFi and 720P on mobile networks.
    abrConfig.wifiMaxResolution = TTVideoEngineResolutionType1080P;
    abrConfig.mobileMaxResolution = TTVideoEngineResolutionTypeFullHD;

    return abrConfig;
}
```
