---
title: "React Native Player SDK: Adaptive Bitrate Streaming (ABR)"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/abr-playback-rn"
---

Adaptive Bitrate Streaming (ABR) is a feature where the player automatically and seamlessly switches between multiple resolution (bitrate) tiers based on factors such as current network bandwidth and device performance. This ensures that users maintain a smooth, high\-quality viewing experience even during network fluctuations, minimizing buffering. For example, in a Wi\-Fi environment, the player can automatically select the 1080p high\-definition tier; when the network switches to mobile data or the signal weakens, the player automatically downgrades to 720p or lower to avoid playback interruption. Once the network recovers, it switches back to the high\-definition tier.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Because ABR network probing requires a certain response time, it is better suited for medium\-to\-long video scenarios. For short videos or micro\-dramas, it is recommended to use the <strong>Initial Bitrate Selection</strong> feature to optimize the experience.</div>


<span id="98b17fa5"></span>
## Restrictions


* ABR supports both **MP4** and **HLS** formats. If using the MP4 format, you must ensure that videos of different resolutions are **frame\-aligned**. If you are unsure, please contact technical support for verification.

* ABR is only supported in **Vid** and **VideoModel mode**.

* ABR playback is supported by Premium Edition. Ensure your license includes ABR functionality. For details, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).


<span id="f2cf3b6e"></span>
## Core integration flow

<span id="98640d32"></span>
### Step 1: Enable ABR globally

During the SDK initialization phase, set `EnableABR` to `true` to enable the ABR feature globally.

```TypeScript
import { initEnv, ResolutionType } from '@byteplus/react-native-vod-player';

initEnv({
  // ... other initialization configurations
  /** Enable ABR strategy globally */
  EnableABR: true,
  /** 
   * iOS: Default ABR resolution.
   * This resolution is used for the first video played during a cold start of the player or when no network speed information is available.
   */
  DefaultABRResolution: ResolutionType.High
});
```


<span id="b450664b"></span>
### Step 2: Configure and bind the ABR strategy


1. **Create a strategy object**: Call the `createABRConfig` method to create an ABR strategy object, defining the bitrate selection behavior under different network environments.

   ```TypeScript
   import {Dimensions, PixelRatio} from 'react-native';
   import { createABRConfig } from '@byteplus/react-native-vod-player';
   
   const screen = Dimensions.get('window');
   const screenWidthPx = PixelRatio.getPixelSizeForLayoutSize(screen.width);
   const screenHeightPx = PixelRatio.getPixelSizeForLayoutSize(screen.height);
   const displayWidthPx = PixelRatio.getPixelSizeForLayoutSize(
     Math.min(screen.width, screen.height),
   );
   const displayHeightPx = Math.round(displayWidthPx * (16 / 9));
   
   const abrConfig = createABRConfig({
     screenWidth: screenWidthPx,  // Device screen width (physical pixels)
     screenHeight: screenHeightPx,  // Device screen height (physical pixels)
     displayWidth: displayWidthPx, // Video rendering area width (physical pixels)
     displayHeight: displayHeightPx, // Video rendering area height (physical pixels)
     defaultResolution: ResolutionType.High, // Default resolution used when no speed info is available or at first play.
     wifiMaxResolution: ResolutionType.ExtremelyHigh, // Max resolution tier for Wi-Fi (1080P)
     mobileMaxResolution: ResolutionType.SuperHigh,  // Max resolution tier for mobile networks (720P)
   });
   ```
   


The detailed parameters for the `ABRConfigParams` object are as follows:


|**Parameter** |**Type** |**Default value** |**Description** |
|---|---|---|---|
|`defaultResolution` |`ResolutionType` |`ResolutionType.High` (480P) |Default resolution tier used during cold start or when speed info is missing. |
|`wifiMaxResolution` |`ResolutionType` |`ResolutionType.ExtremelyHigh` (1080P) |The upper resolution limit on Wi\-Fi networks. |
|`mobileMaxResolution` |`ResolutionType` |`ResolutionType.SuperHigh` (720P) |The upper resolution limit on mobile networks. |
|`screenWidth` |`number` |`-` |Device screen width in physical pixels. Used for accurate bitrate decisions. |
|`screenHeight` |`number` |`-` |Device screen height in physical pixels. |
|`displayWidth` |`number` |`-` |Video rendering area width in physical pixels. |
|`displayHeight` |`number` |`-` |Video rendering area height in physical pixels. |



2. **Bind to the player**: Once the ABR strategy object is created and the player is ready, call the `bindABRConfig` method to bind it to the player instance.

   ```TypeScript
   // player is the instance obtained via the usePlayer() hook
   if (player && abrConfig) {
     player.bindABRConfig(abrConfig);
   }
   ```
   

3.  **(Optional) Dynamically update strategy**: If the scenario changes during playback (for example, entering full\-screen mode or changing view size), update the ABR configuration to adapt to the new view size or resolution strategy.

   ```TypeScript
   const newAbrConfig = createABRConfig(newConfig)
   
   player.setABRConfig(newAbrConfig)
   ```
   


<span id="ca50ae61"></span>
### Step 3: Enable ABR playback


1. Enable seamless switching and playing cached content:

   ```TypeScript
   // Enable seamless switching for HLS videos
   await player.enableHLSSeamlessSwitch(true);
   // Enable seamless switching for MP4 videos
   // await player.enableMP4SeamlessSwitch(true);
   
   // Enable playing cached content
   player.enablePlayCachedSource();
   ```
   

2. **Set the resolution to** **`Auto`**:

   * You can specify this directly when constructing the playback source:

   
   <Tabs>
   <Tab zoneid="yGt41rC6wh" title="Vid mode">
   <TabTitle>Vid mode</TabTitle>
   
   ```TypeScript
   import { createVidSource, ResolutionType } from '@byteplus/react-native-vod-player';
   
   const source = createVidSource({
      vid: '******',
      playAuthToken: '************',
      resolution: ResolutionType.Auto
   })
   ```
   
   
   
   </Tab>
   <Tab zoneid="Zg3v443geZ" title="VideoModel mode">
   <TabTitle>VideoModel mode</TabTitle>
   
   ```TypeScript
   import { createVidSource, createVideoModelSource, ResolutionType } from '@byteplus/react-native-vod-player';
   
   const source = createVideoModelSource({
      vid: '******',
      duration: 634.567, // video duration
      resolution: ResolutionType.Auto, // default video resolution when playback starts
      playInfoList: [...]
   })
   ```
   
   
   
   </Tab>
   </Tabs>
   

   * Alternatively, after the playback source is constructed, call `configResolution` to set the resolution to `Auto`:


```TypeScript
// Switch to automatic tier selection (Enables ABR)
player.configResolution(ResolutionType.Auto);

// Switch to a fixed resolution (Disables ABR)
player.configResolution(ResolutionType.High);
```


<span id="fd04ebce"></span>
## Interaction and monitoring during playback

<span id="ed3c619b"></span>
### Get the current actual resolution


* **Proactive retrieval**:

   ```TypeScript
   const curRealResolution = player.getCurrentResolution();
   ```
   

* **Callback listening**: If you need to update the UI in real\-time (such as changing the label on a resolution selection button), it is recommended to listen for resolution change events.

   ```TypeScript
   player.setListener({
     onVideoBitrateChanged: (resolution, bitrate) => {
       // Triggered when ABR switches tiers
       // resolution is the specific actual tier (such as ResolutionType.High), not Auto
       console.log(`ABR strategy has automatically switched resolution to: ${resolution}`);
       updateUIScale(resolution);
     },
   });
   ```
   


<span id="32b6857f"></span>
### Build the UI resolution option list

In Vid and VideoModel modes, the `supportedResolutionTypes()` method only returns fixed tiers supported by the video source. If you need to display an "Auto" option in the UI, you must manually add it to the list.

```TypeScript
import { ResolutionType } from '@byteplus/react-native-vod-player';

const list = player.supportedResolutionTypes();
const listWithAuto = [ResolutionType.Auto, ...list];
// Render the resolution list including the Auto option
renderResolutionList(listWithAuto);
```


<span id="61b52e38"></span>
## Advanced usage

<span id="3654ee76"></span>
### Integration with preloading strategy

If you want to use the [Preloading strategy](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-basic-features) in conjunction with ABR, you need to set the `PreloadTaskFactory` callback. This ensures that when starting in "Auto" mode, the preloaded resolution selected by the ABR strategy matches the actual startup resolution, thereby hitting the preload cache and speeding up startup.

```TypeScript
import { setPreloadTaskConfig, ResolutionType } from '@byteplus/react-native-vod-player';

// Set configuration for preload tasks
setPreloadTaskConfig({
    preloadResolution: ResolutionType.Auto,
    ABRConfig: abrConfig
})

// Initialize preload task factory
setPreloadTaskFactory()
```


<span id="a7e6040a"></span>
### Integration with custom preloading

If you use [Custom preloading](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-custom-preloading), you must set the resolution to `Auto` and pass the ABR strategy configuration when creating the task. This ensures the actual tier used for preloading is determined by the ABR strategy.

```TypeScript
/**
 * Preload configuration interface
 */
export interface PreloadConfig {
  /** Preload size (bytes), default 800KB */
  preloadSize?: number;
  /** Preload resolution, effective only on Android */
  preloadResolution?: ResolutionType;
  /** ABR configuration for preloading, effective only on Android */
  ABRConfig?: TTVideoABRStartupConfig | TTVideoABRConfig;
}

const taskId = preloadVidSource(
    vidSource,
    {
     preloadSize: 800 * 1024,
     preloadResolution: ResolutionType.Auto,  // Set to Auto tier
     ABRConfig: startupAbrConfig,    // ABR strategy config
    })
```


<span id="55d53f98"></span>
### Integration with pre\-rendering strategy

If you want to use the [Pre-rendering strategy](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-basic-features) with ABR, you need to enable ABR\-related features and bind the ABR strategy configuration within the `onPlayerCreated` callback.

```TypeScript
const abrStartupConfig = createStartupConfig(config, (resolution) => {
   // ...
 });
 
 setPreRenderCallback({
     async onPlayerCreated(player: TTVideoEngine, source: VideoSource) {
       // Enable playing cached content
       player.enablePlayCachedSource();
       // Enable seamless switching for HLS
       await player.enableHLSSeamlessSwitch(true);
       // Enable seamless switching for MP4
       // await player.enableMP4SeamlessSwitch(true);
       // Bind ABR strategy configuration
       player.bindABRConfig(abrStartupConfig);
     }
 })
```
