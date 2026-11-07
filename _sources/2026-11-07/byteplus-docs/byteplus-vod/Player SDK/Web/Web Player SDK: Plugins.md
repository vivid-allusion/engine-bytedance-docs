---
title: "Web Player SDK: Plugins"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-plugins-web"
---

VePlayer uses plugins to implement its functionalities, whether they are simple buttons or include complex playback logic. This plugin\-based design improves the maintainability and flexibility of the code. VePlayer provides two types of plugins:


* Built\-in plugins. These plugins come pre\-packaged with VePlayer. You can obtain plugin instances, disable plugins, or configure plugins as needed.

* Business plugins. These are custom plugins that you can integrate into VePlayer. To use them, you need to register and configure the plugins yourself.


This article introduces the functionalities and usage of plugins in detail.

<span id="a3e200ef"></span>
## Working with plugins in VePlayer

<span id="9f81fd93"></span>
### Getting plugin instances

To get a plugin instance, use the `getPlugin` method and provide the plugin name as an argument. Once you have the plugin instance, you can call its APIs. Here's a sample code snippet:

```JavaScript
const playerSdkIns = new VePlayer({
  ...
})

// Get the PIP (Picture-in-Picture) plugin instance
const pipInstance = playerSdkIns.player.getPlugin('pip') 
// const pipInstance = playerSdkIns.player.plugins.pip

// Call the PIP plugin's API to switch to Picture-in-Picture mode
pipInstance.switchPIP()
```


<span id="5178c4d4"></span>
### Registering plugins

To use a business plugin, you need to set the `plugins` parameter when initializing the VePlayer instance and provide the plugin name to register it. Built\-in plugins do not require registration. Here's a sample code snippet:

```JavaScript
import DemoPlugin from 'demoplugin'

const playerSdkIns = new VePlayer({
  ...,
  plugins: [DemoPlugin],
})
```


You can also register a plugin after initialization by calling the `registerPlugin` method. Here's a sample code snippet:

```JavaScript
import DemoPlugin from 'demoplugin'

const playerSdkIns = new VePlayer({
  ...
})
playerSdkIns.player.registerPlugin(DemoPlugin)
```


<span id="e44c0ff1"></span>
### Disabling plugins

To disable built\-in plugins, you can use the following methods:


* When initializing the VePlayer instance, set the `ignores` parameter and provide the names of the plugins (case\-insensitive) that you want to disable. For example, to disable the playback rate adjustment and PiP plugins:

   ```JavaScript
   ignores: ['playbackRate', 'pip']
   ```
   

* For some plugins, you can disable or hide them as shown below:

   ```JavaScript
   controls: false,
   
   // Or
   controls: {
     disable: true,
   }
   ```
   


<span id="8664d2a2"></span>
### Configuring plugins

VePlayer allows you to configure the specific behavior of each plugin by providing the plugin name and its configuration options. For example, to configure the progress bar plugin:

```JavaScript
progress: {
   isDragingSeek: true, // Whether to update currentTime during dragging
   closeMoveSeek: true, // Whether to disable seeking by moving the slider
}
```


Please note that the above code is just an example and the actual configuration options may vary depending on the specific plugin.

<span id="e57ebd5a"></span>
## Built\-in plugins

VePlayer comes with built\-in plugins that are displayed by default or under specific conditions.

<span id="c425b0a3"></span>
### Built\-in plugins with UI

Below is a table listing the available built\-in plugins with UI.


|Plugin name (case\-insensitive) |Description |Whether displayed by default |
|---|---|---|
|controls |The control bar plugin |Yes |
|progress |The playback progress bar plugin |Yes |
|fullscreen |The fullscreen toggle plugin in the control bar, used to switch the current video to fullscreen. |Yes |
|playbackRate |The playback rate adjustment plugin for PC |Yes |
|PlaybackRateMobilePlugin |The playback rate adjustment plugin for H5 |Yes |
|volume |The volume adjustment plugin |Yes |
|sdkDefinitionPlugin |The resolution switching plugin |Displayed only when multiple resolutions are available |
|definitionMobilePlugin |The resolution switching plugin for H5 |Displayed only when multiple resolutions are available |
|time |The control bar plugin for displaying play time and duration |Yes |
|poster |The cover preview plugin |Only displayed when a cover image is available |
|start |The button for toggling between play and pause |Yes |
|enter |The loading button displayed during the initialization of the player |Yes |
|pip |The picture\-in\-picture plugin |Yes |
|sdkToastPlugin |The toast plugin |Displayed only when switching resolutions or resuming playback |
|sdkUnmutePlugin |The unmute plugin |Displayed only when the video is mute at the start of playback |
|sdkErrorPlugin |The error message plugin |Displayed only when a serious error occurs that prevents playback, shows the error message, and provides a retry function |
|DanmuPlugin |The Danmu plugin |No |
|progresspreview |The progress bar preview plugin for PC |No |
|MenuPlugin |The right\-click menu plugin |No |
|miniprogress |The mini progress bar plugin |No |
|screenShot |The screenshot shortcut |No |
|rotate |The rotate button |No |
|download |The download button |No |
|miniscreen |The button for entering mini window mode |No |
|dynamicbg |Dynamic background blur rendering plugin |No |


<span id="41d3afd9"></span>
### Built\-in plugins without UI

Below is a table listing the available built\-in plugins without UI.


|Plugin name (case\-insensitive) |Description |Whether enabled by default |
|---|---|---|
|keyboard |The shortcut key plugin for PC |Only enabled on PC |
|mobile |The user interaction plugin for mobile web |Only enabled on H5 |
|pc |The user interaction plugin for mobile PC |Only enabled on PC |
|HlsPlayer |The HLS playback plugin |Only enabled when playing non\-encrypted HLS videos |
|FLVPlayer |The FLV playback plugin |Only enabled when playing FLV videos |
|EncryptHlsPlugin |The encrypted HLS playback plugin |Only enabled when playing encrypted HLS videos |
|DashPlugin |The DASH playback plugin |Only enabled when playing DASH videos |
|Mp4EncryptPlayer |The encrypted MP4 playback plugin, also used to support MSE playback mode for MP4 videos |Only enabled when playing encrypted MP4 videos or enabling MP4 MSE playback mode |
|xgVodLogger |The quality log reporting plugin |Only enabled when `xgVodLogger` is configured |


<span id="ddb1dcff"></span>
## Business plugins

Configure the `plugins` option to import the business plugins provided by VePlayer.

<span id="8b134de6"></span>
### External subtitle

VePlayer supports displaying subtitles in the WebVTT format. To use external subtitles, you need to register the external subtitle plugin by adding `VePlayer.Subtitle` to the `plugins` parameter. You can then configure the plugin by setting the `Subtitle` parameter and providing a list of subtitles with their respective URLs, text, and default settings. Here's a sample code snippet:

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { Subtitle } from '@byteplus/veplayer';

const playerSdk = new VePlayer({
  id: 'mse',
  url: "https://xx.mp4",
  width: 600,
  height: 400,
  // Register the external subtitle plugin
  plugins: [VePlayer.Subtitle],
  // If you import the plugin using npm, use the following code
  // plugins: [Subtitle],
  // Configure the external subtitle plugin
  Subtitle: {
    isDefaultOpen: true,
    list: [
      {
        "url": "https://subtitle1.vtt",
        "text": "Chinese and English",
        "isDefault": true
      },
      {
        "url": "https://subtitle2.vtt",
        "text": "Chinese and Japanese",
        "isDefault": false
      }
    ]
  },
});
```


<span id="54f065ff"></span>
### Memory play

VePlayer supports memory play, which allows users to resume playing a video from where they left off in their last session. To enable memory play, you need to register the memory play plugin by adding `VePlayer.MemoryPlay` to the `plugins` parameter. You also need to provide a unique `memoryId` for the video through the `MemoryPlay` option. Here's a sample code snippet:

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { MemoryPlay } from '@byteplus/veplayer';
const playerSdk = new VePlayer({
    id: 'mse',
    url: "https://xx.mp4",
    width: 600,
    height: 400,
    // Register the memory play plugin
    plugins: [VePlayer.MemoryPlay],
    // To import the plugin using npm, use the following code
    // plugins: [MemoryPlay],
    MemoryPlay: {
        // Provide a unique memoryId
        memoryId: 'example_memory_id'
    },
});
```


By default, VePlayer uses the browser's `localStorage` API to store the playback time. This means that the stored playback time cannot be shared across different devices or platforms. If you need to share the playback time through a service, you can do so by calling the `getTime` and `saveTime` functions. The `getTime` function should retrieve the playback time for a given `memoryId`, and the `saveTime` function should save the playback time for a given `memoryId`. Here's a sample code snippet:

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { MemoryPlay } from '@byteplus/veplayer';

const playerSdk = new VePlayer({
    id: 'mse', 
    url: "https://xx.mp4",
    width: 600,
    height: 400,
    // Register the memory play plugin
    plugins: [VePlayer.MemoryPlay],
    // To import the plugin using npm, use the following code
    // plugins: [MemoryPlay],
    MemoryPlay: {
        memoryId: 'example_memory_id', // Provide a unique memoryId
        getTime: async (id) => {
            // ... async processing
            // const time = await getTimeApi(id);
            return time; // Return the playback time
        },
        saveTime: async (id, time) => {
            // Call the API to store the playback time
        }
    },
});
```


VePlayer stores the playback time when the page is hidden, the player is destroyed, or the page is unloaded. Please note that during page unload, if the provided `saveTime` function is asynchronous, the API call may not complete.

<span id="f423adf6"></span>
### Video mirroring

VePlayer offers a video mirroring feature. To enable this functionality, you simply need to register the mirroring plugin by including it in the `plugins` parameter when creating an instance of the player. See the sample code below:

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { MirrorPlugin } from '@byteplus/veplayer';

const playerSdk = new VePlayer({
  id: 'mse',
  url: "https://xx.mp4",
  height: 400,
  // Register the mirroring Plugin
  plugins: [VePlayer.MirrorPlugin],
  // To import the plugin using npm, use the following code
  // plugins: [MirrorPlugin],
});
```


<span id="a1241558"></span>
### **Playlist**

VePlayer supports the playlist feature, which allows you to automatically play videos in a given video list in sequential order. With a playlist, you can engage your viewers with a collection of your videos. VePlayer provides the playlist UI, as well as the **Open/Hide playlist** and **Play next** buttons. See the following picture for what a playlist looks like:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6aaa6914b9ff4070852cf2559fd5dfa3~tplv-goo7wpa0wc-image.image) </span>

To use the playlist feature, you need to register the playlist plugin when initializing the player instance. You can also configure the playlist through the`playListPlugin` parameter. See the following sample code:

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { PlayListPlugin } from '@byteplus/veplayer';

const playerSdkIns = new VePlayer({
  id: 'video',
  width: 800,
  height: 600,
  // Register the playlist plugin
  plugins: [VePlayer.playListPlugin],
  // To import the plugin using npm, use the following code
  // plugins: [PlayListPlugin],
  // Configure the playlist plugin
  playListPlugin: {
    list: [
      {
        url: 'xx.demo.com/1.mp4',
        poster: 'xx.demo.com/1.jpg',
        vid: '67ghsadd8a78s9df8',
        title: 'Remember to bring a little simple everyday',
      },
      {
        playAuthToken: 'demovideoplayAuthToken',
        poster: 'xx.demo.com/2.jpg',
        vid: '67ghsadd8a78s213df8',
        title: 'The night came quietly, with the heat and light',
      },
      {
        url: 'xx.demo.com/3.mp4',
        poster: 'xx.demo.com/3.jpg',
        vid: '67ghsaddhh78s9df8',
        title: 'Watching a beautiful fireworks at night will make you feel good',
      },
      {
        url: 'xx.demo.com/4.mp4',
        poster: 'xx.demo.com/4.jpg',
        vid: '67ghiodd8a78s9df8',
        title: 'Gentle and lazy sea breeze',
      },
    ],
  },
});
```


In addition, the playlist plugin provides APIs and events, which are explained as follows:

<span id="e15266be"></span>
#### **APIs**

The following example shows how to play the next video:

```JavaScript
// Play the next video
playerSdkIns.getPlugin('playListPlugin').next();
```


The table below lists the APIs supported by the playlist plugin.


|**API Name** |**Type** |**Parameter** |**Returns** |**Description** |
|---|---|---|---|---|
|next |`() => void` |None |None |Play the next video. If the current video is the last one, it will jump to the first video. |
|prev |`() => void` |None |None |Play the previous video. If the current video is the first one, it will jump to the last video. |
|changeList |`(items: listItem[]) => void` |Array of playlist items |None |Update the playlist. |
|setIndex |`(index: number) => void` |Index of the video to be played |None |Play a specified video. |


<span id="3f418038"></span>
#### **Events**

The following example shows how to listen for changes in the playlist item:

```JavaScript
playerSdkIns.on('play_list_item_change', data =>
  console.log('play_list_item_change, current item: ', data),
);
```


The table below lists the events supported by the playlist plugin.


|**Event** **enum** |**Parameter** |**Description** |
|---|---|---|
|play_list_change |Array of playlist items |Playlist update |
|play_list_item_change |Playlist item |Playlist item change |


<span id="3d2f3262"></span>
### Dynamic watermarking

VePlayer supports dynamic watermarking, which allows you to dynamically overlay custom text on the player. This helps track the source of leaks in copyrighted videos when screen recordings or other leaks occur. To use dynamic watermarking, you need to register the dynamic watermark plugin through the `plugins` parameter when instantiating the player, and then configure the dynamic watermark through the `dynamicwatermark` parameter. The following sample code will add the dynamic watermark to the player with the specified text:

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { DynamicWatermarkPlugin } from '@byteplus/veplayer';

var playerSdk = new VePlayer({
  id: 'mse',
  url: "https://voddemo-play.volcvod.com/dem0.mp4",
  width: 640,
  height: 360,
  codec: 'h264',
  // Register the dynamic watermark plugin
  plugins: [ VePlayer.DynamicWatermarkPlugin ],
  // To import the plugin using npm, use the following code
  // plugins: [DynamicWatermarkPlugin],
  // Configure the dynamic watermark plugin
  dynamicwatermark: {
    enable: true, // [Required] true-Enable, false-Disable.
    content: 'VePlayer SDK', // [Required] Watermark text. String type, displayed in one line without line breaks.
    // The following parameters are optional
    // displayType: 1, // Watermark display type. Number type, 0-Fixed position, 1-Full screen scroll (play container), 2-Random blinking. Default value is 1.
    // opacity: 0.3, // Opacity. Number type, range: [0~1]. Default value is 0.3.
    // tickerSpeed: 'MODERATE', // Movement speed. String type, "MODERATE"-Moderate, "FAST"-Fast, "SLOW"-Slow. No blinking if displayType is 0 and tickerSpeed is not set.
    // fontSize: 12, // Watermark font size. Number or String type, in pixels. String type must include the unit. Default value is 12.
    // fontColor: '#FFFFFF', // Watermark color. String type. Default value is "#FFFFFF".
    // top: undefined, // Watermark's top starting position relative to the play container. Number type, in pixels. Default value is 0.
    // left: undefined, // Watermark's left starting position relative to the play container. Number type, in pixels. Default value is 0.
    // right: undefined, // Watermark's right starting position relative to the play container. Number type, in pixels.
    // bottom: undefined, // Watermark's bottom starting position relative to the play container. Number type, in pixels.
  },
  vodLogOpts: {
    vtype: 'MP4',
    tag: 'Normal Video',
    line_app_id: 348293,
    line_user_id: 'veplayer_web_demo'
  }
});
```


<span id="1263c6ce"></span>
### Quality degradation

VePlayer supports quality degradation that automatically switches to a lower bitrate video based on network conditions. This helps to reduce buffering and improve the playback experience when playing videos with multiple bitrate options.

Before you can make use of the quality degradation feature, it's important to understand two terms: video freezing and long freezing.


* **Video freezing**: Video freezing occurs when the playback of a video is interrupted and needs to wait for certain processes to continue. This interruption can be caused by insufficient buffer or decoding issues. Video freezing starts when the `WAITING` event is triggered and ends when the `PLAYING` event is triggered. You can listen to these events using the following code:

   ```JavaScript
   veplayer.on(VePlayer.Events.WAITING, () => {
     console.log('Freezing starts')
     veplayer.once(VePlayer.Events.PLAYING, () => {
       console.log('Freezing ends')
     })
   })
   ```
   

* **Long freezing**: Long freezing refers to freezing that lasts for a significant amount of time. This usually happens due to poor network conditions or a high video bitrate. By default, VePlayer considers freezing that lasts longer than 5 seconds as a long freezing event. However, you have the flexibility to customize this duration threshold by modifying the `longWaitingTime` parameter. You can listen to long freezing events using the following code:

   ```JavaScript
   veplayer.on(VePlayer.Events.LONGWAITING, () => console.log('Long freezing occurred'))
   ```
   


When a long freezing event occurs, VePlayer triggers its quality degradation logic. This means that it automatically switches to a lower bitrate video or prompts the user to switch to a lower bitrate video. By doing this, it ensures a smoother playback experience by adapting the video quality to the current network conditions.

To implement the quality degradation feature, you need to follow these steps:


1. Register the quality degradation plugin by including it in the `plugins` parameter when you create the player.

2. Configure the plugin using the `DefinitionDemotePlugin` parameter.

3. Choose one of the resolution levels to be the automatic level. This level will be used when the user selects the automatic option.

4. Depending on the selected level, the player will trigger different resolution degradation logic.

   * For automatic level: If there is a long freezing during playback, the player will automatically switch to the next resolution level based on the degradation order you configured. If the lowest resolution level is reached, no further degradation will occur. After the network recovers, the player will not automatically switch back to high\-bitrate video playback. To enable automatic degradation, do the following:

      * Set the `isNeedAutoDemote` parameter to true.

      * Mark one of the resolution levels as the automatic level.

      * Configure the degradation order of the resolution levels using the `demotePriority` parameter.

   * For Non\-automatic level: If there is a long buffering, the player will display a prompt box in the upper left corner of the progress bar. This prompt box will remind the user about video freezing and provide a button to manually degrade to the next resolution level.


The sample code for quality degradation under different playback modes is as follows:


<Tabs>
<Tab zoneid="aKsLFYUEVd" title="DirectUrl">
<TabTitle>DirectUrl</TabTitle>

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { DefinitionDemotePlugin } from '@byteplus/veplayer';

var veplayer = new VePlayer({
    id: 'mse',
    url: "//demo.video.com/1.mp4",
    width: 640,
    height: 360,
    // Register quality degradation plugin
    plugins: [VePlayer.DefinitionDemotePlugin],
    // To import the plugin using npm, use the following code
    // plugins: [DefinitionDemotePlugin],
    // Configure quality degradation plugin
    DefinitionDemotePlugin:{
      // Configure the degradation order
      demotePriority: ['uhd', 'hd', 'ld']
    },
    // Specify the default level, and set the url to the corresponding url in the playList
    url: '',
    playList: [
      {
        streamType: 'hls',
        definition: 'ld',
        definitionTextKey: 'LD', // Resolution multi-language key
        url: '',
      },
      {
        streamType: 'hls',
        definition: 'hd',
        definitionTextKey: 'HD', // Resolution multi-language key
        url: '',
      },
      {
        streamType: 'hls',
        // Mark this level as automatic level
        definition: 'auto', 
        definitionTextKey: 'AUTO',
        // Mark the actual resolution mapped by automatic level
        mapDefinition: 'uhd',
        url: '',
      },
    ],
    languages: {
      // Resolution multi-language translation
      en: {
        SD: 'SD',
        LD: 'LD',
        HD: 'HD',
        UD: 'UD',
        UHD: 'UHD',
        AUTO: 'Auto',
      },
    },
  });
```



</Tab>
<Tab zoneid="ZVFdIURTwq" title="Vid">
<TabTitle>Vid</TabTitle>

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { DefinitionDemotePlugin } from '@byteplus/veplayer';

var veplayer = new VePlayer({
    id: 'mse',
    width: 640,
    height: 360,
    // Register quality degradation plugin
    plugins: [VePlayer.DefinitionDemotePlugin],
    // To import the plugin using npm, use the following code
    // plugins: [DefinitionDemotePlugin],
    // Configure quality degradation plugin
    DefinitionDemotePlugin:{
      // Configure the degradation order
      demotePriority: ['1080p', '720p', '480p', '360p'],
    },
    getVideoByToken: {
      playAuthToken: 'xxxplayAuthToken',
      defaultDefinition: '1080p',
      // Mark the 1080p level as automatic level
      autoDemoteDefinition: '1080p',
      // Set the multi-language key for the automatic level
      autoDemoteDefinitionTextKey: 'AUTO' 
    }
    // Resolution multi-language translation
    languages: {
      zh: {
        SD: 'SD',
        LD: 'LD',
        HD: 'HD',
        UD: 'UD',
        UHD: 'UHD',
        AUTO: 'Auto',
      },
    },
  });
```



</Tab>
</Tabs>


<span id="f60340a5"></span>
### Implementing Google IMA ads

This section shows you how to add [Google IMA ads](https://developers.google.com/interactive-media-ads/docs/sdks/html5/client-side/get-started) to your video using VePlayer. It covers both CDN and NPM integration, explores different ad options like VAST, VMAP, and schedules, and includes code examples to help you get started.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">This plugin is supported since v1.12.0.</div>


<span id="e2de98f0"></span>
#### Integration

```JavaScript
// To import the plugin using npm, use the following code
// import VePlayer, { AdsPlugin } from '@byteplus/veplayer'
// import '@byteplus/veplayer/index.min.css';

const playerSdk = new VePlayer({
  id: 'veplayer',
  width: 600,
  height: 400,
  streamType: 'hls',
  url: 'https://veplayer-vod-cdn.bytepluscdn.com/fc11b3b3fd9fb329d4921c5886ac0c88/79749259/dash/hls-v11187g50000cqaveufak5vaadei7u60/tos-sgcomm1-v-0ebc06aace7614ac-sg/5a9e879c72ef4dd6ab7a9588a6b16b00/main.m3u8?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=9a5fba0195f54553a78f0b8d1d87b435%2F20240730%2F%2F%2Faws4_request&X-Amz-Date=20240730T065937Z&X-Amz-Expires=315360600&X-Amz-Signature=35d167446077e20d3d41dc918ba54a7353871ad4607dde34c9f2102527aeae81&X-Amz-SignedHeaders=host&X-Amz-SignedQueries=X-Amz-Algorithm%3BX-Amz-Credential%3BX-Amz-Date%3BX-Amz-Expires%3BX-Amz-SignedHeaders%3BX-Amz-SignedQueries%3BX-Amz-UriRange%3Bsgw-endpoint&X-Amz-UriRange=0%2C+109&sgw-endpoint=veplayer-vod-cdn.bytepluscdn.com',
  vodLogOpts: {
    line_app_id: XXXX, // [Required] The Application ID, which is an integer value. You can obtain it from the SDK management > Applications page in the BytePlus VOD console.
  },
  plugins: [VePlayer.AdsPlugin],
  // To import the plugin using npm, use the following code
  // plugins: [AdsPlugin],
  ad: {
    adType: 'google-ima',
    ima: {
      adTagUrl: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_ad_samples&sz=640x480&cust_params=sample_ct%3Dnonlinearvpaid2js&ciu_szs=728x90%2C300x250&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&impl=s&correlator=',
    },
  },
});
```


<span id="bb35d7dc"></span>
#### Configurations

<span id="f4306e8d"></span>
##### ad


|Property |Type |Description |
|---|---|---|
|adType |string |(Required) Ad client that will be used to display advertisements.<br><br>Supported value:<br><br><br>* `google-ima`: Use the Google IMA SDK for ad insertion. |
|ima |object |IMA Configurations. |


<span id="ec03649f"></span>
##### ad.ima


|Property |Type |Description |
|---|---|---|
|adTagUrl |string |URL of the ad tag for IMA plugins, can be a URL to a VMAP or VAST file. |
|schedule |array |Load an entire advertising schedule, containing multiple ad breaks. |


<span id="117c2424"></span>
##### ad.ima.schedule


|Property |Type |Description |
|---|---|---|
|offset |string |When to play the configured ad tag.<br><br>Supported values:<br><br><br>* `pre`: (string) Ad plays as a preroll.<br><br>* `post`: (string) Ad plays as a postroll.<br><br>* (timecode): (string) Ad plays at a specific time, in `HH:MM:SS:sss` format. |
|tag |string |URL of the ad tag for IMA plugins. Must be a URL to a VAST file. |


<span id="c57de3c6"></span>
#### Examples

<span id="1c392331"></span>
##### Use VAST for preroll

```TypeScript
{
    url: '//pull-demo.volcfcdnrd.com/live/st-4536521.m3u8',
    ad: {
        adType: 'google-ima',
        ima: {
            // VAST
            adTagUrl: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&impl=s&correlator=',
        },
    },
}
```


<span id="5ee9ee12"></span>
##### Use VMAP for preroll, midroll and postroll

```TypeScript
{
    url: '//pull-demo.volcfcdnrd.com/live/st-4536521.m3u8',
    // MUST have if midroll exists
    hls: {
        disconnectTime: Number.POSITIVE_INFINITY,
        maxLatency: Number.POSITIVE_INFINITY,
    },
    ad: {
        adType: 'google-ima',
        ima: {
            // VMAP
            adTagUrl: 'https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/vmap_ad_samples&sz=640x480&cust_params=sample_ar%3Dpremidpostlongpod&ciu_szs=300x250&gdfp_req=1&ad_rule=1&output=vmap&unviewed_position_start=1&env=vp&impl=s&cmsid=496&vid=short_onecue&correlator=',
        },
    },
}
```


<span id="e850de3f"></span>
##### Use Schedule for preroll, midroll and postroll

```TypeScript
{
    url: '//pull-demo.volcfcdnrd.com/live/st-4536521.m3u8',
    // MUST have if midroll exists
    hls: {
        disconnectTime: Number.POSITIVE_INFINITY,
        maxLatency: Number.POSITIVE_INFINITY,
    },
    ad: {
        adType: 'google-ima',
        ima: {
            schedule: [
                {
                    offest: 'pre',
                    // VAST
                    tag: 'ad tag url'
                },
                {
                    offest: '00:00:15',
                    // VAST
                    tag: 'ad tag url'
                },
                {
                    offest: 'post',
                    // VAST
                    tag: 'ad tag url'
                },
            ]
        },
    },
} 
```


<span id="de7ab0fd"></span>
## Custom plug\-ins

When using VePlayer, you can extend the functionality of the player using a plug\-in mechanism. The plug\-in mechanism in VePlayer is defined based on the player lifecycle, providing commonly used APIs and related lifecycle callback functions. This mechanism allows you to perform specific functions at different stages of the player's lifecycle. You don't have to worry about how plug\-ins interact with the player, or about installing and uninstalling. You can customize the plug\-in configuration, instantiate plug\-ins based on the configuration when instantiating the player, and install these plug\-ins after player instantiation is complete. This allows you to add or remove specific plug\-ins as needed. A description of the custom plug\-in mechanism is provided below, along with examples.

<span id="088942ff"></span>
### Base type plug\-ins

<span id="b216ed03"></span>
#### BasePlugin

A `BasePlugin` is used to implement playback logic without a UI and contains the complete plug\-in lifecycle (except for the `render` method). The `pluginName` static attribute is a required parameter that is used as a unique identifier when installing and storing plug\-in instances. Example usage:

```JavaScript
// demoBasePlugin.js
import { BasePlugin } from '@byteplus/veplayer';
export default class DemoBasePlugin extends BasePlugin {
  /**
   * The name of the plugin (must be declared) will serve as the unique key value for the plugin instance.
   * This parameter is also the passthrough key value for the plugin's configuration on the SDK, for example:
   * var p = new VePlayer({
   *   demoBasePlugin: {
   *     text: 'This is the configuration information for the plugin demoBasePlugin.'
   *   }
   * })
   * After the plugin's afterCreate, you can access this configuration parameter via this.config.text.
   **/
  static get pluginName() {
    return 'demoBasePlugin';
  }

  static get defaultConfig() {
    return {
      text: 'This is the default text for the plugin demoBasePlugin.',
    };
  }

  constructor(args) {
    super(args);
  }

  afterPlayerInit() {
    // TODO: The logic after the player kernel calls start to initialize the playback source.
  }

  afterCreate() {
    // You can add DOM event listeners in afterCreate.

    this.on('play', () => {
      console.log('Play play callback');
    });
  }

  destroy() {
    // Logic when the player kernel is destroyed.
  }
}
```


<span id="9f604990"></span>
#### Plugin

`Plugin` is the base type with UI plug\-ins, derived from `BasePlugin`. In addition to having a full lifecycle callback, it also has a built\-in `render` method and some DOM\-related APIs. Example usage:

```JavaScript
import { Plugin } from '@byteplus/veplayer';

const { POSITIONS } = Plugin;

// demoPlugin.js
export default class demoPlugin extends Plugin {
  // The name of the plugin will serve as the unique key value for the plugin instance.
  static get pluginName() {
    return 'demoPlugin';
  }

  static get defaultConfig() {
    return {
      // It is mounted on the right side of the controls. If not specified, it is mounted on the root node of the player kernel by default.
      position: POSITIONS.CONTROLS_RIGHT,
    };
  }

  constructor(args) {
    super(args);
  }

  beforePlayerInit() {
    // TODO: The logic before the player kernel calls start to initialize the playback source.
  }

  afterPlayerInit() {
    // TODO: The logic after the player kernel calls start to initialize the playback source.
  }

  afterCreate() {
    this.icon = this.find('.icon');
    this.onIconClick = e => {
      console.log('Callback for clicking an element with the class icon');
    };
    this.onClick = () => {
      console.log('Click event on the current plugin root node.');
      const eventData = {a: 1 }
      this.emiit('custom_event', eventData) 
    };
    // Bind a click event to the element with the class name .icon inside the current plugin's root node.
    this.bind('.icon', 'click', this.onIconClick);
    // Bind a click event to the root node of the current plugin.
    this.bind('click', this.onClick);
    //TODO: Some logic after the plugin is instantiated.
  }

  destroy() {
    this.unbind('.icon', 'click', this.onIconClick);
    this.unbind('click', this.onClick);
    this.icon = null;
    // Some logic when the player kernel is destroyed.
  }

  render() {
    return `<div class="demo-plugin">This is a demo plugin<div class="icon"></div></div>`;
  }
}
```


<span id="c8e2875a"></span>
### Configuration items

<span id="ab51b729"></span>
#### position configuration item

The `position` plug\-in configuration item can be used to specify where the UI plug\-in is mounted in the DOM. The optional value is a static attribute of an enumeration value for the plug\-in type. The specific values are as follows:

```JavaScript
Plugin.POSITIONS = { 
  ROOT: 'root',                     // Mounted on the root node.
  ROOT_LEFT: 'rootLeft',            // Mounted on the left sidebar of the player container. 
  ROOT_RIGHT: 'rootRight',          // Mounted on the right sidebar of the player container. 
  ROOT_TOP: 'rootTop',              // Mounted on the top sidebar of the player container.
  CONTROLS_LEFT: 'controlsLeft',    // Mounted on the left side of the player control bar.
  CONTROLS_RIGTH: 'controlsRight',  // Mounted on the right side of the player control bar. 
  CONTROLS_CENTER: 'controlsCenter' // Mounted in the middle control bar position of the player control bar.
}
```


The defined positions are shown below:

**Default layout**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e926c25a65279e91e97232beee44314a.png) </span>

**Flex layout**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e39fafca559942b56234517f2fd42f1a.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you do not specify the <code>position</code> or the <code>root</code> parameter, the plug\-in is mounted under the root node by default.</div>


* <div data-tips="true" data-tips-type="tip">ROOT_TOP, ROOT_RIGHT, and ROOT_LEFT are automatically hidden when the player goes out of focus.</div>


* <div data-tips="true" data-tips-type="tip">In the flex layout on a small mobile phone screen, the middle position adapts automatically. The middle position is usually the progress bar.</div>



<span id="ad389d89"></span>
#### mode configuration item

The mode configuration item of the Controls plug\-in can be used to specify the layout of the control bar. The images below show the effect of the three layout methods:

**normal**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_955652db9b3f858b080611f0ab47d7a3.png) </span>

**flex**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_867654ae76519f7936b2366c0ea77821.png) </span>

**bottom**

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97977c6fd7186fa3a42cfadbdf6ad6de.png) </span>

<span id="5443f2a4"></span>
#### index configuration item

The `index` plug\-in configuration item is a number that specifies the position where the UI plug\-in is inserted on the parent node. The smaller the number, the higher the position. If the `index` values are the same, they are inserted in the order of registration. `index` can be used to adjust the order of plug\-ins by configuring the overlay.

<span id="a0a1b470"></span>
### API reference for the base type plug\-in

<span id="17c9c9a8"></span>
#### Lifecycle hook function

The `BasePlugin` provides lifecycle hook functions. These functions are called by the player at specific times, which facilitates the implementation of custom business logic. The following is the API definition of the base type plug\-in's lifecycle hook function:

```JavaScript
declare class BasePlugin {
    // A callback triggered when the plugin instance is created but before any other operations are performed. Information such as the player kernel (player) and plugin configuration (config) can be accessed from the args.
    beforeCreate(args: IBasePluginOptions): void;
    // A callback triggered after the plugin instance is created. At this point, all built-in objects, such as this.player, can be accessed. If it is a UI plugin, you can also access the current plugin's root node, such as this.el.
    afterCreate(): void;
    // A callback triggered before the player initializes the playback source. This is the only lifecycle hook where asynchronous operations can be performed. If executing asynchronous operations, please handle asynchronous errors properly to prevent blocking subsequent playback.
    beforePlayerInit(): void;
    // A callback triggered after all plugins created during the player kernel initialization are completed. At this stage, all registered plugin instances can be accessed for inter-plugin dependency interactions.
    onPluginsReady(): void;
    // A callback triggered after the player kernel executes the start logic and initializes the playback source.
    afterPlayerInit(): void;
    destroy(): void;
    // ...
}
```


<span id="26c4fefe"></span>
#### Static attributes or methods

The `BasePlugin` provides the following static attributes and methods:


* `pluginName`: The plug\-in name, which is the unique ID of the plug\-in. You need to pass in this name when fetching the plug\-in instance. For example, to fetch the built\-in `play` plug\-in instance:

   ```JavaScript
   const playPluginIns = playerSdk.getPlugin('play');
   ```
   

* `defineGetterOrSetter ()`: Used to define getters and setters for objects.

* `defaultConfig ()`: Used to define the default configuration for plug\-ins. For example, the default configuration of the built\-in `poster` plug\-in is as follows:

   ```JavaScript
   static get defaultConfig () {
     return {
       isEndedShow: true,
       hideCanplay: false,
       notHidden: false,
       poster: '',
       fillMode: 'fixWidth'
     }
   }
   ```
   


<span id="c21ac21b"></span>
#### Instance attributes

A `BasePlugin` instance contains the following basic attributes, which can be used to fetch information about the player kernel:


* `player`: The player kernel instance.

* `playerConfig`: Player kernel configuration.

* `pluginName`: Plug\-in name.

* `domEventType`: The event type supported by the current plug\-in. Return `touch` on the H5 side and return `mouse` on the PC side.

* `root`: If the current plug\-in is a UI plug\-in, it is the root node DOM of the UI and is fetched using `this.root`; otherwise it is `null`.


<span id="952be70e"></span>
#### Multilingual API

The `BasePlugin` provides the following multilingual\-related APIs:


* `get lang(): string;`: Current language, for example, `en` or `zh-cn`.

* `get i18n(): import("../lang/i18n").IXGI18nText;`: Current multilingual mapping configuration. You can use the key to fetch the translation of each text in the current language.

* `get i18nKeys(): {[propName: string]: string;};`: Current multilingual key.


<span id="12be1cac"></span>
#### Event APIs

The `BasePlugin` provides an event\-related API, which you can use to implement event listeners, remove listeners, and trigger events. The related API is defined below:


* `on(event: string | Array<string>, callback: Function)`: Adds an event listener. Use this API to listen for events with the specified name. Example code:

   ```JavaScript
   this.on(VePlayer.Events.PLAY, () => { 
     console.log('play') 
   }) 
   // Listen to multiple events simultaneously.
   this.on([VePlayer.Events.ENDED, VePlayer.Events.PAUSE], () => { 
     console.log('ended or pause') 
   }) 
   ```
   

* `once(event: string, callback: Function)`: Adds a one\-time event listener, that is, the event will not be listened to again after it has been triggered. Example code:

   ```JavaScript
   this.once(VePlayer.Events.PLAY, () => { 
     console.log('play') 
   }) 
   ```
   

* `off(event: string, callback: Function)`: Cancels the event listener. Example code:

   ```JavaScript
   this.off(VePlayer.Events.PLAY, () => { 
     console.log('play') 
   }) 
   // Unsubscribe from multiple event listeners simultaneously.
   this.off([VePlayer.Events.ENDED, Events.PAUSE], () => { 
     console.log('ended or pause') 
   }) 
   ```
   

* `offAll()`: Cancels the listener for all events in this plug\-in. Example code:

   ```JavaScript
   this.off(VePlayer.Events.PLAY, () => { 
     console.log('play') 
   }) 
   ```
   

* `emit(event: string, ...res: any[])`: Triggers a custom event. Example code:

   ```JavaScript
   this.emit('customEvent', () => { 
     console.log('customEvent') 
   })
   ```
   

   Custom events are not in the forwarded `VePlayer.Events` list, so you need to listen to custom events as follows:

   ```JavaScript
   playerSdk.on('ready', () => {
       // You can listen for custom events only after the core is ready.
       playerSdk.player.on('customEvent', (...args) => {
           console.log('customEvent', args);
       });
   });
   ```
   

* `emitUserAction(event: any, action: string, params?: {})`: Triggers a user action event named `VePlayer.Events.USER_ACTION`. The second parameter specifies the type of user event and the third parameter is the custom event parameter. Example code:

   ```JavaScript
   handleClick(e) {
     this.emitUserAction(e, 'custom_click', {name: 'custom_click'})
   }
   ```
   


<span id="a05b4125"></span>
#### Other built\-in APIs


* `show()`: Displays the current plug\-in. Example code:

   ```JavaScript
   // The default is to use block.
   plugin.show()
   // The specified display plugin name is flex.
   plugin.show('flex')
   ```
   

* `hide()`: Hides the current plug\-in.

* `find(selector: string)`: Searches under the root node of the current plug\-in. The `querySelector` used in the bottom layer. Example code:

   ```JavaScript
   // Get the DOM element with the class name .icon under the current UI plugin.
   this.icon = this.find('.icon')
   // Get the DOM element with the tag name li under the current UI plugin.
   this.lis = this.find('li')
   ```
   

* `bind(selector: string, event: string, handler: Function)`: Adds an event proxy to the DOM that matches the selector. The corresponding API to cancel the event proxy is `unbind`. Can be called during `destroy`. Example code:

   ```JavaScript
   // Event delegation for li a elements under the root node of the current UI plugin.
   this.bind('li a', 'click', this.clickHandler)
   this.unbind('li a', 'click', this.clickHandler)
   
   // Add an event listener to the root node of the current plugin, with the target element being this.el.
   this.bind('click', this.clickHandler)
   this.unbind('click', this.clickHandler)
   
   // Add the same event delegation for multiple events on the same selector.
   this.bind('li a', ['click', 'touched'], this.clickHandler)
   this.unbind('li a', ['click', 'touched'], this.clickHandler)
   ```
   

* `unbind(selector: string, event: string, handler: Function)`: Cancels the event proxy for the DOM that matches the selector, which can be called during `destroy`.

* `setStyle(name: string, value: string: string)`: Configures the style for the root node of the current UI plug\-in. Example code:

   ```JavaScript
   // Set a single style.
   this.setStyle('height', '40px')
   // Set multiple styles.
   this.setStyle({
     'height': '40px',
     'width': '40px'
   })
   ```
   

* `setAttr(name: string, value: string)`: Configures the attribute for the root node of the current UI plug\-in. Example code:

   ```JavaScript
   // Set a single property.
   this.setAttr('data-url', 'http://ixigua.com')
   // Set multiple properties.
   this.setAttr({
     'data-id': 1,
     'data-name': 'name' 
   })
   ```
   

* `setHtml (htmlStr: string, callback: Function)`: Resets the HTML structure of the current root node. Example code:

   ```JavaScript
   this.setHtml(<div class="icon">Reset icon</div>, () => {
     console.log('dom reset completed')
   })
   ```
