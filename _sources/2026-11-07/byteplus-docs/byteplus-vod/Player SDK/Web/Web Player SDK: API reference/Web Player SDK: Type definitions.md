---
title: "Web Player SDK: Type definitions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-type-definitions"
---

<span id="edrmtype"></span>
## EDRMTYPE  

Type：`enum`

DRM / encryption playback type.


|Property |Value |Description |
|---|---|---|
|DRM_ENCRYPT |`'drm_encrypt'` |Commercial DRM. |
|PRIVATE_ENCRYPT |`'private_encrypt'` |Legacy private encryption. |
|PRIVATE_ENCRYPT_UPGRADE |`'private_encrypt_upgrade'` |Upgraded private encryption. |
|STANDARD_ENCRYPT |`'standard_encrypt'` |HLS standard encryption. |


<span id="imobileconfig"></span>
## IMobileConfig  

Type：`interface`

Mobile interaction configuration.

<span id="disablegesture"></span>
### disableGesture  

Type：`boolean | undefined`

Whether to disable gestures. Gesture includes:


* Horizontal gesture to fast forward/rewind

* Left gesture to adjust brightness

* Right gesture to adjust volume (iOS not available)


<span id="gesturex"></span>
### gestureX  

Type：`boolean | undefined`

Whether to enable horizontal gesture processing. Horizontal gesture includes fast forward/rewind.

<span id="gesturey"></span>
### gestureY  

Type：`boolean | undefined`

Whether to enable vertical gesture processing. Vertical gesture includes screen right and screen left. Default left to adjust brightness, right to adjust volume. The left and right range ratio is set through scopeL and scopeR.

<span id="scopel"></span>
### scopeL  

Type：`number | undefined`

The left gesture range ratio, the value is 0\-1.

<span id="scoper"></span>
### scopeR  

Type：`number | undefined`

The right gesture range ratio, the value is 0\-1.

<span id="darkness"></span>
### darkness  

Type：`boolean | undefined`

Whether to enable left dimming function. Because the web端无法调用系统的亮度，这个功能实际使用透明蒙层实现。

<span id="maxdarkness"></span>
### maxDarkness  

Type：`number | undefined`

The maximum darkness of the player, i.e., the maximum transparency of the transparent layer.

<span id="gradient"></span>
### gradient  

Type：`"normal" | "none" | "top" | "bottom" | undefined`

Whether to enable vertical gradient shadow, i.e., there is a shadow in the upper and lower range when the player is activated.


* normal: normal shadow

* none: no shadow

* top: only upper shadow

* bottom: only lower shadow


<span id="istouchingseek"></span>
### isTouchingSeek  

Type：`boolean | undefined`

Whether to update the player's currentTime when the touchMove event is triggered (i.e., when the gesture is slid). During the gesture movement, the player's fast forward/rewind is not directly called, and the currentTime is set when the toucheEnd event is triggered.

<span id="minimovestep"></span>
### miniMoveStep  

Type：`number | undefined`

The minimum step of the gesture movement, the unit is px, i.e., the sliding distance exceeding which is considered as sliding, to reduce unnecessary sliding gesture event triggers.

<span id="pressrate"></span>
### pressRate  

Type：`number | undefined`

The long press fast forward speed.

<span id="disableactive"></span>
### disableActive  

Type：`boolean | undefined`

Whether to disable the time preview sprite panel.

<span id="disabletimeprogress"></span>
### disableTimeProgress  

Type：`boolean | undefined`

Whether to disable the time progress bar, i.e., not to show the mini progress bar when dragging.

<span id="hidecontrolsactive"></span>
### hideControlsActive  

Type：`boolean | undefined`

Whether to hide the control bar when dragging.

<span id="hidecontrolsend"></span>
### hideControlsEnd  

Type：`boolean | undefined`

Whether to hide the control bar when the gesture ends.

<span id="moveduration"></span>
### moveDuration  

Type：`number | undefined`

The duration of the player area when fast forward/rewind is performed, i.e., the duration corresponding to the full passage of the player area, the unit is ms.

<span id="closedbclick"></span>
### closedbClick  

Type：`boolean | undefined`

Whether to disable the double\-click to switch pause/play ability, same as closeVideoDblclick.

<span id="disablepress"></span>
### disablePress  

Type：`boolean | undefined`

Whether to disable the long press to adjust the speed.

<span id="disableseekicon"></span>
### disableSeekIcon  

Type：`boolean | undefined`

Whether to disable the fast forward/rewind button prompt.

<span id="istartconfig"></span>
## IStartConfig  

Type：`interface`

播放器中间切换暂停/播放的按钮。

<span id="isshowpause"></span>
### isShowPause  

Type：`boolean | undefined`

暂停是否常驻

<span id="isshowend"></span>
### isShowEnd  

Type：`boolean | undefined`

是否播放结束常驻

<span id="disableanimate"></span>
### disableAnimate  

Type：`boolean | undefined`

是否禁用点击动画

<span id="mode"></span>
### mode  

Type：`"auto" | "hide" | "show" | undefined`

按钮的跟随模式


* hide：起播之后隐藏

* show：常驻一直存在

* auto：自动跟随，播放器激活时即player.isActive=true的时候显示，否则隐藏


<span id="positions"></span>
## POSITIONS  

Type：`enum`

Plugin button position.


|Property |Value |Description |
|---|---|---|
|ROOT |`'root'` |Player root node. |
|ROOT_LEFT |`'rootLeft'` |Left side of the player root node. |
|ROOT_RIGHT |`'rootRight'` |Right side of the player root node. |
|ROOT_TOP |`'rootTop'` |Top of the player root node. |
|CONTROLS_LEFT |`'controlsLeft'` |Left side of the control bar. |
|CONTROLS_RIGTH |`'controlsRight'` |Left side of the control bar (legacy typo: `controlsRight`). |
|CONTROLS_RIGHT |`'controlsRight'` |Right side of the control bar. |
|CONTROLS_CENTER |`'controlsCenter'` |Center of the control bar. |


<span id="sourceconfig"></span>
## SourceConfig  

Playback source data. Supports `url`, `playList`, or `vid` with `playAuthToken`, plus `urlExpireTimestamp` for the new URL.

**Type**

```ts
Pick<
  IPlayerConfig,
  'url' | 'playList' | 'getVideoByToken' | 'urlExpireTimestamp'
>
```


<span id="imaskconfig"></span>
## IMaskConfig  

Type：`interface`

<span id="maskurl"></span>
### maskUrl  

Type：`string`

<span id="maskoffset"></span>
### maskOffset  

Type：`number | undefined`

<span id="interval"></span>
### interval  

Type：`number | undefined`

<span id="playmodetype"></span>
## PlayModeType  

Music loop mode:


* `'order'`: Play in order

* `'sloop'`: Single track loop

* `'loop'`: Playlist loop

* `'random'`: Shuffle playlist


**Type**

```ts
'order' | 'sloop' | 'loop' | 'random'
```


<span id="imusiclistitem"></span>
## IMusicListItem  

Type：`interface`

<span id="src"></span>
### src  

Type：`string`

Music playback URL.

<span id="vid"></span>
### vid  

Type：`string | number`

Unique music ID.

<span id="poster"></span>
### poster  

Type：`string | undefined`

Music cover image URL.

<span id="title"></span>
### title  

Type：`string | undefined`

Music title.

<span id="toggle-modes"></span>
## TOGGLE_MODES  

Type：`enum`

播放列表展示面板触发动作类型。


|Property |Value |Description |
|---|---|---|
|CLICK |`'click'` |Mouse click. |
|HOVER |`'hover'` |Mouse hover. |


<span id="ivideoinfo"></span>
## IVideoInfo  

Type：`interface`

<span id="playlist"></span>
### playList  

Type：[Stream](https://docs.byteplus.com/en/docs/25/options#stream)`[]`

<span id="vid"></span>
### vid  

Type：`string`

<span id="defaultdefinitiondata"></span>
### defaultDefinitionData  

Type：[Stream](https://docs.byteplus.com/en/docs/25/options#stream)

<span id="codec"></span>
### codec  

Type：[ICodecType](https://docs.byteplus.com/en/docs/25/options#icodectype)

<span id="dashopts"></span>
### dashOpts  

Type：`{ Data: IGetPlayInfoRes; } | undefined`

**Member**


|Name |Type |Description |
|---|---|---|
|Data |`IGetPlayInfoRes` |\- |


<span id="authtoken"></span>
## AuthToken  

Type：`class`

<span id="new-authtoken"></span>
### new AuthToken()

**Type**

```ts
constructor(args)
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|args |any |Yes |None |\- |


<span id="isplaybytoken"></span>
### isPlayByToken  

Type：`boolean`

<span id="isencrypt"></span>
### isEncrypt  

Type：`boolean`

<span id="tokeninfo"></span>
### tokenInfo  

Type：[ITokenInfo](https://docs.byteplus.com/en/docs/25/36345#itokeninfo)

<span id="keytokeninfo"></span>
### keyTokenInfo  

Type：[ITokenInfo](https://docs.byteplus.com/en/docs/25/36345#itokeninfo)

<span id="thirdpartydrmauthtokeninfo"></span>
### thirdPartyDrmAuthTokenInfo  

Type：[ITokenInfo](https://docs.byteplus.com/en/docs/25/36345#itokeninfo)

<span id="config"></span>
### config  

Type：[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/options#iplayauthtokenconfig)

<span id="privatedrmauthtoken"></span>
### privateDrmAuthToken  

Type：`string`

<span id="useunioninfodrm"></span>
### useUnionInfoDRM  

Type：`boolean`

<span id="sessionid"></span>
### sessionId  

Type：`string`

<span id="retrycount"></span>
### retryCount  

Type：`number`

<span id="playinfo"></span>
### playInfo  

Type：`VideoInfoRes | undefined`

<span id="beforeplayercreate"></span>
### beforePlayerCreate()  

**Type**

```ts
() => Promise<void>
```


**Return Value**

`Promise<void>`

<span id="getvideoinfo"></span>
### getVideoInfo()  

**Type**

```ts
() => Promise<{ vid: string; playList: Stream[]; codec: ICodecType; defaultDefinition: string | undefined; } | undefined>
```


**Return Value**

`Promise<{ vid: string; playList: Stream[]; codec: ICodecType; defaultDefinition: string | undefined; } | undefined>`

<span id="getvideos"></span>
### getVideos()  

**Type**

```ts
() => Promise<any>
```


**Return Value**

`Promise<any>`

<span id="getprivatedrminfo"></span>
### getPrivateDrmInfo()  

**Type**

```ts
(playList: Stream[], vid: string, streamType: string) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|playList |[Stream](https://docs.byteplus.com/en/docs/25/options#stream)[] |Yes |None |\- |
|vid |string |Yes |None |\- |
|streamType |string |Yes |None |\- |


**Return Value**

`Promise<void>`

<span id="getthumbnailconfig"></span>
### getThumbnailConfig()  

**Type**

```ts
(thumbs: IThumbInfoItem[]) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|thumbs |IThumbInfoItem[] |Yes |None |\- |


<span id="getbarragemaskurl"></span>
### getBarrageMaskUrl()  

**Type**

```ts
(url: string) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|url |string |Yes |None |\- |


<span id="fairplay"></span>
### fairplay()  

**Type**

```ts
(videoInfo: IVideoInfo) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|videoInfo |[IVideoInfo](https://docs.byteplus.com/en/docs/25/36345#ivideoinfo) |Yes |None |\- |


<span id="init"></span>
### init()  

**Type**

```ts
() => void
```


<span id="initconfig"></span>
### initConfig()  

**Type**

```ts
(getVideoByToken: IPlayAuthTokenConfig) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|getVideoByToken |[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/options#iplayauthtokenconfig) |Yes |None |\- |


<span id="updateauthtoken"></span>
### updateAuthToken()  

**Type**

```ts
(getVideoByToken: IPlayAuthTokenConfig, isNewVideo: boolean) => Promise<void>
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|getVideoByToken |[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/options#iplayauthtokenconfig) |Yes |None |token信息 |
|isNewVideo |boolean |Yes |None |是否新视频，即是否为切换视频 |


**Return Value**

`Promise<void>`

<span id="checkplayauthtokenvalid"></span>
### checkPlayAuthTokenValid()  

**Type**

```ts
() => boolean
```


**Return Value**

`boolean`

<span id="checkkeytokenvalid"></span>
### checkKeyTokenValid()  

**Type**

```ts
() => boolean
```


**Return Value**

`boolean`

<span id="checkdrmauthtokenvalid"></span>
### checkDrmAuthTokenValid()  

**Type**

```ts
() => boolean
```


**Return Value**

`boolean`

<span id="static-pluginname"></span>
### `static` pluginName  

Type：`string`

`Readonly`,

<span id="itokeninfo"></span>
## ITokenInfo  

Type：`interface`

<span id="action"></span>
### Action  

Type：`string | undefined`

<span id="codec"></span>
### Codec  

Type：[ICodecType](https://docs.byteplus.com/en/docs/25/options#icodectype)` | undefined`

<span id="filetype"></span>
### FileType  

Type：[VideoFileTypes](https://docs.byteplus.com/en/docs/25/36345#videofiletypes)` | `[AudioFileTypes](https://docs.byteplus.com/en/docs/25/36345#audiofiletypes)` | undefined`

<span id="format"></span>
### Format  

Type：`string | undefined`

<span id="ssl"></span>
### Ssl  

Type：`0 | 1 | undefined`

<span id="version"></span>
### Version  

Type：`string | undefined`

<span id="vid"></span>
### Vid  

Type：`string | undefined`

<span id="x-algorithm"></span>
### 'X\-Algorithm'  

Type：`string | undefined`

<span id="x-credential"></span>
### 'X\-Credential'  

Type：`string | undefined`

<span id="x-expires"></span>
### 'X\-Expires'  

Type：`string | number | undefined`

<span id="x-date"></span>
### 'X\-Date'  

Type：`string | undefined`

<span id="x-signature"></span>
### 'X\-Signature'  

Type：`string | undefined`

<span id="x-signedqueries"></span>
### 'X\-SignedQueries'  

Type：`string | undefined`

<span id="drmtype"></span>
### DrmType  

Type：`string | undefined`

<span id="playauthids"></span>
### PlayAuthIds  

Type：`string | undefined`

<span id="videofiletypes"></span>
## VideoFileTypes  

Type：`enum`


|Property |Value |Description |
|---|---|---|
|VIDEO |`'video'` |\- |
|EVIDEO |`'evideo'` |\- |
|DRM_EVIDEO |`'drm_evideo'` |\- |


<span id="audiofiletypes"></span>
## AudioFileTypes  

Type：`enum`


|Property |Value |Description |
|---|---|---|
|AUDIO |`'audio'` |\- |
|EAUDIO |`'eaudio'` |\- |
|DRM_AUDIO |`'drm_eaudio'` |\- |


<span id="preloadformat"></span>
## PreloadFormat  

Type：`enum`

Preload resource format.


|Property |Value |Description |
|---|---|---|
|MP4 |`'mp4'` |\- |
|HLS |`'hls'` |\- |


<span id="ilicenseconfig"></span>
## ILicenseConfig  

Type：`interface`

<span id="license"></span>
### license  

Type：`string | `[IlicenseContent](https://docs.byteplus.com/en/docs/25/36345#ilicensecontent)

<span id="autoupload"></span>
### autoUpload  

Type：`boolean | undefined`

<span id="expiredifftime"></span>
### expireDiffTime  

Type：`number | undefined`

<span id="expirecallback"></span>
### expireCallback  

**Type**

```ts
(expireDiffTime?: number) => void
```


**Parameters**


|Name |Type |Required |Default |Description |
|---|---|---|---|---|
|expireDiffTime |number \| undefined |No |None |\- |


<span id="ilicensecontent"></span>
## IlicenseContent  

Type：`interface`

<span id="content"></span>
### content  

Type：`string`

<span id="sign"></span>
### sign  

Type：`string`

<span id="mainurl"></span>
### mainUrl  

Type：`string | undefined`

<span id="licenseedition"></span>
## LicenseEdition  

Type：`enum`


|Property |Value |Description |
|---|---|---|
|EDITION_STANDARD |`'standard_edition'` |\- |
|EDITION_PREMIUM |`'premium_edition'` |\- |
|EDITION_NONE |`'none_edition'` |\- |


<span id="licensestatus"></span>
## LicenseStatus  

Type：`enum`


|Property |Value |Description |
|---|---|---|
|LICENSE_STATUS_INVALID |`0` |\- |
|LICENSE_STATUS_OK |`1` |\- |
|LICENSE_STATUS_EXPIRED |`2` |\- |
|LICENSE_STATUS_ERROR_DOMAIN_NOT_MATCH |`401` |\- |


<span id="licensefeature"></span>
## LicenseFeature  

Type：`enum`


|Property |Value |Description |
|---|---|---|
|H265 |`'h265'` |\- |
|PRELOAD |`'preload'` |\- |
|ADAPT_RANGE |`'adaptRange'` |\- |
|ABR |`'abr'` |\- |
