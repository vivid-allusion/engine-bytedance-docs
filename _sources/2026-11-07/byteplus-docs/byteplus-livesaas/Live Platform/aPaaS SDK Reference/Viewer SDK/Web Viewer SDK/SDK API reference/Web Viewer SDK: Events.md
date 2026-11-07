---
title: "Web Viewer SDK: Events"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/events"
---

<span id="8dc10ebf"></span>
## SDKEventsOn

Type: `interface`

<span id="9c9808ec"></span>
### player.play

Triggered when the player plays a video.

```TypeScript
() => void
```


<span id="d5f99339"></span>
### player.playing

Triggered when the player resumes playing a video after the video is paused or freezes.

```TypeScript
() => void
```


<span id="88ceb878"></span>
### player.pause

Triggered when a video is paused.

```TypeScript
() => void
```


<span id="5a73f0eb"></span>
### player.ended

Triggered when a video ends.

```TypeScript
() => void
```


<span id="5a2cf424"></span>
### player.destroy

Triggered when the player is destroyed.

```TypeScript
() => void
```


<span id="23e7aee8"></span>
### player.ratechange

Triggered when the playback speed changes.

```TypeScript
(rate: number) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|rate |Number |The playback speed.<br><br>Valid values:<br><br><br>* `0.5`: Half speed.<br><br>* `0.75`: 0.75 times speed.<br><br>* `1`: Normal speed.<br><br>* `1.25`: 1.25 times speed.<br><br>* `1.5`: 1.5 times speed.<br><br>* `2`: Double speed. |


<span id="b703ce9a"></span>
### player.fullscreen_change

Triggered when the full\-screen mode changes.

```TypeScript
(isFullScreen: boolean) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|isFullScreen |Boolean |Indicates whether the viewer enters or exits the full screen.<br><br><br>* `true`: Enters the full screen.<br><br>* `false`: Exits the full screen. |


<span id="6c44f68d"></span>
### player.pip_change

Triggered when the small\-window mode changes on PCs.

```TypeScript
(isPip: boolean) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|isPip |Boolean |Indicates whether the viewer switches to or from small\-window mode on PCs.<br><br>Valid values:<br><br><br>* `true`: Switches to small\-window mode.<br><br>* `false`: Switches to the original screen from small\-window mode. |


<span id="33a46182"></span>
### player.waiting

Triggered when the player waits for data to be loaded.

```TypeScript
() => void
```


<span id="0cb32046"></span>
### player.status

Triggered when the live room status changes.

```TypeScript
(status: string) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|status |String |The live room status.<br><br>Valid values:<br><br><br>* Live<br><br>* Preview<br><br>* Playback<br><br>* Over |


<span id="a87308eb"></span>
### player.vodConfigChange

The preview and playback breakpoint event for resumption.

When the player is playing a preview or playback, the event is triggered under the following conditions:


* Viewers close the viewing page on PCs.

* The `pagehide` event of WebView is triggered or viewers manually drag the progress bar on mobile devices.


```TypeScript
(VodInfo: { vid: string; currentTime: number; duration: number;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|VodInfo |\- |The video (preview or playback) information. |
|vid |String |The video ID, which is the unique identifier of the video. |
|currentTime |Number |The current playback time point. Unit: seconds. |
|duration |Number |The total length of the video. Unit: seconds. |


<span id="64d88d3e"></span>
### comment.focus

Triggered when the comment text box under the menu for chat interaction is clicked or tapped.

```TypeScript
() => void
```


<span id="1ee55848"></span>
### comment.send

Triggered when a comment is sent.

```TypeScript
(msg: string) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|msg |String |The sent comment. |


<span id="6e1a3846"></span>
### comment.nickNameClick

Triggered when a nickname is clicked or tapped in the chat area.

```TypeScript
(data: { Nickname: string; ExternalId: string; isTop: boolean; isPresenter: boolean;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|data |\- |Information of the user whose nickname is clicked or tapped. |
|Nickname |String |The user's nickname. |
|ExternalId |String |The external user ID. |
|isTop |Boolean |Indicates whether the comment is pinned to the top of the chat area.<br><br><br>* `true`: Pinned to the top.<br><br>* `false`: Not pinned to the top. |
|isPresenter |Boolean |Indicates whether the user is the host.<br><br><br>* `true`: The host.<br><br>* `false`: Not the host. |


<span id="c91cc8cb"></span>
### permission.need

You can use this event to determine whether the login process of your own account system needs to be triggered.

If the value of `mode` is `1` and the value of `disabledLogin` is `true`, the event is triggered in scenarios where user information is required, for example, when a viewer clicks the comment text box or likes a comment.

After the event is triggered, you need to trigger the login process of your own account system and update the token obtained when the value of `mode` is `1` to that obtained when the value of `mode` is `2` by using the `updateMode2Token` method.

```TypeScript
() => void
```


<span id="a92d7f8b"></span>
### lines.number

Triggered when the number of lines changes.

```TypeScript
(lines: number) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|lines |Number |* The number of live sources when the live room status is **Live**.<br><br>* The number of playbacks when the live room status is **Playback**. |


<span id="59ec7864"></span>
### activity.status

Triggered when the live room status changes.

```TypeScript
(status: 1 | 2 | 3 | 4) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|status |1 \| 2 \| 3 \| 4 |The live room status.<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |


<span id="44166c70"></span>
### reservation.click

Triggered when the **Book now** button is clicked or tapped.

```TypeScript
() => void
```


<span id="799a1022"></span>
### reservation.attend

Triggered when the live stream is booked.

```TypeScript
(tel: string) => void
```


**Parameter**


|Name |Data Type |Description |
|---|---|---|
|tel |String |The phone number for booking. |


<span id="2011f69b"></span>
### card.click

Triggered when a product card under the menu for product cards is clicked or tapped.

You can set the value of `disableCardRedirect` to `true` and listen for this event to implement the redirection feature by yourself.

```TypeScript
(card: { text: string; url: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|card |\- |The product card information. |
|text |String |The product name. |
|url |String |The product URL.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |


<span id="7f70dfa5"></span>
### card.configChange

Triggered when a product card's information changes.

```TypeScript
(productInfo: ProductInfo) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|productInfo |[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#fe534689)[] |The updated product card information. |


<span id="9c17df67"></span>
### popularity.configChange

Triggered when the number of viewers shown on the viewing page changes.

```TypeScript
(data: {Popularity?:number, PeopleCountEnable?:boolean}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|data |\- |The popularity information. |
|Popularity |Number |The number of viewers shown on the viewing page. |
|PeopleCountEnable |Boolean |Whether the **Popularity display** feature is enabled. Valid values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. |


<span id="163fd7d0"></span>
### floatingCard.update

Triggered when a floating product card is updated.

```TypeScript
(productInfo: ProductInfo) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|productInfo |[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#fe534689)[] |The updated product card information. |


<span id="d6026ee7"></span>
### floatingCard.click

Triggered when a floating product card is clicked or tapped.

You can set the value of `disableCardRedirect` to `true` and listen for this event to implement the redirection feature by yourself.

```TypeScript
(card: { text: string; url: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|card |\- |The product card information. |
|text |String |The product name. |
|url |String |The product URL.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |


<span id="9bff3721"></span>
### lottery.click

Triggered when the lucky draw icon is clicked or tapped.

```TypeScript
(award: { awardId: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|awardId |String |The lucky draw ID |


<span id="09d83b77"></span>
### lottery.attend

Triggered when a viewer participates in a lucky draw.

```TypeScript
(award: { awardId: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|awardId |String |The lucky draw ID |


<span id="4175a516"></span>
### lottery.result

Triggered when winners are selected. The event is triggered only if the viewer is in the live room when winners are selected.

```TypeScript
(award: { awardId: string; ifWin: boolean;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|awardId |String |The lucky draw ID |
|ifWin |Boolean |Indicates whether the viewer wins the prize.<br><br><br>* `true`: Wins the prize.<br><br>* `false`: Does not win the prize. |


<span id="95464d32"></span>
### lottery.winInfo

Triggered when a viewer submits the personal information after winning a prize.

```TypeScript
(award: { awardId: string; awardTel: string; awardAddress?: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|awardId |String |The lucky draw ID |
|awardTel |String |The phone number entered by the viewer.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |
|awardAddress |String |The shipping address entered by the viewer.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |


<span id="e290813e"></span>
### lotteryTicket.click

Triggered when the prize claim link of voucher prizes is clicked or tapped.

```TypeScript
(award: { url: string; ActivityId: string; TaskAwardId: string; TaskAwardItemId: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|url |String |The prize claim link. |
|ActivityId |String |The activity ID of the live room. |
|TaskAwardId |String |The lucky draw configuration ID. |
|TaskAwardItemId |String |The prize ID for a watch time\-based lucky draw. |


<span id="5e56de30"></span>
### taskAwardPanel.pop

Triggered when the dialog box of a watch time\-based lucky draw is displayed.

```TypeScript
(award: { config: TaskAwardConfig | null; viewedTime: number; isLogin: boolean; winningRecordMap: Map<string, IRecordInfo>;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|config |TaskAwardConfig \| null |The configurations of the watch time\-based lucky draw activity.<br><br><br>* `TaskAwardId: string`: The activity ID.<br><br>* `TaskAwardRule: TaskAwardRuleItem[]`: Lucky draw rules, including `index: number` (sequence number of the prize, with 0 being the first prize, 1 being the second prize, and so on), `TaskAwardItemId: string` (ID of the prize), and `WatchTime: number` (requirement on the total watch time. Unit: minutes).<br><br>* `TaskAwardStartTime: number`: The time when the lucky draw activity starts in Unix timestamp format. Unit: seconds.<br><br>* `TaskAwardEndTime: number`: The time when the lucky draw activity ends in Unix timestamp format. Unit: seconds.<br><br>* `TaskAwardStatus`: The activity status.<br><br>   * `NULL(-1)`: No lucky draw. Reserved for future use.<br><br>   * `INIT(0)`: Initialization. The activity has not started.<br><br>   * `START(1)`: The activity is in progress.<br><br>   * `END(2)`: The activity is over.<br><br>   * `CLOSE(3)`: The activity is closed. |
|viewedTime |Number |The total watch time accumulated by the viewer. Unit: seconds. |
|isLogin |Boolean |Indicates whether the viewer has logged in to the live room.<br><br><br>* `true`: Logged in.<br><br>* `false`: Not logged in. |
|winningRecordMap |Map<string, IRecordInfo\> |The winning record of the viewer. |


<span id="1ba87761"></span>
### taskAwardBox.click

Triggered when the winning result of a watch time\-based lucky draw is clicked or tapped.

```TypeScript
(award: { index: number; WatchTime: number;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|index |Number |The sequence number of the treasure box, which starts from 0. |
|WatchTime |Number |The total watch time accumulated by the viewer. Unit: minutes. |


<span id="0062c289"></span>
### share.click

Triggered when **Share** is clicked on PCs or **Copy link** or **Save QR code** is tapped on mobile devices.

```TypeScript
() => void
```


<span id="b649c7cc"></span>
### poster.click

Triggered when the invitation poster is clicked or tapped.

```TypeScript
() => void
```


<span id="d05864eb"></span>
### adFloating.click

Triggered when a floating ad is clicked or tapped. The event is triggered only when an embedded link is configured for the ad.

You can set the value of `disableAdFloatingRedirect` to `true` and listen for this event to implement the redirection feature by yourself.

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|ad |\- |The ad information. |
|AdvertisementRedirectUrl |String |The embedded link. |


<span id="c1ff1133"></span>
### adMiddle.click

Triggered when an in\-page ad is clicked or tapped. The event is triggered only when an embedded link is configured for the ad.

You can set the value of `disableAdMiddleRedirect` to `true` and listen for this event to implement the redirection feature by yourself.

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|ad |\- |The ad information. |
|AdvertisementRedirectUrl |String |The embedded link. |


<span id="3d0f7998"></span>
### adAccount.click

Triggered when a host account is clicked or tapped. The event is triggered only when an embedded link is configured for the host account.

You can set the value of `disableAdAccountRedirect` to `true` and listen for this event to implement the redirection feature by yourself.

```TypeScript
(account: { AccountHeadRedirectUrl: string;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|account |\- |The host account information. |
|AccountHeadRedirectUrl |String |The embedded link. |


<span id="1fc6e72e"></span>
### ready

Triggered when the initialization of the Web Viewer SDK is complete. The event being triggered does not mean the player has started playing the video.

```TypeScript
() => void
```


<span id="93a24cfc"></span>
### menu.click

Triggered when a menu is clicked or tapped.

```TypeScript
(tab: { terminal: 'pc' | 'mobile'; layout?: 'portrait'; tab: number;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|tab |\- |Information about the menu. |
|terminal |"pc" \| "mobile" |The terminal type of the viewer.<br><br><br>* `"pc"`: PCs.<br><br>* `"mobile"`: Mobile devices. |
|layout |"portrait" \| undefined |If the parameter value is `"portrait"`, it indicates the viewer clicked or tapped the menu in a live room of portrait mode on mobile devices. |
|tab |Number |The menu type.<br><br><br>* `3`: The menu for chat interaction.<br><br>* `31`: The menu for top comments.<br><br>* `5`: The menu for aggregated live streams.<br><br>* `2`: The menu for product cards.<br><br>* `1`: The menu for graphics.<br><br>* `4`: The menu for interaction tools.<br><br>* `6`: The menu for Q&A.<br><br>* `7`: The menu for embedded link. |


<span id="750ccd04"></span>
### thumbs.click

Triggered when the live room is liked.

```TypeScript
(thumb: { count: number;}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|thumb |\- |The like information. |
|count |Number |The number of likes. |


<span id="96c0ddb3"></span>
### lines.current

Triggered under the following conditions:


* A viewer clicks or taps a live source when the live room status is **Live**.

* A viewer clicks or taps a playback video when the live room status is **Playback**.


Generally, the event is used with the `switchChannel` API.

```TypeScript
(lines: number) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|lines |Number |A zero\-based index value, indicating the sequence of the clicked or tapped live source or playback video in the live room. |


<span id="75c92017"></span>
### activity.pcu

Triggered when a viewer enters the viewing page. This event is used to check whether the total peak concurrent users (PCU) of all your live rooms with the status of **Live** under your account exceeds the concurrency upper limit after you subscribe to the live concurrent viewers package. For more information, see [Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#db59dce3).

```TypeScript
(value: {isPCUFull: boolean}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|value |\- |The PCU information. |
|isPCUFull |Boolean |Whether the total PCU of all your live rooms with the status of **Live** under your account exceeds the concurrency upper limit. Valid values:<br><br><br>* `true`: Exceeds the limit.<br><br>* `false`: Does not exceed the limit. |


<span id="7bd143bd"></span>
### shopCart.click

Triggered when the shopping cart icon on the viewing page of mobile devices is tapped.

Set the value of `disabledShopCartClick` to `true`, and then listen to this event to implement your own logic. For more information about `disabledShopCartClick`, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).

```TypeScript
() => void
```


<span id="d476ef36"></span>
### gift.click

Triggered when a gift is clicked or tapped by a viewer, regardless of the `disableSendGift` setting.

```TypeScript
(value:{data:{"GiftId": number; "GiftName": string; "GiftImage": string; "GiftPrice": string; "Index": number}}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|data |\- |Gift information. |
|GiftId |Number |ID of the gift, which is unique for each kind of gift. |
|GiftName |String |Name of the gift. |
|GiftImage |String |URL of the gift image. |
|GiftPrice |String |Unit price of the gift. |
|Index |Number |Index of the gift, indicating the gift position on the viewing page. |


<span id="83e8b67c"></span>
### gift.sendError

Triggered when an error occurs due to insufficient points or a request exception while viewers send gifts, regardless of the `disableSendGift` setting.

Set the value of `disableSendGift` to `true`, and then listen to this event to implement your own logic, such as displaying a page asking viewers to top up points when an insufficient points error occurs. For more information about `disableSendGift`, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).

```TypeScript
(value:{data:string|number}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|data |string |number |


<span id="e862732b"></span>
### gift.show

Triggered when viewers send gifts, regardless of the `disableSendGift` setting.

Set the value of `disableSendGift` to `true`, and then listen to this event to implement your own logic, such as customizing the gift effect. For more information about `disableSendGift`, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).

```TypeScript
(value: {data: GiftInfo[]}) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|data |[GiftInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#e7c20786)[] |Information about the sent gift and the user who sent the gift. |


<span id="4fa82edf"></span>
### giftPoint.result

Triggered when:


* The gift point is updated after viewers send gifts

* `webSDK.emit('gift.pointQuery')` is called after viewers actively query the gift point


```TypeScript
(value: { point: number }) => void
```


**Parameters**


|Name |Data Type |Description |
|---|---|---|
|point |number |The current gift point of the viewer. |


**Usage example**

```TypeScript
// Step 1. Actively query the gift point
webSDK.emit('gift.pointQuery');

// Step 2. Listen for the result
webSDK.on('giftPoint.result', point => {
  console.log('Current gift point:', point);
  // You can update UI or trigger custom logic here
});
```


<span id="d83da9df"></span>
## SDKEventsEmit

Type: `enum`


|Property |Value |Description |
|---|---|---|
|play |`'player.play'` |Plays a video. |
|pause |`'player.pause'` |Pauses a video. |
|pip |`'player.pip'` |Switches to or from small\-window mode on PCs.<br><br><br>* `true`: Switches to small\-window mode.<br><br>* `false`: Switches to the original screen from small\-window mode.<br><br><br>Sample code:<br><br>```JavaScript```<br>```webSDK.emit('player.pip', {```<br>```    ifShow: true,```<br>```})```<br> |
|comment.send |`'comment.send'` |Sends a comment.<br><br>Sample code:<br><br>```JavaScript```<br>```webSDK.emit('comment.send', 'BytePlus Live');```<br> |
|comment.disabled |`'comment.disabled'` |Disables or enables the comment text box.<br><br><br>* Disable: `webSDK.emit('comment.disabled', true)`<br><br>* Enable: `webSDK.emit('comment.disabled', false)`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This event can only be emitted after setting whether to disable the comment text box and the placeholder text for the disabled comment text box using the <code>disabledCommentConfig</code> parameter. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/parameters#b6fb0c34">Options</a>.</div><br> |
|gift.send |`'gift.send'` |Sends a specific number of gifts after the [gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#d476ef36) event is triggered. The default value of `count` is `1`. You can customize the value of `count` as needed.<br><br>We recommend that the value of `disableSendGift` is set to `true` to disable the gift sending logic related to UI.<br><br>Sample code:<br><br>```JavaScript```<br>```webSDK.emit('gift.send', {```<br>```    ...value.data,```<br>```    count:10 // The number of gifts to send.```<br>```  });```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about <code>disableSendGift</code>, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/parameters">Parameters</a>.</div><br> |
|gift.pointQuery |`'gift.pointQuery'` |Querys the gift point of the viewer. |
|playbackListBtn.click |`'playbackListBtn.click'` |Clicks the playback collection button. |
