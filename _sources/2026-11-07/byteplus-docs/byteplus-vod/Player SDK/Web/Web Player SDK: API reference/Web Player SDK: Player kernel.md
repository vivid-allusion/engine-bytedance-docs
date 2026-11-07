---
title: "Web Player SDK: Player kernel"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-player-sdk-player-kernel"
---

The player kernel provides the playback functionality of the SDK instance. The kernel provides the following attributes and API methods to enable the development of flexible playback features.

The sample code for fetching the player kernel and calling the API is shown below.

```JavaScript
 const playerSdk = new VePlayer({
   id: 'video',
   width: 800,
   height: 500,
   url: 'xx.mp4'
 });

 // Get Attribute: Current Playback Time
 const curTime = playerSdk.player.currentTime;

 // Get Status Attribute: Is the Current Video on Pause?
 const isPaused = playerSdk.player.paused;

 // Call API: Play Video
 playerSdk.player.play().then(() => {
   // Playback successful.
 }).catch(() => {
   // Playback failed, typically occurs during autoplay without user interaction.
 });
```


<span id="7979aa3d"></span>
## Attributes

Most player kernel attributes are read\-only, but some are writable. For example, the video `duration` is a read\-only attribute, so it cannot be set using the Set method. The video `volume` supports both the Get method and Set method, so you can use the kernel to get or set the volume.

```javascript
  const playerSdk = new VePlayer({
    id: 'video',
    width: 800,
    height: 500,
    url: 'xx.mp4'
  });

  // Get Video Duration
  const duration = playerSdk.player.duration;

  // Get Video Volume
  const curVolume = playerSdk.player.volume;
  // Set Video Volume
  playerSdk.player.volume = 0.1;
```



|Parameter |Type |Read/write type |Description |
|---|---|---|---|
|config |Object |Read\-only |Configuration object for the current player |
|root |HTMLElement |Read\-only |Player outer container DOM object |
|video |Object |Read\-only |The media object, usually `videoElement` or `audioElement` |
|autoplay |Boolean |Readable and writable |Sets/returns autoplay attributes |
|buffered |TimeRange |Read\-only |Returns the currently buffered time range |
|played |TimeRange |Read\-only |Returns the time range of the audio/video already played |
|crossOrigin |String |Readable and writable |Sets/returns whether it is cross\-domain |
|currentSrc |String |Readable and writable |Sets/returns the playback URL of the current video |
|currentTime |Number |Readable and writable |Sets/returns the current playback time of the video, in seconds |
|duration |Number |Read\-only |Returns the video duration, in seconds |
|cumulateTime |Number |Read\-only |Returns the total playback duration of the video, in seconds |
|volume |Number |Readable and writable |Sets/returns the video volume (0 to 1) |
|muted |Boolean |Readable and writable |Sets/returns the video mute state |
|defaultMuted |Boolean |Read\-only |Sets whether to mute by default; only takes effect during initialization |
|playbackRate |Number |Readable and writable |Sets/returns the current video playback speed |
|error |MediaError |String |Read\-only |
|errorNote |String |Read\-only |Media error object constants, same as media error code constants |
|loop |Boolean |Readable and writable |Sets/returns whether loop is enabled |
|src |String |Readable and writable |Sets/returns the URL of the current video (setting this parameter is equivalent to switching the video source of the video that is currently playing) |
|lang |String |Readable and writable |Sets/returns the current language |
|control |Plugin |Readable and writable |Player control bar plug\-in object. For more information about the control bar, see [Web Player SDK: Plugins](https://docs.byteplus.com/docs/byteplus-vod/docs-plugins-web). |
|innerContainer |HTMLElement |Read\-only |Built\-in container DOM object. This attribute exists only if the screen and control bar do not overlap, that is, if `config.marginControls` is `true`. |


<span id="6f48a955"></span>
### State attributes


|**Parameter** |**Type** |**Read/write type** |**Description** |||
|---|---|---|---|---|---|
|state |String |Read\-only |The current state of the player. All state enumeration values are described below: |||
||||**Enumeration name** |**Enumeration value** |**Description** |
||||ERROR |0 |A playback error occurred |
||||INITIAL |1 |Initialization |
||||READY |2 |The configuration, event, or plug\-in has been initialized/bound/instantiated |
||||ATTACHING |3 |Enters the media object mounting phase |
||||ATTACHED |4 |The media object has been mounted in the DOM |
||||NOTALLOW |5 |Playback is blocked |
||||RUNNING |6 |Playback has started successfully and the player has entered the playback process |
||||ENDED |7 |Playback has ended |
||||DESTROYED |8 |The player instance has been destroyed |
|ended |Boolean |Read\-only |Whether the current video has finished playing |||
|paused |Boolean |Read\-only |Whether the current video is paused |||
|networkState |String |Read\-only |The network state of the video. The values are listed below: |||
||||**Enumeration name** |**Enumeration value** |**Description** |
||||NETWORK_EMPTY |0 |If there is currently no data, the `readyState` value is `HAVE_NOTHING`. |
||||NETWORK_IDLE |1 |`HTMLMediaElement` is active and the asset has been selected, but the network is not being used. |
||||NETWORK_LOADING |2 |The browser is downloading `HTMLMediaElement` data. |
||||NETWORK_NO_SOURCE |3 |`HTMLMediaElement` source not found. |
|readyState |String |Read\-only |The ready state of the video. The values are listed below: |||
||||**Enumeration name** |**Enumeration value** |**Description** |
||||HAVE_NOTHING |0 |No information on media assets is available. |
||||HAVE_METADATA |1 |Enough media assets have been retrieved to initialize metadata. Fast forward/rewind does not throw an exception. |
||||HAVE_CURRENT_DATA |2 |Data for the current playback position is available, but not sufficient to play the next frame. |
||||HAVE_FUTURE_DATA |3 |Data on the current playback position and at least a short period of time in the future is available (data for at least two or more frames). |
||||HAVE_ENOUGH_DATA |4 |There is enough data available and the download rate is sufficient for the media asset to play uninterrupted until the end. |
|isFullscreen |Boolean |Read\-only |Whether the player is in the full\-screen state |||
|isCssfullScreen |Boolean |Read\-only |Whether the player is in webpage full\-screen state |||
|isSeeking |Boolean |Read\-only |Whether it is in fast forward/rewind state |||
|isActive |Boolean |Read\-only |Whether it is in focus. The control bar is displayed when in the focus state. |||


<span id="a6554e04"></span>
## API

<span id="1407a511"></span>
### play

Starts playback.

 **`@return`**`{ Promise<void> | null }`

```javascript
playerSdk.player.play() // OR
playerSdk.player.play().then(() => {// Playback successfully}).catch(() => {// Playback failed, usually occurs during autoplay without user interaction})
```


<span id="44068150"></span>
### pause

Pauses playback.

```javascript
playerSdk.player.pause()
```


<span id="486c48f0"></span>
### start

Starts the player, starts loading media assets, and initializes the `video` element.

 **`@param`**`{ string } url` video URL.

```javascript
playerSdk.player.start(url)
```


<span id="62ecccc5"></span>
### replay

The playback progress goes back to the opening scene and the video plays again. This usually occurs at the end of playback.

```javascript
playerSdk.player.replay()
```


<span id="1d1f85ff"></span>
### seek

Jumps to a certain point in time, and then continues playback.

 **`@param`**`{ number } time`. The parameter is a number type and the unit is seconds.

```javascript
playerSdk.player.seek(20)
```


<span id="582d3418"></span>
### reload

Reloads the video.

```javascript
playerSdk.player.reload()
```


<span id="6cceadc2"></span>
### resetState

Resets the current instance state. Pauses the video and sets the current instance state back to the state before the start of playback. The calculation result for the playback duration is cleared and the class name on the player container DOM is reset to the state before the start of playback.

<span id="4b66e297"></span>
### reset

Resets the instance state, unregisters all registered components, and restores the configuration of the current instance to its default value.

<span id="460f9f0c"></span>
### setConfig

Updates the configuration information. If the new configuration list contains configuration items for the built\-in plug\-in, the `setConfig` for the built\-in plug\-in is called to update it.

 **`@param`**`{config)} newConfig`

```javascript
playerSdk.player.setConfig({url: 'Another url',})
```


<span id="910918d2"></span>
### destroy

Destroys the player kernel object. When the object is destroyed, all built\-in objects are destroyed at the same time and the `Events.DESTROY` event is issued during the API call.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After the player kernel instance has been destroyed, clear player kernel instance references to free up memory.</div>


* <div data-tips="true" data-tips-type="warning">Calling API operations after the player instance is destroyed may throw an exception.</div>



```javascript
playerSdk.player.destroy() // destroy player
playerSdk.player = null // Set the instance reference to null.
```


<span id="bc9795d4"></span>
### resetState

Attempts to pause the `MediaElement` and restores the player UI state.

```javascript
playerSdk.player.resetState()
```


<span id="2a9509ed"></span>
### focus

The player obtains focus. After calling the API, `playerSdk.player.isActive` becomes `true` and the SDK triggers the `Events.playerSdk.player_FOCUS` event.

 **`@param`**`{ { autoHide?: boolean, delay?: number } } data`


* `autoHide` indicates whether automatic hiding is required. The default is `true`, which means that after the `delay` duration has elapsed, `playerSdk.player.blur()` is called automatically.

* `delay` is the time until auto hide, in milliseconds. When `autoHide: false`, this parameter is ignored and `playerSdk.player.config.inactive` is fetched by default.


<span id="02c04bac"></span>
### blur

The player goes out of focus. After calling the API, `playerSdk.player.isActive` will become `false` and the SDK will trigger the `Events.playerSdk.player_BLUR` event.

 **`@param`**`{ { ignorePaused?: boolean } } data`

`ignorePaused` indicates whether to ignore the pause state. The default value is `true`, so the focus state is not canceled when paused by default.

<span id="c787d079"></span>
### canPlayType

Detects whether the current browser can play the specified video type.


*  **`@param`**`{ string } mimeType` is the `MimeType` to be detected

*  **`@return`**`{ boolean }` indicates whether the video type can be played


```javascript
const mimeType = 'video/mp4; codecs="avc1.64001E, mp4a.40.5"'
playerSdk.player.canPlayType(mimeType);
```


<span id="da2c8efe"></span>
### getBufferedRange

Returns the buffer time range in which `currentTime` is located.


* If  **`@param`**`{ TimeRanges? } buffered` is not provided, `playerSdk.player.buffered` is fetched

*  **`@return`**`{ [number, number] }` [start, end] returns the buffer start and end times


```javascript
const [start, end] = playerSdk.player.getBufferedRange();
```


<span id="a3f56e46"></span>
### checkBuffer

Verifies that a certain point in time is within the current buffer range.


*  **`@param`**`{number} time` is the point in time

*  **`@return`**`{ boolean }`


```javascript
const flag = playerSdk.player.checkBuffer(10);
```


<span id="4674e81e"></span>
### getFullscreen

Fetches the full\-screen state.

```javascript
// Listen for fullscreen changes.
playerSdk.on(Events.FULLSCREEN_CHANGE, (isFullscreen) => {if (isFullscreen) {// fullscreen} else {// exit fullscreen}})// The player has entered fullscreen mode.
playerSdk.player.getFullscreen()
```


<span id="2f2a0864"></span>
### exitFullscreen

Exits the full\-screen state. When this API is called, the SDK will trigger the `Events.FULLSCREEN_CHANGE` event and change `isFullscreen` to `false`.

```javascript
playerSdk.player.exitFullscreen()
```


<span id="ed586c07"></span>
### getCssFullscreen

Fetches the webpage full\-screen state.

```javascript
// Listen for fullscreen changes on the webpage.
playerSdk.on(Events.CSS_FULLSCREEN_CHANGE, (isFullscreen) => {if (isFullscreen) {// fullscreen on webpage} else {// exit fullscreen on webpage}})
playerSdk.player.getCssFullscreen()
```


<span id="55da1c93"></span>
### exitCssFullscreen

Exits the webpage full\-screen state. When this API is called, the SDK will trigger the `Events.CSS_FULLSCREEN_CHANGE` event and change `isFullscreen` to `false`.

```javascript
playerSdk.player.exitCssFullscreen()
```


<span id="f072ba74"></span>
### addClass

Adds the CSS class name to the player container `playerSdk.player.root`.

 **`@param`**`{ string } className` is the class name

```javascript
playerSdk.player.addClass('className')
```


<span id="3c7484ef"></span>
### removeClass

Removes the CSS class name from the player container `playerSdk.player.root`.

 **`@param`**`{ string } className` is the class name

```javascript
playerSdk.player.removeClass('className')
```


<span id="75ff235a"></span>
### hasClass

Determines whether the player container `playerSdk.player.root` has a CSS class name.


*  **`@param`**`{ string } className` is the class name

*  **`@return`**`{ boolean }`


```javascript
const flag = playerSdk.player.hasClass('className')
```


<span id="b55c2f7a"></span>
### setAttribute

Sets attributes for the player container `playerSdk.player.root`.


*  **`@param`**`{ string } key` is the attribute name

*  **`@param`**`{ string } value` is the attribute value


```javascript
playerSdk.player.setAttribute('key', 'value')
```


<span id="738bc8f5"></span>
### resize

Adjusts the player size. If you configure `fitVideoSize` or `videoFillMode` during initialization, or the video screen rotates, calling this API operation will trigger overall size calculation based on the video screen and the current player container size.

```javascript
playerSdk.player.resize()
```


<span id="ad3d6d19"></span>
### getPlugin

Fetches a plug\-in instance from the current player.

 **`@param`**`{ string } pluginName`

```javascript
const pluginInstance = playerSdk.player.getPlugin('pluginName')
```


<span id="907282a3"></span>
### registerPlugin

Registers a plug\-in with the current player.


*  **`@param`**`{ {plugin: function, options: object} | function } plugin` is the plug\-in struct function.

*  **`@param`**`{ {[propName: string]: any}?` `}` is an optional configuration for the config plug\-in configuration list.

*  **`@return`**`{ object } pluginInstance` returns the plug\-in instance.


```javascript
const pluginInstance = playerSdk.player.registerPlugin(MyPlugin)
```


<span id="8a2027d0"></span>
### unRegisterPlugin

Destroys or unregisters a plug\-in on the current player.


*  **`@param`**`{ { pluginName: string } | string } Plugin` is the plug\-in instance or plug\-in name.

*  **`@param`**`{ boolean } removedFromConfig` indicates whether to also remove the instance from `playerSdk.player.config.plugins` when it is unregistered. The default state is `false`.


```javascript
const pluginInstance = playerSdk.player.unRegisterPlugin(pluginName)
```
