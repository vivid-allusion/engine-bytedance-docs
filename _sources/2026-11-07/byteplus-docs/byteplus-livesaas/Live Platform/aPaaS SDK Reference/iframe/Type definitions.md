---
title: "Type definitions"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/iframe-type-definitions"
---

<span id="7a4fc916"></span>
## PortraitMenuIcon

Type: `enum`

The icon of a live room in portrait mode on mobile devices.


|Property |Value |Description |
|---|---|---|
|shoppingCart |`'shoppingCart'` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/286c6e7fd7e4468bafb15b8b3447b2ea~tplv-goo7wpa0wc-image.image) </span> |
|share |`'share'` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f2bfeddb3ae44cbb20217dcbe7cba30~tplv-goo7wpa0wc-image.image) </span> |
|info |`'info'` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34bbff62b47d4f0d9dd60c5fbf7251c4~tplv-goo7wpa0wc-image.image) </span> |
|images |`'images'` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b769e18d6601428f9e9c2071dceede58~tplv-goo7wpa0wc-image.image) </span> |
|notification |`'notification'` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00b7dbe0a1554b87b88f8fffd17756b1~tplv-goo7wpa0wc-image.image) </span> |


<span id="fa52e27e"></span>
## UAInfo

Type: `interface`

The environment information configured for the menu for product cards.

<span id="f94c7c26"></span>
### UAAddress

Type: `string`

The environment UA (User Agent).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If viewers on mobile devices tap a product card on platforms whose environment UA includes this parameter value, they will be redirected to the direct URL of the product card. If they tap the product card on other platforms, they will be redirected to the product URL of the product card.</div>


<span id="84982d26"></span>
### UAName

Type: `string`

The environment name.

<span id="0c0d8d3f"></span>
## TaskAwardConfig

Type: `interface`

The configurations for this watch time\-based lucky draw activity.

<span id="63de4d99"></span>
### TaskAwardId

Type: `string`

The ID for this watch time\-based lucky draw activity.

<span id="ddd61320"></span>
### TaskAwardStatus

Type: `0 | 1 | 2 | 3`

The status for this watch time\-based lucky draw activity. Valid values:


* `NULL(-1)`: No lucky draw activity. Reserved for future use.

* `INIT(0)`: Initialization, meaning the activity has not started.

* `START(1)`: The activity is in progress.

* `END(2)`: The activity is over.

* `CLOSE(3)`: The activity is closed.


<span id="b2baf812"></span>
### TaskAwardInstructions

Type: `string`

The description for this watch time\-based lucky draw activity.

<span id="91c0fdba"></span>
### TaskAwardIcon

Type: `string`

The lucky draw icon for this watch time\-based lucky draw activity.

<span id="7c7d4ffe"></span>
### TaskAwardRule

Type: [TaskAwardRuleItem](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#a1ff791f)[]

The lucky draw rules.

<span id="d1e36a19"></span>
### TaskAwardStartTime

Type: `number`

The start time for this watch time\-based lucky draw activity. Unix timestamp format. Unit: seconds.

<span id="be6fed24"></span>
### TaskAwardEndTime

Type: `number`

The end time for this watch time\-based lucky draw activity. Unix timestamp format. Unit: seconds.

<span id="a1ff791f"></span>
## TaskAwardRuleItem

Type: `interface`

The rules for watch time\-based lucky draws.

<span id="3a5b446d"></span>
### WatchTime

Type: `number`

The total watch time required to participate in the lucky draw. Unit: minutes.

<span id="32c0304f"></span>
### AwardItemName

Type: `string`

The prize name.

<span id="a2104233"></span>
### AwardItemIcon

Type: `string`

The prize icon.

<span id="9f542feb"></span>
### AwardItemType

Type: `1 | 2 | 3 | 4`

The prize type. Valid values:


* `1`: Physical prizes.

* `2`: Virtual prizes.

* `3`: Custom prizes.

* `4`: Voucher prizes.


<span id="af0a3ea1"></span>
### TaskAwardItemId

Type: `string`

The prize ID.

<span id="76183646"></span>
### AwardCount

Type: `number`

The number of prizes.

<span id="a4c6ed13"></span>
### index

Type: `number`

The sequence number of the prize. The sequence number of the first prize is 0, that of the second prize is 1, and so on.

<span id="5a950de5"></span>
## IRecordInfo

Type: `interface`

The winning records of the current viewer.

<span id="c85fd7ac"></span>
### AwardItemName

Type: `string | undefined`

The lucky draw name.

<span id="e76acfd4"></span>
### TaskAwardItemId

Type: `string`

The prize ID.

<span id="7388ac63"></span>
### TaskAwardItemName

Type: `string`

The prize name.

<span id="cdd48f24"></span>
### Status

Type: [TaskAwardItemResult](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#de2931c2)

The lucky draw result.

<span id="44a1f49e"></span>
### CreateTime

Type: `number`

The time of winning the prize. Unix timestamp format. Unit: seconds.

<span id="8cc00316"></span>
### Phone

Type: `string | undefined`

The recipient's phone number.

<span id="3368a481"></span>
### Address

Type: `string | undefined`

The recipient's shipping address.

<span id="970376a0"></span>
### ReceiverName

Type: `string | undefined`

The recipient's name.

<span id="de2931c2"></span>
## TaskAwardItemResult

Type: `enum`

The lucky draw result.


|Property |Value |Description |
|---|---|---|
|INIT |`-1` |Initialization, meaning the lucky draw has not started yet. |
|UNATTENDED |`0` |Not participated in the lucky draw. |
|WIN |`1` |Won the prize. |
|LOSE |`2` |Did not win the prize. |
|ATTENDING |`3` |Participated in the lucky draw. |
