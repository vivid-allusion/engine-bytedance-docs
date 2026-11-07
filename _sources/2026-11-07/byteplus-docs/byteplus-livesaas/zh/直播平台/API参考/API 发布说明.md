---
title: "API 发布说明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-release-notes-zh-CN"
---

BytePlus Live API 发布说明为所有 API 和回调更新提供全面且按时间顺序记录的日志。您可以使用本文档跟踪新功能、重大变更和增强项，确保您的应用保持兼容并及时更新。

<span id="july-2026"></span>
## 2026年7月


|API/回调 |接口行为 |发布日期 |
|---|---|---|
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN) |新增`UAInfo`和`DirectUrls`参数，以支持商品卡片的多环境直达链接功能。 |2026\-07\-23 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN) |新增`UAInfo`和`DirectUrls`参数，以支持商品卡片的多环境直达链接功能。 |2026\-07\-23 |
|BytePlus Live API Endpoint |支持将 BytePlus Live API 的推荐 Endpoint 更新为 `https://livesaas.byteplusapi.com`。原 Endpoint `https://open.byteplusapi.com` 仍可继续使用。 |2026\-07\-10 |


<span id="april-2026"></span>
## 2026年4月


|API/回调 |接口行为 |发布日期 |
|---|---|---|
|[GetVoteListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI-zh-CN) |调用`GetVoteListAPI`，获取指定直播间的投票配置信息。 |2026\-04\-01 |
|[GetVoteStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-CN) |调用`GetVoteStatisticsAPI`，获取直播间的投票数据。 |2026\-04\-01 |
|[UpdatePresenterAwardConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig-zh-CN) |调用`UpdatePresenterAwardConfigAPI`，为直播间新增、更新或删除实时抽奖。 |2026\-04\-01 |
|[ListAwardConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-CN) |调用`ListAwardConfigsAPI`，获取抽奖的配置信息。 |2026\-04\-01 |
|[SendAward](https://docs.byteplus.com/docs/byteplus-livesaas/SendAward-zh-CN) |调用`SendAward`，在直播间发起实时抽奖。 |2026\-04\-01 |
|[WithdrawAward](https://docs.byteplus.com/docs/byteplus-livesaas/WithdrawAward-zh-CN) |调用`WithdrawAward`，撤回直播间的实时抽奖。注意，已撤回的抽奖无法再次发送或更新。 |2026\-04\-01 |
|[UpdateActivityQuizConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-CN) |调用`UpdateActivityQuizConfigAPI`，更新指定直播间未发送答题的配置信息。 |2026\-04\-01 |
|[ListActivityQuizConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-CN) |调用`ListActivityQuizConfigsAPI`，获取指定直播间的答题配置信息。 |2026\-04\-01 |
|[ListQuizStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-CN) |调用`ListQuizStatisticsAPI`，分页获取答题及其互动数据列表。数据包括指定直播间的参与人数、答对人数及其他相关信息。 |2026\-04\-01 |
|[GetQuizDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI-zh-CN) |调用`GetQuizDataAPI`，获取指定直播间某次答题的详细信息。包括参与人数、答对人数及各选项内容。 |2026\-04\-01 |
|[GetCheckInListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI-zh-CN) |调用`GetCheckInListAPI`，获取指定直播间全部签到或指定签到信息，包括签到ID、参与人数、签到时长等。 |2026\-04\-01 |
|[GetCheckInRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-CN) |调用`GetCheckInRecordStatisticsAPI`，获取指定直播间的签到记录。 |2026\-04\-01 |
|[UpdateFloatingAdvertisementAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateFloatingAdvertisement-zh-CN) |调用`UpdateFloatingAdvertisementAPI`，更新指定直播间浮窗广告的状态、链接及其他配置信息。 |2026\-04\-01 |
|[GetTaskAwardItemListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-CN) |调用`GetTaskAwardItemListAPI`，获取直播间已发送的基于观看时长抽奖的奖品列表。 |2026\-04\-01 |
|[ListAwardRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-CN) |调用`ListAwardRecordStatisticsAPI`，获取指定直播间某次抽奖的参与或中奖观众列表。 |2026\-04\-01 |
|[ActivityAwardInfoCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityAwardInfoCallBack-zh-CN) |当发起实时抽奖时，BytePlus Live会向你的自定义URL发送POST请求，并在请求体中传递直播间ID、奖品信息、中奖者信息等数据。 |2026\-04\-01 |
|[ActivityTaskAwardInfoCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack-zh-CN) |当用户参与基于观看时长的抽奖并中奖时，BytePlus Live会向你的自定义URL发送POST请求，并在请求体中传递直播间ID、奖品信息及中奖者信息。 |2026\-04\-01 |
|[CheckinStatusModifyCallback](https://docs.byteplus.com/docs/byteplus-livesaas/CheckinStatusModifyCallback-zh-CN) |当发生签到事件（如签到创建、删除、发送或截止时间到达）时，BytePlus Live会向你的自定义URL发送POST请求，并在请求体中传递直播间ID及更新后的签到状态。 |2026\-04\-01 |


<span id="january-2026"></span>
## 2026年1月


|API/回调 |接口行为 |发布日期 |
|---|---|---|
|[ActivityAutoReplayCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityautoreplaycallback-zh-CN) |新增参数`LiveStartTime`和`LiveEndTime`，用于展示与回放视频对应的直播流的开始时间和结束时间。 |2026\-01\-27 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi-zh-CN) |该API已弃用。如需帮助，请联系技术支持。 |2026\-01\-14 |


<span id="november-2025"></span>
## 2025年11月


|API/回调 |接口行为 |发布日期 |
|---|---|---|
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |为`LanguageType`新增以下取值：<br><br><br>* `13`：塔加拉语。<br><br>* `14`：高棉语。<br><br>* `15`：老挝语。<br><br>* `16`：缅甸语。<br><br>* `17`：马来语。<br><br>* `18`：印地语。<br><br>* `19`：法语。<br><br>* `20`：德语。<br><br>* `21`：意大利语。 |2025\-11\-12 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) | | |
|[UpdateAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateawarditem) |支持管理账号下奖品，包括添加、更新、删除及获取奖品信息。 |2025\-11\-12 |
|[GetAwardItemList](https://docs.byteplus.com/en/docs/byteplus-livesaas/getawarditemlist) | |2025\-11\-12 |
|[DeleteAwardItem](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteawarditem) | |2025\-11\-12 |


<span id="august-2025"></span>
## 2025年8月


|API/Callback |接口行为 |发布日期 |
|---|---|---|
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN) |商品卡片中`Title`和`Remark`的字符限制提升至3315。 |2025\-08\-12 |


<span id="july-2025"></span>
## 2025年7月


|API/Callback |接口行为 |发布日期 |
|---|---|---|
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |* 新增请求参数`FollowerUserName`，用于获取由指定账号创建的直播间。<br><br>* 新增返回调用结果参数`VerticalCoverImage`和`SubAccountName`，用于获取直播间竖屏模式下的封面图URL及创建直播间所用账号。 |2025\-07\-17 |
|[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) |支持获取BytePlus Live中指定账号的STS签名。该签名允许你通过iframe将BytePlus Live控制台的功能模块嵌入到你的页面中。 |2025\-07\-15 |
|[ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi) |支持获取媒体库下视频库或临时存储的视频信息，包括视频ID和名称。 |2025\-07\-15 |
|[TempToMediaActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/temptomediaactivitymediaapi) |支持将临时存储的视频转移到视频库指定分类进行永久存储。 |2025\-07\-15 |
|[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree) |支持获取账号下默认分类或指定分类及其子分类的信息。 |2025\-07\-15 |


<span id="february-2025"></span>
## 2025年2月


|API/Callback |接口行为 |发布日期 |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |新增请求参数`SortBy`、`SortOrder`和`SiteTagNews`，可根据指定规则和顺序对直播间进行排序，并根据分类标签值筛选直播间。 |2025\-02\-25 |
|[ExplainProduct](https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct) |支持将商品固定在菜单顶部，并以悬浮窗形式展示。也可取消固定商品，使其恢复至原始位置并移除悬浮窗展示。 |2025\-02\-20 |
|[ActivityExplainProductCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityexplainproductcallBack-zh-CN) |新增回调`ActivityExplainProductCallBack`，当直播间中的商品处于以下任一情况时触发：<br><br><br>* 固定在菜单顶部，并在观看页以悬浮窗形式展示。<br><br>* 恢复至菜单下原始位置，并不再在观看页以悬浮窗形式展示。 |2025\-02\-20 |


<span id="january-2025"></span>
## 2025年1月


|API/Callback |接口行为 |发布日期 |
|---|---|---|
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) |新增请求参数`ExternalPlatformId`，可根据外部平台ID筛选主播账号。 |2025\-01\-16 |


<span id="december-2024"></span>
## 2024年12月


|API/Callback |接口行为 |发布日期 |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |新增返回调用结果参数`SiteTags`，用于获取每个直播间的分类标签列表。 |2024\-12\-05 |


<span id="november-2024"></span>
## 2024年11月


|API/Callback |接口行为 |发布日期 |
|---|---|---|
|[ListActivityProductCommons](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons) |支持一次性获取一个或多个直播间的商品库信息。 |2024\-11\-21 |
|[UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) |支持添加主播账号、更新已有主播账号信息、删除主播账号，以及获取账号下主播账号的信息。 |2024\-11\-07 |
|[DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) | |2024\-11\-07 |
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) | |2024\-11\-07 |
|[UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) |支持更新与直播间关联的主播账号，并配置是否在直播间启用账号设置功能。 |2024\-11\-07 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |新增返回调用结果参数`IsFollowEnable`，用于指示观众是否允许在观看页关注主播。 |2024\-11\-07 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |新增请求参数`SortBy`和`SortOrder`，用于设置返回直播间的排序规则和顺序。 |2024\-11\-07 |


<span id="october-2024"></span>
## 2024年10月


|API/回调 |接口行为 |发布时间 |
|---|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN) |新增请求参数IsBeginLiveEnable，用于指定是否开启直播流开播时间功能。 |2024\-10\-10 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi-zh-CN) |新增返回调用结果参数IsBeginLiveEnable，用于指示直播流开播时间功能是否已开启。 |2024\-10\-10 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |* 新增请求参数IsBeginLiveEnable，用于指定是否开启直播流开播时间功能。<br><br>* 新增请求参数`IsInteractiveEnable`，用于指定是否允许主播仅在网页端直播页面管理指定互动工具。<br><br>* 新增请求参数`InteractiveShowSetting`，用于指定主播可在网页端直播页面管理的互动工具。 |2024\-10\-10 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |* 新增返回调用结果参数`IsBeginLiveEnable`，用于指示直播流开播时间功能是否已开启。功能开启后，仅可在指定开播时间后开播。<br><br>* 新增返回调用结果参数`IsInteractiveEnable`，用于指示主播是否仅可在网页端直播页面管理指定互动工具。<br><br>* 新增返回调用结果参数`InteractiveShowSetting`，用于指示主播可在网页端直播页面管理的互动工具。 |2024\-10\-10 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi-zh-CN) |新增错误码`200027`。 |2024\-10\-10 |
|[ResumeLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-resumelivestreamapi-zh-CN) |新增错误码`200027`。 |2024\-10\-10 |


<span id="september-2024"></span>
## 2024年9月


|API/回调 |接口行为 |发布时间 |
|---|---|---|
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |支持获取BytePlus账号下所有已存在直播间的基本信息，包括IAM用户创建的直播间，包含封面图、虚拟热度、主播账号及创建时间。 |2024\-09\-26 |


<span id="august-2024"></span>
## 2024年8月


|API/回调 |接口行为 |发布时间 |
|---|---|---|
|[CreateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/createactivityproductlibrary) |支持在指定直播间新增一个或多个商品库。随后可在直播间从Shopify商品库或自有系统商品库获取商品。 |2024\-08\-15 |
|[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) |支持在指定直播间更新商品库信息，包括商品库名称、类型及配置。 |2024\-08\-15 |
|[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) |支持在指定直播间删除一个或多个商品库。 |2024\-08\-15 |
|[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig) |支持获取指定直播间内商品配置，包括商品库的ID、名称、类型及配置。 |2024\-08\-15 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN) |新增返回调用结果参数`ExternalProductId`。 |2024\-08\-15 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN) |新增请求参数`ExternalProductId`。 |2024\-08\-15 |


<span id="july-2024"></span>
## 2024年7月


|API/回调 |接口行为 |发布时间 |
|---|---|---|
|[ActivityClickReservationCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityclickreservationcallBack-zh-CN) |新增回调`ActivityClickReservationCallBack`。 |2024\-07\-23 |
|[GetActivityReservationAPIV2](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2) |新增API`GetActivityReservationAPIV2`。 |2024\-07\-23 |


<span id="june-2024"></span>
## 2024年6月


|API/回调 |接口行为 |发布时间 |
|---|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN) |新增请求参数`EndTime`和`IsAutoEndEnable`。 |2024\-06\-25 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |新增请求参数`EndTime`和`IsAutoEndEnable`。 |2024\-06\-25 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |新增返回调用结果参数`EndTime`和`IsAutoEndEnable`。 |2024\-06\-25 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi-zh-CN) |新增返回调用结果参数`EndTime`和`IsAutoEndEnable`。 |2024\-06\-25 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi-zh-CN) |将`ForbidTime`参数的最大值和默认值从7 × 24 × 60 × 60修改为31 × 24 × 60 × 60。 |2024\-06\-12 |
|[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN) |支持在网页端直播页面获取已上传文件列表，或在指定直播间的互动工具菜单下获取发送的文件列表。 |2024\-06\-06 |
|[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-CN) |支持获取通过网页浏览器在直播页面上传或在指定直播间互动工具菜单下发送的文件下载 URL。 |2024\-06\-06 |
|[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-CN) |支持获取问答菜单下的问题。 |2024\-06\-06 |
|[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-CN) |支持获取问答菜单下指定问题的回复。 |2024\-06\-06 |
|[ActivityQuestionChatCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityquestionchatcallback-zh-CN) |当用户在问答菜单下发送问题时，BytePlus Live 会向您的自定义 URL 发送 POST 请求，并将问题数据放在请求体中。 |2024\-06\-06 |


<span id="may-2024"></span>
## 2024年5月


|API/回调 |接口行为 |发布时间 |
|---|---|---|
|[GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-CN) |支持获取直播间直播页面的 URL，允许主播通过网页浏览器开播，无需登录。返回的 URL 会在指定时间后失效。 |2024\-05\-31 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |新增返回调用结果参数`IsVideoChatDisplayed`、`IsSharedAddressDisplayed`和`IsReleaseNoticeDisplayed`。 |2024\-05\-31 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |新增请求参数`IsVideoChatDisplayed`、`IsSharedAddressDisplayed`和`IsReleaseNoticeDisplayed`。 |2024\-05\-31 |
|[DelActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-delactivityantidirtapi-zh-CN) |新增请求参数`DeleteAll`。 |2024\-05\-10 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |新增请求参数`HostAccountId`、`HostAccountName`和`LiveMode`，以及返回调用结果参数`HostAccountId`、`HostAccountName`和`LiveMode`。 |2024\-05\-10 |
|[ListUserBehaviorDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-CN) |新增请求参数`ScrollId`，以及返回调用结果参数`ScrollId`和`SilenceStatus`。 |2024\-05\-10 |
|[PollingChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-CN) |新增返回调用结果参数`IsTipOff`。 |2024\-05\-10 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN) |新增返回调用结果参数`ProductsPosition`和`DefaultRedirectImage`。 |2024\-05\-10 |
|[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN) |新增请求参数`InviteToken`、`AvatarUrl`和`CustomComment`。 |2024\-05\-10 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |新增请求参数`IsReservationSmsEnable`。 |2024\-05\-10 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |新增返回调用结果参数`IsReservationSmsEnable`。 |2024\-05\-10 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi-zh-CN) |新增返回调用结果参数`VerticalCoverImage`和`LiveMode`。 |2024\-05\-10 |
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN) |新增请求参数`LiveMode`。 |2024\-05\-10 |


<span id="february-2024"></span>
## 2024年2月


|**API/回调** |**接口行为** |**发布时间** |
|---|---|---|
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN) |新增返回调用结果参数`TagName`。 |2024\-02\-29 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN) |新增请求参数`TagName`。 |2024\-02\-29 |
|[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-CN) |支持获取 BytePlus 账号下直播间模版列表。 |2024\-02\-29 |


<span id="january-2024"></span>
## 2024年1月


|**API/回调** |**接口行为** |**发布时间** |
|---|---|---|
|[GetActivityQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-CN) |支持在指定时间范围内获取某个直播间的直播流质量数据。 |2024\-01\-23 |
|[GetAccountQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-CN) |支持在指定时间范围内获取 BytePlus 账号下所有直播间的直播流质量数据。 |2024\-01\-23 |


<span id="november-2023"></span>
## 2023年11月


|**API/回调** |**接口行为** |**发布时间** |
|---|---|---|
|[UpdateBusinessAccountInfoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebusinessaccountinfoapi-zh-CN) |支持更新直播间内品牌账号信息。 |2023\-12\-21 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi-zh-CN) |支持获取直播间内品牌账号信息。 |2023\-12\-21 |
|[GetAccountDataByTimeIntervalAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi-zh-CN) |支持获取 BytePlus 账号下所有直播间的数据，包括累计观看次数和独立观众数。 |2023\-11\-30 |
|[ListActivityDetailAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-CN) |支持获取 BytePlus 账号下指定直播间的数据，包括累计直播时长和每位观众的平均观看时长。 |2023\-11\-30 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |新增请求参数`VerticalCoverImageUrl`。 |2023\-11\-30 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |新增返回调用结果参数`VerticalCoverImageUrl`。 |2023\-11\-30 |
