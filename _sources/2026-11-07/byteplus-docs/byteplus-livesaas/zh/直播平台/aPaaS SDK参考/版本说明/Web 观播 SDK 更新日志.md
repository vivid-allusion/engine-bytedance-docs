---
title: "Web 观播 SDK 更新日志"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-changelog-zh-CN"
---

在此处查找 Web 观播 SDK 的所有变更。

<span id="d7e0d7a1"></span>
## 2026年8月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2026\-08\-12 |2.0.31 |**功能优化**<br><br>更新了 CSS 样式。 |


<span id="july-2026"></span>
## 2026年7月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2026\-07\-23 |2.0.30 |**功能优化**<br><br><br>* 新增对商品卡片多环境直达链接功能的支持。<br><br>* 新增在直播模板中配置**点赞**和**人气展示**的支持。<br><br><br>**兼容性变更**<br><br>自 v2.0.30 起，集成 SDK 时，域名已由`https://res.bytepluscdn.com/obj/bp-console-fe-sg`变更为`https://res.gcloudcache.com/bp-fe`。更多信息，请参见[集成方式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN#855885cc)。 |


<span id="0bc95836"></span>
## 2026年2月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2026\-02\-02 |2.0.27\-beta.4 |**问题修复**<br><br>修复了部分问题。 |


<span id="8e7d0d0f"></span>
## 2026年1月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2026\-01\-12 |2.0.27\-beta.2（仅用于播放器集成）和 2.0.27\-beta.3 |本次发布包含内部优化。无功能变更，现有使用方式不受影响。<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">为保证服务稳定和持续支持，请升级到最新版本。详情请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN#7f20b494">Step 1: 导入 CSS 和 JS 资源</a>。</div><br> |
|2026\-01\-06 |2.0.27 |**问题修复**<br><br>修复了部分问题。 |


<span id="67d0f65a"></span>
## 2025年12月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-12\-10 |2.0.25 |**功能优化**<br><br><br>* 人气展示<br><br>   * 新增参数`disablePopularityShow`，用于指定是否关闭观看页观众数量的展示。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>   * 新增`popularity.configChange`事件，当观看页展示的观众数量发生变化时触发。更多信息，请参见[popularity.configChange](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#9c17df67)。<br><br>* 商品<br><br>   * 新增参数`shopCartIcon`，用于指定购物车图标配置。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>   * 新增参数`disabledShowExplainCard`，用于指定商品被推荐时是否关闭观看页商品浮窗。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>   * 新增`floatingCard.update`事件，当商品浮窗被更新时触发。更多信息，请参见[floatingCard.update](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#163fd7d0)。 |


<span id="3cc7c0a1"></span>
## 2025年11月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-11\-12 |2.0.24 |**功能优化**<br><br>新增`defaultLang`参数对更多语言的支持。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br><br>* 塔加拉语<br><br>* 高棉语<br><br>* 老挝语<br><br>* 缅甸语<br><br>* 马来语<br><br>* 印地语<br><br>* 法语<br><br>* 德语<br><br>* 意大利语 |


<span id="62f42b28"></span>
## 2025年10月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-10\-16 |2.0.23 |**新功能**<br><br><br>* 商品<br><br>   * 新增[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-web-zh-CN#fe534689)类型。<br><br>   * 新增`card.configChange`事件，当商品卡片配置发生变化时触发。更多信息，请参见[card.configChange](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#7f70dfa5)。<br><br>   * 新增以下 API。更多信息，请参见[API](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN)。<br><br>      * `getProductList()`<br><br>      * `updateProductInfo()`<br><br>* 回放列表<br><br>   * 新增以下参数：<br><br>      * `vodSwitchMode`：用于指定自定义点播回放模式。<br><br>      * `enablePlaybackSwitchBtn`：用于控制播放列表按钮的显示。<br><br>      * `enablePlaybackListPopup`：用于控制回放合集列表的显示。<br><br>      * `playbackMode`：用于指定回放合集列表的播放模式。更多信息，请参见[选项](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#b6fb0c34)。<br><br>   * 新增`playbackListBtn.click`事件，当点击回放合集按钮时触发。更多信息，请参见[SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#71bec5a0)。<br><br>   * 新增以下 API，用于自定义观看页回放合集列表。更多信息，请参见[API](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN)。<br><br>      * `showPlaybackListPopup()`<br><br>      * `hidePlaybackListPopup()`<br><br>      * `getPlayBackListInfo()`<br><br>      * `lockPlayBackVods()`<br><br>      * `unlockPlayBackVods()`<br><br>* 新增`preloadActivity()` API，用于预加载和缓存直播间数据，加速基于 feed 的房间创建。更多信息，请参见[API](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN)。 |


<span id="46cb2a55"></span>
## 2025年9月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-09\-18 |2.0.22 |**问题修复**<br><br>修复了部分问题。 |
|2025\-09\-05 |2.0.21 |**兼容性变更**<br><br>自 v2.0.21 起，集成 SDK 时，域名已由`https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm`变更为`https://res.bytepluscdn.com/obj/bp-console-fe-sg`。更多信息，请参见[集成方式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN#855885cc)。 |


<span id="0d3910db"></span>
## 2025年8月


|发布时间 |版本 |接口行为 |
|---|---|---|
|2025\-08\-28 |2.0.20 |**新功能**<br><br><br>* 礼物<br><br>   * 新增[giftPoint.result](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#4fa82edf)事件，当礼物积分被更新或观众主动查询礼物积分时触发。<br><br>   * 新增 gift.pointQuery 事件，用于查询观众的礼物积分。更多信息，请参见[SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#71bec5a0)。 |
|2025\-08\-12 |2.0.19 |新增参数`shareUrl`，允许为直播间设置自定义分享 URL。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。 |


<span id="7ab40088"></span>
## 2025年7月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-07\-15 |2.0.17 |**新功能**<br><br><br>* 礼物<br><br>   * 新增参数`disableSendGift`，用于指定当观众点击或轻触**Send**发送礼物时，是否禁用 BytePlus Live 的送礼逻辑。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>   * 新增[gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#d476ef36)事件，该事件在观众点击或轻触礼物时触发。<br><br>   * 新增[gift.sendError](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#83e8b67c)事件，该事件在观众送礼时因积分不足或请求异常导致错误发生时触发。你可以通过将`disableSendGift`的值设置为`true`并监听该事件，实现自定义逻辑。<br><br>   * 新增[gift.show](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#e862732b)事件，该事件在观众送礼时触发。<br><br>   * 新增`gift.send`事件，在你将`disableSendGift`的值设置为`true`且[gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#d476ef36)事件被触发后，用于发送指定数量的礼物。更多信息，请参见[SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#71bec5a0)。<br><br>* 商品<br><br>   * 新增参数`disabledShopCartClick`，用于指定当观众在移动设备观看页点击购物车图标时，是否禁用展示商品列表的功能。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>   * 新增[shopCart.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#7bd143bd)事件，该事件在移动设备观看页的购物车图标被点击时触发。你可以通过将`disabledShopCartClick`的值设置为`true`并监听该事件，实现自定义逻辑。 |
|2025\-07\-01 |2.0.16 |**已修复的问题**<br><br>修复了部分问题。 |


<span id="20ba9ed9"></span>
## 2025年5月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-05\-15 |2.0.15 |**新功能**<br><br>新增`pcuConfig`参数和[activity.pcu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#75c92017)事件。可通过上述内容自定义当所有直播间的峰值并发用户数（PCU）超过账号并发上限时显示的错误页面。更多信息，请参见[Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-ios-zh-CN#db59dce3)。 |


<span id="8a775a08"></span>
## 2025年3月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2025\-03\-19 |2.0.13 |**新功能**<br><br>评论输入框<br><br><br>* 新增`disabledCommentConfig`参数，用于禁用评论输入框并设置其占位文本。更多信息，请参见[选项](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN#b6fb0c34)。<br><br>* 新增`comment.disabled`事件。配置`disabledCommentConfig`参数的未开启状态和占位文本后，可以触发该事件以动态禁用或启用评论输入框。更多信息，请参见[Events](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#sdkeventsemit)。<br><br>* 新增对评论输入框未开启状态样式自定义的支持。更多信息，请参见[自定义未开启评论输入框的样式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-ios-zh-CN#86db69f2)。 |


<span id="3d235239"></span>
## 2024年12月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-12\-10 |2.0.11 |* **兼容性变更**<br><br>   参数值变更<br><br>   用于指定观看页默认语言的参数`defaultLang`，其繁体中文值由`zh-Hant`变更为`zh-hant`。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>* **优化**<br><br>   提升了表情显示速度。 |


<span id="be911f23"></span>
## 2024年10月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-10\-10 |2.0.6 |**新功能**<br><br>观看页多语言<br><br><br>* 新增对观看页以下语言的支持：<br><br>   * 泰语<br><br>   * 越南语<br><br>   * 阿拉伯语<br><br>   * 土耳其语<br><br>   * 西班牙语<br><br>   * 印尼语<br><br>   * 葡萄牙语<br><br>   * 俄语<br><br>* 新增参数`defaultLang`，用于配置观看页的默认语言。无论观众在 PC 端浏览器的默认语言或移动设备系统语言为何，页面将在观众进入直播间时设置为配置的默认语言。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>* 如果你在观看页有自己的语言切换按钮，可以先调用[getPageLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#35db7c0e)获取观看页支持的语言，再调用[switchLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#a58b37a7)切换到指定语言。 |


<span id="f2533834"></span>
## 2024年9月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-09\-12 |2.0.5 |优化了签到功能，包括将签到时长的单位由分钟改为秒，并将未按时签到的观众踢出。 |
|2024\-09\-05 |2.0.4 |修复了一些问题。 |


<span id="910cf611"></span>
## 2024年8月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-08\-23 |2.0.3 |新增支持在竖屏模式下自定义直播间图标的样式和背景色。更多信息，请参见[自定义图标的样式和背景色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-ios-zh-CN#1b8b0536)。 |
|2024\-08\-15 |2.0.2 |新增支持在横屏模式下移动端显示购物车图标。 |


<span id="87c57f2d"></span>
## 2024年7月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-07\-23 |2.0.1 |优化了预约直播流的逻辑。 |
|2024\-07\-09 |2.0.0 |优化了观看页的 UI 风格。 |


<span id="cf28c503"></span>
## 2024年6月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-06\-24 |1.3.8 |* 导入 CSS 和 JS 资源时，移除了 URL 中 `byteplus` 跟在 `mobile/` 或 `pc/` 后的部分。更多信息，请参见[集成方式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-web-zh-CN#855885cc)。<br><br>* 修复了一些问题。 |
|2024\-06\-07 |1.3.3 |新增支持超低延迟功能。 |
|2024\-06\-06 |1.3.2 |修复了一些问题。 |


<span id="990338d3"></span>
## 2024年5月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-05\-10 |1.3.1 |* 新增参数`mobileGesture`、`showLikeInPlayer`、`disableLotteryTicketRedirect`、`extra`、`disableRotateFullscreen`、`disableLivePauseButton` 和 `loginInToThumbUp`。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>* 删除参数`isBytePlus`、`playerCustomLoading` 和 `unloginIcon`。<br><br>* 新增事件[lotteryTicket.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#e290813e)、[player.vodConfigChange](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#a87308eb)、[menu.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#93a24cfc) 和 [thumbs.click](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#750ccd04)。<br><br>* 新增 API [getVodPlayInfo()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#cb44cfa8)。 |


<span id="7234a4ad"></span>
## 2024年4月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-04\-29 |1.1.22 |优化了礼物打赏功能，包括：<br><br><br>* 调整了默认礼物。<br><br>* 优化了礼物特效。<br><br>* 现在观众可在直播间处于“直播”、“回放”或“已结束”状态时发送礼物。此前仅支持在“直播”状态下发送礼物。 |
|2024\-04\-09 |1.1.21 |* 新增参数`closePlayVideoFocus`，用于指定观众进入观看页时，是否自动滚动到正在播放预告、回放或直播视频的播放器。更多信息，请参见[Web 观播 SDK：参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-the-viewer-sdk-for-web-zh-CN)。<br><br>* 新增[lines.current](https://docs.byteplus.com/docs/byteplus-livesaas/docs-bdlliveengine-zh-CN#96c0ddb3)事件，当观众点击“直播”状态的直播源或“回放”状态的视频时触发。<br><br>* 新增[switchChannel()](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-the-viewer-sdk-for-web-zh-CN#88ab1ee1)API，可切换到指定的“直播”状态直播源或“回放”状态视频。 |


<span id="f3d67bbd"></span>
## 2024年1月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2024\-01\-18 |1.1.14 |新增支持在移动端竖屏模式下显示播放器 Logo。 |


<span id="87c920be"></span>
## 2023年12月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-12\-14 |1.1.13 |新增支持在移动端横屏模式下显示播放器 Logo。 |


<span id="0c01bcd6"></span>
## 2023年11月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-11\-30 |1.1.12 |新增支持在移动端横屏和竖屏模式下显示不同的封面。 |
|2023\-11\-16 |1.1.11 |* 优化了观看页的投票样式。<br><br>* 新增支持将 BytePlus Live 控制台的配色同步到竖屏模式下的直播间。 |


<span id="9b0800a3"></span>
## 2023年10月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-10\-16 |1.1.10 |修复了一些问题。 |
|2023\-10\-10 |1.1.8 |修复了一些问题。 |


<span id="e6d88c3f"></span>
## 2023年8月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-08\-24 |1.1.7 |修复了一些问题。 |


<span id="db2ebae4"></span>
## 2023年7月


|发布日期 |版本 |接口行为 |
|---|---|---|
|2023\-07\-31 |1.1.6 |修复了一些问题。 |
|2023\-07\-20 |1.1.5 |修复了一些问题。 |
