---
title: "Web Viewer SDK release notes"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-changelog"
---

Find all changes to the Web Viewer SDK here.

<span id="d7e0d7a1"></span>
## August 2026


|Release Date |Version |Description |
|---|---|---|
|2026\-08\-12 |2.0.31 |**Improvements**<br><br>Updated CSS styles. |


<span id="july-2026"></span>
## July 2026


|Release Date |Version |Description |
|---|---|---|
|2026\-07\-23 |2.0.30 |**Improvements**<br><br><br>* Added support for the product card multi\-environment direct URL feature.<br><br>* Added support for configuring **Like** and **Popular display** in live templates.<br><br><br>**Compatibility changes**<br><br>Since v2.0.30, when integrating the SDK, the domain has been changed from `https://res.bytepluscdn.com/obj/bp-console-fe-sg` to `https://res.gcloudcache.com/bp-fe`. For more information, see [Integration method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#855885cc). |


<span id="0bc95836"></span>
## February 2026


|Release Date |Version |Description |
|---|---|---|
|2026\-02\-02 |2.0.27\-beta.4 |**Issues fixed**<br><br>Fixed some issues. |


<span id="8e7d0d0f"></span>
## January 2026


|Release Date |Version |Description |
|---|---|---|
|2026\-01\-12 |2.0.27\-beta.2 (For player\-only integration) and 2.0.27\-beta.3 |This release includes internal improvements. There are no functional changes, and existing usage is not affected.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">To ensure service stability and continued support, please update to the latest version. For details, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#7f20b494">Step 1: Import CSS and JS resources</a>.</div><br> |
|2026\-01\-06 |2.0.27 |**Issues fixed**<br><br>Fixed some issues. |


<span id="67d0f65a"></span>
## December 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-12\-10 |2.0.25 |**Improvements**<br><br><br>* Popularity display<br><br>   * Added the parameter `disablePopularityShow`, which specifies whether to disable the display of the number of viewers on the viewing page. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>   * Added the `popularity.configChange` event, which is triggered when the number of viewers shown on the viewing page changes. For more information, see [popularity.configChange](https://docs.byteplus.com/docs/byteplus-livesaas/events#9c17df67).<br><br>* Products<br><br>   * Added the parameter `shopCartIcon`, which specifies the shopping cart icon configuration. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>   * Added the parameter `disabledShowExplainCard`, which specifies whether to disable floating product cards on the viewing page when the product is featured. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>   * Added the `floatingCard.update` event, which is triggered when a floating product card is updated. For more information, see [floatingCard.update](https://docs.byteplus.com/docs/byteplus-livesaas/events#163fd7d0). |


<span id="3cc7c0a1"></span>
## November 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-11\-12 |2.0.24 |**Improvements**<br><br>Added support for additional languages for the `defaultLang` parameter. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br><br>* Tagalog<br><br>* Khmer<br><br>* Lao<br><br>* Burmese<br><br>* Malay<br><br>* Hindi<br><br>* French<br><br>* German<br><br>* Italian |


<span id="62f42b28"></span>
## October 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-10\-16 |2.0.23 |**New features**<br><br><br>* Products<br><br>   * Added the [ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/type-definitions#fe534689) type.<br><br>   * Added the `card.configChange` event, which is triggered when the configuration of a product card changes. For more information, see [card.configChange](https://docs.byteplus.com/docs/byteplus-livesaas/events#7f70dfa5).<br><br>   * Added the following APIs. For more information, see [API](https://docs.byteplus.com/docs/byteplus-livesaas/api).<br><br>      * `getProductList()`<br><br>      * `updateProductInfo()`<br><br>* Playback list<br><br>   * Added the following parameters:<br><br>      * `vodSwitchMode`: Specifies a custom VOD playback mode.<br><br>      * `enablePlaybackSwitchBtn`: Controls the visibility of the playlist button.<br><br>      * `enablePlaybackListPopup`: Controls the visibility of the playback collection list.<br><br>      * `playbackMode`: Specifies the playback mode for the playback collection list. For more information, see [Options](https://docs.byteplus.com/docs/byteplus-livesaas/parameters#b6fb0c34).<br><br>   * Added the `playbackListBtn.click` event, which is triggered when the playback collection button is clicked. For more information, see [SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/events#71bec5a0).<br><br>   * Added the following APIs for customizing the playback collection list on the viewing page. For more information, see [API](https://docs.byteplus.com/docs/byteplus-livesaas/api).<br><br>      * `showPlaybackListPopup()`<br><br>      * `hidePlaybackListPopup()`<br><br>      * `getPlayBackListInfo()`<br><br>      * `lockPlayBackVods()`<br><br>      * `unlockPlayBackVods()`<br><br>* Added the `preloadActivity()` API for preloading and caching live room data to accelerate room creation during feed\-based transitions. For more information, see [API](https://docs.byteplus.com/docs/byteplus-livesaas/api). |


<span id="46cb2a55"></span>
## September 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-09\-18 |2.0.22 |**Issues fixed**<br><br>Fixed some issues. |
|2025\-09\-05 |2.0.21 |**Compatibility changes**<br><br>Since v2.0.21, when integrating the SDK, the domain has been changed from `https://mediaservice-fe.bytepluscdn.com/obj/vcloud-fe-sgcomm` to `https://res.bytepluscdn.com/obj/bp-console-fe-sg`. For more information, see [Integration method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#855885cc). |


<span id="0d3910db"></span>
## August 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-08\-28 |2.0.20 |**New features**<br><br><br>* Gifts<br><br>   * Added the [giftPoint.result](https://docs.byteplus.com/docs/byteplus-livesaas/events#4fa82edf) event, which is triggered when the gift point is updated or viewers actively query the gift point.<br><br>   * Added the gift.pointQuery event, which is used to query the gift point of the viewer. For more information, see [SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/events#71bec5a0). |
|2025\-08\-12 |2.0.19 |Added the parameter `shareUrl`, which allows you to set a custom share URL for the live room. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters). |


<span id="7ab40088"></span>
## July 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-07\-15 |2.0.17 |**New features**<br><br><br>* Gifts<br><br>   * Added the parameter `disableSendGift`, which specifies whether to disable BytePlus Live's gift sending logic when viewers click or tap **Send** to send gifts. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>   * Added the [gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#d476ef36) event, which is triggered when a gift is clicked or tapped by a viewer.<br><br>   * Added the [gift.sendError](https://docs.byteplus.com/docs/byteplus-livesaas/events#83e8b67c) event, which is triggered when an error occurs due to insufficient points or a request exception while viewers send gifts. You can implement your own logic by setting the value of `disableSendGift` to `true` and listening to this event.<br><br>   * Added the [gift.show](https://docs.byteplus.com/docs/byteplus-livesaas/events#e862732b) event, which is triggered when viewers send gifts.<br><br>   * Added the `gift.send` event, which is used to send a specific number of gifts after you set the value of `disableSendGift` to `true` and the [gift.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#d476ef36) event is triggered. For more information, see [SDKEventsEmit](https://docs.byteplus.com/docs/byteplus-livesaas/events#71bec5a0).<br><br>* Products<br><br>   * Added the parameter `disabledShopCartClick`, which specifies whether to disable the feature of displaying the product list when viewers tap the shopping cart icon on the viewing page of mobile devices. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>   * Added the [shopCart.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#7bd143bd) event, which is triggered when the shopping cart icon on the viewing page of mobile devices is tapped. You can implement your own logic by setting the value of `disabledShopCartClick` to `true` and listening to this event. |
|2025\-07\-01 |2.0.16 |**Issues fixed**<br><br>Fixed some issues. |


<span id="20ba9ed9"></span>
## May 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-05\-15 |2.0.15 |**New features**<br><br>Added the `pcuConfig` parameter and the [activity.pcu](https://docs.byteplus.com/docs/byteplus-livesaas/events#75c92017) event. Use these to customize the error page that displays when the peak concurrent users (PCU) across all your live rooms exceeds the account's concurrency limit. For more information, see [Customizing the error page](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#db59dce3). |


<span id="8a775a08"></span>
## March 2025


|Release Date |Version |Description |
|---|---|---|
|2025\-03\-19 |2.0.13 |**New features**<br><br>Comment text box<br><br><br>* Added the `disabledCommentConfig` parameter to disable the comment text box and set its placeholder text. For more information, see [Options](https://docs.byteplus.com/docs/byteplus-livesaas/parameters#b6fb0c34).<br><br>* Added the `comment.disabled` event. After configuring the disabled state and placeholder text with the `disabledCommentConfig` parameter, you can emit this event to dynamically disable or enable the comment text box. For more information, see [Events](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#sdkeventsemit).<br><br>* Added support for customizing the style of the disabled comment text box. For more information, see [Customizing the style of the disabled comment text box](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#86db69f2). |


<span id="3d235239"></span>
## December 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-12\-10 |2.0.11 |* **Compatibility changes**<br><br>   Parameter value change<br><br>   The parameter `defaultLang`, used for specifying the default language of the viewing page, has its Traditional Chinese value changed from `zh-Hant` to `zh-hant`. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>* **Improvements**<br><br>   Improved the emoji display speed. |


<span id="be911f23"></span>
## October 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-10\-10 |2.0.6 |**New features**<br><br>Multiple languages on the viewing page<br><br><br>* Added support for the following languages on the viewing page:<br><br>   * Thai<br><br>   * Vietnamese<br><br>   * Arabic<br><br>   * Turkish<br><br>   * Spanish<br><br>   * Indonesian<br><br>   * Portuguese<br><br>   * Russian<br><br>* Added the parameter `defaultLang` to configure the default language for the viewing page. The page will be set to the configured default language when viewers join the live room, regardless of their browsers' default language on PCs or their system language on mobile devices. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>* If you have your own button for switching languages on the viewing page, you can first call [getPageLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/api#35db7c0e) to get the languages supported by the viewing page and then call [switchLanguage()](https://docs.byteplus.com/docs/byteplus-livesaas/api#a58b37a7) to switch to the specified language. |


<span id="f2533834"></span>
## September 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-09\-12 |2.0.5 |Optimized the check\-in feature, including changing the unit of check\-in duration from minutes to seconds and kicking out viewers who fail to check in on time. |
|2024\-09\-05 |2.0.4 |Fixed some issues. |


<span id="910cf611"></span>
## August 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-08\-23 |2.0.3 |Added support for customizing the style and background color of icons in live rooms in portrait mode. For more information, see [Customizing the style and background color of icons in live rooms in portrait mode](https://docs.byteplus.com/docs/byteplus-livesaas/feature-implementation#1b8b0536). |
|2024\-08\-15 |2.0.2 |Added support for displaying the shopping cart icon on mobile devices in landscape mode. |


<span id="87c57f2d"></span>
## July 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-07\-23 |2.0.1 |Optimized the logic for booking a live stream. |
|2024\-07\-09 |2.0.0 |Optimized the UI style on the viewing page. |


<span id="cf28c503"></span>
## June 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-06\-24 |1.3.8 |* Removed `byteplus` following `mobile/` or `pc/` from the URL when importing CSS and JS resources. For more information, see [Integration method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk#855885cc).<br><br>* Fixed some issues. |
|2024\-06\-07 |1.3.3 |Added support for the ultra\-low latency feature. |
|2024\-06\-06 |1.3.2 |Fixed some issues. |


<span id="990338d3"></span>
## May 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-05\-10 |1.3.1 |* Added parameters `mobileGesture`, `showLikeInPlayer`, `disableLotteryTicketRedirect`, `extra`, `disableRotateFullscreen`, `disableLivePauseButton`, and `loginInToThumbUp`. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>* Deleted parameters `isBytePlus`, `playerCustomLoading`, and `unloginIcon`.<br><br>* Added the events [lotteryTicket.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#e290813e), [player.vodConfigChange](https://docs.byteplus.com/docs/byteplus-livesaas/events#a87308eb), [menu.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#93a24cfc), and [thumbs.click](https://docs.byteplus.com/docs/byteplus-livesaas/events#750ccd04).<br><br>* Added the API [getVodPlayInfo()](https://docs.byteplus.com/docs/byteplus-livesaas/api#cb44cfa8). |


<span id="7234a4ad"></span>
## April 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-04\-29 |1.1.22 |Optimized the gift rewards feature, including:<br><br><br>* Adjusted the default gifts.<br><br>* Improved the gift effects.<br><br>* Viewers can now send gifts when a live room is in the 'Live', 'Playback', or 'Over' status. Previously, this was only possible in the 'Live' status. |
|2024\-04\-09 |1.1.21 |* Added the parameter `closePlayVideoFocus` to specify whether to automatically scroll to the player that is playing a preview, playback, or live video when viewers enter the viewing page. For more information, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).<br><br>* Added the [lines.current](https://docs.byteplus.com/docs/byteplus-livesaas/events#96c0ddb3) event, which is triggered when a viewer clicks a live source (in 'Live' status) or a playback video (in 'Playback' status).<br><br>* Added the [switchChannel()](https://docs.byteplus.com/docs/byteplus-livesaas/api#88ab1ee1) API, which switches to a specified live source (in 'Live' status) or a specified playback video (in 'Playback' status). |


<span id="f3d67bbd"></span>
## January 2024


|Release Date |Version |Description |
|---|---|---|
|2024\-01\-18 |1.1.14 |Added support for displaying the player logo in portrait mode on mobile devices. |


<span id="87c920be"></span>
## December 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-12\-14 |1.1.13 |Added support for displaying the player logo in landscape mode on mobile devices. |


<span id="0c01bcd6"></span>
## November 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-11\-30 |1.1.12 |Added support for displaying different covers for landscape and portrait modes on mobile devices. |
|2023\-11\-16 |1.1.11 |* Optimized the voting style on the viewing page.<br><br>* Added support for synchronizing color configurations from the BytePlus Live console to live rooms in portrait mode. |


<span id="9b0800a3"></span>
## October 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-10\-16 |1.1.10 |Fixed some issues. |
|2023\-10\-10 |1.1.8 |Fixed some issues. |


<span id="e6d88c3f"></span>
## August 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-08\-24 |1.1.7 |Fixed some issues. |


<span id="db2ebae4"></span>
## July 2023


|Release Date |Version |Description |
|---|---|---|
|2023\-07\-31 |1.1.6 |Fixed some issues. |
|2023\-07\-20 |1.1.5 |Fixed some issues. |
