---
title: "API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/api"
---

<span id="40775529"></span>
## IDanmuItem


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|id |String |Yes |None |The comment ID. Set the parameter to a globally unique random value in the live room. |
|txt |String |Yes |None |The content of the bullet comment. |
|isPresenter |Boolean |No |None |Specifies whether the bullet comment is sent by the host. Valid values:<br><br><br>* `true`: By the host.<br><br>* `false`: Not by the host. |
|isSelf |Boolean |No |None |Specifies whether the bullet comment is sent by the current user. Valid values:<br><br><br>* `true`: By the current user.<br><br>* `false`: Not by the current user. |
|duration |Number |No |None |The duration during which the bullet comment is displayed on the screen. Unit: milliseconds. |


<span id="7ea0d771"></span>
## ILang

The viewing page language information.


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|label |String |Yes |None |The specific name of the language. Valid values:<br><br><br>* `简中`: Simplified Chinese.<br><br>* `EN`: English.<br><br>* `日本語`: Japanese.<br><br>* `繁中`: Traditional Chinese.<br><br>* `한국인`: Korean.<br><br>* `แบบไทย`: Thai.<br><br>* `Tiếng Việt`: Vietnamese.<br><br>* `بالعربية` : Arabic.<br><br>* `Türkçe`: Turkish.<br><br>* `Español`: Spanish.<br><br>* `Bahasa Indonesia`: Indonesian.<br><br>* `Português`: Portuguese.<br><br>* `Русский`: Russian. |
|value |Number |Yes |None |The value corresponding to each language. Valid values:<br><br><br>* `0`: Simplified Chinese.<br><br>* `1`: English.<br><br>* `2`: Japanese.<br><br>* `3`: Traditional Chinese.<br><br>* `4`: Korean.<br><br>* `5`: Thai.<br><br>* `6`: Vietnamese.<br><br>* `7`: Arabic.<br><br>* `8`: Turkish.<br><br>* `9`: Spanish.<br><br>* `10`: Indonesian.<br><br>* `11`: Portuguese.<br><br>* `12`: Russian. |


<span id="6ec26091"></span>
## ILangMap

The viewing page language.


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|languageOptional |[ILang](https://docs.byteplus.com/docs/byteplus-livesaas/api#7ea0d771)[] |Yes |`-` |The languages supported by the viewing page. |
|currentLang |[ILang](https://docs.byteplus.com/docs/byteplus-livesaas/api#7ea0d771) |Yes |`-` |The current language of the viewing page. |


<span id="40cc095d"></span>
## WebSDKBase

Type:`class`

<span id="338057e9"></span>
### getPlayerInstance()

Gets the player instance.

```TypeScript
() => any
```


**Return value**

`any`

<span id="794f6502"></span>
### destroy()

Destroys the SDK.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the current viewing page no longer requires the SDK, you can call this API to destroy the SDK and release resources. However, we do not recommend you rebuild the SDK after its destruction. If the SDK is needed again, we recommend that you integrate the SDK into a new viewing page instead of destroying and rebuilding the SDK.</div>


```TypeScript
() => void
```


<span id="e4f32962"></span>
### preloadActivity()

Preloads and caches live room data to accelerate room creation during feed\-based transitions.

Call this method before switching live rooms in feed\-based scenarios to reduce loading latency. After calling this method, if a live room is created within **1 minute**, the SDK will reuse the cached data to accelerate the room creation process.

```TypeScript
(conf: SDKConf) => Promise<void>
```


**Parameter**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|conf |[SDKconf](https://docs.byteplus.com/docs/byteplus-livesaas/parameters#2c9e46bc) |Yes |None |The SDK configurations used to preload activity data. |


<span id="e41839ed"></span>
### sendDanmu()

Sends a bullet comment.

```TypeScript
(payload: IDanmuItem[]) => void
```


**Parameters**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|payload |[IDanmuItem](https://docs.byteplus.com/docs/byteplus-livesaas/api#40775529)[] |Yes |`-` |The configurations for the bullet comment. |


<span id="8ba13e15"></span>
### updateModulesConf()

Dynamically updates the `modules` or `options` configurations of the SDK.

For example, you can call this API to implement small\-window mode on mobile devices. For more information about the effect, see the [demo](https://live.byteplus.com/demo/sdk/index.mobile.pip.html).

```TypeScript
(conf: Partial<SDKConfAll>) => void
```


**Parameter**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|conf |Partial |Yes |None |The SDK configurations to be updated. For details, see [SDKconf](https://docs.byteplus.com/docs/byteplus-livesaas/parameters#2c9e46bc). |


<span id="4f4ea3d6"></span>
### updateMode2Token()

Updates the token obtained when the value of `mode` is `1` to that obtained when the value of `mode` is `2`.

```TypeScript
 (token: string) => Promise<{ status: boolean; info: string;}>
```


**Parameter**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|token |String |Yes |None |The token obtained when the value of `mode` is `2`. |


**Return value**

`Promise<{ status: boolean; info: string; }>`


* `status`: Indicates whether the update is successful.

   * `true`: Successful.

   * `false`: Failed.

* `info`: The error message.


<span id="6db63c70"></span>
### seekVideo()

Seeks to a specified time point in a preview or playback.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the video has never been played on WeChat with an iOS device before, calling this API cannot seek to a specified time point.</div>


```TypeScript
(param: { time: number;}) => void
```



|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|param |\- |Yes |`-` |Configurations for seeking to a specified time point in a preview or playback. |
|time |Number |Yes |None |The time point to be seeked to. Unit: seconds. |


<span id="cb44cfa8"></span>
### getVodPlayInfo()

Gets the information of a preview or playback.

```TypeScript
() => { vid: string; currentTime: number; duration: number;}
```


**Return value**

`{ vid: string; currentTime: number; duration: number; }`


* `vid`: The video ID, which is the unique identifier of the video.

* `currentTime`: The current playback time point. Unit: seconds.

* `duration`: The total length of the video. Unit: seconds.


<span id="88ab1ee1"></span>
### switchChannel()

Switches to the specified live source if the live room is in **Live** status, and switches to the specified playback video if the live room is in **Playback** status.

```TypeScript
webSDK.switchChannel(index);
```



|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|index |Number |Yes |None |The sequence of a live source or playback video in the live room.<br><br>For example, if the value is `0`, call this API to switch to the first live source or playback video in the live room. If the value is `1`, call this API to switch to the second live source or playback video in the live room. |


<span id="35db7c0e"></span>
### getPageLanguage()

Gets the languages supported by the viewing page and the current language of the viewing page. This method is usually used together with the [switchLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/api#a58b37a7) method, and is suitable for scenarios where you have your own button for switching languages on the viewing page.

```TypeScript
() => ILangMap
```


**Return value**

[ILangMap](https://docs.byteplus.com/docs/byteplus-livesaas/api#6ec26091)

<span id="a58b37a7"></span>
### switchLanguage()

Switches to the specified viewing page language. This method is suitable for scenarios where you have your own button for switching languages on the viewing page.

```TypeScript
(lang: number) => void
```



|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|lang |Number |Yes |None |The viewing page language to switch to. You can first call [getPageLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/api#35db7c0e) to get the languages supported by the viewing page and then use one of the languages as the parameter value. Valid values:<br><br><br>* `0`: Simplified Chinese.<br><br>* `1`: English.<br><br>* `2`: Japanese.<br><br>* `3`: Traditional Chinese.<br><br>* `4`: Korean.<br><br>* `5`: Thai.<br><br>* `6`: Vietnamese.<br><br>* `7`: Arabic.<br><br>* `8`: Turkish.<br><br>* `9`: Spanish.<br><br>* `10`: Indonesian.<br><br>* `11`: Portuguese.<br><br>* `12`: Russian. |


<span id="186d390f"></span>
### **showPlaybackListPopup()** 

Displays the playback collection list popup window on the viewing page. This method is usually used together with the [hidePlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api#8484f7d1) method, and is suitable for scenarios where you have your own playback list on the viewing page.

```Plain
() => void
```


<span id="8484f7d1"></span>
### **hidePlaybackListPopup()** 

Hides the playback collection list popup window on the viewing page. This method is usually used together with the [showPlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api#186d390f) method, and is suitable for scenarios where you have your own playback list on the viewing page.

```Plain
() => void
```


<span id="15a73849"></span>
### **getPlayBackListInfo()** 

Gets the playback collection list information on the viewing page. This method is usually used together with the [showPlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api#186d390f) and [hidePlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api#8484f7d1) method, and is suitable for scenarios where you have your own playback list on the viewing page.

```Plain
() => Array<{ vid: string; poster: string; name: string; duration: number }>
```


**Return value:** 

Returns an array of playback videos.

`Array<{ vid: string; poster: string; name: string; duration: number }>`

Each item contains:


* `vid`: The video ID, which is the unique identifier of the video.

* `poster`: Video thumbnail URL with protocol header.

* `name`: The video name.

* `duration`: The total length of the video. Unit: seconds.


<span id="67c44fd2"></span>
### **lockPlayBackVods()** 

Locks specified videos in the playback collection list. This method is usually used together with the [unlockPlayBackVods()](https://docs.byteplus.com/docs/byteplus-livesaas/api#cddd4919) method to restrict videos for paid access or VIP\-only access.

```Plain
(vids: string[]) => void
```


**Parameter**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|`vids` |`string[]` |Yes |None |An array of video IDs to lock. Locked videos cannot be played. |


<span id="cddd4919"></span>
### **unlockPlayBackVods()** 

Unlocks previously locked playback videos. This method is usually used together with the [lockPlayBackVods()](https://docs.byteplus.com/docs/byteplus-livesaas/api#67c44fd2) method to restrict videos for paid access or VIP\-only access.

```Plain
(vids: string[]) => void
```


**Parameter**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|`vids` |`string[]` |Yes |None |An array of video IDs to unlock. |


<span id="ada4c709"></span>
### getProductList()

Gets the list of products displayed on the view page.

```TypeScript
() => Promise<ProductInfo[]>
```


**Return value**

`ProductInfo[]`

Array of product objects. For more information, see [ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#fe534689).

<span id="bd140bf3"></span>
### updateProductInfo()

Updates one or more products' information.

```TypeScript
(props: Partial<ProductInfo>[]) => Promise<void>
```


**Parameters**


|Name |Data Type |Required |Default Value |Description |
|---|---|---|---|---|
|`props` |`Partial<ProductInfo>[]` |Yes |None |Array of product information object with optional fields to update. Each object **must include the** **`Id`** of the product to identify which product to update. Only the fields provided will be updated; other fields remain unchanged. For more information, see [ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#fe534689). |
