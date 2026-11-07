---
title: "Player SDK for Web: Methods and properties"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178"
---

## VePlayerLive

Type：`class`

### Property

|Property |Type |Description |
|---|---|---|
|playTime |number |`Readonly` Obtain the duration that has been played, excluding pause and waiting time, with the unit of seconds. |
|readyState |0 \| 2 \| 1 \| 3 \| 4 |`Readonly` Gets the readiness of the video.<br><br><br>* `0`: HAVE_NOTHING, which means there is no information about the media resources.<br><br>* `1`: HAVE_METADATA, which means enough media resources have been retrieved to initialize the metadata and fast\-forward/rewind will not raise an exception.<br><br>* `2`: HAVE_CURRENT_DATA, which means the data for the current playback position is available, but there is not enough data to play the next frame.<br><br>* `3`: HAVE_FUTURE_DATA, which means there is enough data for the current playback position and at least a short period in the future (at least two following frames).<br><br>* `4`: HAVE_ENOUGH_DATA, which means there is enough data and the download rate is sufficient for the video to be played without interruption until the end. |
|buffered |TimeRanges |`Readonly` Gets the currently buffered time range. |
|played |TimeRanges |`Readonly` Gets the time range of the audio/video that has been played. |
|cumulateTime |number |`Readonly` Sets or gets the current playback position of the video, in seconds. |
|isFocused |boolean |`Readonly` Gets whether the player has focus. The control bar is displayed when the player has focus. |
|isFullscreen |boolean |`Readonly` Gets whether the player is in full\-screen mode, in which the player covers the entire desktop. |
|isCssFullscreen |boolean |`Readonly` Gets whether the player is in full\-window mode, in which the player covers the entire browser window. |
|networkState |0 \| 2 \| 1 \| 3 |`Readonly` Gets the network condition of the video.<br><br><br>* `0`: NETWORK_EMPTY, which means there is no data yet, and `readyState` is `HAVE_NOTHING`.<br><br>* `1`: NETWORK_IDLE, which means the `HTMLMediaElement` element is active and the resources have been selected, but the network is not in use.<br><br>* `2`: NETWORK_LOADING, which means the browser is downloading the data of the `HTMLMediaElement` element.<br><br>* `3`: NETWORK_NO_SOURCE, the media source is not found according to the `src` property of the `HTMLMediaElement` element. |
|paused |boolean |`Readonly` Gets whether the current video is suspended. |
|ended |boolean |`Readonly` Gets whether the current video has finished playing. |
|state |number |`Readonly` Gets the current state of the player.<br><br><br>* `0`: ERROR, which means a playback error occurred<br><br>* `1`: INITIAL, which means initialization<br><br>* `2`: READY, which means the configuration/event/plug\-in has been initialized/bound/instantiated<br><br>* `3`: ATTACHING, which means the media object is being mounted.<br><br>* `4`: ATTACHED, which means the media object has been mounted in the DOM<br><br>* `5`: NOTALLOW, which means the playback is blocked<br><br>* `6`: RUNNING, which means the playback has started successfully<br><br>* `7`: ENDED, which means the playback has ended<br><br>* `8`: DESTROYED, which means the player instance is destroyed |
|url |string |`Readonly` Gets the current pull stream address. |
|source |string |`Readonly` Gets the current playback source ID. |
|playerVersion |string |`Readonly` Retrieve the player SDK version number. |
|definition |string |`Readonly` Gets the current resolution ID. |
|crossOrigin |string |Gets the player's cross\-domain configurations. For more information, refer to [crossorigin](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin). |
|volume |number |Gets the volume of the video. The value range is [0,1]. |
|muted |boolean |Gets whether the video is muted.<br><br><br>* `true`: Muted.<br><br>* `false`: Not muted. |
|lang |string |Gets the current language. |

### openLog()

Enables log upload.

**Type**

```ts
() => void
```

### closeLog()

Disables log upload.

**Type**

```ts
() => void
```

### openInfoPanel()

Turns on the information panel, which displays basic information including stream format, frame rate, bitrate, GOP, video resolution, codec, buffer time, and playback progress. If software decoding is used, the software decoding efficiency and CPU consumption will also be displayed.

**Type**

```ts
() => void
```

### closeInfoPanel()

Turns off the information panel.

**Type**

```ts
() => void
```

### openAbr()

Enable the Adaptive Bitrate Streaming (ABR) switching feature.

**Type**

```ts
() => void
```

### closeAbr()

Disable the Adaptive Bitrate Streaming (ABR) switching feature.

**Type**

```ts
() => void
```

### updateDrmConfig()

Use this method to update DRM configuration.

**Type**

```ts
(config: Drm) => Promise<void | undefined>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[Drm](https://docs.byteplus.com/en/docs/24/docs-1155423#drm) |Yes |None |A configuration object containing settings for Fairplay DRM. |

**Return Value**

`Promise<void | undefined>`

### switchAbr()

Modify ABR configuration, including enabling or disabling the ABR feature and adjusting other resolutions.

**Type**

```ts
(options: { enable: boolean; bitrate: number;}) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |*  |Yes |*  |Configuration of ABR. |
|enable |boolean |Yes |`-` |Whether to enable the ABR function.<br><br><br>* `true`: Enabled ;<br><br>* `false`: Disabled |
|bitrate |number |Yes |None |Switch the bitrate corresponding to the Adaptive Bitrate (ABR) live stream. |

### getRTMNetWorkInfo()

Obtain the network assessment information of RTM pull streaming.

**Type**

```ts
() => RTMNetWorkInfo
```

**Return Value**

[RTMNetWorkInfo](https://docs.byteplus.com/en/docs/24/docs-1155423#rtmnetworkinfo)

### getRTMStats()

Obtain the playback information of RTM pull stream.

**Type**

```ts
() => Promise<StatsSnapShoot>
```

**Return Value**

`Promise<`[StatsSnapShoot](https://docs.byteplus.com/en/docs/24/docs-1155423#statssnapshoot)`>`

### getFLVStats()

Obtain the playback information of FLV pull streaming.

**Type**

```ts
() => FlvStats
```

**Return Value**

[FlvStats](https://docs.byteplus.com/en/docs/24/docs-1155423#flvstats)

### updatePlaylist()

This method is used to update the playlist, supporting updates to source, resolution, and related information.

**Type**

```ts
(playlist: Source[], target?: string | { definition?: string; source?: string;}, needUpdateProtocol?: boolean) => Promise<void>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|playlist |[Source](https://docs.byteplus.com/en/docs/24/docs-1155423#source)[] |Yes |None |The playlist, consisting of multiple `Source` type elements. |
|target |*  |No |*  |An optional target configuration, which can specify the resolution or source. Providing this information helps update the playback source for a specific resolution or stream. |
|definition |string \| undefined |No |None |The resolution ID. |
|source |string \| undefined |No |None |The playback resource ID. |
|needUpdateProtocol |boolean |Yes |`true` |Whether the protocol needs to be updated.<br><br><br>* `true`: Forces the protocol update to ensure compatibility with the playback configuration or source.<br><br>* `false`: Does not update the protocol and continues to use the current configuration. |

**Return Value**

`Promise<void>`

### switch()

Switches the pull stream address, playback source, or resolution.

**Type**

```ts
(target: string | { definition?: string; source?: string;}, options?: { fallbackToFirstDefinition?: boolean; seamless?: boolean;}) => Promise<Definition>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|target |*  |Yes |*  |The target pull stream address, playback source, or resolution. |
|definition |string \| undefined |No |None |The resolution ID. |
|source |string \| undefined |No |None |The playback source ID. |
|options |*  |No |*  |More configurations. |
|fallbackToFirstDefinition |boolean \| undefined |No |`false` |Whether to downgrade to the first resolution in the playlist when the player cannot play with the specified resolution. |
|seamless |boolean \| undefined |No |None |Whether seamless switching is enabled.<br><br><br>* `true`: Enables seamless switching, ensuring no interruption during playback.<br><br>* `false`: Disables seamless switching, which may cause interruptions during playback. |

**Return Value**

`Promise<`[Definition](https://docs.byteplus.com/en/docs/24/docs-1155423#definition)`>`

### once()

Call this method to listen for the specified event. The event handler is executed only once.

**Type**

```ts
(event: string, callback: (data?: any) => any) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The name representing the event. |
|callback |(data?: any) =\> any |Yes |None |Callback functions representing events. |

### off()

Stops listening for a specified event.

**Type**

```ts
(event: string, callback: (data?: any) => any) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|callback |(data?: any) =\> any |Yes |None |The callback function for the event. |

### emit()

Triggers a specified event.

**Type**

```ts
(event: string, data?: any) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|data |any |Yes |None |The event information. |

### offAll()

Stops listening to any player event.

**Type**

```ts
() => void
```

### on()

Listens for a specified event.

**Type**

```ts
(event: string, callback: (data?: any) => any) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|event |string |Yes |None |The event name. |
|callback |(data?: any) =\> any |Yes |None |The callback function for the event. |

### play()

Starts playback.

**Type**

```ts
() => any
```

**Return Value**

`any`

### pause()

Pauses playback.

**Type**

```ts
() => void
```

### requestPIP()

Turns on Picture\-in\-Picture (PIP).

**Type**

```ts
() => void
```

### exitPIP()

Turns off Picture\-in\-Picture (PIP).

**Type**

```ts
() => void
```

### retry()

Retries stream\-pulling.

**Type**

```ts
() => void
```

### focus()

The player gets focus. When the method is called, `veplayer.isFocused` will become `true` and the `PLAYER_FOCUS` event will be triggered.

**Type**

```ts
(data?: { autoHide?: boolean; delay?: number;}) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|data |*  |No |*  |Related configurations. |
|autoHide |boolean \| undefined |No |`true` |Whether auto\-blur is enabled.<br><br><br>* `true`: Enables auto\-blur, meaning `blur()` will be automatically called after the specified delay time.<br><br>* `false`: Disables auto\-blur, meaning `blur()` will not be automatically called after the delay. |
|delay |number \| undefined |No |`3000` |Delay duration (in milliseconds) before auto\-blur is triggered. This takes effect only when `autoHide` is set to `true`. |

### blur()

The player loses focus. When the method is called, `veplayer.isFocused` will become `false` and the `PLAYER_BLUR` event will be triggered.

**Type**

```ts
(data?: { ignorePaused?: boolean;}) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|data |*  |No |*  |The related configurations. |
|ignorePaused |boolean \| undefined |No |`false` |Whether the player retains focus when paused. The default is `true`, meaning the player will not automatically lose focus during pause. |

### canPlayType()

Determine whether the browser supports the playback format.

**Type**

```ts
(type: string) => boolean
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|type |string |Yes |None |The playback format. |

**Return Value**

`boolean`

### requestFullscreen()

Turns the player into full\-screen mode, in which the player covers the entire desktop. If the player is in full\-window mode when the method is called, it will automatically exit full\-window mode, and the `Events.FULLSCREEN_CHANGE` event will be triggered.

**Type**

```ts
(el?: HTMLElement) => Promise<void>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node in which the player is displayed in full\-screen mode. |

**Return Value**

`Promise<void>`

### exitFullscreen()

Exits full\-screen mode. After the method is called, `veplayer.isFullscreen` will become `false` and the `Events.FULLSCREEN_CHANGE` event will be triggered.

**Type**

```ts
(el?: HTMLElement) => Promise<void>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node of the full screen effect. |

**Return Value**

`Promise<void>`

### requestCssFullscreen()

Turns the player into full\-window mode, in which the player covers the entire browser window. If the player is in full\-screen mode when the method is called, it will automatically exit full\-screen mode, and the `Events.CSS_FULLSCREEN_CHANGE` event will be triggered.

**Type**

```ts
(el?: HTMLElement) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|el |HTMLElement \| undefined |No |None |The DOM node in which the player is displayed in full\-window mode. |

### exitCssFullscreen()

Exits the full\-window mode. When the method is called, `veplayer.isFullscreen` will become `false` and the `Events.CSS_FULLSCREEN_CHANGE` event will be triggered.

**Type**

```ts
() => void
```

### registerPlugin()

Registers a specified plug\-in to the current player.

**Type**

```ts
(plugin: Function | { plugin: Function; options: object;}, config?: { [propName: string]: any; } | undefined) => any
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|Plugin |*  |Yes |*  |The plugin constructor. |
|plugin |Function |Yes |None |The plugin constructor. |
|options |object |Yes |None |The plugin configurations. |
|config |{ [propName: string]: any; } \| undefined |No |None |The plugin configurations. |

**Return Value**

`any`

### unRegisterPlugin()

Destroys or unregisters a specified plugin from the player.

**Type**

```ts
(plugin: any) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|Plugin |any |Yes |None |The plugin instance or name. |

### showIcon()

Displays the icon of a specified plugin.

**Type**

```ts
(pluginNames: string[]) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|PluginNames |string[] |Yes |None |The plugin name. |

### hideIcon()

Hides the icon of a specified plugin.

**Type**

```ts
(pluginNames: string[]) => void
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|PluginNames |string[] |Yes |None |The plugin name. |

### destroy()

Destroys the player instance.

**Type**

```ts
() => void
```

## createLivePlayer()

Creates a live player.

**Type**

```ts
(options?: LiveVePlayerOptions) => Promise<VePlayerLive>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[LiveVePlayerOptions](https://docs.byteplus.com/en/docs/24/docs-1155423#liveveplayeroptions) \| undefined |No |None |The player settings. |

**Return Value**

`Promise<`[VePlayerLive](https://docs.byteplus.com/en/docs/24/7606#veplayerlive)`>` The player instance.

**Example**

```js
VePlayer.createLivePlayer({
 height: 360,
 url: options.url,
}).then(function (veplayer) {
 veplayer.on(VePlayer.live.Events.CANPLAY, function () {
   console.log('An canplay event has occurred')
 });
}).catch(error => {
 console.log('Fails to create the player. Error message:', error);
});;
```

## prepare()

Initialize player strategy.

**Type**

```ts
(options: PrepareOptions) => Promise<VeStrategyManager | undefined>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[PrepareOptions](https://docs.byteplus.com/en/docs/24/docs-1155423#prepareoptions) |Yes |None |Configure strategy parameters. |

**Return Value**

`Promise<`[VeStrategyManager](https://docs.byteplus.com/en/docs/24/ref#vestrategymanager)` | undefined>`

**Example**

```js
live.prepare({
 appId: '***',
 userId: '***',
 strategies: {
  rtmAdaptiveBuffer: true,
 },
}).then(function () {
 VePlayer.createLivePlayer({
  height: '300px',
  url: 'https://pulldomain.com/appname/streamname.sdp',
  logger: {
    userId: '***',
    appId: '***',
  },
 });
});
```

## isRTMSupported()

Checks whether the current browser supports playing an RTM stream.

**Type**

```ts
() => Promise<boolean>
```

**Return Value**

`Promise<boolean>`

## isRTMSupportCodec()

Whether the current browser supports playing an RTM stream encoded in H.264.

**Type**

```ts
(codec?: string) => Promise<boolean>
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string |Yes |`'h264'` |The stream codec. Supports `H264` currently. |

**Return Value**

`Promise<boolean>`

## isMseSupported()

Check whether the current browser supports the MSE (MediaSource Extends) API and check whether the MSE API supports the incoming video encoding information (MIME format).

> **说明**

> Usage scenario: Check whether the PC\-side browser and Android\-side browser support the incoming encoding information.

**Type**

```ts
(codec?: string | undefined) => boolean
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if MSE supports the H.264 encoding format. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if MSE supports the H.265 encoding format. If supported, it can meet the playback requirements of most H.265 videos. |

**Return Value**

`boolean`

## isSoftDecodeSupported()

Checks whether the current browser supports software decoding.

**Type**

```ts
() => Promise<boolean>
```

**Return Value**

`Promise<boolean>`

## isMMSSupported()

Check whether the current browser supports the MMS (ManagedMediaSource) API and check whether the MMS API supports the incoming video encoding information (MIME format).

> **说明**

* > Usage scenario: Check whether the Safari browser and Chrome browser on the iOS side support the incoming encoding information.

* > Browsers with iOS 17.1 or above start to support MMS.

**Type**

```ts
(codec?: string | undefined) => any
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if MMS supports the H.264 encoding format. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if MMS supports the H.265 encoding format. If supported, it can meet the playback requirements of most H.265 videos. |

**Return Value**

`any`

## isFLVSupported()

Check whether the current browser supports the encoding information of FLV format streams.

> **说明**

* > When this method is called in a browser on a PC or Android device, it is the same as when the isMseSupported method is called with the default encoding format.

* > When this method is called in a browser on an iOS device, it is the same as when the isMMSSupported method is implemented.

**Type**

```ts
(codec?: string | undefined) => boolean
```

**Parameters**

|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|codec |string \| undefined |No |`'h264'` |The media type and codec information string to be checked is represented in MIME format, for example, `video/mp4;codecs="av01.0.01M.08"`. You can also use the following parameter values to quickly check whether the H.264 and H.265 video coding formats are supported.<br><br><br>* `Codec.H264` (default value): Check if the H.264 encoding format is supported. If supported, it can meet the playback requirements of most H.264 videos.<br><br>* `Codec.H265`: Check if the H.265 encoding format is supported. If supported, it can meet the playback requirements of most H.265 videos. |

**Return Value**

`boolean`

## isRTMSeiSupported()

Check whether the current browser supports receiving SEI (Supplemental Enhancement Information) messages from RTM streams.

**Type**

```ts
() => Promise<boolean>
```

**Return Value**

`Promise<boolean>`

* `true`: Receiving SEI messages from RTM streams is supported.

* `false`: Receiving SEI messages from RTM streams is not supported.

## setLicenseConfig()

Configure the SDK license.

**Type**

```ts
(params: LicenseConfig) => Promise<void>
```

**Parameters**

|Parameter Name |Type |Description |
|---|---|---|
|`params` |[LicenseConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#licenseconfig) |The license configuration parameters. |
