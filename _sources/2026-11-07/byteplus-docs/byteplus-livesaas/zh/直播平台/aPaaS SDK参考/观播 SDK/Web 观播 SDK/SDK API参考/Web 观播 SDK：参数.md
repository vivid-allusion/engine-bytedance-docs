---
title: "Web 观播 SDK：参数"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN"
---

<span id="2c9e46bc"></span>
## SDKconf

这些参数用于配置 SDK，以便在观看页展示直播间。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SDK 配置优先于 BytePlus Live 控制台和服务端 OpenAPI 中配置的设置。</div>



|名称 |类型 |必填 |默认值 |描述 |
|---|---|---|---|---|
|activityId |Integer |是 |不适用 |直播间的活动 ID。<br><br>一个直播间对应一个活动 ID。<br><br>获取活动 ID 可通过以下方法之一：<br><br><br>* 调用 [CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN)。<br><br>* 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，在直播间左上角查找 ID。 |
|service |String |是 |不适用 |服务名称，仅用于标记。<br><br>配置 BytePlus Live 白名单后，技术支持会将该参数值同步给你。 |
|mode |Integer |是 |不适用 |认证模式。<br><br><br>* `1`：公开模式。观众以嘉宾模式进入直播间，在需要用户信息的场景（如点击评论输入框、参与抽奖）时，必须输入昵称或通过手机号登录直播间完成嘉宾注册。<br><br>* `2`：自定义模式。观众通过你的 Web 应用中的用户信息进入直播间，可直接进行评论、参与抽奖等操作。 |
|token |String |是 |不适用 |用户 token。<br><br><br>* 若 `mode` 的值为 `1`，可通过调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN) 或进入 **Producer** \> **Page embedding** \> **Web SDK embedding**，在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播间页面获取用户 token。<br><br>* 若 `mode` 的值为 `2`，可通过调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN) 获取用户 token。 |
|modules |[模块](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#b56510d0)[] |是 |不适用 |模块配置。 |
|options |Partial<[选项](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#b6fb0c34)\> |否 |不适用 |可选参数。 |


<span id="b56510d0"></span>
## 模块


|名称 |类型 |必填 |默认值 |描述 |
|---|---|---|---|---|
|id |String |是 |不适用 |页面元素 ID，用于指定要渲染模块的位置和尺寸。 |
|mode |String |是 |不适用 |模块名称。<br><br><br>* `player`：播放器模块。建议 PC 端最小宽度为 640 px。<br><br>* `menu`：菜单模块。SDK 支持渲染多种菜单类型：聊天互动、图文、商品卡片、互动工具、问答、内嵌链接。建议 PC 端最小宽度为 320 px。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">互动工具的菜单只有在<a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live console</a>中打开<strong>Display menu</strong> 开关时才会显示在观看页上。   </div><br>   <br><br>* `lines`：多线路模块，用于直播源和回放列表。无需指定高度，模块会自适应高度。<br><br>* `mobile`：移动设备横屏模式下的全页模块，包含播放器、多线路和菜单模块。该模块仅支持移动设备，不能与其他模块同时使用。关于效果详情，请参见 [demo](https://live.byteplus.com/demo/sdk/index.mobile.all.html)。<br><br>* `mobile-portrait`：移动设备竖屏模式下的全页模块，包含播放器、多线路和菜单模块。该模块仅支持移动设备，不能与其他模块同时使用。关于效果详情，请参见 [demo](https://live.byteplus.com/demo/sdk/index.mobile.all-portrait.html)。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当参数值设置为<code>player</code>、<code>menu</code>或<code>lines</code>时，只能集成这些模块专属的功能。要在移动设备上集成不属于任何模块的功能，例如预约、主播账号和页头图，可以将参数值设置为<code>mobile</code>或<code>mobile-portrait</code>，以集成全页模块。</div><br> |
|menu |String[] |否 |无 |仅当`modules.mode`的值为`menu`时，此参数生效。<br><br>使用此参数配置需要展示的菜单类型。例如，可以将其设置为`["comment", "imagetext"]`。如未指定，则会展示所有菜单类型。<br><br><br>* `comment`：聊天互动菜单。<br><br>* `imagetext`：互动工具菜单。<br><br>* `cardlist`：商品卡片菜单。<br><br>* `bandcontent`：图文菜单。<br><br>* `session`：问答菜单。<br><br>* `embeddedurl`：内嵌链接菜单。 |


<span id="b6fb0c34"></span>
## 选项


|名称 |类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|origin |字符串 |否 |`"https://live.byteplus.com"` |业务请求的域名。如无特殊需求，无需配置此参数。 |
|saveUserInfo |布尔值 |否 |`true` |当`mode`的值为`1`时，指定是否缓存用户信息。<br><br><br>* `true`：缓存。<br><br>* `false`：不缓存。 |
|mobileBackgroundTransparent |布尔值 |否 |`false` |指定移动端模块背景是否透明。<br><br><br>* `true`：透明。在观看页展示您的背景图片或颜色。<br><br>* `false`：不透明。 |
|mobileGetUserId |布尔值 |否 |`true` |指定是否允许观众在移动端通过快速点击观看页左上角五次获取自己的用户ID。<br><br><br>* `true`：开启。<br><br>* `false`：关闭。 |
|basicPolling |布尔值 |否 |`true` |指定是否启用轮询API实时更新直播间信息。<br><br><br>* `true`：开启。<br><br>* `false`：关闭。 |
|pcPlayerHeader |布尔值 |否 |`false` |指定是否在PC端播放器顶部展示直播间名称及描述等信息。<br><br><br>* `true`：展示。<br><br>* `false`：不展示。 |
|playerRetryTimes |整数 |否 |`1` |播放器因网络异常无法播放视频时的重试次数。切换主流与备流或降级至低质量流后问题仍未解决，则视为重试失败。如需无限重试，将参数值设置为0。 |
|disabledLogin |布尔值 |否 |`false` |指定是否禁用BytePlus Live内置登录系统。通常此参数与事件配合使用。系统禁用后，需自行实现用户登录逻辑。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|disableCardRedirect |布尔值 |否 |`false` |指定是否禁用观众点击商品卡片后跳转至其他页面或观看页浮层的功能。通常此参数与或事件配合使用。功能禁用后，需自行实现跳转逻辑。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|disableAdFloatingRedirect |布尔值 |否 |`false` |指定是否禁用观众点击浮标广告后跳转至其他页面或观看页浮层的功能。通常此参数与[adFloating.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#d05864eb)事件配合使用。功能禁用后，需自行实现跳转功能。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|disableAdMiddleRedirect |布尔值 |否 |`false` |指定是否禁用观众点击页中广告后跳转至其他页面或观看页浮层的功能。通常此参数与事件配合使用。功能禁用后，需自行实现跳转逻辑。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|disableAdAccountRedirect |Boolean |否 |`false` |指定是否禁用观众点击或轻触主播账号后跳转到其他页面的功能。通常，该参数与事件一起使用。如果该功能被禁用，则必须自行实现跳转逻辑。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|purePlayer |Boolean |否 |`false` |指定是否显示纯播放器。纯播放器指不包含交互按钮（如进度条）的播放器。<br><br><br>* `true`：显示纯播放器，播放器中不包含任何交互按钮。<br><br>* `false`：显示常规播放器，播放器中包含交互按钮。 |
|videoFillMode |String |否 |`'auto'` |指定视频在播放器中的填充模式。<br><br><br>* `cover`：缩放视频以保持视频长宽比，同时填满播放器的整个内容框。如果视频长宽比与播放器不一致，视频会被裁剪以适配。<br><br>* auto：缩放视频以保持视频长宽比，同时适配播放器的内容框。整个视频都会显示，如果长宽比不一致，则会出现黑边。<br><br>* `fill`：调整视频尺寸以填满播放器。视频长宽比可能会发生变化。<br><br>* `fillWidth`：拉伸视频宽度以填满播放器宽度，视频高度保持不变。<br><br>* `fillHeight`：拉伸视频高度以填满播放器高度，视频宽度保持不变。<br><br><br>该参数仅在移动设备横屏模式和 PC 上生效。<br><br>移动设备竖屏模式下的视频填充方式会根据源流的视频长宽比变化。 |
|softSolution |Boolean |否 |无 |指定是否强制开启或禁用移动设备播放器的软解。此功能可防止部分移动浏览器或应用使用其内置播放器，确保视频在 SDK 播放器内播放。<br><br><br>* `true`：强制开启。<br><br>* `false`：强制禁用。 |
|disableReservationCell |Boolean |否 |`false` |指定是否禁用显示直播预约弹窗的功能。通常，该参数与[reservation.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#44166c70)事件一起使用。如果该功能被禁用，则必须自行实现直播预约功能。换句话说，必须通过`isReserved`参数指定当前观众是否已预约你的直播流，并手动调用`updateModulesConf` API 更新预约状态。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|isReserved |Boolean |否 |无 |指定当前观众是否已预约直播流。<br><br><br>* `true`：已预约。<br><br>* `false`：未预约。 |
|lotteryIcon |[lotteryIcon](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#3f23b8e9) |否 |无 |抽奖图标。支持的图片格式与`img`标签支持的格式一致。 |
|emojiIcon |String |否 |无 |观众在 PC 上点击或轻触发送表情时使用的图标。将参数值设置为图标的 URL。支持的图片格式与 img 标签支持的格式一致。 |
|moreActionExpandPc |Boolean |否 |`false` |指定是否将省略号图标中的选项以图标形式显示在 PC 聊天互动菜单下。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |
|playerBackgroundTransparent |Boolean |否 |`false` |指定播放器中未被视频填充的区域是否为透明。<br><br><br>* `true`：透明。显示封面图。<br><br>* `false`：不透明。该区域显示为黑色。 |
|disablePlayerCover |Boolean |否 |`false` |指定是否禁用封面图。<br><br><br>* `true`：在播放器中显示背景图片或颜色。<br><br>* `false`：在播放器中显示封面图。 |
|mobilePlayerIconIgnoreList |String[] |否 |无 |指定要在移动设备播放器中隐藏哪些图标。<br><br><br>* `editNickname`：用于修改观众昵称的图标。<br><br>* `notification`：用于开启或关闭系统通知的图标。<br><br>* `language`：用于切换其他语言的图标。<br><br>* `share`：用于分享直播间海报、二维码或链接的图标。 |
|riskWarning |Boolean |否 |`true` |指定是否开启提醒弹窗。<br><br><br>* `true`：开启。<br><br>* `false`：关闭。 |
|portraitMenuExtends |[PortraitMenuConf](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#0eef80a1)[] |否 |无 |指定移动设备竖屏模式下直播间的图标或按钮。 |
|mobileGesture |[mobileGesture](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#85e1fb94) |否 |无 |移动设备播放器手势配置。 |
|showLikeInPlayer |Boolean |否 |`false` |指定是否在播放器中显示直播间点赞图标。<br><br><br>* `true`：在播放器中显示。默认显示在播放器右下角。你可以通过覆盖`class`属性`bytelive-player-like-button`的样式来调整图标位置。<br><br>* `false`：显示在评论输入框右侧。 |
|disableLotteryTicketRedirect |Boolean |否 |`false` |指定是否禁用观众点击或触碰券奖品领奖链接后跳转到其他页面的功能。通常该参数与[lotteryTicket.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#e290813e)事件一起使用。若该功能被禁用，你需要自行实现跳转功能。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|extra |String |否 |不适用 |同步到 BytePlus Live 的额外参数，可用于与观众关联。例如，你可以将参数值设置为`Marketing department`，以便将观众所在部门从你的账号系统同步到 BytePlus Live。 |
|disableRotateFullscreen |Boolean |否 |`false` |指定是否禁用移动设备观众旋转至横屏模式时自动全屏功能。<br><br><br>* `true`：禁用。观众旋转至横屏模式时不会自动触发全屏，也不会弹出提示。<br><br>* `false`：启用。 |
|disableLivePauseButton |Boolean |否 |`false` |指定是否在直播流过程中隐藏播放器暂停按钮。<br><br><br>* `true`：隐藏。<br><br>* `false`：不隐藏。 |
|loginInToThumbUp |Boolean |否 |`false` |指定观众是否必须登录后才能点赞直播流。<br><br><br>* `true`：观众必须登录。若未登录，点击或触碰点赞图标时会触发[permission.need](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#c91cc8cb)事件。<br><br>* `false`：无需登录。 |
|closePlayVideoFocus |Boolean |否 |无 |指定观众进入观看页时是否自动滚动到正在播放预告、回放或直播视频的播放器。<br><br><br>* `true`：自动滚动。<br><br>* `false`：不自动滚动。 |
|defaultLang |String |否 |不适用 |观看页的默认语言。无论观众在 PC 端的浏览器默认语言还是移动设备的系统语言如何，页面将在观众进入直播间时设置为已配置的默认语言。<br><br>如未指定，默认语言将与观众在 PC 端的浏览器默认语言或移动设备的系统语言保持一致。<br><br>有效值：<br><br><br>* `zh`：简体中文。<br><br>* `en`：英文。<br><br>* `ja`：日文。<br><br>* `zh-hant`：繁体中文。<br><br>* `ko`：韩文。<br><br>* `th`：泰文。<br><br>* `vi`：越南文。<br><br>* `ar`：阿拉伯文。<br><br>* `tr`：土耳其文。<br><br>* `es`：西班牙文。<br><br>* `id`：印尼文。<br><br>* `pt`：葡萄牙文。<br><br>* `ru`：俄文。<br><br>* `tl`：塔加洛语。<br><br>* `km`：高棉语。<br><br>* `lo`：老挝语。<br><br>* `my-MM`：缅甸语。<br><br>* `ms`：马来语。<br><br>* `hi`：印地语。<br><br>* `fr`：法语。<br><br>* `de`：德语。<br><br>* `it`：意大利语。 |
|disabledCommentConfig | |否 |无 |用于指定是否禁用评论输入框，以及禁用状态下输入框的占位文本。<br><br><br>* `disabled`：是否禁用评论输入框。有效值：<br><br>   * `true`：禁用。若禁用，观众点击评论输入框时无法输入内容。<br><br>   * `false`：启用。<br><br>* `placeholder`：禁用状态下评论输入框的占位文本。 |
|pcuConfig | |否 |无 |如订阅直播并发观众套餐，当观众尝试进入直播间且所有直播间的并发峰值用户数（PCU）超出账号限制时，将显示错误页面。<br><br>可通过该参数自定义错误页面的文本和图片。更多信息请参见 [Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-ios-zh-CN#db59dce3)。 |
|disableSendGift |Boolean |否 |false |用于指定当观众点击或触摸 **Send** 发送礼物时，是否禁用 BytePlus Live 与 UI 相关的送礼逻辑。<br><br><br>* `true`：禁用。你需自行实现与 UI 相关的送礼逻辑，例如设置送礼数量及自定义礼物效果。<br><br>* `false`：启用。 |
|shopCartIcon |String |否 |无 |用于配置购物车图标。可上传 GIF 或 PNG 图片自定义购物车图标。 |
|disabledShopCartClick |Boolean |否 |false |用于指定观众在移动端观看页点击购物车图标时，是否禁用展示商品列表功能。<br><br>通常该参数与 [shopCart.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#7bd143bd) 事件配合使用。如将参数值设置为 `true`，需自行实现相关逻辑。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|disabledShowExplainCard |Boolean |否 |false |用于指定当商品被推荐时，是否禁用观看页上的商品浮窗。<br><br><br>* `true`：禁用。禁用后，商品被推荐时商品卡片不会固定在观看页上。<br><br>* `false`：启用。 |
|disablePopularityShow |Boolean |否 |false |用于指定是否禁用人气展示，即观看页显示的观众数量。<br><br><br>* `true`：禁用。<br><br>* `false`：启用。 |
|shareUrl |String |否 |无 |用于自定义直播间分享链接。URL 必须包含协议（如 https://）。如未设置或留空，将使用控制台中的分享地址。适用于链接、邀请海报和流。 |
|vodSwitchMode |Boolean |否 |false |用于指定是否启用 VOD（视频点播）流回放模式。<br><br><br>* `true`：启用 VOD 流播放模式。视频以信息流样式展示，便于交互式浏览。<br><br>* `false`：禁用点播信息流模式。视频以传统列表样式展示。 |
|enablePlaybackSwitchBtn |boolean |否 |true |指定是否在播放器中显示**回放合集**按钮。<br><br><br>* `true`：显示回放合集按钮。观众可通过该入口访问回放列表。<br><br>* `false`：隐藏回放合集按钮。 |
|enablePlaybackListPopup |boolean |否 |true |指定是否显示回放合集列表窗口。<br><br><br>* `true`：显示回放合集列表窗口。观众可在列表中查看并选择回放视频。<br><br>* `false`：隐藏回放合集列表窗口。即使点击**回放合集**按钮，也不会显示回放列表。 |
|playbackMode |Number |否 |1 |指定回放合集列表的播放模式。<br><br><br>* `1`：按列表顺序播放视频。<br><br>* `2`：循环播放列表中的所有视频。<br><br>* `3`：仅循环播放当前视频。 |


<span id="3f23b8e9"></span>
### lotteryIcon


|名称 |类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|attendIcon |String |否 |无 |未选出获奖者时显示的抽奖图标。将参数值设置为`1: '图标图片的 URL'`。<br><br>如需在日语、简体中文和繁体中文观看页配置图标，分别将`1`替换为`2`、`0`和`3`，并将 URL 替换为各语言对应的图片地址。 |
|openIcon |String |否 |无 |选出获奖者时显示的抽奖图标。将参数值设置为`1: '图标图片的 URL'`。<br><br>如需在日语、简体中文和繁体中文观看页配置图标，分别将`1`替换为`2`、`0`和`3`，并将 URL 替换为各语言对应的图片地址。 |


<span id="0eef80a1"></span>
### PortraitMenuConf


|名称 |类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|icon |String |否 |无 |移动端竖屏模式下直播间的图标。<br><br>可选值：<br><br><br>* `shoppingCart`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9adb88ab716e4de29b64b30da2d172c4~tplv-goo7wpa0wc-image.image) </span><br><br>* `share`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afdd86ef695443b39100c134f6769ea9~tplv-goo7wpa0wc-image.image) </span><br><br>* `info`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ddc0bd06c2e4637908514ae37de4355~tplv-goo7wpa0wc-image.image) </span><br><br>* `images`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09bdfb69f4e34879963e4dfc4c7c690b~tplv-goo7wpa0wc-image.image) </span><br><br>* `notification`<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eda4fc851cea4601ae4bd55055915038~tplv-goo7wpa0wc-image.image) </span> |
|render |String |否 |无 |移动端竖屏模式下直播间的图标或按钮。示例：`<div style="color: #fff">Go</div>`<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该优先级低于<code>icon</code>参数，因此如果需要通过<code>render</code>参数自定义图标或按钮，请不要为<code>icon</code>参数设置值。</div><br> |
|name |String |否 |无 |图标或按钮的名称，当观众点击省略号图标时，会显示在对应的图标或按钮下方。 |
|key |String |是 |无 |图标或按钮的唯一标识。 |
|onClick |Function |否 |无 |点击事件回调，点击图标或按钮时会触发。返回值为`key`参数的值。 |
|index |Number |否 |`0` |图标或按钮的显示顺序。参数值越大，图标或按钮越靠左显示。如果参数值大于 70，观众需点击省略号图标后才能看到该图标或按钮。最多直接展示 4 个图标和按钮（含默认项）。更多图标可通过省略号（...）菜单访问。 |


<span id="85e1fb94"></span>
### mobileGesture


|名称 |类型 |是否必填 |默认值 |接口行为 |
|---|---|---|---|---|
|disableGesture |Boolean |否 |`false` |指定是否在移动端禁用手势操作。<br><br><br>* `true`：禁用。观众无法通过在预告或回放时左右滑动拖动进度条。<br><br>* `false`：启用。 |
