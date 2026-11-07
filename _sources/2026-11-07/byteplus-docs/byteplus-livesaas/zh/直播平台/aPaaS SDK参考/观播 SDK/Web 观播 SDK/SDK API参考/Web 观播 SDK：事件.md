---
title: "Web 观播 SDK：事件"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN"
---

<span id="8dc10ebf"></span>
## SDKEventsOn

类型：`interface`

<span id="9c9808ec"></span>
### player.play

当播放器开始播放视频时触发。

```TypeScript
() => void
```


<span id="d5f99339"></span>
### player.playing

当播放器在暂停或缓冲后恢复播放时触发。

```TypeScript
() => void
```


<span id="88ceb878"></span>
### player.pause

当视频被暂停时触发。

```TypeScript
() => void
```


<span id="5a73f0eb"></span>
### player.ended

当视频播放结束时触发。

```TypeScript
() => void
```


<span id="5a2cf424"></span>
### player.destroy

当播放器被销毁时触发。

```TypeScript
() => void
```


<span id="23e7aee8"></span>
### player.ratechange

当播放速度发生变化时触发。

```TypeScript
(rate: number) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|rate |Number |回放速度。<br><br>有效值：<br><br><br>* `0.5`：半速。<br><br>* `0.75`：0.75倍速。<br><br>* `1`：正常速度。<br><br>* `1.25`：1.25倍速。<br><br>* `1.5`：1.5倍速。<br><br>* `2`：双倍速。 |


<span id="b703ce9a"></span>
### player.fullscreen_change

当全屏模式发生变化时触发。

```TypeScript
(isFullScreen: boolean) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|isFullScreen |Boolean |表示播放器是否进入或退出全屏模式。<br><br><br>* `true`：进入全屏。<br><br>* `false`：退出全屏。 |


<span id="6c44f68d"></span>
### player.pip_change

当画中画（PiP）模式发生变化时触发。

```TypeScript
(isPip: boolean) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|isPip |Boolean |表示观众在PC端是否切换到或退出画中画模式。<br><br>有效值：<br><br><br>* `true`：进入画中画模式。<br><br>* `false`：退出画中画模式。 |


<span id="33a46182"></span>
### player.waiting

当播放器等待数据加载时触发。

```TypeScript
() => void
```


<span id="0cb32046"></span>
### player.status

当直播间状态发生变化时触发。

```TypeScript
(status: string) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|status |String |直播间状态。<br><br>有效值：<br><br><br>* Live<br><br>* 预告<br><br>* 回放<br><br>* Over |


<span id="a87308eb"></span>
### player.vodConfigChange

用于从断点恢复预告或回放的事件。

当播放器正在播放预告或回放时，在以下情况下会触发该事件：


* 观众在 PC 端关闭观看页。

* WebView 的 `pagehide` 事件被触发，或观众在移动端手动拖动进度条。


```TypeScript
(VodInfo: { vid: string; currentTime: number; duration: number;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|VodInfo |\- |视频（预告或回放）信息。 |
|vid |String |视频ID，即视频的唯一标识符。 |
|currentTime |Number |当前播放时间，单位为秒。 |
|duration |Number |视频总时长。单位：秒。 |


<span id="64d88d3e"></span>
### comment.focus

当点击或触摸聊天互动菜单下的评论输入框时触发。

```TypeScript
() => void
```


<span id="1ee55848"></span>
### comment.send

当发送评论时触发。

```TypeScript
(msg: string) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|msg |String |发送的评论。 |


<span id="6e1a3846"></span>
### comment.nickNameClick

当在聊天区域点击或触摸昵称时触发。

```TypeScript
(data: { Nickname: string; ExternalId: string; isTop: boolean; isPresenter: boolean;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|data |\- |被点击或触碰昵称的用户信息。 |
|Nickname |String |用户昵称。 |
|ExternalId |String |外部用户ID。 |
|isTop |Boolean |表示评论是否置顶于聊天区域。<br><br><br>* `true`：已置顶。<br><br>* `false`：未置顶。 |
|isPresenter |Boolean |表示用户是否为主播。<br><br><br>* `true`：主播。<br><br>* `false`：非主播。 |


<span id="c91cc8cb"></span>
### permission.need

可通过该事件判断是否需要触发自有账号系统的登录流程。

当`mode`的值为`1`且`disabledLogin`的值为`true`时，在需要用户信息的场景下会触发该事件，例如观众点击评论输入框或点赞评论时。

该事件触发后，必须发起自有账号系统的登录流程。然后，使用`updateMode2Token`方法将 token 从 mode 1 token 更新为 mode 2 token。

```TypeScript
() => void
```


<span id="a92d7f8b"></span>
### lines.number

当行数发生变化时触发。

```TypeScript
(lines: number) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|lines |Number |* 直播间状态为**Live**时的直播源数量。<br><br>* 直播间状态为**回放**时的回放数量。 |


<span id="59ec7864"></span>
### activity.status

当直播间状态发生变化时触发。

```TypeScript
(status: 1 | 2 | 3 | 4) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|status |1 |2<br><br><br>* `1`：Live。<br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：Over。 |


<span id="44166c70"></span>
### reservation.click

当点击或触摸**立即预约**按钮时触发。

```TypeScript
() => void
```


<span id="799a1022"></span>
### reservation.attend

当预约直播流时触发。

```TypeScript
(tel: string) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|tel |String |预约联系电话。 |


<span id="2011f69b"></span>
### card.click

当点击或触摸商品卡片时触发。

可将`disableCardRedirect`的值设置为`true`，并监听该事件以实现自定义跳转逻辑。

```TypeScript
(card: { text: string; url: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|card |\- |商品卡片信息。 |
|text |String |商品名称。 |
|url |String |商品URL。<br><br>该参数是否有值取决于控制台配置或调用服务端 API（如支持）。 |


<span id="7f70dfa5"></span>
### card.configChange

当商品卡片信息发生变化时触发。

```TypeScript
(productInfo: ProductInfo) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|productInfo |[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-web-zh-CN#fe534689)[] |已更新的商品卡片信息。 |


<span id="9c17df67"></span>
### popularity.configChange

当观看页展示的观众人数发生变化时触发。

```TypeScript
(data: {Popularity?:number, PeopleCountEnable?:boolean}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|data |\- |人气信息。 |
|Popularity |Number |在观看页展示的观众数量。 |
|PeopleCountEnable |Boolean |**人气展示**功能是否已开启。有效值：<br><br><br>* `true`：已开启。<br><br>* `false`：未开启。 |


<span id="163fd7d0"></span>
### floatingCard.update

当商品浮窗被更新时触发。

```TypeScript
(productInfo: ProductInfo) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|productInfo |[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-web-zh-CN#fe534689)[] |已更新的商品卡片信息。 |


<span id="d6026ee7"></span>
### floatingCard.click

当点击或触摸商品浮窗时触发。

可将`disableCardRedirect`的值设置为`true`，并监听该事件以自行实现跳转功能。

```TypeScript
(card: { text: string; url: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|card |\- |商品卡片信息。 |
|text |String |商品名称。 |
|url |String |商品URL。<br><br>该参数是否有值取决于控制台配置或调用服务端 API（如支持）。 |


<span id="9bff3721"></span>
### lottery.click

当点击或触摸抽奖图标时触发。

```TypeScript
(award: { awardId: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|awardId |String |抽奖 ID |


<span id="09d83b77"></span>
### lottery.attend

当观众参与抽奖时触发。

```TypeScript
(award: { awardId: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|awardId |String |抽奖 ID |


<span id="4175a516"></span>
### lottery.result

当抽奖结果产生时触发。仅当观众在直播间时抽奖结果产生才会触发该事件。

```TypeScript
(award: { awardId: string; ifWin: boolean;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|awardId |String |抽奖 ID |
|ifWin |Boolean |表示观众是否中奖。<br><br><br>* `true`: 中奖。<br><br>* `false`: 未中奖。 |


<span id="95464d32"></span>
### lottery.winInfo

当观众中奖后提交个人信息时触发。

```TypeScript
(award: { awardId: string; awardTel: string; awardAddress?: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|awardId |String |抽奖 ID |
|awardTel |String |观众填写的手机号。<br><br>该参数是否有值取决于控制台配置或调用服务端 API（如支持）。 |
|awardAddress |String |观众填写的收货地址。<br><br>该参数是否有值取决于控制台配置或调用服务端 API（如支持）。 |


<span id="e290813e"></span>
### lotteryTicket.click

当点击或触摸券类奖品的领奖链接时触发。

```TypeScript
(award: { url: string; ActivityId: string; TaskAwardId: string; TaskAwardItemId: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|url |String |领奖链接。 |
|ActivityId |String |直播间的活动 ID。 |
|TaskAwardId |String |抽奖配置 ID。 |
|TaskAwardItemId |String |基于观看时长抽奖的奖品 ID。 |


<span id="5e56de30"></span>
### taskAwardPanel.pop

当展示观看时长抽奖的对话框时触发。

```TypeScript
(award: { config: TaskAwardConfig | null; viewedTime: number; isLogin: boolean; winningRecordMap: Map<string, IRecordInfo>;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|config |TaskAwardConfig |null<br><br><br>* `TaskAwardId: string`: 活动 ID。<br><br>* `TaskAwardRule: TaskAwardRuleItem[]`: 抽奖规则，包括 `index: number`（奖品的序号，0 表示一等奖，1 表示二等奖，依此类推）、`TaskAwardItemId: string`（奖品 ID）、以及 `WatchTime: number`（总观看时长要求，单位：分钟）。<br><br>* `TaskAwardStartTime: number`: 抽奖活动开始时间（Unix 时间戳格式）。单位：秒。<br><br>* `TaskAwardEndTime: number`: 抽奖活动结束时间（Unix 时间戳格式）。单位：秒。<br><br>* `TaskAwardStatus`: 活动状态。<br><br>   * `NULL(-1)`: 无抽奖。预留，供后续使用。<br><br>   * `INIT(0)`: 初始化。活动尚未开始。<br><br>   * `START(1)`: 活动进行中。<br><br>   * `END(2)`: 活动已结束。<br><br>   * `CLOSE(3)`: 活动已关闭。 |
|viewedTime |Number |观众累计观看时长。单位：秒。 |
|isLogin |Boolean |表示观众是否已登录直播间。<br><br><br>* `true`: 已登录。<br><br>* `false`: 未登录。 |
|winningRecordMap |Map<string, IRecordInfo\> |观众的中奖记录。 |


<span id="1ba87761"></span>
### taskAwardBox.click

当点击或触摸观看时长抽奖的中奖结果时触发。

```TypeScript
(award: { index: number; WatchTime: number;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|award |\- |抽奖信息。 |
|index |Number |宝箱的序号，从 0 开始。 |
|WatchTime |Number |观众累计观看时长。单位：分钟。 |


<span id="0062c289"></span>
### share.click

在 PC 端点击**分享**，或在移动端点击**复制链接**或**保存二维码**时触发。

```TypeScript
() => void
```


<span id="b649c7cc"></span>
### poster.click

当点击或触摸邀请海报时触发。

```TypeScript
() => void
```


<span id="d05864eb"></span>
### adFloating.click

当点击或触摸浮标广告时触发。仅当广告配置了内嵌链接时才会触发该事件。

可以将`disableAdFloatingRedirect`的值设置为`true`，并监听该事件以自行实现跳转功能。

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|ad |\- |广告信息。 |
|AdvertisementRedirectUrl |String |内嵌链接。 |


<span id="c1ff1133"></span>
### adMiddle.click

当点击或触摸页中广告时触发。仅当广告配置了内嵌链接时才会触发该事件。

可以将`disableAdMiddleRedirect`的值设置为`true`，并监听该事件以自行实现跳转功能。

```TypeScript
(ad: { AdvertisementRedirectUrl: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|ad |\- |广告信息。 |
|AdvertisementRedirectUrl |String |内嵌链接。 |


<span id="3d0f7998"></span>
### adAccount.click

当点击或触摸主播账号时触发。仅当主播账号配置了内嵌链接时才会触发该事件。

可以将`disableAdAccountRedirect`的值设置为`true`，并监听该事件以自行实现跳转功能。

```TypeScript
(account: { AccountHeadRedirectUrl: string;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|account |\- |主播账号信息。 |
|AccountHeadRedirectUrl |String |内嵌链接。 |


<span id="1fc6e72e"></span>
### ready

当 Web 观播 SDK 初始化完成时触发。触发该事件并不代表视频播放已开始。

```TypeScript
() => void
```


<span id="93a24cfc"></span>
### menu.click

当点击或触摸菜单时触发。

```TypeScript
(tab: { terminal: 'pc' | 'mobile'; layout?: 'portrait'; tab: number;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|tab |\- |菜单信息。 |
|terminal |"pc" |"mobile"<br><br><br>* `"pc"`: 电脑。<br><br>* `"mobile"`: 移动设备。 |
|layout |"portrait" |undefined |
|tab |Number |菜单类型。<br><br><br>* `3`: 聊天互动菜单。<br><br>* `31`：精选评论菜单。<br><br>* `5`：聚合直播流菜单。<br><br>* `2`：商品卡片菜单。<br><br>* `1`：图形菜单。<br><br>* `4`：互动工具菜单。<br><br>* `6`：问答菜单。<br><br>* `7`：内嵌链接菜单。 |


<span id="750ccd04"></span>
### thumbs.click

当直播间被点赞时触发。

```TypeScript
(thumb: { count: number;}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|thumb |\- |点赞信息。 |
|count |Number |点赞数量。 |


<span id="96c0ddb3"></span>
### lines.current

在以下情况下触发：


* 当直播间状态为**直播**时，观众点击或触摸直播源。

* 当直播间状态为**回放**时，观众点击或触摸回放视频。


通常与`switchChannel` API 配合使用。

```TypeScript
(lines: number) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|lines |Number |被点击或触摸的直播源或回放视频的从零开始的索引。 |


<span id="75c92017"></span>
### activity.pcu

当观众进入观看页时触发。该事件用于在你订阅直播并发观众数套餐后，检查你账号下所有状态为**直播**的直播间总 PCU 是否超过并发上限。更多信息，请参见[Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-ios-zh-CN#db59dce3)。

```TypeScript
(value: {isPCUFull: boolean}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|value |\- |PCU 信息。 |
|isPCUFull |Boolean |你账号下所有状态为**Live**的直播间的总 PCU 是否超过并发上限。有效值：<br><br><br>* `true`：超出上限。<br><br>* `false`：未超出上限。 |


<span id="7bd143bd"></span>
### shopCart.click

当在移动端观看页点击购物车图标时触发。

将`disabledShopCartClick`的值设置为`true`，然后监听该事件以实现自定义逻辑。关于`disabledShopCartClick`的更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。

```TypeScript
() => void
```


<span id="d476ef36"></span>
### gift.click

无论`disableSendGift`设置如何，观众点击或触摸礼物时触发。

```TypeScript
(value:{data:{"GiftId": number; "GiftName": string; "GiftImage": string; "GiftPrice": string; "Index": number}}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|data |\- |礼物信息。 |
|GiftId |Number |该类型礼物的唯一 ID。 |
|GiftName |String |礼物名称。 |
|GiftImage |String |礼物图片的 URL。 |
|GiftPrice |String |礼物刊例价。 |
|Index |Number |礼物索引，表示礼物在观看页上的位置。 |


<span id="83e8b67c"></span>
### gift.sendError

无论`disableSendGift`设置如何，观众送礼物时因积分不足或请求异常导致错误时触发。

将`disableSendGift`的值设置为`true`，然后监听该事件以实现自定义逻辑，例如在积分不足时弹出提示观众充值积分的页面。关于`disableSendGift`的更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。

```TypeScript
(value:{data:string|number}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|data |string |number |


<span id="e862732b"></span>
### gift.show

无论`disableSendGift`设置如何，观众送礼物时触发。

将`disableSendGift`的值设置为`true`，然后监听该事件以实现自定义逻辑，例如自定义礼物效果。有关`disableSendGift`的更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。

```TypeScript
(value: {data: GiftInfo[]}) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|data |[GiftInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-web-zh-CN#e7c20786)[] |已发送礼物及发送用户的信息。 |


<span id="4fa82edf"></span>
### giftPoint.result

触发时机：


* 观众送出礼物后礼物点数被更新

* 观众主动查询礼物点数后调用`webSDK.emit('gift.pointQuery')`


```TypeScript
(value: { point: number }) => void
```


**参数**


|名称 |数据类型 |接口行为 |
|---|---|---|
|point |number |观众当前的礼物积分余额。 |


**使用示例**

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

类型：`enum`


|属性 |值 |接口行为 |
|---|---|---|
|play |`'player.play'` |播放视频。 |
|pause |`'player.pause'` |暂停视频。 |
|pip |`'player.pip'` |在 PC 上切换至小窗模式或从小窗模式切回。<br><br><br>* `true`：切换至小窗模式。<br><br>* `false`：从小窗模式切回原屏幕。<br><br><br>示例代码：<br><br>```JavaScript```<br>```webSDK.emit('player.pip', {```<br>```    ifShow: true,```<br>```})```<br> |
|comment.send |`'comment.send'` |发送评论。<br><br>示例代码：<br><br>```JavaScript```<br>```webSDK.emit('comment.send', 'BytePlus Live');```<br> |
|comment.disabled |`'comment.disabled'` |禁用或启用评论输入框。<br><br><br>* 禁用：`webSDK.emit('comment.disabled', true)`<br><br>* 启用：`webSDK.emit('comment.disabled', false)`<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅在通过<code>disabledCommentConfig</code>参数配置评论输入框的禁用状态和占位符文本后，才能触发此事件。更多信息请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#b6fb0c34">选项</a>。</div><br> |
|gift.send |`'gift.send'` |在[gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#d476ef36)事件触发后，发送指定数量的礼物。`count` 的默认值为`1`。你可以根据需要自定义`count`的值。<br><br>建议将`disableSendGift`的值设置为`true`，以禁用默认的 UI 相关礼物发送逻辑。<br><br>示例代码：<br><br>```JavaScript```<br>```webSDK.emit('gift.send', {```<br>```    ...value.data,```<br>```    count:10 // The number of gifts to send.```<br>```  });```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">关于<code>disableSendGift</code>的更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN">Web 观播 SDK：参数</a>。</div><br> |
|gift.pointQuery |`'gift.pointQuery'` |查询观众的礼物积分余额。 |
|playbackListBtn.click |`'playbackListBtn.click'` |模拟点击回放列表按钮。 |
