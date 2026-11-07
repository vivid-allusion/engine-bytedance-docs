---
title: "Events"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/iframe-events"
---

You can perform your own subsequent actions after detecting a specific event.

The sample code is as follows.

```JavaScript
 window.addEventListener('message', (event) => {
        try {
          if (event.origin.includes('byteoc.com')) {
              const data = JSON.parse(event.data);
              switch (data.action) {
                case 'player.play': // Replace player.play with a specific event.
                  // Perform your own subsequent actions after detecting the event.
                  console.log('====== ', data.action, ' -- ', data.payload, ' ======' );
                  break
                default:
                  return;
              }
          }
        } catch (e) {
        }
      });
```


<span id="5310bb0f"></span>
## Player\-related events

<span id="5de6ff14"></span>
### player.play

Triggered when the player plays a video.

**Type**

```TypeScript
() => void
```


<span id="c5ccd8c0"></span>
### player.playing

Triggered when the player resumes playing a video after the video is paused or freezes.

**Type**

```TypeScript
() => void
```


<span id="ae7c6a17"></span>
### player.pause

Triggered when a video is paused.

**Type**

```TypeScript
() => void
```


<span id="f5570586"></span>
### player.ended

Triggered when a video ends.

**Type**

```TypeScript
() => void
```


<span id="1df2cbfd"></span>
### player.destroy

Triggered when the player is destroyed.

**Type**

```TypeScript
() => void
```


<span id="97923f78"></span>
### player.ratechange

Triggered when the playback speed changes.

**Type**

```TypeScript
(rate: number) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|rate |number |The playback speed. Valid values:<br><br><br>* `0.5`: Half speed.<br><br>* `0.75`: 0.75 times speed.<br><br>* `1`: Normal speed.<br><br>* `1.25`: 1.25 times speed.<br><br>* `1.5`: 1.5 times speed.<br><br>* `2`: Double speed. |


<span id="787bc751"></span>
### player.fullscreen_change

Triggered when the full\-screen mode changes.

**Type**

```TypeScript
(isFullScreen: boolean) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|isFullScreen |boolean |Indicates whether the viewer enters or exits full\-screen mode. Valid values:<br><br><br>* `true`: Enters full\-screen mode.<br><br>* `false`: Exits full\-screen mode. |


<span id="a3ea9ff6"></span>
### player.pip_change

Triggered when the small\-window mode changes on PCs.

**Type**

```TypeScript
(isPip: boolean) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|isPip |boolean |Indicates whether the viewer switches to or from small\-window mode on PCs. Valid values:<br><br><br>* `true`: Switches to small\-window mode.<br><br>* `false`: Switches to the original screen from small\-window mode. |


<span id="9c528f98"></span>
### player.waiting

Triggered when the player waits for data to be loaded.

**Type**

```TypeScript
() => void
```


<span id="5a4cade5"></span>
### player.status

Triggered when the live room status changes.

**Type**

```TypeScript
(status: string) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|status |string |The live room status. Valid values:<br><br><br>* `Live`.<br><br>* `Preview`.<br><br>* `Playback`.<br><br>* `Over`. |


<span id="97b9fa47"></span>
### player.vodConfigChange

The preview and playback breakpoint event for resumption.

When the player is playing a preview or playback, the event is triggered under the following conditions:


* Viewers close the embedded page on PCs.

* The `pagehide` event of WebView is triggered or viewers manually drag the progress bar on mobile devices.


**Type**

```TypeScript
(VodInfo: { vid: string; currentTime: number; duration: number;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|VodInfo |\- |The video (preview or playback) information. |
|vid |string |The video ID, which is the unique identifier of the video. |
|currentTime |number |The current playback time point. Unit: seconds. |
|duration |number |The total length of the video. Unit: seconds. |


<span id="bf8927b0"></span>
### lines.number

Triggered when the number of lines changes.

**Type**

```TypeScript
(lines: number) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|lines |number |The number of live sources when the live room status is **Live**.<br><br>The number of playbacks when the live room status is **Playback**. |


<span id="14eddf0f"></span>
## Non\-player\-related events

<span id="26367ebd"></span>
### activity.status

Triggered when the live room status changes.

**Type**

```TypeScript
(status: 1 | 2 | 3 | 4) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|status |1 \| 2 \| 3 \| 4 |The live room status. Valid values:<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |


<span id="bc6080db"></span>
### comment.focus

Triggered when the comment text box under the menu for chat interaction is clicked or tapped.

**Type**

```TypeScript
() => void
```


<span id="abae6f89"></span>
### comment.send

Triggered when a comment is sent.

**Type**

```TypeScript
(msg: string) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|msg |string |The sent comment. |


<span id="2607d498"></span>
### comment.nickNameClick

Triggered when a nickname is clicked or tapped in the chat area.

**Type**

```TypeScript
(data: { Nickname: string; ExternalId: string; isTop: boolean; isPresenter: boolean;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|data |\- |Information of the user whose nickname is clicked or tapped. |
|Nickname |string |The user's nickname. |
|ExternalId |string |The external user ID. |
|isTop |boolean |Indicates whether the comment is pinned to the top of the chat area. Valid values:<br><br><br>* `true`: Pinned to the top.<br><br>* `false`: Not pinned to the top. |
|isPresenter |boolean |Indicates whether the user is the host. Valid values:<br><br><br>* `true`: The host.<br><br>* `false`: Not the host. |


<span id="e5744da6"></span>
### reservation.click

Triggered when the **Book now** button is clicked or tapped.

**Type**

```TypeScript
() => void
```


<span id="a3268a56"></span>
### reservation.attend

Triggered when the live stream is booked.

**Type**

```TypeScript
(tel: string) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|tel |string |The phone number for booking. |


<span id="23b68bf7"></span>
### card.click

Triggered when a product card under the menu for product cards is clicked or tapped.

You can set the value of `disableCardRedirect` to `true` and listen to this event to implement the redirection feature of product cards yourself.

**Type**

```TypeScript
(card: { text: string; url: string; UAInfos: UAInfo[]; DirectUrls: string[];}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|card |\- |The configurations of the menu for product cards. |
|text |string |The product name of the product card. |
|url |string |The product URL of the product card.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |
|UAInfos |[UAInfo](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#fa52e27e)[] |The environment information configured for the menu for product cards.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |
|DirectUrls |string[] |The direct URL of the product card.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |


<span id="f777e233"></span>
### floatingCard.click

Triggered when a floating product card is clicked or tapped.

You can set the value of `disableCardRedirect` to `true` and listen to this event to implement the redirection feature of product cards yourself.

**Type**

```TypeScript
(card: { text: string; url: string; UAInfos: UAInfo[]; DirectUrls: string[];}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|card |\- |The configurations of the menu for product cards. |
|text |string |The product name of the product card. |
|url |string |The product URL of the product card.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |
|UAInfos |[UAInfo](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#fa52e27e)[] |The environment information configured for the menu for product cards.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |
|DirectUrls |string[] |The direct URL of the product card.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |


<span id="72a80fd4"></span>
### lottery.click

Triggered when the lucky draw entry is clicked or tapped.

**Type**

```TypeScript
(award: { awardId: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|awardId |string |The lucky draw ID. |


<span id="75bc74f3"></span>
### lottery.attend

Triggered when a viewer participates in a lucky draw.

**Type**

```TypeScript
(award: { awardId: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|awardId |string |The lucky draw ID. |


<span id="a655c11e"></span>
### lottery.result

Triggered when lucky draw winners are selected. The event is triggered only if the viewer is in the live room when winners are selected.

**Type**

```TypeScript
(award: { awardId: string; ifWin: boolean;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The lucky draw results. |
|awardId |string |The lucky draw ID. |
|ifWin |boolean |Indicates whether the viewer wins the prize. Valid values:<br><br><br>* `true`: Wins the prize.<br><br>* `false`: Does not win the prize. |


<span id="600cb3bb"></span>
### lottery.winInfo

Triggered when a viewer submits the personal information after winning a prize.

**Type**

```TypeScript
(award: { awardId: string; awardTel: string; awardAddress?: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The personal information submitted after winning a prize. |
|awardId |string |The lucky draw ID. |
|awardTel |string |The phone number entered by the viewer.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |
|awardAddress |string \| undefined |The shipping address entered by the viewer.<br><br>Whether the parameter has a value depends on the configurations set in the console or by calling a server\-side API (if supported). |


<span id="2515d473"></span>
### lotteryTicket.click

Triggered when the prize claim link of a voucher prize is clicked or tapped.

You can set the value of `disableLotteryTicketRedirect` to `true` and listen to this event to implement the redirection feature of prize claim links yourself.

**Type**

```TypeScript
(award: { url: string; ActivityId: string; TaskAwardId: string; TaskAwardItemId: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The voucher prize information. |
|url |string |The prize claim link. |
|ActivityId |string |The activity ID of the live room. |
|TaskAwardId |string |The lucky draw configuration ID. |
|TaskAwardItemId |string |The prize ID for a watch time\-based lucky draw. |


<span id="fbefd1f5"></span>
### taskAwardPanel.pop

Triggered when the dialog box of a watch time\-based lucky draw is displayed.

**Type**

```TypeScript
(award: { config: TaskAwardConfig | null; viewedTime: number; isLogin: boolean; winningRecordMap: Map<string, IRecordInfo>;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|config |[TaskAwardConfig](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#0c0d8d3f) \| null |The configurations for this watch time\-based lucky draw activity. |
|viewedTime |number |The total watch time accumulated by the viewer. Unit: seconds. |
|isLogin |boolean |Indicates whether the viewer has logged in to the live room. Valid values:<br><br><br>* `true`: Logged in.<br><br>* `false`: Not logged in. |
|winningRecordMap |Map<string, [IRecordInfo](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#5a950de5)\> |The winning records of the current viewer. |


<span id="3da23797"></span>
### taskAwardBox.click

Triggered when the winning result of a watch time\-based lucky draw is clicked or tapped.

**Type**

```TypeScript
(award: { index: number; WatchTime: number;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|award |\- |The lucky draw information. |
|index |number |The sequence number of the treasure box, which starts from `0`. |
|WatchTime |number |The total watch time accumulated by the viewer. Unit: minutes. |


<span id="9e5a6efa"></span>
### share.click

Triggered when **Share** is clicked on PCs or **Copy link** or **QR code** is tapped on mobile devices.

**Type**

```TypeScript
() => void
```


<span id="134982cf"></span>
### poster.click

Triggered when the invitation poster is clicked or tapped.

**Type**

```TypeScript
() => void
```


<span id="4a058ac8"></span>
### adFloating.click

Triggered when a floating ad is clicked or tapped. The event is triggered only when a URL is configured in the console or by calling a server\-side API (if supported).

You can set the value of `disableAdFloatingRedirect` to `true` and listen to this event to implement the redirection feature of floating ads yourself.

**Type**

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|ad |\- |The floating ad information. |
|AdvertisementRedirectUrl |string |The embedded link of the floating ad. |


<span id="e0aa9f45"></span>
### adMiddle.click

Triggered when an in\-page ad is clicked or tapped. The event is triggered only when a URL is configured in the console or by calling a server\-side API (if supported).

You can set the value of `disableAdMiddleRedirect` to `true` and listen to this event to implement the redirection feature of in\-page ads yourself.

**Type**

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|ad |\- |The in\-page ad information. |
|AdvertisementRedirectUrl |string |The embedded link of the in\-page ad. |


<span id="2d145963"></span>
### adAccount.click

Triggered when a host account is clicked or tapped. The event is triggered only when a URL is configured in the console or by calling a server\-side API (if supported).

You can set the value of `disableAdAccountRedirect` to `true` and listen to this event to implement the redirection feature of host accounts yourself.

**Type**

```TypeScript
(account: { AccountHeadRedirectUrl: string;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|account |\- |The host account information. |
|AccountHeadRedirectUrl |string |The embedded link of the host account. |


<span id="c57787dc"></span>
### menu.click

Triggered when a menu bar is clicked or tapped.

**Type**

```TypeScript
(tab: { terminal: 'pc' | 'mobile'; layout?: 'portrait'; tab: number;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|tab |\- |The menu bar information. |
|terminal |"pc" \| "mobile" |The terminal type of the viewer. Valid values:<br><br><br>* `"pc"`: PCs.<br><br>* `"mobile"`: Mobile devices. |
|layout |"portrait" \| undefined |The parameter value is fixed to `"portrait"`, meaning the viewer clicked or tapped the menu bar in a live room of portrait mode on mobile devices. |
|tab |number |The menu type. Valid values:<br><br><br>* `3`: The menu for chat interaction.<br><br>* `31`: The menu for top comments.<br><br>* `5`: The menu for aggregated live streams.<br><br>* `2`: The menu for product cards.<br><br>* `1`: The menu for graphics.<br><br>* `4`: The menu for interaction tools.<br><br>* `6`: The menu for Q&A.<br><br>* `7`: The menu for embedded link. |


<span id="ec5cb488"></span>
### thumbs.click

Triggered when the live room is liked.

**Type**

```TypeScript
(thumb: { count: number;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|thumb |\- |The like information. |
|count |number |The number of likes. |


<span id="9de15ba7"></span>
### feature.click

Triggered when the interactive feature button is clicked or tapped.

**Type**

```TypeScript
(feature: { feature: string; status: boolean;}) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|feature |\- |The interactive feature information. |
|feature |string |The interactive features. Valid values:<br><br><br>* `Comment`: Comments.<br><br>* `Gift`: Gift rewards.<br><br>* `Lottery`: Real\-time lucky draws.<br><br>* `Thumb`: Liking comments.<br><br>* `Reservation`: Booking live streams.<br><br>* `Question`: Q&A.<br><br>* `CheckIn`: Check\-ins.<br><br>* `Vote`: Votes.<br><br>* `Questionnaire`: Questionnaires.<br><br>* `TaskAward`: Watch time\-based lucky draws. |
|status |boolean |Whether to prevent the subsequent execution of the interactive feature. Valid values:<br><br><br>* `true`: Prevents the subsequent execution.<br><br>* `false`: Does not prevent the subsequent execution. |


<span id="20f7305c"></span>
### customInteractionIcons.click

Triggered when the custom floating interaction tool is clicked or tapped.

**Type**

```TypeScript
(key: string) => void
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|key |string |The unique identifier of the floating interaction tool. |
