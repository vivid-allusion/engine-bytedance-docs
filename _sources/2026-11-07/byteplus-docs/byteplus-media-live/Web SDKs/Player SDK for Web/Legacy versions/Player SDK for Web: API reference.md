---
title: "Player SDK for Web: API reference"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-api-reference"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This article is applicable to 1.x versions of the BytePlus MediaLive Player SDK for Web. We highly recommend upgrading to the latest version for optimized player experiences.</div>


This article introduces the methods, callbacks, and parameters of the BytePlus MediaLive Player SDK for Web (also known as VePlayer).

<span id="Parameters"></span>
## **Parameters**

You can configure the player by setting `options` when creating a VePlayer instance:

```javascript
var player = new VePlayer(options);
```


The following list contains part of the configurations the player supports:


* Pull stream addresses and protocols

* Language settings

* Software and hardware decoding

* Playback controls


<span id="options"></span>
### **options**

Configurations for VePlayer.


|**Parameter** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|isLive |Boolean |false |Whether you want to play a live stream. Always set it to `true`. |
|id |String |None |The ID of the container in which VePlayer will be inserted. You must set either `id` or `root`. If you set both parameters, VePlayer will be inserted into the container specified by `root`. |
|root |HTMLElement |None |The ID of the container in which VePlayer will be inserted. You must set `id` or `root`. If you set both parameters, VePlayer will be inserted into the container specified by `root`. |
|url |String |None |Pull stream address. You can concatenate an address manually or use the [address generator](https://docs.byteplus.com/byteplus-media-live/docs/address-generator) to generate an address. You must set either `url` or `playList`. |
|playList |Array |None |A list of pull stream addresses. For details, see [playListItem](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#playListItem). You must set either `url` or `playList`. |
|plugins |Any |None |A custom plugin. You can pass in multiple plugins and separate them by a comma. |
|languages |Object |None |The dictionary the player refers to when displaying text in the user interface. Use this parameter in conjunction with `lang`, which sets the player language. You can define your custom dictionary or use the [default dictionary](https://docs.byteplus.com/byteplus-media-live/docs/default-dictionary). Define your dictionary with the format: `{[key: string]: object;}`. For example, `{ zh: { PIP: '画中画' }, en: { PIP: 'pip' }}`. |
|useSoftDecoding |Boolean |false |Whether to use software decoding.<br><br><br>* `true`: Use software decoding.<br><br>* `false`: Do not use software decoding.<br><br><br>The player may be hijacked in certain Android browsers, causing some functions to be unavailable. You can use software decoding to solve this issue.<br><br>Mobile browsers do not support playing streams in FLV format. If you need to play this format, use software decoding.<br><br>[Some browsers](https://caniuse.com/?search=HEVC) do not support the H.265 encoding format. If you need to play the video in this encoding format, use software decoding.<br><br>Software decoding depends on the device's CPU. Playing high\-bitrate and high\-resolution videos will cause high CPU occupancy rates. |
|enableH265Degrade |Boolean |false |Whether to enable automatic degradation to H.265 software decoding. Once enabled, if the browser does not support H.265 hardware decoding, the SDK automatically switches to H.265 software decoding.<br><br><br>* `true`: Enable automatic degradation.<br><br>* `false`: Disable automatic degradation. |
|codec |boolean |'h265' |The encoding format of the video stream. It is recommended to set this parameter if you enable automatic degradation to H.265 software decoding by setting `enableH265Degrade` to `true`. |
|sdkErrorPlugin |[SdkErrorConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#SdkErrorConfig) |None |Error information. You can configure the text, image, and refresh button once the player encounters an error. |
|rtm |[RtmConfig](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#RtmConfig) |None |Real Time Media (RTM) configuration. This parameter takes effect only if you set `url` to an RTM pull\-stream address. |
|width |String｜Number |100% |The width of the player.<br><br>If you set `width` to a string that contains a percentage sign, for example, `'30%'`, the SDK takes the value as the relative width of the player compared to the container. If the string does not contain a percentage sign, for example, `'300'` or `'300px'`, the SDK takes the value as the absolute width of the player, in pixels.<br><br>If you set `width` to a number, for example, `300`, the SDK takes the value as the absolute width of the player, in pixels. |
|height |String｜Number |100% |The height of the player.<br><br>If you set `height` to a string that contains a percentage sign, for example, `'30%'`, the SDK takes the value as the relative height of the player compared to the container. If the string does not contain a percentage sign, for example, `'300'` or `'300px'`, the SDK takes the value as the absolute height of the player, in pixels.<br><br>If you set `height` to a number, for example, `300`, the SDK takes the value as the absolute height of the player, in pixels. |
|volume |Number |0.6 |The default volume of the player. Valid range: [0, 1] |
|autoplay |Boolean |true |Whether to enable automatic playback.<br><br><br>* `true`: Enable automatic playback.<br><br>* `false`: Disable automatic playback. The playback starts only when the end user clicks the play button. |
|autoplayMuted |Boolean |true |Whether to mute the audio during automatic playback. This parameter takes place only if you set `autoplay` to `true`.<br><br><br>* `true`: Mute the audio during automatic playback.<br><br>* `false`: Do not mute the audio during automatic playback. |
|poster |String |None |The URL of the cover image. |
|pip |Boolean |true |Whether to enable Picture\-in\-Picture (PiP).<br><br><br>* `true`: Enable PiP.<br><br>* `false`: Disable PiP. |
|fullscreen |[fullscreen](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#fullscreen) |None |Configurations relating to full\-screen mode. |
|lang |String |zh |The player's display language. Default languages include:<br><br><br>* `zh`<br><br>* `en`<br><br>* `jp`<br><br>* `zh-hk` |
|liveInfoPanel |[LiveInfoPanel](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#LiveInfoPanel) |None |A panel that displays the stream information. The SDK supports displaying information about HLS and FLV streams. Before using the panel, you must first add the LiveInfoPanel plugin: `plugins: [window.VePlayer.LiveInfoPanel]`. |
|timeShiftPlugin |[timeShiftPlugin](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#2f07a993) |None |Time\-shifting configurations. For how to implement the time\-shifting feature, refer to [Time shifting](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-features#cc924516). |
|liveLogger |[liveLogger](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#liveLogger) |None |Log configurations. |
|Subtitle |[Subtitle](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#subtitle) |None |Subtitle configurations. The player displays subtitles only if you specify this parameter. |


<span id="fullscreen"></span>
### **fullscreen**

Configurations relating to full\-screen mode.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|rotateFullscreen |Boolean |false |Whether to enable automatic rotation to landscape mode. Once enabled, if the user holds the phone in portrait orientation and switches the player to full\-screen mode, the SDK rotates the player by 90 degrees to landscape mode. This feature is often used on mobile devices. This parameter overrides the setting of `useCssFullscreen`.<br><br><br>* `true`: Enable automatic rotation to landscape mode.<br><br>* `false`: Disable automatic rotation to landscape mode. |
|useCssFullscreen |Boolean |false |Whether to use full\-window or full\-screen mode.<br><br><br>* `true`: Full\-window mode, in which the player covers the browser window.<br><br>* `false`: Full\-screen mode, in which the player covers the entire desktop. |
|needBackIcon |Boolean |false |Whether to display the return button in the upper right corner of the player when the player is in full\-screen mode. This feature is often used on mobile devices.<br><br><br>* `true`: Display the button.<br><br>* `false`: Do not display the button. |


<span id="playListItem"></span>
### **playListItem**

Details about pull stream addresses. You can configure multiple addresses with different resolutions.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|streamType |String |None |Pull\-stream protocol. If the pull stream address you specify in `playList` does not have a suffix, you must set `streamType`. Supported values include:<br><br><br>* `rtm`<br><br>* `flv`<br><br>* `mp4`<br><br>* `hls` |
|url |String |None |Pull stream address. You can concatenate an address manually or use the [address generator](https://docs.byteplus.com/byteplus-media-live/docs/address-generator) to generate an address. This parameter is required. |
|definition |String |None |Video resolution of the stream, which corresponds to the [transcoding template](https://docs.byteplus.com/byteplus-media-live/docs/configuring-transcoding) you configure in the BytePlus MediaLive console. You can pass in multiple pull stream addresses with the same source ID (`lineId`) but different resolutions. Suggested values include:<br><br><br>* `uhd`<br><br>* `hd`<br><br>* `sd`<br><br>* `ld`<br><br>* `ao` |
|definitionTextKey |String |The value of `definition` |The language key for the video resolution of the stream. By default, the value of `definition` is displayed in the player. Use it in conjunction with `languages`. For example, if you set `definitionTextKey` to `HD_TEXT_KEY` and set `languages` to `{ en: { HD_TEXT_KEY: 'High definition' }}`, the player displays **High definition** as the stream's resolution. |
|lineId |String |None |Source ID. You can pass in multiple pull stream addresses with the same source ID but different resolutions (`definition`). |
|lineTextKey |String |None |The language key for the stream ID. For example, if you set `lineTextKey` to `LINE_ONE` and set `languages` set to `{ en: { LINE_ONE: 'Line one' }}`, the player displays **Line one** as the stream's ID. |
|backUrlList |Array |None |Backup pull stream address. If you set `sdkErrorPlugin.isNeedDemoteBack` to `true`, if an error occurs in the main stream, the player automatically switches to the backup stream. |


<span id="SdkErrorConfig"></span>
### **SdkErrorConfig**

The player's error information. You can configure the text, image, and refresh button once the player encounters an error.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|errorImg |Boolean |true |Whether to display an image when an error occurs.<br><br><br>* `true`: Displays an image.<br><br>* `false`: Do not display an image. |
|errorTips |Boolean |true |Whether to display the error message when reporting an error. The default error message is "An error occurred while playing, click refresh to try", which can be customized by configuring `errorTips` in `languages`.<br><br>For example, you can set `languages` to { en: { errorTips: 'Player error' } }. |
|isNeedRefreshButton |Boolean |true |Whether to display the refresh button when an error occurs.<br><br><br>* `true`: Displays the button.<br><br>* `false`: Do not display the button. |
|retryLoopNum |Number |1 |The number of retries before displaying an error on the player's user interface. |
|isNeedDemoteBack |Boolean |false |Whether to downgrade to the backup stream when an error occurs during playback.<br><br><br>* `false`: Do not downgrade. The player displays the error message.<br><br>* `true`: Switch to the backup stream, defined by `playListItem.backUrlList`, when an error occurs. |


<span id="RtmConfig"></span>
### **RtmConfig**

Configurations for pulling an RTM stream


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|loadTimeout |Number |5000 |The maximum wait time for a retry to pull the stream, in milliseconds. |
|retryDelay |Number |1000 |The interval between each retry to pull the stream, in milliseconds. |
|retryCount |Number |0 |The maximum number of retries to pull the stream. |
|backupURL |String |None |The backup FLV or HLS streams the player switches to when failing to pull an RTM stream.<br><br>If you specify `backupURL`, the player enables automatic switching.<br><br>If you do not specify `backupURL`, the player reports an error when it fails to play an RTM stream without switching to backup streams. |
|backupStreamType |String |None |The protocol of the backup pull stream address, which needs to be configured in conjunction with `backupURL`. Supported values include:<br><br><br>* flv<br><br>* hls |
|delayHint |Number |0 |The buffer time of the audio and video, in seconds. |


<span id="LiveInfoPanel"></span>
### **LiveInfoPanel**

Configurations for the panel that displays the stream information in the player. The stream information includes the stream's format, bitrate, and frame rate, in the player.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|visible |Boolean |true |Whether to display the panel.<br><br><br>* `true`: Display the panel.<br><br>* `false`: Do not display the panel. |
|showH265Info |Boolean |false |Whether to display H.265 related information, such as decoding efficiency and CPU consumption.<br><br><br>* `true`: Display the information.<br><br>* `false`: Do not display the information.<br><br><br>The player displays H.265 related information only if `showH265Info` is `true` and if the browser is using software decoding. |


<span id="2f07a993"></span>
### timeShiftPlugin

Configurations for time shifting.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|livingStartTime |Number |The current time |The time the live stream session started. Unix timestamp in seconds. The time must be specified according to the time zone of the browser. |
|maxMoveTime |Number |604800 |The maximum amount of time shifting available during playback, in seconds. For example, if you set `maxMoveTime` to `60`, it means that anything streamed more than 60 seconds ago will no longer be available to playback. Valid range: [6,604800]. |


<span id="liveLogger"></span>
### **liveLogger**

Configurations for log upload.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|appId |String |None |The app ID, which is the unique identifier of your app. Contact [BytePlus technical support](https://www.byteplus.com/en/support) for your app ID. |
|enable |Boolean |true |Whether to enable uploading logs to the BytePlus MediaLive servers.<br><br><br>* `true`: Enable log uploading.<br><br>* `false`: Disable log uploading. |
|userId |String |None |The user ID. We highly recommend that you set it to a value that identifies a unique user. Technical support may need the information to identify problems. If you do not define `userId` and `deviceId`, the SDK will generate random user IDs and device IDs, which will then be stored in the browser cache. |
|deviceId |String |None |The device ID. We highly recommend that you set it to a value that identifies a unique user device. Technical support may need the information to identify problems. If you do not define `userId` and `deviceId`, the SDK will generate random user IDs and device IDs, which will then be stored in the browser cache. |


<span id="200897d1"></span>
### **Subtitle**

Configurations for the video subtitles.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|isDefaultOpen |Boolean |None |Whether to display subtitles by default.<br><br><br>* `true`: Display subtitles by default.<br><br>* `false`: Do not display subtitles by default. |
|mode |"external" |"native" |None |
|updateMode |String |'live' |Always set it to `'live'`. |
|style |[style](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#d1c656ee) |None |Configurations for the subtitle's style. |


<span id="d1c656ee"></span>
### **style**

Configurations for the subtitle's style.


|**Name** |**Data Type** |**Default Value** |**Description** |
|---|---|---|---|
|follow |Boolean |true |Whether to adjust the subtitle's position according to the player's control panel.<br><br><br>* `true`: Adjust.<br><br>* `false`: Do not adjust. |
|mode |String |'stroke' |The font display mode.<br><br><br>* `'stroke'`: Add a stroke to the text.<br><br>* `'bg'`: Add a shadow to the text. |
|followBottom |Integer |50 |Whether to adjust the subtitle's position according to the vertical position of the player's control panel.<br><br><br>* `true`: Adjust.<br><br>* `false`: Do not adjust. |
|fitVideo |Boolean |true |Whether to adjust the font size according to the video size.<br><br><br>* `true`: Adjust.<br><br>* `false`: Do not adjust. |
|offsetBottom |Integer |4 |The percentage of the distance between subtitles and the bottom of the video compared with the height of the video. |
|baseSizeX |Integer |49 |The default font size when a user holds the phone in landscape orientation. |
|baseSizeY |Integer |28 |The default font size when a user holds the phone in portrait orientation. |
|minSize |Integer |16 |The minimum font size on PC devices. |
|minMobileSize |Integer |13 |The minimum font size on mobile devices. |
|line |'single' |'double' |'three' |
|fontColor |String |'#fff' |Font color. |


<span id="Methods"></span>
## **Methods**

This section introduces you to the methods of VePlayer , using `player.on()` as an example, the invocation example is shown below.

```javascript
var player = new VePlayer(options)

player.on('player_create_finish', () => {
    console.log('The player is created.')
})
```


The list of methods is as follows.


|**Name** |**Description** |
|---|---|
|[on()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#on()) |Listens for an event. |
|[once()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#once()) |Listens for an event only once. |
|[off()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#off()) |Stops listening for an event. |
|[destroy()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#destroy()) |Destroys the player. |
|[player.play()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#play()) |Start the playback. |
|[player.pause()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#pause()) |Pause the playback. |
|[player.retry()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#retry()) |Refresh the player. |
|[player.switchURL()](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#switchURL()) |Switch to another pull stream address. |


<span id="on()"></span>
### **on()** 

Listens for a pull\-stream event.

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**Parameter**


* `Action`: type is `string`

* `Func`: type is `(... args: any []) => void`


<span id="once()"></span>
### **once()** 

Listens for a pull\-stream event only once.

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**Parameter**


* `Action`: type is `string`

* `Func`: type is `(... args: any []) => void`


<span id="off()"></span>
### **off()** 

Stops listening for an event.

```typescript
(action: string, func: (...args: any[]) => void) => void
ts
```


**Parameter**


* `Action`: type is `string`

* `Func`: type is `(... args: any []) => void`


<span id="destroy()"></span>
### **destroy()** 

Destroys the current player instance.

```typescript
() => Promise<void>
```


<span id="play()"></span>
### **play()** 

Starts the playback.

```typescript
() => Promise<void>
```


**Sample code**

Sample 1

```javascript
var veplayer = new VePlayer(options)

veplayer.player.play()
```


Sample 2

```javascript
var veplayer = new VePlayer(options)

veplayer.player.play().then(() => {
    // Actions to take if the playback starts successfully.
}).catch(() => {
    // Actions to take if the playback fails to start. It usually happens to automatic playback without any user interaction.
})
```


<span id="pause()"></span>
### **pause()** 

Pauses the playback.

```typescript
() => void
```


**Sample code**

```javascript
var veplayer = new VePlayer(options)
veplayer.player.pause()
```


<span id="retry()"></span>
### **retry()** 

Refreshes the player.

```TypeScript
() => void
```


**Sample code**

```javascript
var veplayer = new VePlayer(options)
veplayer.player.retry()
```


<span id="switchURL()"></span>
### **switchURL()** 

Switches to another pull stream address.

```TypeScript
(src: string) => void
```


**Parameter**


* `src`: type is `string`


**Sample code**

```javascript
var veplayer = new VePlayer(options)
veplayer.switchURL('http://example.com');
```


<span id="Events"></span>
## **Events**

The SDK can listen for the following events:


|**Event** |**Event value** |**Description** |
|---|---|---|
|PLAYER_CREATED_FINISH |'player_create_finish' |The players is created. |
|PLAYER_REBUILD |'player_rebuild' |The player is created again after being destroyed. |
|CANCEL_UNMUTE |'cancel_unmute' |Unmute. |
|REFRESH_CLICK |'refresh_click' |The user clicks the refresh button. |
|PLAY_BACKUP_CHANGE |'play_backup_change' |Downgrading is triggered after an error occurs. |
|PLAY_BACKUP_CHANGE_FINISH |'play_backup_change_finish' |Downgrading is complete after an error occurs. |
|PLAY_ERROR_BUTTON_CLICK |'play_error_button_click' |A retry is triggered after an error occurs. |
|PlAY_URL_CHANGE |'play_url_change' |The player switches to a new pull stream address. |
|SHOW_PLAY_ERROR |'show_play_error' |The player displays an error. |
|LONG_WAITING |'long_waiting' |The maximum wait time is exceeded, after which a downgrade may occur. |
|INNER_DEFINITION_CHANGE |'inner_definition_change' |The player switches to another resolution. |
|LINE_CHANGE |'line_change' |The player switches to another source. |
|ENDED |'ended' |The live stream has ended. |
