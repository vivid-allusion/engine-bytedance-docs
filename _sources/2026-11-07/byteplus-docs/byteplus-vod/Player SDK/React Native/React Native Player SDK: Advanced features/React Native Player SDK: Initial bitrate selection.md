---
title: "React Native Player SDK: Initial bitrate selection"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/initial-bitrate-selection-rn"
---

The initial bitrate selection feature allows the player to intelligently choose the most appropriate resolution before playback begins, based on current network conditions, user history, or specific strategies. This feature optimizes the user's first\-frame experience by avoiding slow startup or buffering in weak networks caused by high bitrates, as well as poor image quality in strong networks caused by low bitrates. For example, you can configure a strategy to start at 1080P in a Wi\-Fi environment and 480P on mobile networks, saving user data while accelerating the startup speed.

<span id="6866ed14"></span>
## Global initialization

You must enable the initial bitrate selection feature globally during the SDK initialization phase. Set the `EnableStartSelect` parameter to `true` when calling the `initEnv` method.

```TypeScript
import { initEnv } from '@byteplus/react-native-vod-player';

initEnv({
  // ... other initialization configurations
  EnableStartSelect: true,
});
```


This is a global switch. Once enabled, you still need to separately configure and bind an initial bitrate selection strategy for each player instance or preload task for the strategy to take effect.

<span id="ef6d746d"></span>
## Platform implementation

Due to differences in the underlying implementation between Android and iOS, please refer to the corresponding configuration methods for each platform.

<span id="349b62dd"></span>
### Android

<span id="c995540c"></span>
#### Create an initial bitrate selection strategy

Call `createStartupConfig` to create a strategy object that defines the bitrate decision logic at startup.

```TypeScript
import { Dimensions, PixelRatio } from 'react-native';
import { createStartupConfig, ResolutionType } from '@byteplus/react-native-vod-player';

const screen = Dimensions.get('window');
const screenWidthPx = PixelRatio.getPixelSizeForLayoutSize(screen.width);
const screenHeightPx = PixelRatio.getPixelSizeForLayoutSize(screen.height);
const displayWidthPx = PixelRatio.getPixelSizeForLayoutSize(
  Math.min(screen.width, screen.height),
);
const displayHeightPx = Math.round(displayWidthPx * (16 / 9));

const startupConfig = createStartupConfig({
  screenWidth: screenWidthPx,  // Device screen width (physical pixels)
  screenHeight: screenHeightPx,  // Device screen height (physical pixels)
  displayWidth: displayWidthPx, // Video rendering area width (physical pixels)
  displayHeight: displayHeightPx, // Video rendering area height (physical pixels)
  defaultResolution: ResolutionType.High, // Default resolution used when no speed info is available or at first play.
  wifiMaxResolution: ResolutionType.ExtremelyHigh, // Max resolution tier for Wi-Fi (1080P)
  mobileMaxResolution: ResolutionType.SuperHigh,  // Max resolution tier for mobile networks (720P)
  userSelectedResolution: ResolutionType.SuperHigh, // If the user previously selected 720P, this tier is prioritized
});
```


The detailed parameters for the `StartupConfigParams` object are as follows:


|**Parameter** |**Type** |**Default value** |**Description** |
|---|---|---|---|
|`defaultResolution` |`ResolutionType` |`ResolutionType.High` (480P) |Default resolution tier used during cold start or when speed info is missing. |
|`wifiMaxResolution` |`ResolutionType` |`ResolutionType.ExtremelyHigh` (1080P) |The upper resolution limit on a Wi\-Fi network. |
|`mobileMaxResolution` |`ResolutionType` |`ResolutionType.SuperHigh` (720P) |The upper resolution limit on a mobile network. |
|`screenWidth` |`number` |*  |Device screen width in **physical pixels**. Used for accurate bitrate decisions. |
|`screenHeight` |`number` |*  |Device screen height in physical pixels. |
|`displayWidth` |`number` |*  |Video rendering area width in physical pixels. |
|`displayHeight` |`number` |*  |Video rendering area height in physical pixels. |
|`userSelectedResolution` |`ResolutionType` |*  |The resolution previously selected by the user. If provided, the strategy prioritizes user preference over network conditions. |


<span id="59f5a161"></span>
#### Listen for selection results

You can set a callback function for each configuration. Once the selection decision is complete, the SDK calls this function and passes the final selected resolution as a parameter.

```TypeScript
import { createStartupConfig, ResolutionType } from '@byteplus/react-native-vod-player';

createStartupConfig(config, (resolution: ResolutionType) => {
  // Update the resolution label in the UI here
  console.log(`Selection complete. Resolution ${resolution}`)
})
```


<span id="a6deb29d"></span>
#### Bind and enable initial bitrate selection

Enable the playback source cache for the player instance and bind the initial bitrate selection configuration to it.

```TypeScript
// Enable playing cached content
player.enablePlayCachedSource();
// Bind the initial bitrate selection configuration
player.bindABRConfig(startupConfig);
```


<span id="8bce3bca"></span>
### iOS

The implementation for iOS is simpler.

<span id="2198e5b4"></span>
#### Enable initial bitrate selection

After the player is created and before setting the playback source, enable the playback cache and the initial bitrate selection feature.

```TypeScript
// Enable playing cached content
player.enablePlayCachedSource();
// Enable the initial bitrate selection
player.enableStartupSelect();
```


<span id="26c1624e"></span>
#### Listen for selection results

Use the specific listener method to obtain the final resolution decision.

```TypeScript
player.setStartupSelectedResolutionListener((resolution: ResolutionType) => {
  // Handle the selection result
  console.log(`Selection complete. Resolution ${resolution}`)
})
```


<span id="24c132c8"></span>
## Advanced usage (Android only)

<span id="55f1afed"></span>
#### Integration with preloading strategy

If you use the [Preloading strategy](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-basic-features) with initial bitrate selection, you must set the `PreloadTaskFactory` callback. This ensures that in "Auto" mode, the SDK can determine a preload tier that matches the initial tier, ensuring the preload cache is successfully hit and accelerating video loading.

```TypeScript
import { setPreloadTaskConfig, ResolutionType } from '@byteplus/react-native-vod-player';

// Configure the preload task
setPreloadTaskConfig({
    preloadResolution: ResolutionType.Auto,
    ABRConfig: abrStartupConfig
})

// Initialize the preload task factory
setPreloadTaskFactory()
```


<span id="d72ebabe"></span>
#### Integration with custom preloading

If you use [Custom preloading](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-custom-preloading), you must set the preload resolution to `Auto` and pass the ABR strategy configuration when creating the task. The actual tier will then be determined by the ABR strategy.

```TypeScript
/**
 * Preload configuration interface
 */
export interface PreloadConfig {
  /** Preload size in bytes, default 800KB */
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
     ABRConfig: abrStartupConfig,    // Initial bitrate selection configuration
    })
```


<span id="bde650f9"></span>
#### Integration with pre\-rendering strategy

If you use the [Pre-rendering strategy](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-basic-features) with initial bitrate selection, you need to enable the relevant switch and bind the selection configuration within the `onPlayerCreated` callback.

```TypeScript
import { createStartupConfig, ResolutionType } from '@byteplus/react-native-vod-player';
 
 const abrStartupConfig = createStartupConfig(config, (resolution) => {
   // ...
 });
 
 setPreRenderCallback({
     onPlayerCreated(player: TTVideoEngine, source: VideoSource) {
       // Enable playing cached content
       player.enablePlayCachedSource();
       // Bind the initial bitrate selection configuration
       player.bindABRConfig(abrStartupConfig);
     }
 })
```
