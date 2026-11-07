---
title: "Parameters"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/iframe-parameters"
---

You can add the following parameters in the embedded link to achieve specific features.

Here is an example.

```Plain
<iframe src="https://live.byteplus.com/1323/6****21?platform=pc"></iframe>
```


<span id="1203c8d5"></span>
## Basic parameters


|Name |Type |Required |Default Value |Description |
|---|---|---|---|---|
|platform |string |No |None |The platform to display the embedded page. If not specified, the platform will be determined based on the viewer's device, meaning that the embedded page will display the PC version on a PC and the mobile version on a mobile device.<br><br>Valid values:<br><br><br>* `pc`: PCs.<br><br>* `mobile`: Mobile devices. |
|mode |string |No |None |Feature modules. Applicable to scenarios where you are embedding specific modules. Valid values:<br><br><br>* `player`: The player.<br><br>* `comment`: The menu for chat interaction, including the list of top comments.<br><br>* `imagetext`: The menu for interaction tools.<br><br>* `bandcontent`: The menu for graphics.<br><br>* `cardlist`: The menu for product cards.<br><br>* `polylive`: The menu for aggregated live streams.<br><br>* `session`: The menu for Q&A.<br><br>* `menu`: The combination of multiple menus, which must be used together with the `menu` parameter.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When embedding a specific menu, make sure that the corresponding menu has been added to the viewing page. For the menu for interaction tools, make sure the <strong>Display menu</strong> switch is turned on.</div><br> |
|menu |string |No |None |The combination of menus to be embedded. This parameter takes effect only when the value of `mode` is `menu`. Separate multiple parameter values with underscores (_). For example, `menu=comment_imagetext`.<br><br>Valid values:<br><br><br>* `comment`: The menu for chat interaction, including the list of top comments.<br><br>* `imagetext`: The menu for interaction tools.<br><br>* `bandcontent`: The menu for graphics.<br><br>* `cardlist`: The menu for product cards.<br><br>* `polylive`: The menu for aggregated live streams.<br><br>* `session`: The menu for Q&A. |


<span id="17f0a114"></span>
## Non\-player\-related parameters


|Name |Type |Required |Default Value |Description |
|---|---|---|---|---|
|tabTitle |boolean |No |`true` |Whether to display the menu bar. Valid values:<br><br><br>* `true`: Displays the menu bar.<br><br>* `false`: Does not display the menu bar and only shows the specific content under the menu. We recommend that you set the value to `false` only when the embedded page displays a single menu to avoid affecting the display of the menu content. |
|portrait |integer |No |Not applicable |Add this parameter to display the embedded page in portrait mode on mobile devices. The parameter value is fixed to `1`.<br><br>This parameter only takes effect when the value of `platform` is `mobile` and you are embedding the full page. |
|background |string |No |Not applicable |Add this parameter to set the background color to transparent. The parameter value is fixed to `transparent`. |
|language |string |No |`all` |The default language of the embedded page. Valid values:<br><br><br>* `all`: The same as the default browser language on PCs or the system language on mobile devices.<br><br>* `cn`: Simplified Chinese.<br><br>* `en`: English.<br><br>* `jp`: Japanese.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Make sure that you have configured multiple corresponding languages for the viewing page in the console.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After setting the value to <code>all</code>:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If Simplified Chinese is not configured as the viewing page language in the console, but the default browser language or the system language is Simplified Chinese, then the default language of the embedded page will be Simplified Chinese.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the default browser language or the system language is not among the languages configured or supported in the console, then the default language of the embedded page will be English.</div><br> |
|customAuthRedirect |boolean |No |`true` |Whether viewers are allowed to be redirected to the login page of your own account system. This parameter takes effect only when the comment restriction is set to **Custom**.<br><br>Valid values:<br><br><br>* `true`: Allowed.<br><br>* `false`: Not allowed. You must implement the redirection feature yourself. |
|pcPlayerHeader |boolean |No |`false` |Whether to display information such as the live room name and description on the top of the player for PCs. Valid values:<br><br><br>* `true`: Displays the information.<br><br>* `false`: Does not display the information. |
|mobileBackgroundTransparent |boolean |No |`false` |Whether the background of mobile devices is transparent. Valid values:<br><br><br>* `true`: Transparent. Displays the background image or color of your own page.<br><br>* `false`: Not transparent. |
|disableCardRedirect |boolean |No |`false` |Whether to disable the feature of redirecting viewers to another page or the floating layer on the embedded page after they click or tap a product card. Generally, this parameter is used with the [card.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#23b68bf7) or [floatingCard.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#f777e233) event. If this feature is disabled, you must implement the redirection feature yourself. Valid values:<br><br><br>* `true`: Disables the feature.<br><br>* `false`: Enables the feature. |
|disableAdFloatingRedirect |boolean |No |`false` |Whether to disable the feature of redirecting viewers to another page or the floating layer on the embedded page after they click or tap a floating ad. Generally, this parameter is used with the [adFloating.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#4a058ac8) event. If this feature is disabled, you must implement the redirection feature yourself. Valid values:<br><br><br>* `true`: Disables the feature.<br><br>* `false`: Enables the feature. |
|disableAdMiddleRedirect |boolean |No |`false` |Whether to disable the feature of redirecting viewers to another page or the floating layer on the embedded page after they click or tap an in\-page ad. Generally, this parameter is used with the [adMiddle.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#e0aa9f45) event. If this feature is disabled, you must implement the redirection feature yourself. Valid values:<br><br><br>* `true`: Disables the feature.<br><br>* `false`: Enables the feature. |
|disableAdAccountRedirect |boolean |No |`false` |Whether to disable the feature of redirecting viewers to another page after they click or tap a host account. Generally, this parameter is used with the [adAccount.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#2d145963) event. If this feature is disabled, you must implement the redirection feature yourself. Valid values:<br><br><br>* `true`: Disables the feature.<br><br>* `false`: Enables the feature. |
|moreActionExpandPc |boolean |No |`false` |Whether to display the options in the ellipsis icon as icons under the menu for chat interaction on PCs. Valid values:<br><br><br>* `true`: Displays as icons.<br><br>* `false`: Does not display as icons. |
|disableReservationCell |boolean |No |`false` |Whether to disable the feature of displaying the live booking dialog box. Generally, this parameter is used with the [reservation.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#e5744da6) event. If this feature is disabled, you must implement the live booking feature yourself. Valid values:<br><br><br>* `true`: Disables the feature.<br><br>* `false`: Enables the feature. |
|disableLotteryTicketRedirect |boolean |No |`false` |Whether to disable the feature of redirecting viewers to another page after they click or tap the prize claim link of a voucher prize. Generally, this parameter is used with the [lotteryTicket.click](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-events#2515d473) event. If this feature is disabled, you must implement the redirection feature yourself. Valid values:<br><br><br>* `true`: Disables the feature.<br><br>* `false`: Enables the feature. |
|loginInToThumbUp |boolean |No |`false` |Whether viewers must log in to the live room before liking the live room. Valid values:<br><br><br>* `true`: Viewers must log in. If they are not logged in, the login process is triggered when they like the live room.<br><br>* `false`: Login is not required. |
|customInteractionIcons |[CustomInteractionIcons](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-parameters#b4164922)[] |No |\- |The floating interaction tools. |
|portraitMenuExtends |[PortraitMenuConf](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-parameters#5b4f929f)[] |No |\- |The icons or buttons of a live room in portrait mode on mobile devices. |


<span id="b4164922"></span>
### CustomInteractionIcons

The parameters related to floating interaction tools.


|Name |Type |Required |Default Value |Description |
|---|---|---|---|---|
|key |string |Yes |None |The unique identifier of the floating interaction tool. |
|img |string |Yes |None |The image URL of the floating interaction tool. Supported image formats are the same as those supported by the `img` tag. |
|text |string |Yes |None |The text at the bottom of the floating interaction tool. |


<span id="5b4f929f"></span>
### PortraitMenuConf

The parameters related to the icons or buttons of a live room in portrait mode on mobile devices.


|Name |Type |Required |Default Value |Description |
|---|---|---|---|---|
|name |string |Yes |None |The name of the icon or button, which is displayed under the corresponding icon or button when viewers tap the ellipsis icon. |
|icon |[PortraitMenuIcon](https://docs.byteplus.com/docs/byteplus-livesaas/iframe-type-definitions#7a4fc916) |No |\- |The icon of a live room in portrait mode on mobile devices. |
|render |string |No |None |The icon or button of a live room in portrait mode on mobile devices. Example: `<div style="color: #fff">Go</div>`. |
|key |string |Yes |None |The unique identifier of the icon or button. |
|index |number |Yes |`0` |The display order of the icon or button. The larger the parameter value, the closer to the left the icon or button is. If the parameter value is larger than 70, viewers can only view the icon or button after tapping the ellipsis icon. At most 4 icons and buttons, including the default ones in your live room, can be displayed at one time. Viewers can only view other icons or buttons after tapping the ellipsis icon. |


<span id="aec39a74"></span>
## Player\-related parameters


|Name |Type |Required |Default Value |Description |
|---|---|---|---|---|
|systemFullScreen |boolean |No |Not applicable |Add this parameter to support native full screen on iOS mobile devices. The parameter value is fixed to `true`. |
|cssFullScreen |boolean |No |Not applicable |Add this parameter to support full screen on iOS mobile devices by using CSS styles. The parameter value is fixed to `true`. |
