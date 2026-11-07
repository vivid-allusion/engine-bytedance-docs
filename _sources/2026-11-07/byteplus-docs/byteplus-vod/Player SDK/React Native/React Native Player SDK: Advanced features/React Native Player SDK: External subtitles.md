---
title: "React Native Player SDK: External subtitles"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-external-subtitles"
---

The "External subtitles" feature enables users to store subtitle files separately from video files and import them while playing the video.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is only supported by the Premium Edition. Please make sure you have purchased the Premium Edition license and added the appropriate dependency.</div>


<span id="6b5bdec1"></span>
## Prerequisites

Before adding the external subtitles, make sure you have:


* [Integrated the SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart).

* If you are playing videos in Vid mode, you need to prepare the subtitle file:

   * If you already have a separate subtitle file, you can upload the subtitle file on the **Video details** page in the [BytePlus VOD console](https://console.byteplus.com/vodpaas), as shown in the following picture.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b5b084b692e416bbbdcf5114f1a7814~tplv-goo7wpa0wc-image.image) </span>

   * If you don't have a separate subtitle file, you can use the [Smart captioning template](https://docs.byteplus.com/docs/byteplus-vod/docs-smart-subtitle-template) to generate the subtitle file.


<span id="bc92c1e8"></span>
## Enabling the external subtitles feature


1. After creating the player, call `enableSubThread` to enable the subtitle feature and improve subtitle loading performance.

   ```TypeScript
   const player = await initPlayer({viewId: 'player'});
   
   // Subtitle switch
   player.enableSubThread(true);
   ```
   

2. Call the `enableSubtitle` method to enable or disable subtitle parsing. When enabled, the player will parse subtitles and provide data through callbacks. If you pass in `false`, the player will stop parsing subtitles, and the subtitle callback will not be triggered. You can use this method as a switch for displaying subtitles.

   ```TypeScript
   // Enable subtitle parsing
   player.enableSubtitle(true);
   ```
   


<span id="3b644295"></span>
## Setting subtitle source

The Player SDK supports two methods to set the subtitle source. Choose the appropriate method based on your specific scenario.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">External subtitles for the pre\-rendered player can only be set within the <code>onPlayerCreated</code> pre\-render callback, where it is also recommended to add the subtitle callback to ensure proper functionality.</div>


<span id="315b532b"></span>
### (Recommended) Method 1: Using the subtitle URL

The application server provides the subtitle address, assembles subtitle data, and the client sets the subtitle information using the `setSubDesInfoModel` method. Ensure the `format` field accurately reflects the subtitle file type — using `webvtt` for WebVTT subtitles and `srt` for SRT subtitles.

```TypeScript
import { createDirectUrlSource } from '@byteplus/react-native-vod-player';

// Subtitle information
const subtitleInfo = {
  list: [
    {
      id: 1,
      language: 'cmn-Hans-CN',
      language_id: 1,
      url: 'https://demo.com/e87a83***961e?auth_key=17607***xt_plain',
      format: 'webvtt',
      sub_id: 1,
    },
    {
      id: 2,
      language: 'eng-US',
      language_id: 2,
      url: 'https://demo.com/e87a83***00eb0a6f3432e?auth_key=1760759306-****lain',
      format: 'webvtt',
      sub_id: 2,
    },
  ],
};
const source = createDirectUrlSource({
  vid: 'v0d032g1***5q6nkalr3ig',
  url: 'https://demo.com/9fc0da***7e97a10b7f9ca7?a=0&auth_key=1760758121-422b49c****w%3D%3D&vl=&vr=',
  cacheKey: 'v0d032g1***alr3ig',
});
player.setVideoSource(source);
// Set subtitle information
player.setSubDesInfoModel(subtitleInfo);
```


<span id="32ab8bcf"></span>
### Method 2: Using Vid and SubtitleToken

Set the subtitle source using Vid and SubtitleToken. Use the BytePlus VOD Server SDK to issue temporary playback tokens and subtitle auth tokens on the application server. Then, call `setSubtitleAuthToken` on the client side to set the subtitle source.

```TypeScript
import { createVidSource } from '@byteplus/react-native-vod-player';

// Video ID
const vid = 'videovid';
// Temporary playback token issued by the server
const playAuthToken = 'playAuthToken';
// Create plaback source
const source = createVidSource({
  vid,
  playAuthToken,
  cacheKey: vid,
});
// Set the video source
player.setVideoSource(source);
// Set the subtitle auth token for subtitle retrieval
player.setSubtitleAuthToken(subtitleToken);
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Ensure that the Vid used for generating <code>playAuthToken</code> and <code>subAuthToken</code> is the same as the one used for creating the source.</div>


<span id="9ee24779"></span>
## Setting subtitle callback

Call `setSubtitleCallback` to set the subtitle callback for updating subtitle status and displaying subtitle content.

```TypeScript
player.setSubtitleCallback({
  onSubtitleInfoCallback(subInfo) {
    // Callback for updating displayed subtitles
    console.log(`Subtitle updated to: ${subInfo.content}`);
  },
  onSubtitleInfoRequested(jsonInfo: string, error?: Error) {
    // Callback triggered when subtitles are requested during Vid playback
    if (!error) {
      const ids = player.getSubtitleIDs();
      if (ids && ids.length) {
        // Switch to the first subtitle
        player.switchSubtitleById(ids[0]);
      }
    }
  },
  onSubLoadFinished(success: boolean) {
    // Completion of current subtitle loading
    console.log(`Current subtitle load: ${success ? 'Success' : 'Fail'}`);
  },
  onSubSwitchCompleted(success: boolean, id: number) {
    // Completion of subtitle switch
    console.log(`Subtitle ${id} switch: ${success ? 'Success' : 'Fail'}`);
  },
});
```


The key callback is `onSubtitleInfoCallback`, which is triggered when subtitles change during playback, including clearing subtitles. Update the displayed subtitles based on the `subInfo` provided in the callback, which includes the subtitle content, duration, and playback time.

```TypeScript
import {useState} from 'react';

// ....

const [curText, setCurText] = useState('');
const [enableSub, setEnableSub] = useState(true);

player.setSubtitleCallback({
  onSubtitleInfoCallback(subInfo) {
    // Callback for updating displayed subtitles
    setCurText(subInfo.content)
  },
});

// ....

return (
    <View>
      {enableSub && (
          <View style={[styles.sub]}>
            <Text>{curText}</Text>
          </View>
      )}
    </View>
)
```


<span id="e74f948d"></span>
## Switching subtitles

Use `getSubtitleIDs` to retrieve the subtitle ID list and then call `switchSubtitleById` with the desired subtitle ID to switch subtitles.

```TypeScript
// Get the subtitle ID list
const ids = player.getSubtitleIDs();
// Switch subtitles
player.switchSubtitleById(ids[0]);
```


If you want to set a default subtitle for playback, call `switchSubtitleById` with the desired subtitle ID before calling `play`.

<span id="edb65005"></span>
## (Optional) Rendering a subtitle switch list UI

In Vid mode, you can render a subtitle switch list UI by handling the subtitle callback `onSubtitleInfoRequested`, which receives a JSON string parameter `jsonInfo`. After parsing this string, the resulting object contains a `list` property — an array whose items are all of the `SubDesInfoModel` type. Each item has the following data structure, with field meanings detailed in the [JSON subtitle information example](https://docs.byteplus.com/docs/byteplus-vod/docs-external-subtitles-android#1c8e6dcc):

```JSON
{
  id: number,
  language: string,
  language_id: number,
  url: string,
  format: string,
  sub_id: number,
}
```


You can use this list data to render the subtitle list UI as follows:

```TypeScript
onSubtitleInfoRequested(jsonInfo: string, error?: Error) {
    // For Vid playback, when subtitles are requested, the player callback is triggered, allowing you to call getSubtitleIDs to obtain the subtitle ID list
    if (!error) {
      try {
        const json = JSON.parse(jsonInfo);
        // Used to render the subtitle list UI
        setVidSubList(json.list);
      } catch (err) {
        console.error(err);
      }
    }
},
```


<span id="5ca2c4cb"></span>
## **Preloading external subtitles**

To improve the loading speed and success rate of subtitles, you can leverage the video preloading strategy to associate an external subtitle file with each video source, allowing it to be preloaded in advance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only one subtitle source can be preloaded per video source.</div>


The configuration method varies depending on the playback source type.

<span id="8179f109"></span>
### **DirectUrl source**

For `DirectUrl` sources, you must provide the complete list of available subtitles when creating the source and explicitly specify which one to preload. When calling `createDirectUrlSource`, pass the following two key parameters:


* `subtitleInfoModel`: A complete object containing information for all available subtitles.

* `subtitleId`: The `sub_id` of the specific subtitle you want to preload.


```TypeScript
import { createDirectUrlSource } from '@byteplus/react-native-vod-player';

const subtitleInfo = {
  list: [
    { language: 'cmn-Hans-CN', language_id: 1, url: '...', format: 'webvtt', sub_id: -987900477 },
    { language: 'eng-US', language_id: 2, url: '...', format: 'webvtt', sub_id: 1868145343 },
  ],
};

const urlSource = createDirectUrlSource({
    vid: 'your_vid_1',
    url: 'https://example.com/video.mp4',
    cacheKey: 'your_cache_key_1',
    // 1. Provide the complete subtitle list
    subtitleInfoModel: subtitleInfo,
    // 2. Specify the ID of the subtitle you want to preload (English subtitles in this case)
    subtitleId: 1868145343, 
});

// Add the configured video source to the preload task list
setStrategySources([urlSource, /* other sources */]);
```


When playing this video, you must first set the same subtitle information and then switch to the subtitle ID that was specified for preloading.

```TypeScript
// Enable the subtitle feature
player.enableSubThread(true);
player.enableSubtitle(true);

// 1. You must pass the same subtitleInfoModel used during preloading
player.setSubDesInfoModel(subtitleInfo);

// 2. Switch to the subtitle ID specified for preloading
player.switchSubtitleById(1868145343);
```


<span id="8c37c3f1"></span>
### **Vid source**

For `Vid` sources, the subtitle list is fetched dynamically, so the preloading process is different. You need to specify a target language, and the player will automatically preload the matching subtitle after the list is retrieved. When creating a `Vid` source, you must provide a `subtitleAuthToken` in addition to the `playAuthToken`.

```TypeScript
import { createVidSource } from '@byte/react-native-vod-player';

const vidSource = createVidSource({
   vid: 'your_vid_2',
   playAuthToken: 'your_play_auth_token',
   subtitleAuthToken: 'your_subtitle_auth_token',
});
```


Before starting the preload tasks, use the following functions to inform the preload module which language to prioritize:


* `setDefaultPreloadTaskFeature(languageId)`: Sets the target subtitle's [language ID](https://docs.byteplus.com/en/docs/byteplus-vod/docs-subtitle-language). The preloading module will search for and download the subtitle matching this ID. If a match is not found, it will default to preloading the first subtitle in the list.

* `setPreloadTaskFactory()`: Applies the settings and starts the preload tasks.


```TypeScript
// Set the target language for preloading to English (language_id = 2)
setDefaultPreloadTaskFeature(2);

// Start the preload tasks
setPreloadTaskFactory();

// You can also dynamically update the target language later
// setDefaultPreloadTaskFeature(1); // Update to Chinese
```


When playing the video, you need to find the subtitle that matches the `language_id` you set in Step 2 within the subtitle info callback, and then actively switch to it.

```TypeScript
// Enable the subtitle feature
player.enableSubThread(true);
player.enableSubtitle(true);

// Set the token required for subtitle requests
player.setSubtitleAuthToken('your_subtitle_auth_token');

// Set the subtitle callback to perform the switch after the list is fetched
player.setSubtitleCallback({
  onSubtitleInfoRequested: (jsonInfo, error) => {
    if (error) {
      console.error('Failed to request subtitle info:', error);
      return;
    }
    
    const data = JSON.parse(jsonInfo);
    // Assuming the target language_id for preloading was set to 2 (English)
    const targetLanguageId = 2; 
    
    // Find the subtitle that matches the preloaded language ID
    const targetSub = data.list.find((s: any) => s.language_id === targetLanguageId);
    
    if (targetSub) {
      // Switch to the target subtitle; this will use the cached data if available
      player?.switchSubtitleById(targetSub.sub_id);
    }
  },
});
```


<span id="1396c8d3"></span>
### **Verifying a successful preload**

Regardless of the source type, you can listen for the `onSubtitleHitCacheChange` event to confirm if a subtitle has successfully hit the preload cache.

```TypeScript
player.setListener({
  onSubtitleHitCacheChange: (subtitleKey, subCacheSize) => {
    if (subCacheSize > 0) {
        console.log(`Subtitle cache hit! Key: ${subtitleKey}, Size: ${subCacheSize} bytes`);
    }
  },
});
```


Preloading is a best\-effort optimization and its execution can be affected by network conditions, device performance, and the player's buffering strategy. If a preload task has not completed by the time you switch to the next video, the player will still request the subtitle file online as normal. Playback will not be affected, but the loading acceleration from preloading will not be available.
