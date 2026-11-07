---
title: "Web Player SDK: Methods"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-methods"
---

<span id="veplayer"></span>
## VePlayer

Type：`class`

<span id="property"></span>
### Property


|Property |Type |Description |
|---|---|---|
|player |any |Player core instance. See [Player core](https://www.volcengine.com/docs/4/1249083). |
|src |string |Return the current video URL. |
|preLoadData | |`Readonly` Whether the current playback hit preloaded data. |
|musicMode |[PlayModeType](https://docs.byteplus.com/en/docs/25/ref#playmodetype) |Get music play mode. |
|musicTimeScale |number |Get music seek time step. |
|musicList |[IMusicListItem](https://docs.byteplus.com/en/docs/25/ref#imusiclistitem)[] |Get the music playlist. |
|region |TRegionType |`Readonly` Get the configured API region. |
|userRegion |TRegionType |`Readonly` Get the configured API region. |
|`static` sdkVersion |string |SDK version |
|`static` isMMSSupported |typeof isMMSSupported |Whether iOS MMS is supported. |


<span id="new-veplayer"></span>
### new VePlayer()

Constructor.

**Type**

```ts
constructor(configs: IPlayerConfig)
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|configs |[IPlayerConfig](https://docs.byteplus.com/en/docs/25/options#iplayerconfig) |Yes |None |\- |


<span id="on"></span>
### on()  

Listen for an event.

**Type**

```ts
(action: string, func: (...args: any[]) => void) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|action |string |Yes |None |\- |
|...func |(...args: any[]) =\> void |Yes |None |\- |


<span id="emit"></span>
### emit()  

Emit an event.

**Type**

```ts
(action: string, payload?: any) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|action |string |Yes |None |\- |
|payload |any |Yes |None |\- |


<span id="once"></span>
### once()  

Listen for an event; the handler runs only once.

**Type**

```ts
(action: string, func: (...args: any[]) => void) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|action |string |Yes |None |\- |
|...func |(...args: any[]) =\> void |Yes |None |\- |


<span id="off"></span>
### off()  

Remove an event listener.

**Type**

```ts
(action: string, func: (...args: any[]) => void) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|action |string |Yes |None |\- |
|...func |(...args: any[]) =\> void |Yes |None |\- |


<span id="setveerror"></span>
### _setVeError()  

**Type**

```ts
() => void
```


<span id="updatemediasource"></span>
### updateMediaSource()  

Update the media source. You can call this method to update the address and expiration timestamp before the video playback address expires.

**Type**

```ts
(source: SourceConfig) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|source |Pick<T, K\> |Yes |None |The media source configuration. See SourceConfig. Supports passing video playback address `url`, playback list `playList`, or `vid` and `playAuthToken`, and also includes the expiration timestamp `urlExpireTimestamp` of the new address. |


**Return Value**

`Promise<void>`

<span id="changepluginsicon"></span>
### changePluginsIcon()  

**Type**

```ts
(pluginName: any, IsShow: any) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|pluginName |any |Yes |None |\- |
|IsShow |any |Yes |None |\- |


**Return Value**

<span id="switchauthtoken"></span>
### switchAuthToken()  

Replace the temporary play token during playback to switch the video source.

**Type**

```ts
(config: IPlayAuthTokenConfig, isNewVideo?: boolean) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/options#iplayauthtokenconfig) |Yes |None |\- |
|isNewVideo |boolean |Yes |`true` |*  |


**Return Value**

`Promise<void>`

<span id="updateauthtoken"></span>
### updateAuthToken()  

Update the temporary play token.

**Type**

```ts
(config: IPlayAuthTokenConfig) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/options#iplayauthtokenconfig) |Yes |None |\- |


**Return Value**

`Promise<void>`

<span id="playnext"></span>
### playNext()  

Play the next video.

**Type**

```ts
(config: IPlayerConfig, isNewVideo?: boolean) => Promise<any>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[IPlayerConfig](https://docs.byteplus.com/en/docs/25/options#iplayerconfig) |Yes |None |\- |
|isNewVideo |boolean |Yes |`true` |*  |


**Return Value**

`Promise<any>`

<span id="changedefinition"></span>
### changeDefinition()  

Switch definition (resolution).

**Type**

```ts
(definition: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|definition |string |Yes |None |\- |


<span id="getdefinitionlist"></span>
### getDefinitionList()  

Get the definition list. Each item has `definition`, `url`, and `selected` (true for the active level).

**Type**

```ts
() => { [propName: string]: any; definition: string; url: IUrl; selected: boolean; }[]
```


**Return Value**

`Array<{ definition: string; url: IUrl; selected: boolean; [propName: string]: any; }>`

<span id="getaudiotracks"></span>
### getAudioTracks()  

Get the audio track list. For HLS, tracks come from hls.js; on iOS native playback, from `HTMLMediaElement.audioTracks`.

**Notes**

Each item includes `id`, `name`, `lang`, `channels`, `default`, and `selected`. Returns an empty array when there is at most one track.

**Type**

```ts
() => AudioTrackInfo[]
```


**Return Value**

[AudioTrackInfo](https://docs.byteplus.com/en/docs/25/75893#audiotrackinfo)`[]`

<span id="getcurrentaudiotrack"></span>
### getCurrentAudioTrack()  

Get the currently active audio track.

**Notes**

For HLS, from hls.js; on iOS native playback, from `HTMLMediaElement.audioTracks`. Returns `null` when no track is active.

**Type**

```ts
() => AudioTrackInfo | null
```


**Return Value**

[AudioTrackInfo](https://docs.byteplus.com/en/docs/25/75893#audiotrackinfo)` | null`

<span id="switchaudiotrack"></span>
### switchAudioTrack()  

Switch audio track.

**Notes**

Emits `Events.AUDIO_TRACK_CHANGE` when done. PC and mobile audio track plugins update selection automatically.

**Type**

```ts
(track: AudioTrackInfo) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|track |[AudioTrackInfo](https://docs.byteplus.com/en/docs/25/75893#audiotrackinfo) |Yes |None |Target audio track object from `getAudioTracks()`. |


<span id="musicadd"></span>
### musicAdd()  

Add a track to the playlist.

**Type**

```ts
(meta: IMusicListItem) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|meta |[IMusicListItem](https://docs.byteplus.com/en/docs/25/ref#imusiclistitem) |Yes |None |\- |


<span id="musicrandom"></span>
### musicRandom()  

Get a random track from the playlist.

**Type**

```ts
() => IMusicListItem
```


**Return Value**

[IMusicListItem](https://docs.byteplus.com/en/docs/25/ref#imusiclistitem)

<span id="musicnext"></span>
### musicNext()  

**Type**

```ts
() => void
```


<span id="musicprev"></span>
### musicPrev()  

**Type**

```ts
() => void
```


<span id="musicsetindex"></span>
### musicSetIndex()  

Play a specific track in the playlist.

**Type**

```ts
(index: number) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|index |number |Yes |None |\- |


<span id="musicforward"></span>
### musicForward()  

**Type**

```ts
() => void
```


<span id="musicbackward"></span>
### musicBackward()  

**Type**

```ts
() => void
```


<span id="musicremove"></span>
### musicRemove()  

Remove a track from the playlist.

**Type**

```ts
(vid: string | number) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|vid |string \| number |Yes |None |\- |


<span id="musicsetabcycle"></span>
### musicSetAbCycle()  

Set AB loop playback between two points.

**Type**

```ts
(start: number | IABCycle, end?: number, loop?: boolean, ext?: { [propName: string]: any; } | undefined) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|start |number \| [IABCycle](https://docs.byteplus.com/en/docs/25/options#iabcycle) |Yes |None |\- |
|end |number \| undefined |No |None |\- |
|loop |boolean \| undefined |No |None |\- |
|ext |{ [propName: string]: any; } \| undefined |No |None |\- |


<span id="musicremoveabcycle"></span>
### musicRemoveAbCycle()  

Remove AB loop playback.

**Type**

```ts
() => void
```


<span id="getloguserid"></span>
### getLogUserId()  

**Type**

```ts
() => string
```


**Return Value**

`string`

<span id="getplugin"></span>
### getPlugin()  

Get a plugin instance.

**Type**

```ts
(pluginName: string) => null | BasePlugin
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|pluginName |string |Yes |None |\- |


**Return Value**

`null | BasePlugin`

<span id="destroy"></span>
### destroy()  

Destroy the current player instance.

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="static-prepare"></span>
### `static` prepare()  

Playback strategy pre\-initialization configuration.

**Type**

```ts
(options: StrategyInitOptions) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|options |[StrategyInitOptions](https://docs.byteplus.com/en/docs/25/options#strategyinitoptions) |Yes |None |\- |


**Return Value**

`Promise<void>`

<span id="static-setpreloadscene"></span>
### `static` setPreloadScene()  

Set preload mode.

**Type**

```ts
(preloadScene: PreloadScene, options?: IPreloadUpdateConfig) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|preloadScene |[PreloadScene](https://docs.byteplus.com/en/docs/25/options#preloadscene) |Yes |None |\- |
|options |IPreloadUpdateConfig \| undefined |No |None |\- |


<span id="static-addpreloadlist"></span>
### `static` addPreloadList()  

Add videos to the preload list.

**Type**

```ts
(list: IPreloadStream[]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|list |[IPreloadStream](https://docs.byteplus.com/en/docs/25/options#ipreloadstream)[] |Yes |None |\- |


<span id="static-setpreloadlist"></span>
### `static` setPreloadList()  

Set the preload list, replacing the current list.

**Type**

```ts
(list: IPreloadStream[]) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|list |[IPreloadStream](https://docs.byteplus.com/en/docs/25/options#ipreloadstream)[] |Yes |None |\- |


**Return Value**

`Promise<void>`

<span id="static-setlicenseconfig"></span>
### `static` setLicenseConfig()  

**Type**

```ts
(config: ILicenseConfig) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|config |[ILicenseConfig](https://docs.byteplus.com/en/docs/25/ref#ilicenseconfig) |Yes |None |\- |


**Return Value**

`Promise<void>`

<span id="static-checklicense"></span>
### `static` checkLicense()  

**Type**

```ts
() => Promise<LicenseEdition>
```


**Return Value**

`Promise<`[LicenseEdition](https://docs.byteplus.com/en/docs/25/ref#licenseedition)`>`

<span id="static-checkmodulelist"></span>
### `static` checkModuleList()  

**Type**

```ts
() => Promise<string[]>
```


**Return Value**

`Promise<string[]>`

<span id="static-checklicensestatus"></span>
### `static` checkLicenseStatus()  

**Type**

```ts
() => Promise<LicenseStatus>
```


**Return Value**

`Promise<`[LicenseStatus](https://docs.byteplus.com/en/docs/25/ref#licensestatus)`>`

<span id="static-checklicensemoduleauth"></span>
### `static` checkLicenseModuleAuth()  

**Type**

```ts
(module: string, featureName: LicenseFeature) => Promise<boolean>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|module |string |Yes |None |\- |
|featureName |[LicenseFeature](https://docs.byteplus.com/en/docs/25/ref#licensefeature) |Yes |None |\- |


**Return Value**

`Promise<boolean>`

<span id="static-generateencryptinfo"></span>
### `static` generateEncryptInfo()  

**Type**

```ts
(unionId: string, streamType: 'hls' | 'mp4' | 'dash') => Promise<EncryptInfo | undefined>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|unionId |string |Yes |None |用户唯一id |
|streamType |"mp4" \| "hls" \| "dash" |Yes |None |私有加密视频的格式/协议，取值有：hls、mp4、dash。 |


**Return Value**

`Promise<EncryptInfo | undefined>`

<span id="audiotrackinfo"></span>
## AudioTrackInfo  

Type：`interface`

Return type of `getAudioTracks()` / `getCurrentAudioTrack()`; can be passed directly to `switchAudioTrack()`.

<span id="selected"></span>
### selected  

Type：`boolean`

Whether this is the currently active track. Always `true` when returned by `getCurrentAudioTrack()`.

<span id="audiotrack"></span>
## AudioTrack  

Type：`interface`

HLS audio track object. Extends `AudioTrackOption` with list index and display name.

<span id="id"></span>
### id  

Type：`number`

Track index in the `audioTracks` list (number on both hls.js and native paths).

<span id="name"></span>
### name  

Type：`string`

Display name (derived from `lang` / `name` or from the manifest).

<span id="default"></span>
### default  

Type：`boolean`

Whether this is the default track in the manifest.
