---
title: "Web Player SDK: Basic features"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-web"
---

The VePlayer performs video playback by using the HTML5 `<video/>` tag and can meet most video playback needs. This article explains how to implement the basic functions of VePlayer.

<span id="bbe9f867"></span>
## Calling the API

The basic functions of VePlayer are implemented by the attributes or API operations of the player kernel. The sample code for fetching the player kernel is shown below:

```JavaScript
 const playerSdk = new VePlayer({
   id: 'video',
   width: 800,
   height: 500,
   url: 'xx.mp4'
 });

 playerSdk.on('ready', () => {
   // Obtain player kernel
  const player = playerSdk.player;
  console.log('player core', player);
 })
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Player kernel creation is an asynchronous process. It is not possible to fetch the kernel immediately after player instantiation because the creation of the kernel is not yet complete. You can fetch the player kernel using the <code>player</code> attribute of the SDK instance after the SDK triggers an event (such as the <code>ready</code> event).</div>


* <div data-tips="true" data-tips-type="tip">For a detailed description of the attributes and interfaces of the player kernel, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-player-sdk-player-kernel">Web Player SDK: Player kernel</a>.</div>


* Attributes for fetching the player kernel. The sample code below fetches the current playback time:

   ```JavaScript
   const playerSdk = new VePlayer({
     id: 'video',
     width: 800,
     height: 500,
     url: 'xx.mp4'
   });
   
   // ...
   // Get the current playback time
   const currentTime = playerSdk.player.currentTime;
   ```
   

* Method for calling the player kernel. The sample code below shows the method for calling the player:

   ```JavaScript
   const playerSdk = new VePlayer({
     id: 'video',
     width: 800,
     height: 500,
     url: 'xx.mp4'
   });
   
   // ...
   // Manually trigger playback
   const btn = document.getElementById('play_btn');
   btn.addEventListener('click', (e) => {
     playerSdk.player.play();
   })
   ```
   


<span id="343b061e"></span>
## Playing in Vid mode

If you have purchased and integrated the [BytePlus Video on Demand (VOD) service](https://www.byteplus.com/en/product/vod), you can play videos in Vid mode. This section describes the procedure for implementing `Vid+PlayAuthToken` video playback.

<span id="632573b8"></span>
### Fetching a temporary playback token

You need to use `Vid` to generate temporary playback tokens on the app server. In addition to information such as the video ID, the parameters of the temporary playback token can also specify the video resolution, transcoding type, container format, and other information. For more information, see [Playing videos with temporary playback tokens](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default video fetched is the unencrypted video in <code>mp4</code> format. If <code>playAuthToken</code> does not contain information such as the format and resolution, you can use <code>Format</code> and <code>Definition</code> in <code>reqParams</code> to pass through parameters. Further details on the parameters can be found in <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a>.</div>


<span id="e6715721"></span>
### Configuring parameters

When instantiating VePlayer, configure the `getVideoByToken` parameter and pass in the Vid playback configuration. For a detailed description of the parameters, see [IPlayAuthTokenConfig](https://docs.byteplus.com/docs/byteplus-vod/docs-web-api-reference#6311e54f). Sample code:

```JavaScript
const playerSdk = new VePlayer({
  id: 'player-container',
  width: 800,
  height: 500,
  lang: 'en',
  getVideoByToken: {
    playAuthToken: 'TemporaryplayAuthToken', // Need to obtain from the server
    definitionMap: {
      'original': {
        definition: 'ori',
        definitionTextKey: 'ORI'
      },
      '360p': {
        definition: 'ld',
        definitionTextKey: 'LD'
      },
      '480p': {
        definition: 'sd',
        definitionTextKey: 'SD'
      },
      '720p': {
        definition: 'hd',
        definitionTextKey: 'HD'
      }
    }
  },
  languages: {
    en: {
      ORI: 'Original',
      LD: 'Smooth',
      SD: 'SD',
      HD: 'HD'
    }
  },
});
```


VePlayer will fetch the video playback address from the VOD service. By default, the first address that meets the conditions is used as the playback address, and the resolution list is automatically set.

If you need to process the video information yourself, you can call the `Service` method provided by VePlayer to fetch the video playback address before the player is instantiated. Sample code is shown below.

```JavaScript
const Service = window.VePlayer.Service;

const playAuthToken = ' TemporaryplayAuthToken'; // need to obtain from the server
Service.url(playAuthToken, '//vod.volcengineapi.com').then((res) => {
  // Processing Video Information on the Business Side
  const player = new VePlayer({
    id: 'mse',
    width: 800,
    height: 500,
    url: res.PlayInfoList[0].MainPlayUrl,
  });
}).catch((e) => {
  console.log(e);
});
```


<span id="bb550bea"></span>
### Switching videos

If you need to switch the video asset, you can do so by passing in a new temporary playback token. Sample code:

```JavaScript
playerSdk.switchAuthToken({
    playAuthToken: 'new playAuthToken'
});
```


<span id="717c64d2"></span>
### Automatically updating the temporary playback token

Temporary playback tokens have a defined validity time, and we recommend that you fetch and use them only when playback is needed. If the temporary playback token expires, the video will not play. VePlayer provides the `onTokenExpired` event, which allows you to automatically update expired tokens. Sample code:

```JavaScript
const playerSdk = new VePlayer({
  id: 'video',
  width: 800,
  height: 500,
  getVideoByToken: {
    playAuthToken: 'video_playAuthToken'
  },
  onTokenExpired: () => {
    return new Promise(resolve => {
      // Call API to obtain a new temporary playback Token
      getNewToken().then(res => {
        resolve({
          playAuthToken: 'new playAuthToken', // New temporary playback Token 
          keyToken: 'new keyToken' // Pass in new keyToke when playing HLS encryption videos.
        })
      })
    });
  }
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>onTokenExpired</code> must be returned by an <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-web-api-reference#6311e54f">IPlayAuthTokenConfig</a> type asynchronous Promise function.</div>


<span id="06d750ed"></span>
## Fetching the playback status

`playerSdk.player.state` can be used to fetch the current playback status of the player. Sample code:

```JavaScript
const playerSdk = new VePlayer({
  id: 'video',
  width: 800,
  height: 500,
  url: 'xx.mp4'
});

// Gets playback state
const playerState = playerSdk.player.state;
```


The table below provides the enumeration values of the playback statuses.


|Name |Value |Description |
|---|---|---|
|ERROR |0 |A playback error occurred. |
|INITIAL |1 |Initialization in progress. |
|READY |2 |Configuration, events, plug\-ins, and other elements have been initialized, bound, or instantiated. |
|ATTACHING |3 |Media object mounting in progress. |
|ATTACHED |4 |The media object has been mounted in the DOM. |
|NOTALLOW |5 |Playback is blocked. |
|RUNNING |6 |Playback has started successfully and the player has entered the playback process. |
|ENDED |7 |Playback has ended. |
|DESTROYED |8 |The player kernel instance has been destroyed. |


<span id="ad54b612"></span>
## Listening for player error

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">It is highly recommended to <a href="https://docs.byteplus.com/docs/byteplus-vod/common-playback-configurations#8793e0fe">Configure cross\-domain access</a> for the domain used in the video playback address to facilitate SDK analysis of playback errors.</div>


Starting from version 1.10.0, when the player encounters an error that prevents it from continuing playback, it will display a playback error UI, which includes the error description, error code, browser\-based device ID, and playback time, as shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c728667e116471590f08feccee6edaa~tplv-goo7wpa0wc-image.image) </span>

In addition, the browser's console will also display more detailed error information, as shown in the figure below:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Sometimes, an error will be triggered multiple times during a single playback. Please refer to the first error message printed.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d9e12b92f5648a0bbd11b1dfc5160b1~tplv-goo7wpa0wc-image.image) </span>

You can also obtain error information by listening to the error event. The sample code is as follows:

```TypeScript
const playerSdk = new VePlayer({
    // ...
});

interface IVeError {
  playerVersion: string; // Player version
  currentTime: number; // Playback time of the video when the error occurred
  duration: number; // Video duration
  ended: boolean; // Whether playback is complete
  readyState: number; // Video readiness state
  networkState: number; // Network state
  src: string; // Video address
  errorType: VE_ERROR_TYPE_MAP; // Error type
  errorCode: number; // Error code
  httpCode?: number; // Playback address HTTP code
  message: string;  // Error message
  mediaError?: MediaError; // Media element error object
  originError?: string; // Original error stack
  host: string; // Video address domain
  veErrorCode?: number; // Error code (added since 1.10.0)
  veErrorType?: string; // Error type (added since 1.10.0)
  veErrorMessage?: string; // Error message (added since 1.10.0)
  displayMessage?: string;  // Error message displayed in the player UI
  videoInfo: {
    isMSE?: number; // Whether MSE
    vtype?: string; // Video format
    drmEncryptType?: string; // Encryption type
    vid?: string; // Video vid
  };
  ext: unknown; // Extended information
  ex?: string; // Other information
}

// Listen for player error information
playerSdk.on(VePlayer.Events.ERROR, (err: IVeError) => {
  console.error('player error: ', err);
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">For the specific meaning of the veErrorCode error code and corresponding recommended handling methods, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-error-code#0a81251d">Error codes of the Web Player SDK</a>.</div>


If you are still unable to determine the cause and handling method of the error, please follow these steps to further troubleshoot the issue:


1. Copy the device ID on the playback error UI interface. The device ID corresponds to the `vodLogOpts.line_user_id` field in your player instantiation configuration. If this field is not configured, the system will automatically generate a random ID.

2. Go to the BytePlus VOD console's **Endpoint tracker** page, enter the device ID, and search for playback details related to that device. For more information, please refer to [Endpoint tracker](https://docs.byteplus.com/docs/byteplus-vod/docs-end-point-tracker).

3. If you still cannot locate the issue, please take screenshots of the error UI and the error message printed in the browser console, and then [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) to contact the BytePlus technical support team.


<span id="e2664428"></span>
## Setting volumes

Volume settings include volume adjustment and mute settings. The default UI of VePlayer provides a volume settings plug\-in, which you can use to adjust the volume or mute/unmute. You can use the following methods to customize the UI:


* Sample code for volume settings:

   ```javascript
   // Configure the volume by passing the "volume" parameter during instantiation.
   const playerSdk = new VePlayer({
     id: 'video',
     width: 800,
     height: 500,
     volume: 0.2,
     url: 'xx.mp4'
   });  
   
   // Set the volume using the "player" instance.
   playerSdk.player.volume = 0.2;
   ```
   

* Sample code for mute settings:

   ```javascript
   playerSdk.player.muted = false;
   ```
   


<span id="d0bda33d"></span>
## Setting playback speed

VePlayer has a default playback speed configuration plug\-in that provides the playback speed options 0.5x, 0.75x, 1x, 1.25x, 1.75x, and 2x. Users can adjust the playback speed as desired. If you want to configure a different speed, you can use the sample code below.

```JavaScript
const playerSdk = new VePlayer({
  id: 'video',
  width: 800,
  height: 500,
  url: 'xx.mp4'
});  

// Setting the playback speed
playerSdk.player.playbackRate = 3;
```


The sample code for fetching the current playback speed is shown below:

```JavaScript
const playbackRate = playerSdk.player.playbackRate
```


<span id="6d28cb6b"></span>
## Switching the resolution

VePlayer provides a resolution switching plug\-in that allows users to switch between different video resolutions. The actual effect is shown in the image below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc17ac4e750244a2a94b9fecd948290a~tplv-goo7wpa0wc-image.image) </span>

<span id="14d52d49"></span>
### Displaying multiple resolutions

To enable the resolution switching function, you need to prepare multiple versions of the same video in different resolutions. You can use the BytePlus VOD media processing function to fetch different resolution versions of the same video. See [Audio and video transcoding](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-and-video-transcoding) for more information.

The method for implementing the display resolution switching plug\-in differs among different playback modes.


<Tabs>
<Tab zoneid="iL8iY2VlK4" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

If you play videos using the `vid` and `playAuthToken`, the BytePlus VOD service will send video playback URLs with multiple resolutions to the SDK. The SDK will automatically display a resolution switch icon. If you want to customize the text for each resolution, you can set the `definitionMap` parameter as shown in the following example code:

```JavaScript
const playerSdk = new VePlayer({
    id: 'video',
    width: 800,
    height: 500,
    getVideoByToken: {
        playAuthToken: 'yourplayAuthToken',
        definitionMap: {
            'original': 'Original',
            '360p': 'ld',
            '480p': 'sd',
            '720p': 'hd',
            '1080p': 'uhd·',
        },
    },
});
```



</Tab>
<Tab zoneid="BRtDZZBsOh" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

If you videos using URLs, you need to set the `playList` parameter. Each object in the array should contain the `url` parameter and the `definition` parameter. Here's an example code:

```JavaScript
const playerSdk = new VePlayer({
    id: 'video',
    width: 800,
    height: 500,
    playList: [
        {
            url: 'xx480.mp4',
            definition: 'sd'
        },
        {
            url: 'xx720.mp4',
            definition: 'hd'
        },
        {
            url: 'xx1080.mp4',
            definition: 'uhd'
        }
    ]
});
```



</Tab>
</Tabs>


<span id="7ca3e5f8"></span>
### Displaying one resolution

In the following scenarios where there is only one video resolution, VePlayer does not display the resolution switching plug\-in by default:


* Only the `url` address is set in the instantiation parameters.

* Only one stream is set in `playList`.

* The server returns only one stream during Vid mode playback.


If you still want the resolution switching plug\-in to be displayed, set the `alwaysShowDefinition` instantiation parameter to `true`. If you also need to customize the text for this resolution, the implementation differs for different playback modes. Sample code:


<Tabs>
<Tab zoneid="mMoacCC1if" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

Using Vid+PlayAuthToken mode to play sample code as below：

```javascript
{`
```



</Tab>
<Tab zoneid="IR07YXdkfu" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

Using DirectUrl mode to play. Sample code as below：

```javascript
{`
```



</Tab>
</Tabs>


<span id="96b01b51"></span>
## Looping videos

Set the `loop` player parameter to `true` to enable loop playback. Sample code:

```JavaScript
const playerSdk = new VePlayer({
  id: 'video',
  width: 800,
  height: 500,
  loop: true,
  url: 'xx.mp4'
});
```


<span id="8fd6b1f6"></span>
## Playing videos automatically

When Autoplay is enabled, video playback starts automatically after a page has loaded without the need for active interaction by the user (such as clicking the mouse or tapping the screen). Autoplay can be implemented through `autoplay` configuration, when the JavaScript code calls the `play()` method, or through functions such as timers, Promise callbacks, and event listeners.

This feature allows videos to start playing immediately after the page loads, without the user having to manually click the play button.

> Due to restrictions in browser policies, autoplay is not always successful. Browsers, considering the user's perspective, deem it annoying, inconvenient, or offensive for a webpage or application to emit sound automatically without warning. Therefore, autoplay is generally only allowed in specific circumstances.


<span id="cbd60c3b"></span>
### Autoplay configuration and conditions

VePlayer provides four autoplay configurations: `autoplay`, `autoplayMuted`, `enableDegradeMuteAutoplay`, and `enableUserActionAutoplay`. For more information, see [IPlayerConfig](https://docs.byteplus.com/docs/byteplus-vod/docs-web-api-reference#1e8bd55c). However, for autoplay to be successful, the following conditions must be met in the respective browser environments.

<span id="a75e3153"></span>
#### Playing videos automatically on PC

According to the latest PC browser policies, at least the following conditions must be met to allow autoplay:

> For details, see [Google Chrome](https://www.chromium.org/audio-video/autoplay/) for autoplay policies.


* The audio is muted or the volume is set to 0.

* Autoplay is allowed in the following circumstances:

   * The user interacts with the web page (includes clicking, tapping, or pressing a key)

> The callback of the interaction action must be able to track the actual user interaction in the context of the execution of `play ()`. Counterfeit user interactions are not accepted.


   * The website has been allowlisted. If the browser determines that users interact with the media frequently, it will be allowlisted to allow autoplay. In some cases, users can configure this themselves.

      * Chrome automatically evaluates whether to allow autoplay on a site using the Media Engagement Index (MEI).

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can check a site's MEI score at <code>chrome://media-engagement/</code>. Because the browser score is different for each user, some users may be able to autoplay videos on a website while others may not. However, as a user interacts with the website more, their score will increase and they will eventually be able to autoplay videos.         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Some of the most popular video sites, such as Tencent Video, bilibili, and YouTube, have higher rates of site visitor interaction and most users allow autoplay, so these sites are automatically added to the autoplay allowlist by the Chrome algorithm. For more information, see <a href="https://www.chromium.org/audio-video/autoplay/autoplay-pre-seeding-in-chrome/">Autoplay Pre\-Seeding in Chrome</a>.         </div>
         

      * In Safari, users can choose to allow autoplay on a site under **Settings \> Websites \> Auto\-play** or by **right\-clicking in the address bar**.

* The top frame can delegate autoplay permissions to its iframe to allow audio to be played automatically.


<span id="c00704a7"></span>
#### Playing videos automatically on H5 and mobile WebView

Autoplay with sound is disabled by default on H5 and mobile WebView. You can choose to **automatically mute playback**. Sample code:

```javascript
const playerSdk = new VePlayer({
  // ...
  autoplay: true,
  autoplayMuted: true,
  // enableDegradeMuteAutoplay: true, // Enable automatic degradation mute playback; sound playback is not supported.时自动降级到静音自动播放
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It is important to note that muted autoplay will always fail in the following cases:</div>



* <div data-tips="true" data-tips-type="tip">In iOS low power mode, even if the WebView autoplay parameter has been added or videos are muted by default, autoplay will still not be possible, because the system identifies video playback as energy\-consuming behavior.</div>


* <div data-tips="true" data-tips-type="tip">As a result of <a href="https://developers.weixin.qq.com/community/develop/doc/000e640d77cfa001132a6cb8456c01">changes to the Android WeChat WebView autoplay policy</a>, all forms of autoplay are prohibited in Android WeChat.</div>



If you are running the web application on a business\-controlled WebView, you also need to enable the WebView autoplay configuration to allow autoplay.


* For Android, configure [setMediaPlaybackRequiresUserGesture](https://developer.android.com/reference/android/webkit/WebSettings.html#setMediaPlaybackRequiresUserGesture(boolean)). Example code:

   ```java
   myWebView.getSettings().setMediaPlaybackRequiresUserGesture(false);
   ```
   

* For iOS WKWebView, configure [mediaTypesRequiringUserActionForPlayback](https://vsop.byteintl.net/docs/4/68693). Example code:

   ```objectivec
   [self.webvie mediaTypesRequiringUserActionForPlayback:NO];   
   ```
   


<span id="f9bdd0cc"></span>
### Determining whether autoplay was successful

You can use the following methods to determine whether autoplay was successful.

<span id="7d737962"></span>
#### Determinating success based on the API return result

Calling `play()` by using JavaScript code to enable autoplay is not always successful.

In general, you can determine whether it was successful based on the result of the Promise operation returned by `play ()`:


* If successful, a Promise result with the status of `resolve` is returned.

* If unsuccessful, a Promise result with a `NotAllowedError` and status of `rejected` is returned.


Example code:

```javascript
let startPlayPromise = playerSdk.player.play();

if (startPlayPromise !== undefined) {
  startPlayPromise.catch(error => {
    if (error.name === "NotAllowedError") {
      // TODO Do something when not autoplay success
    } else {
      // Handle a load or playback error
    }
  }).then(() => {
    // Start whatever you need to do only after playback
    // has begun.
  });
}
```


<span id="244d9a5a"></span>
#### Checking for autoplay failure events

You can monitor the following Web Player SDK events to determine whether autoplay is blocked:


* `autoplay_was_prevented`

* `autoplay_failed`


Example code:

```javascript
const playerSdk = new VePlayer({
  // ...
  autoplay: true,
});
playerSdk.on('autoplay_was_prevented', () => {
  // TODO something
  console.log('Autoplay is blocked.');
});
```


> If autoplay is `muted` by default and the mute attribute of the player is set to `true` when no user interaction is detected (`playerSdk.player.muted = false`), the browser will force the video to pause in a browser environment that does not support autoplay with sound.


<span id="d3193262"></span>
## Automatically refreshing playback assets after expiration

The video playback URL you fetch from the VOD service has the [Anti-hotlinking with timestamp](https://docs.byteplus.com/docs/byteplus-vod/docs-timestamp-) function enabled by default. During the video playback process, the video URL may expire because the video URL has not been used in time or the user has performed operations such as Seek playback or loop. In this case, the user cannot continue watching the video. VePlayer provides a corresponding event to monitor whether the video playback URL has expired, and allows you to configure the automatic refresh of the video playback URL. With this configuration, even if the video playback URL expires, VePlayer can automatically fetch a valid playback URL, allowing the user to continue watching the video.

<span id="8cd1a0f9"></span>
### Checking whether the playback asset has expired

<span id="6caedfaf"></span>
#### Method 1: Monitor expiration using timestamp comparison

To do this, you need to specify the expiration timestamp for the playback asset. The player polls the client\-side time of the player and compares it with the expired timestamp. At 60 seconds before expiration, the SDK triggers the `Events.MEDIA_EXPIRED` event, indicating that the URL is about to expire.


<Tabs>
<Tab zoneid="e1bumkz9mu" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

When playing in Vid mode, the player automatically fetches the expiration timestamp for each URL. Therefore, to enable URL expiration detection, you simply need to set the `enableUrlExpireCheck` parameter to `true` when instantiating the player. Example code:

```TypeScript
const playerSdk = new VePlayer({
        id: 'video-container',
        getVideoByToken: {
          playAuthToken: 'playAuthTokenxxxx'
        },
        // Enable address expiration detection.
        enableUrlExpireCheck: true,
        vodLogOpts: {
            vtype: 'MP4',
            tag: 'Normal video',
            line_app_id: xxxx,
            line_user_id: 'veplayer_web_demo'
        }
});

playerSdk.on(VePlayer.Events.MEDIA_EXPIRED, (err) => {
      console.log('Address expired', err);
})
```



</Tab>
<Tab zoneid="IQPysegY0N" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

In DirectUrl mode, when your app server sends a URL to the web client, the URL must have an expiration timestamp.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If your app server fetches video playback URLs from a BytePlus VOD service through the <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a> SPI operation, you need to send the <code>MainUrlExpire</code> of each URL to the web client as an expiration timestamp.</div>


When instantiating the player, you need to:


* Set the `enableUrlExpireCheck` parameter to `true` to enable expiration detection.

* Set `urlExpireTimestamp` to the expiration timestamp for this URL.


Example code:

```TypeScript
const playerSdk = new VePlayer({
        id: 'video-container',
        // 1724135102 in the address is an expired timestamp
        url: 'https://voddemo.demo.com/453b1f794dfa49f4819b5d923658411a?auth_key=1724135102-UCQrGayCc9-uxue-c1b5966b82630cd45eefaa0f73b9137a',
        // enable URL expiration check
        enableUrlExpireCheck: true,
        // Expired timestamp setting
        urlExpireTimestamp: 1724135102,
        vodLogOpts: {
            vtype: 'MP4',
            tag: 'Normal video',
            line_app_id: xxxx,
            line_user_id: 'veplayer_web_demo'
        }
    });

playerSdk.on(VePlayer.Events.MEDIA_EXPIRED, (err) => {
      console.log('URL expired ', err);
})
```


If the video has multiple resolutions, each corresponding to a different expiration timestamp, you can set the `urlExpireTimestamp` expiration timestamp individually for each URL in the `playList` playlist configuration item.

Example code:

```TypeScript
const playerSdk = new VePlayer({
        id: 'video-container',
        // Enable URL expiration check
        enableUrlExpireCheck: true,
        playList: [
            {
              url: 'https://voddemo.demo.com/e826c993a2444058915fb494c4fcdabb?a=0&auth_key=1817600800-8882fc603afb49edbb2665e62c95c69b-0-32390643c8637e4d3e46e87a684d5a4b&br=660&bt=660&cd=0%7C0%7C0&ch=0&cr=0&cs=0&cv=1&dr=0&ds=3&er=0&l=20220708180015010204028132080F0005&lr=&mime_type=video_mp4&net=0&pl=0&qs=0&rc=amg6c2o0aTg6ZTQzNGRnM0ApZzg6ZzkzZTxoN2QzNGY3NWdfZy9gMHFrYTBgLS1kYy9zc2IwNS4wM2NhYjZhMi4wNTY6Yw%3D%3D&vl=&vr=',
              definition: '1080p',
              // Expired timestamp setting
              urlExpireTimestamp: 1817600800,
            },
            {
              url: 'https://voddemo.demo.com/453b1f794dfa49f4819b5d923658411a?auth_key=1717582800-830c08a311bb49fab40dbaa90ebd4db3-0-1b61cbd491235c69d89a694bd51a1027',
              definition: '720p',
              // Expired timestamp setting
              urlExpireTimestamp: 1717582800,
            },
        ],
        vodLogOpts: {
            vtype: 'MP4',
            tag: 'Normal video',
            line_app_id: xxxx,
            line_user_id: 'veplayer_web_demo'
        }
    });

playerSdk.on(VePlayer.Events.MEDIA_EXPIRED, (err) => {
      console.log('URL expired', err);
})
```



</Tab>
</Tabs>


<span id="5aa8a896"></span>
#### Method 2: Monitor playback errors

If the expiration time of the video playback URL is unknown, the player will trigger a network error when the URL expires.

To confirm whether the error was caused by an expired URL, the player will actively verify the validity of the URL. Once the player confirms that the URL has expired, it will trigger a URL expiration event to notify that the video asset has expired.

For this function to work properly, the domain name used in the video playback URL must be configured with an HTTP response [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) header.

You can [Configuring HTTP request headers](https://docs.byteplus.com/docs/byteplus-vod/docs-http-response-headers#ad2445c3)[ ](https://docs.byteplus.com/en/docs/byteplus-vod/docs-http-response-headers)using the BytePlus VOD console. We recommend the following configuration:


|Response header name |Response header value |
|---|---|
|Access\-Control\-Allow\-Origin |`*` or contains the origin of the business web page |
|Access\-Control\-Allow\-Methods |`*` or contains `GET,HEAD,OPTIONS` |
|Access\-Control\-Expose\-Headers |`*` or contains the range |


<span id="0ccb8a8e"></span>
### Refreshing the playback asset

You can use the two methods below to refresh the playback asset after it expires.

<span id="92c45ca2"></span>
#### Actively updating the playback asset after detecting an expiration event

You can listen for the `Events.MEDIA_EXPIRED` expiration event. In the listener callback, you can do the following:


1. Fetch new playback asset data from the application server. The playback asset data can be the video playback `URL`, `playList` or `vid`, and `playAuthToken`, and should also contain the `urlExpireTimestamp` expiration timestamp of the new URL.

2. Call the `updateMediaSource` method provided by the SDK to pass the new playback asset data into the SDK.


Sample code:

```TypeScript
const playerSdk = new VePlayer({
  id: 'video-container',
  url: 'https://veplayer.demo.com/453b1f794dfa49f4819b5d923658411a?auth_key=1717547753-UCQrGayCc9-xiong-c1b5966b82630cd45eefaa0f73b9137a',
  enableUrlExpireCheck: true,
  urlExpireTimestamp: 1717547753,
  vodLogOpts: {
    vtype: 'MP4',
    tag: 'Normal video',
    line_app_id: xxx,
    line_user_id: 'veplayer_web_demo',
  },
});

// Monitor expired events
playerSdk.on(VePlayer.Events.MEDIA_EXPIRED, err => {
  console.log('Address expired ', err);
  // Re-acquire a new video playback address and its expiration timestamp from the business server.
  appServer.getPlayUrl().then((res) => {
    playerSdk.updateMediaSource({
      url: res.url,
      urlExpireTimestamp: res.urlExpireTimestamp,
    });
  })
});
```


<span id="21995074"></span>
#### Configuring an expiration callback to automatically refresh the playback asset

You can configure the `onMediaExpired` callback function when you instantiate the player. The callback function should return a data object containing information about the playback asset, which can be the video playback `URL`, `playList` or `vid`, and the `playAuthToken`.

The data object also needs to contain the `urlExpireTimestamp` expiration timestamp for the new URL. When the `Events.MEDIA_EXPIRED` event is triggered, the player automatically calls the `onMediaExpired` callback function and uses the result it returns as the input for the `updateMediaSource` method. This automatically updates the playback asset. Example code:

```TypeScript
const playerSdk = new VePlayer({
        id: 'video-container',
        url: 'https://veplayer.demo.com/d174bc4b9b32482582d3a07816a2104a/main.m3u8?auth_key=1718253922-987655e64a9f4c0dbf568f6397bd6232-0-5c0fa62ad9bcbee2c024b55824350d43',
        enableUrlExpireCheck: true,
        urlExpireTimestamp: 1618246275,
        onMediaExpired: async () => {
          // Re-acquire a new video playback address and its expiration timestamp from the business server.
          const res = await appServer.getPlayUrl();
          return {
            url: res.url,
            urlExpireTimestamp: res.urlExpireTimestamp,
          };
        },
        vodLogOpts: {
            vtype: 'MP4',
            tag: 'Normal video',
            line_app_id: xxx,
            line_user_id: 'veplayer_web_demo'
        }
});

playerSdk.on(VePlayer.Events.MEDIA_EXPIRED, (err) => {
      console.log('Address expired', err);
})
```


<span id="4ce88ba0"></span>
## Configuring the playback asset with `<source />`

VePlayer supports the use of the HTML `<video/> element in the`

[element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/source) to configure video assets in multiple formats in order to ensure compatibility with different browser environments.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">URLs configured with the <code><source/></code> element do not support MSE (Media Source Extension) playback scenarios, such as playing HLS video on PCs or HLS encrypted video on Android devices.</div>


To configure video assets in multiple formats, you need to describe the URL as an array. Each array item should contain the video playback URL `src` and the video container format `type`.

Here, type describes the MIME `type` of the video format, and only supports the playback of video container formats that are directly supported by the browser.

The common container formats and their corresponding MIME types and file extensions are listed below:


|Container format name |Audio ||Video ||
|---|---|---|---|---|
||MIME type |Extension name |MIME type |Extension name |
|3GP |audio/3gpp |.3gp |video/3gpp |.3gp |
|ADTS (Audio Data Transport Stream) |audio/aac |.aac |— |— |
|FLAC |audio/flac |.flac |— |— |
|MPEG\-1/MPEG\-2 (MPG or MPEG) |audio/mpeg |.mpg<br><br>.mpeg |video/mpeg |.mpg<br><br>.mpeg |
||audio/mp3 |.mp3 |||
|MPEG\-4 (MP4) |audio/mp4 |.mp4<br><br>.m4a |video/mp4 |.mp4<br><br>.m4v<br><br>.m4p |
|Ogg |audio/ogg |.oga<br><br>.ogg |video/ogg |.ogv<br><br>.ogg |
|QuickTime Movie (MOV) |— |— |video/quicktime |.mov |
|WAV (Waveform Audio File) |audio/wav |.wav |— |— |
|WebM |audio/webm |.webm |video/webm |.webm |


Example code:

```TypeScript
const playerSdk = new VePlayer({
  id: 'video-container',
  url: [
    {
      // MOV format is supported by Apple devices.
      src: 'https://voddemo-play.volcvod.com/source_video.MOV',
      type: 'video/quicktime'
    },
    {
      src: 'https://voddemo-play.volcvod.com/source_video.mp4',
      type: 'video/mp4',
    },
  ],
  vodLogOpts: {
    vtype: 'MP4',
    tag: ' Normal video',
    line_app_id: xxxx,
    line_user_id: 'veplayer_web_demo'
  }
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use the <code>src</code> attribute of the SDK instance to fetch the video URL of the <code>source</code> actually used for the current playback.</div>


<span id="7ca84ef7"></span>
## Rotating videos

Configure the rotation plug\-in used by the `rotate` configuration. When the user clicks the rotate button, the video rotates 90 degrees.

```javascript
const playerSdk = new VePlayer({
  id: 'video',
  width: 800,
  height: 500,
  url: 'xx.mp4',
  // Configuration item for video rotation button, default value.：{ innerRotate: false, clockwise: false }
  rotate: {
    innerRotate: true, //Rotate internally only.
    clockwise: false // Whether the rotation direction is clockwise.
  }
});
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When <code>innerRotate</code> is false, the width and height of the player must match the resolution of the video.</div>


<span id="d793eb6d"></span>
## Previewing thumbnails on progress bar

VePlayer allows users to drag the progress bar to quickly preview the video content at a selected point in time in thumbnail view. On desktop web browsers, users can preview by hovering their mouse over the target timestamp. On mobile web browsers, users can swipe left or right to reach the target timestamp. \*\*\*\* VePlayer uses server\-side CSS sprites as the preview image asset, and calculates and displays the preview image at the corresponding time point according to the position of the mouse pointer on the front end.

A CSS sprite is a large image composed of multiple screenshot frames, which has the following advantages:


* Small image size: Combining multiple small images into one large image can reduce the size of image files.

* Fewer requests: Integrating images reduces the number of user requests to the server, thereby improving the page opening speed.


An example CSS sprite is shown below. This CSS sprite consists of 13 thumbnails.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_677bd68f86f441f5bcec88d2ab9a37c2.png) </span>

The above CSS sprite results in the following thumbnail preview:


|Desktop |Mobile |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/428fba61bf8c40778013f0a957022ef2~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/123964ecd1f947c0abddc34b198b4ab7~tplv-goo7wpa0wc-image.image) </span> |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Click <a href="https://demo.byteplus.com/common/veplayer/basic/example?tab=function-display">Online Demo</a> to try the progress bar preview thumbnail function and view the sample code.</div>


* <div data-tips="true" data-tips-type="tip">The time accuracy of the thumbnail preview is determined by the screenshot interval. A smaller interval results in higher accuracy, but also increases the size of the sprite sheet and slows down image loading. Developers must therefore consider these trade\-offs.</div>



<span id="d706c821"></span>
### Prerequisites

If you want the CSS sprite to be displayed on the playback device, you must generate the CSS sprite through the BytePlus VOD media processing service first. For details, see [Sprites](https://docs.byteplus.com/docs/byteplus-vod/docs-sprites).

<span id="b62fe36b"></span>
### Implementation

Both `Vid` playback mode and `DirectUrl` playback mode support the display of CSS sprites, but the implementation methods are different. Refer to the code snippets below.


<Tabs>
<Tab zoneid="lxLQ9TygYU" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

When instantiating the player, pass the `getVideoByToken.needThumbs` parameter in the Vid playback configuration and set its value to `true` to display the CSS sprite.

```JavaScript
const playerSdk = new VePlayer({
  id: 'mse',
  width: 800,
  height: 500,
  // Vid playback configuration
  getVideoByToken: {
    playAuthToken: 'TemporaryplayAuthToken', // need to get from server side
    ....
    needThumbs: true
});
```



</Tab>
<Tab zoneid="uRrDjPccmw" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

You need to get the width, height, rows, and columns of the thumbnail in each sprite sheet, as well as the total number of thumbnails and the URL address of each sprite sheet, and then pass them to the player.

```JavaScript
var playerSdk = new VePlayer({
        id: 'mse',
        url: "https://vod-typea.byte-test.com/%E6%B5%8B%***%E8%A7%86%E9%A2%9101.mp4?auth_key=1700723919-0fa7dcfbfce141f89f6***4920703c14d485f569ebf4670d69e", // video address
        width: 640,
        height: 360,
        // In this example, a total of 38 thumbnails were extracted from the video.
        // The more thumbnails extracted, the more accurate the progress bar preview will be. However, larger images will result in slower loading times. You need to make your own judgment based on your business requirements.
        // Each sprite image can contain up to 10*10 = 25 thumbnails, so only one sprite image is needed.
        thumbnail: {
            // Total number of thumbnails.
            pic_num: 38,
            // Thumbnail width
            width: 240,
            // Thumbnail height
            height: 136,
            // The number of thumbnails per column in the sprite image.
            col: 10,
            // The number of thumbnails per row in the sprite image.
            row: 10,
            // Sprite image URL address.
            urls: ["http://p6-vedit-sign.byteimg.com/tos-cn-v-d67d0e/7ea3f6dbc4a049599945e9f96d106c7b_1659088327~tplv-noop.image?x-expires=1690624695&x-signature=q7VjLGZMLehRrN1j9uIgfvIfwMY%3D"]
        }
    });
```



</Tab>
</Tabs>


<span id="5b044378"></span>
## Adding progress bar markers

Progress bar markers are chapter markers on the progress bar that highlight specific time segments. They are often used to emphasize key points. In lengthy videos, they can help provide users with a visual reminder of the video's timeline structure. The effect is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d265d5aba92484a8f3edff3f07d7f4b~tplv-goo7wpa0wc-image.image) </span>

Initialize the player with an array of data for the progress bar markers using the `progressDot` parameter.

```JavaScript
var playerSdk = new VePlayer({
    id: 'video',
    url: "https://www.demo.com/adhasgd7****syh9.mp4",
    progressDot: [
        {
            id: '1',        // Unique ID of the marker
            time: 30,       // Start time of the marker, in seconds
            text: 'Intro',  // Custom text for the marker, not supported on H5 platform
            duration: 2,    // Duration of the marker, in seconds
            style: {        // Custom style of the marke
                background: 'rgb(60, 126, 255)'
            }
        },
        {
            id: '2',
            time: 60,
            text: 'Sample text',
            duration: 20,
            style: {
                background: '#FFF'
            }
        },
        {
            id: '3',
            time: 142,
            text: 'Sample text',
            duration: 2,
            style: {
                background: 'red'
            }
        },
    ],
});
```


After initialization, refer to the following code snippets to create, update, delete, and find markers.


* Create a marker:

   ```JavaScript
   playerSdk.getPlugin('progresspreview').createDot({
     time: 100,
     duration: 20,
     id: '4',
     text: 'new dot text',
     style: {
       background: '#fbbc08'
     }
   })
   ```
   

* Find a marker by ID:

   ```JavaScript
   const dot = playerSdk.getPlugin('progresspreview').findDot('1');
   ```
   

* Update a marker by ID:

   ```JavaScript
   playerSdk.getPlugin('progresspreview').updateDot({
     id: '1',
     time: 20,
     duration: 20,
     text: 'update text',
     style: {
       background: '#35a853'
     }
   })
   ```
   

* Delete a marker by ID:

   ```JavaScript
   playerSdk.getPlugin('progresspreview').deleteDot('1');
   ```
   

* Delete all markers:

   ```JavaScript
   playerSdk.getPlugin('progresspreview').deleteAllDots();
   ```
   

* Update all markers:

   ```JavaScript
   playerSdk.getPlugin('progresspreview').updateAllDots([
       {
         time: 100,
         duration: 20,
         id: '7',
         text: 'Updated text',
         style: {
           background: '#35a853'
         }
       },
       {
         time: 60,
         id: '8',
         text: 'Outro',
         duration: 10,
         style: {
           background: '#FFFFF'
         }
       },
     ])
   }
   ```
   


<span id="9865f44f"></span>
## Playing in MP4 MSE mode

When an MP4 video is played, it usually starts slowly without optimizing the structure of the video MOOV box or performing video transcoding. VePlayer supports the playback of MP4 videos in [MSE](https://developer.mozilla.org/en-US/docs/Web/API/MediaSource) format. This mode starts playback faster and supports cached playback, reducing traffic. The sample code is shown below.

```javascript
const playerSdk = new VePlayer({
    id: 'video',
    width: 800,
    height: 500,
    url: 'xx265.mp4',
    enableMp4MSE: true
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MSE playback mode must confirm the mp4 address. This mode supports cross\-domain requests for the current page domain name and range requests. Cross\-domain operations can be configured by <a href="https://console.byteplus.com/workorder/create">Create Ticket</a>.</div>


<span id="f3158ee1"></span>
## Playing in music player mode

VePlayer supports music player mode, with functions such as music cover, music list, loop, and bitrate switching. The effect is shown in the image below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_58f77afd1c3db677a858c419d8792f3f.png) </span>

To enable music player mode, set the `isMusic` parameter to `true` when instantiating VePlayer. You can also configure the music player. The configuration methods are different in different playback modes.


<Tabs>
<Tab zoneid="ppPlzqTWfr" title="Vid mode">
<TabTitle>Vid mode</TabTitle>

In Vid play mode，The music player can be configured through the `music` parameter.For specific parameter descriptions, please see [IMusicConfig](https://www.volcengine.com/docs/4/1248898#imusicconfig)。Sample code as below：

```js
{`
```



</Tab>
<Tab zoneid="WyXrmnd7fO" title="DirectUrl mode">
<TabTitle>DirectUrl mode</TabTitle>

The example code for configuring the music player mode in DirectUrl playback mode is as follows:

```js
{`
```



</Tab>
</Tabs>


The attributes used in music player mode are shown in the table below.


|Attribute |Readable |Writable |Description |Example |
|---|---|---|---|---|
|musicMode |Yes |Yes |Current playback mode<br><br><br>* order: Play playlist in sequence<br><br>* sloop: Loop single track<br><br>* loop: Loop playlist in sequence<br><br>* random: Random playback |```Plain```<br>```playerSdk.musicMode = 'order'; //Sequential playback```<br> |
|musicTimeScale |Yes |Yes |Fast forward and rewind timespan |```javascript```<br>```playerSdk.musicTimeScale = 10; // Set the time span to 10 seconds.```<br> |
|musicList |Yes |Yes |Music playlist |```json```<br>```playerSdk.musicList = [```<br>```  { title: 'Song1', vid: 'music1', src: 'https://demo.com/music1.mp3'},```<br>```  { title: 'Song2', vid: 'music2', src: 'https://demo.com/music2.mp3'}```<br>```]; // Set the playlist```<br> |


The methods used in music player mode are shown in the table below.


|Method |Description |Parameter |Return |Example |
|---|---|---|---|---|
|musicAdd |Add a song to the playlist |Object, see [Web Player SDK: Type definitions](https://docs.byteplus.com/docs/byteplus-vod/docs-web-type-definitions) for details<br><br><br>* `src`: Music URL<br><br>* `vid`: Unique ID of music<br><br>* `poster`: Music cover<br><br>* `title`: Music title |N/A |```javascript```<br>```playerSdk.musicAdd({```<br>```  src:'https://demo.com/music.mp3',```<br>```  title:'demo_music',```<br>```  vid: 'demo_music',```<br>```  poster: 'https://demo.com/poster.jpg'```<br>```});```<br> |
|musicRemove |Remove a song from the playlist |Delete the Vid corresponding to the song in the song list |N/A |```javascript```<br>```playerSdk.musicRemove('music_list_2');```<br> |
|musicRandom |Fetch a random song from the playlist |N/A |Song information, see [IMusicListItem](https://docs.byteplus.com/docs/undefined/6639d0a3a2277b04d63c349e#imusiclistitem) for details |```javascript```<br>```playerSdk.musicRandom();```<br> |
|musicNext |Play the next song |N/A |N/A |```javascript```<br>```playerSdk.musicNext();```<br> |
|musicPrev |Play the previous song |N/A |N/A |```javascript```<br>```playerSdk.musicPrev();```<br> |
|musicSetIndex |Select the nth song |Number type |N/A |```javascript```<br>```playerSdk.musicSetIndex(2);```<br> |
|musicForward |Fast forward the song by timeScale seconds |N/A |N/A |```javascript```<br>```playerSdk.musicPrev();```<br> |
|musicBackward |Rewind the song by timeScale seconds |N/A |N/A |```javascript```<br>```playerSdk.musicBackward();```<br> |
|musicSetAbCycle |Configure an AB loop |Object, see [IABCycle](https://docs.byteplus.com/docs/byteplus-vod/docs-web-api-reference#0b048cbc) for details<br><br><br>* `start`: AB loop start time<br><br>* `end`: AB loop end time<br><br>* `loop`: Whether AB is looped |N/A |```javascript```<br>```playerSdk.musicSetAbCycle({```<br>```  start: 3,```<br>```  end: 30,```<br>```  loop: true,```<br>```});```<br> |
|musicRemoveAbCycle |Remove the AB loop |N/A |N/A |```javascript```<br>```playerSdk.musicRemoveAbCycle();```<br> |


&nbsp;
