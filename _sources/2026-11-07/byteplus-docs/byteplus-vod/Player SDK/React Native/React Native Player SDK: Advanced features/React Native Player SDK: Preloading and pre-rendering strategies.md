---
title: "React Native Player SDK: Preloading and pre-rendering strategies"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-basic-features"
---

To help you quickly build short video scenarios, the Player SDK provides preloading and pre\-rendering strategies based on real feedback and large\-scale practical experience. For more information, see [Android Player SDK: Best practices for short video scenarios](https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-short-video-best-practices).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="a1e9f198"></span>
## Preloading strategy

<span id="42219e6a"></span>
### Implement preloading strategy

Follow these steps to implement the preloading strategy:


1. Call `enableEngineStrategy` to enable the preloading strategy.

   ```TypeScript
   import { enableEngineStrategy } from '@byteplus/react-native-vod-player';
   
   // Supports SmallVideo (short video scenario) and ShortVideo (medium video scenario)
   enableEngineStrategy('Preload', 'SmallVideo');
   ```
   

2. When the playback source data is first loaded or in a scenario of refreshing the page to display new data, call `setStrategySources` to set the playback source for the playlist.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure that each playback source's <code>vid</code> and <code>cacheKey</code> are unique.   </div>
   

   * Vid playback source:

      ```TypeScript
      import { setStrategySources } from '@byteplus/react-native-vod-player';
      
      const vidData = [
        {
          playAuthToken: 'playAuthToken1',
          vid: 'vid1',
        },
        {
          playAuthToken: 'playAuthToken2',
          vid: 'vid2',
        },
        // ...
      ];
         
      // Set the playback sources for the preloading list  
      setStrategySources(vidData.map(u => createVidSource(u)));
      ```
      

   * DirectUrl playback source:

      ```TypeScript
      import { setStrategySources } from '@byteplus/react-native-vod-player';
      
      const urlData = [
        {
          url: 'https://voddemo-play.volcvod.com/1.mp4',
          vid: 'vid1',
        },
        {
          url: 'https://voddemo-play.volcvod.com/2.mp4',
          vid: 'vid2',
        },
        // ...
      ];
         
      // Set the playback sources for the preloading list  
      setStrategySources(
        urlData.map(u =>
          createDirectUrlSource({
            ...u,
            cacheKey: u.vid,
          } as DirectUrlSourceInitProps),
        ),
      );
      ```
      

3. If you need to add new sources to the preloading list, call `addStrategySources`.

   ```TypeScript
   const newVidData = [...]; 
   addStrategySources(newVidData.map(u => createVidSource(u)));
   ```
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">An incorrect playlist can result in preload failure.</div>


* <div data-tips="true" data-tips-type="warning">The preloading strategy involves preloading videos at index+1, index+2, ... index+n based on the current video's index in the playlist.</div>



<span id="eb07917c"></span>
### Check preloading status

You can monitor preloading is successful by setting the `onCacheChange` callback in the playback status listener.

```TypeScript
player.setListener({
  // cacheSize greater than 0 indicates preloading hit.
  onCacheChange(cacheKey: string, cacheSize: number) {
    if (cacheSize > 0) {
       console.log('video hit preload: ', cacheKey, cacheSize);
    }
  }
});
```


<span id="5a8d9d5c"></span>
### Clear cache

Preloading consumes storage space. You can call `clearAllCaches` to clear the cache.

```TypeScript
import {clearAllCaches} from '@byteplus/react-native-vod-player';

// true: Force delete all cache data.
// false: Do not delete all cache data, but retain the most recently played around 10 data according to the Least Recently Used (LRU) algorithm to optimize the actual playback experience.
clearAllCaches(true);
```


<span id="44a16ad8"></span>
## Pre\-rendering strategy

<span id="b05a7215"></span>
### Implementing pre\-rendering strategy

To implement the prerendering strategy, follow these steps:


1. Call `enableEngineStrategy` to enable the pre\-rendering strategy.

   ```TypeScript
   import { enableEngineStrategy, StrategyType } from '@byteplus/react-native-vod-player';
   
   enableEngineStrategy(StrategyType.PreRender, StrategyScene.SmallVideo);
   ```
   

2. Set pre\-rendering sources at the appropriate time:

   1. When the playback source data is first loaded or in a scenario of refreshing the page to display new data, call `setStrategySources` to set the playback source for the playlist.

      * Vid playback source:

         ```TypeScript
         import { setStrategySources } from '@byteplus/react-native-vod-player';
         
         const vidData = [
           {
             playAuthToken: 'playAuthToken1',
             vid: 'v0d032g1*******5q6nkalr3ig',
             cacheKey: 'v0d032g1*******5q6nkalr3ig'
           },
           {
             playAuthToken: 'playAuthToken2',
             vid: 'v0d032g1*******5q6nkalr3ig',
             cacheKey: 'v0d032g1*******5q6nkalr2ik'
           },
           // ...
           ];
         
         // Set the prerendering source for the playlist
         setStrategySources(vidData.map(u => createVidSource(u)));
         ```
         

      * DirectUrl playback source:

         ```TypeScript
         import { setStrategySources } from '@byteplus/react-native-vod-player';
         
         const urlData = [
           {
             url: 'https://demo/1.mp4',
             vid: 'v0d032g1***kalr3ig',
             cacheKey: 'v0d032g1***nkalr3ig'    
           },
           {
             url: 'https://demo/2.mp4',
             vid: 'v0d032g1***q6nkalr3ig',
             cacheKey: 'v0d032g1***q6nkalr2ik'
           },
         // ...
         ];
         
         // Set the prerendering source for the playlist
         setStrategySources(urlData.map(u => createDirectUrlSource(u)));
         ```
         

   2. If you need to add new sources to the playlist, call `addStrategySources`.

      ```TypeScript
      const newVidData = [...];
      addStrategySources(newVidData.map(u => createVidSource(u)));
      ```
      

3. Call `setPreRenderCallback` to set the prerendering strategy callback, then perform other actions on the engine instance based on your business. For instance, you can monitor `onPlayerCreated` and set the video fill mode, playback start time, and so on.

   ```TypeScript
   import {setPreRenderCallback} from '@byteplus/react-native-vod-player';
   import type {
     TTVideoEngine,
     VideoSource,
   } from '@byteplus/react-native-vod-player';
   
   setPreRenderCallback({
     // Prerendering player creation callback
     onPlayerCreated(player: TTVideoEngine, source: VideoSource) {
       // player: Player
       // source: Playback source
       // You can determine which playback source's playback instance hits prerendering based on the source's vid
       const vid = source.vid();
       // Set subtitles
       player.setSubtitleAuthToken('subtit***letoken');
     },
   });
   ```
   

4. When the user scrolls down to view the next video's view, call `getFirstFrameEngine`, pass in the `source` of the current view to check if pre\-rendering is completed, and display the video cover using the `setView` method.

   ```TypeScript
   import {
     createDirectUrlSource,
     getPreRenderEngine,
     setView,
     initPlayer,
     TTVideoEngine,
   } from '@byteplus/react-native-vod-player';
   import {useMemo, useRef} from 'react';
   
   // (Optional) If you need to specify the scaling mode during player initialization, additionally import FillModeType  
   // import { FillModeType } from '@byteplus/react-native-vod-player'; 
    
   // Index of the current view in the playlist
   const index = 2;
   // Playback data of the current view
   const data = {
     url: 'https://demo/1.mp4?auth_key=182***39',
     vid: 'v02dfa***m239jdg',
     cacheKey: 'v02dfag***imkm239jdg',
     poster:
       'https://demo.com/tos-***533b04/e12bf***4d15c2~tplv-vod-noop.image',
   };
   const viewId = useMemo<string>(() => `pre-player-${index}`, [index]);
   const playerRef = useRef<TTVideoEngine | undefined>();
   
   // ...
   
   const source = createDirectUrlSource(data);
   const preRenderEngine = getPreRenderEngine(source);
   if (preRenderEngine && index !== 0) {
     // If pre-rendering is successful, set the pre-rendering player container
     await setView(preRenderEngine, viewId);
     // Set the initial video scaling mode (FillModeType)
     // For enum values, refer to: https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-features#set-scaling-mode
     // setView(preRenderEngine, viewId, FillModeType.FillModeAspectFill);
     // Hold the player instance
     playerRef.current = preRenderEngine;
   } else {
     // If pre-rendering is failed, create the player using initPlayer
     const player = await initPlayer({viewId});
     player.setVideoSource(source);
     playerRef.current = player;
   }
   
   // Play
   playerRef.current?.play();
   ```
   


<span id="0d7fb9bb"></span>
### Sample code

BytePlus VOD provides detailed [pre-rendering sample code](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-sample-code) to help you better understand how to use the pre\-rendering feature.

<span id="8a89de3e"></span>
## Disabling strategies

Call `clearAllStrategy` when the user exits the short video page or switches to another page to disable all strategies and release resources.

```TypeScript
import { clearAllStrategy } from '@byteplus/react-native-vod-player';

// Disable all strategies
clearAllStrategy();
```
