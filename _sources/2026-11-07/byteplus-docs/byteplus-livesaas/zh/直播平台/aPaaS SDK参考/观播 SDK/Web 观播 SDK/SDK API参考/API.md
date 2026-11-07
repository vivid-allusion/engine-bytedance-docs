---
title: "API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN"
---

<span id="40775529"></span>
## IDanmuItem


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|id |String |是 |无 |评论的唯一ID。请设置为在直播间内唯一的值。 |
|txt |String |是 |无 |弹幕的内容。 |
|isPresenter |Boolean |否 |无 |指定弹幕是否由主播发送。有效值：<br><br><br>* `true`：由主播发送。<br><br>* `false`：非主播发送。 |
|isSelf |Boolean |否 |无 |指定弹幕是否由当前用户发送。有效值：<br><br><br>* `true`：由当前用户发送。<br><br>* `false`：非当前用户发送。 |
|duration |Number |否 |无 |弹幕的显示时长。单位：毫秒。 |


<span id="7ea0d771"></span>
## ILang

观看页的语言信息。


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|label |String |是 |无 |语言名称。有效值：<br><br><br>* `简中`：简体中文。<br><br>* `EN`：英文。<br><br>* `日本語`：日语。<br><br>* `繁中`：繁体中文。<br><br>* `한국인`：韩语。<br><br>* `แบบไทย`：泰语。<br><br>* `Tiếng Việt`：越南语。<br><br>* `بالعربية` ：阿拉伯语。<br><br>* `Türkçe`：土耳其语。<br><br>* `Español`：西班牙语。<br><br>* `Bahasa Indonesia`：印尼语。<br><br>* `Português`：葡萄牙语。<br><br>* `Русский`：俄语。 |
|value |Number |是 |无 |每种语言对应的值。有效值：<br><br><br>* `0`：简体中文。<br><br>* `1`: 英语。<br><br>* `2`: 日语。<br><br>* `3`: 繁体中文。<br><br>* `4`: 韩语。<br><br>* `5`: 泰语。<br><br>* `6`: 越南语。<br><br>* `7`: 阿拉伯语。<br><br>* `8`: 土耳其语。<br><br>* `9`: 西班牙语。<br><br>* `10`: 印度尼西亚语。<br><br>* `11`: 葡萄牙语。<br><br>* `12`: 俄语。 |


<span id="6ec26091"></span>
## ILangMap

定义观看页可用语言及当前语言。


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|languageOptional |[ILang](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#7ea0d771)[] |是 |`-` |观看页支持的语言。 |
|currentLang |[ILang](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#7ea0d771) |是 |`-` |观看页当前语言。 |


<span id="40cc095d"></span>
## WebSDKBase

类型：`class`

<span id="338057e9"></span>
### getPlayerInstance()

获取播放器实例。

```TypeScript
() => any
```


**返回值**

`any`

<span id="794f6502"></span>
### destroy()

销毁SDK。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若当前观看页不再需要SDK，可调用此API销毁SDK并释放资源。但我们不建议在SDK销毁后重新构建SDK。如需再次使用SDK，建议集成SDK到新的观看页，而非销毁后重建SDK。</div>


```TypeScript
() => void
```


<span id="e4f32962"></span>
### preloadActivity()

预加载并缓存直播间数据，以加速基于Feed的切换场景下房间创建。

在基于Feed的场景切换直播间前调用此方法，可减少加载延迟。调用此方法后，若在**1分钟**内创建直播间，SDK将复用缓存数据以加速房间创建流程。

```TypeScript
(conf: SDKConf) => Promise<void>
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|conf |[SDKconf](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#2c9e46bc) |是 |无 |用于预加载活动数据的SDK配置。 |


<span id="e41839ed"></span>
### sendDanmu()

发送弹幕。

```TypeScript
(payload: IDanmuItem[]) => void
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|payload |[IDanmuItem](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#40775529)[] |是 |`-` |弹幕配置。 |


<span id="8ba13e15"></span>
### updateModulesConf()

动态更新SDK的`modules`或`options`配置。

例如，可调用此API在移动设备上实现画中画（PiP）模式。有关效果的更多信息，请参见[demo](https://live.byteplus.com/demo/sdk/index.mobile.pip.html)。

```TypeScript
(conf: Partial<SDKConfAll>) => void
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|conf |Partial |是 |无 |需更新的SDK配置。详情请参见[SDKconf](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#2c9e46bc)。 |


<span id="4f4ea3d6"></span>
### updateMode2Token()

将令牌从`mode=1`升级为`mode=2`。

```TypeScript
 (token: string) => Promise<{ status: boolean; info: string;}>
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|token |String |是 |无 |`mode=2`的token。 |


**返回值**

`Promise<{ status: boolean; info: string; }>`


* `status`：表示更新是否成功。

   * `true`：成功。

   * `false`：失败。

* `info`：错误信息。


<span id="6db63c70"></span>
### seekVideo()

在预告或回放中定位到指定时间点。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在iOS设备上，若视频未曾播放过，此API无法在微信内对视频进行seek操作。</div>


```TypeScript
(param: { time: number;}) => void
```



|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|param |\- |是 |`-` |用于预告或回放中跳转到指定时间点的配置。 |
|time |Number |是 |无 |需跳转的时间点。单位：秒。 |


<span id="cb44cfa8"></span>
### getVodPlayInfo()

获取预告或回放的信息。

```TypeScript
() => { vid: string; currentTime: number; duration: number;}
```


**返回值**

`{ vid: string; currentTime: number; duration: number; }`


* `vid`：视频唯一ID。

* `currentTime`：当前播放时间点。单位：秒。

* `duration`：视频总时长。单位：秒。


<span id="88ab1ee1"></span>
### switchChannel()

切换到指定直播源（房间为直播时）或回放视频（房间为回放模式时）。

```TypeScript
webSDK.switchChannel(index);
```



|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|index |Number |是 |无 |直播源或回放视频的索引。<br><br>例如，index为0切换到第一个源/视频，index为1切换到第二个。 |


<span id="35db7c0e"></span>
### getPageLanguage()

获取观看页支持的语言及当前语言。实现自定义语言切换按钮时，通常与`switchLanguage()`方法配合使用。

```TypeScript
() => ILangMap
```


**返回值**

[ILangMap](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#6ec26091)

<span id="a58b37a7"></span>
### switchLanguage()

切换观看页语言。实现自定义语言切换按钮时使用此方法。

```TypeScript
(lang: number) => void
```



|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|lang |Number |是 |无 |用于切换观看页语言。请使用通过`getPageLanguage()`获取的语言值。有效值：<br><br><br>* `0`：简体中文。<br><br>* `1`: 英语。<br><br>* `2`: 日语。<br><br>* `3`: 繁体中文。<br><br>* `4`: 韩语。<br><br>* `5`: 泰语。<br><br>* `6`: 越南语。<br><br>* `7`: 阿拉伯语。<br><br>* `8`: 土耳其语。<br><br>* `9`: 西班牙语。<br><br>* `10`: 印度尼西亚语。<br><br>* `11`: 葡萄牙语。<br><br>* `12`: 俄语。 |


<span id="186d390f"></span>
### **showPlaybackListPopup()** 

在观看页显示回放合集列表弹窗。此方法通常与[hidePlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#8484f7d1)方法配合使用，适用于观看页有自定义回放列表的场景。

```Plain
() => void
```


<span id="8484f7d1"></span>
### **hidePlaybackListPopup()** 

在观看页隐藏回放合集列表弹窗。此方法通常与[showPlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#186d390f)方法配合使用，适用于观看页有自定义回放列表的场景。

```Plain
() => void
```


<span id="15a73849"></span>
### **getPlayBackListInfo()** 

获取观看页回放合集列表信息。此方法通常与[showPlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#186d390f)和[hidePlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#8484f7d1)方法配合使用，适用于观看页有自定义回放列表的场景。

```Plain
() => Array<{ vid: string; poster: string; name: string; duration: number }>
```


**返回值：** 

返回回放视频数组。

`Array<{ vid: string; poster: string; name: string; duration: number }>`

每项包含：


* `vid`：视频唯一ID。

* `poster`：带协议头的视频缩略图URL。

* `name`：视频名称。

* `duration`：视频总时长。单位：秒。


<span id="67c44fd2"></span>
### **lockPlayBackVods()** 

锁定回放合集列表中的指定视频。此方法通常与[unlockPlayBackVods()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#cddd4919)方法配合使用，用于限制付费或VIP专属视频访问。

```Plain
(vids: string[]) => void
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|`vids` |`string[]` |是 |无 |要锁定的视频 ID 数组。被锁定的视频无法播放。 |


<span id="cddd4919"></span>
### **unlockPlayBackVods()** 

解锁已锁定的回放视频。此方法通常与[lockPlayBackVods()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#67c44fd2)方法配合使用，用于限制付费或VIP专属视频访问。

```Plain
(vids: string[]) => void
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|`vids` |`string[]` |是 |无 |要解锁的视频 ID 数组。 |


<span id="ada4c709"></span>
### getProductList()

获取观看页展示的商品列表。

```TypeScript
() => Promise<ProductInfo[]>
```


**返回值**

`ProductInfo[]`

产品对象数组。更多信息，请参见[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-web-zh-CN#fe534689)。

<span id="bd140bf3"></span>
### updateProductInfo()

更新一个或多个产品的信息。

```TypeScript
(props: Partial<ProductInfo>[]) => Promise<void>
```


**参数**


|名称 |数据类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|`props` |`Partial<ProductInfo>[]` |是 |无 |产品信息对象数组。为识别需要更新的产品，每个对象必须包含产品的 `Id`。仅会更新每个对象中提供的字段，未指定的字段保持不变。更多信息请参见 `ProductInfo`。 |
