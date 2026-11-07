---
title: "API 列表"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-API-list-zh-CN"
---

要将 BytePlus Live 功能集成到您的应用中，您可以使用本全面的 API 参考文档。本文档按功能分类（如直播间、直播流和 Insights），列出了所有可用的 API，帮助您快速定位所需的具体接口。

<span id="live-rooms"></span>
## 直播间


|**API** |**接口行为** |
|---|---|
|[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN) |创建用于直播活动的直播间。 |
|[DeleteActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deleteactivityapi-zh-CN) |删除指定直播间。 |
|[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |获取你的 BytePlus 账号下所有现有直播间的基本信息。 |
|[UpdateActivityStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitystatusapi-zh-CN) |更新直播间的状态。你可以将直播间恢复到**预告**状态，锁定预告，或解锁预告。 |
|[UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-CN) |启动或停止从指定 URL 拉流到直播间。 |
|[GetActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityapi-zh-CN) |获取直播间的基本信息，如状态和观看页地址。 |
|[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN) |获取推流到直播间或从第三方平台拉流所需的信息。 |
|[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |获取直播间的基础配置，如背景图片和预告。 |
|[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |更新直播间的基础配置，如背景图片和预告。 |
|[UpdateLoopVideoAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideoapi-zh-CN) |编辑直播间的循环视频。 |
|[UpdateLoopVideoStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideostatusapi-zh-CN) |启用或禁用循环回放。 |
|[ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi-zh-CN) |禁止直播间中特定直播源的流。流被禁止后，观众将无法观看该流，且不会生成回放。 |
|[ResumeLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-resumelivestreamapi-zh-CN) |恢复直播间中特定直播源的被禁流。 |
|[GetLiveStreamForbidStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi-zh-CN) |检查直播间中指定直播源的流是否被禁播。 |
|[GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-CN) |获取你 BytePlus 账号下直播间模板列表。 |
|[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN) |获取在直播页面通过网页浏览器上传或通过互动工具菜单在指定直播间分享的文件列表。要获取文件的下载 URL，可使用返回调用结果中的文件 ID 调用 [GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-CN)。 |
|[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-CN) |获取在直播页面通过网页浏览器上传或通过互动工具菜单在指定直播间分享的文件下载 URL。 |
|[ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |获取你 BytePlus 账号及 IAM 用户下所有已存在直播间的基础信息，包括封面图、虚拟热度、主播账号和创建时间。 |


<span id="live-streaming"></span>
## 直播流


|**API** |**接口行为** |
|---|---|
|[GetTemporaryLoginTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettemporarylogintokenapi-zh-CN) |获取直播间的密钥，用于开播。 |
|[GetWebPushLiveClientAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getwebpushliveclientapi-zh-CN) |获取直播间直播页面的 URL，允许主播无需登录即可通过网页浏览器开播。 |
|[GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-CN) |获取直播间直播页面的 URL，允许主播无需登录即可通过网页浏览器开播。返回的 URL 在指定时间后失效。 |


<span id="playbacks"></span>
## 回放


|**API** |**接口行为** |
|---|---|
|[UploadReplayAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploadreplayapi-zh-CN) |绑定视频到直播间作为回放。操作前需先将视频上传至媒体库。 |
|[ListMediasAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listmediasapi-zh-CN) |获取当前直播间回放列表中的视频信息。 |
|[UpdateMediaOnlineStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatemediaonlinestatusapi-zh-CN) |发布、撤回或移除回放。操作前需先上传视频作为回放。 |
|[DeleteMediaAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletemediaapi-zh-CN) |从直播间回放列表删除一个视频。 |
|[DeleteMediasAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletemediasapi-zh-CN) |一次最多从直播间回放列表删除 100 个视频。 |


<span id="sensitive-words"></span>
## 敏感词


|**API** |**接口行为** |
|---|---|
|[AddActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addactivityantidirtapi-zh-CN) |向直播间添加敏感词。 |
|[GetActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityantidirtapi-zh-CN) |获取直播间已配置的敏感词列表。你可以选择获取所有敏感词或包含指定关键词的敏感词。 |
|[DelActivityAntidirtAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-delactivityantidirtapi-zh-CN) |从直播间删除敏感词。 |


<span id="insights"></span>
## Insights


|**API** |**接口行为** |
|---|---|
|[GetPageWatchDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi-zh-CN) |获取某个直播间的基础数据，包括页面浏览量、独立页面浏览量、总观看时长等。数据每五分钟更新一次。 |
|[GetAdvertisementDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi-zh-CN) |获取某个直播间的营销数据。 |
|[ListUserBehaviorDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listuserbehaviordataapi-zh-CN) |获取某个直播间的观众行为数据。 |
|[ListQuestionnaireAnswerDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi-zh-CN) |获取某个直播间问卷的答卷数据（最多可查询 10,000 条结果）。 |
|[ListQuestionnaireDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listquestionnairedataapi-zh-CN) |获取某个直播间的问卷数据。 |
|[ListAnActivityStartAndEndTimeAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi-zh-CN) |获取某个直播间每场直播流的开始和结束时间。 |
|[GetAccountDataByTimeIntervalAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi-zh-CN) |获取你 BytePlus 账号下所有直播间的数据，包括累计观看次数和独立观众数。 |
|[ListActivityDetailAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-CN) |获取你 BytePlus 账号下指定直播间的数据，包括总直播时长和平均观看时长。 |
|[GetActivityQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-CN) |获取指定时间范围内某个直播间的直播质量数据。 |
|[GetAccountQualityDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-CN) |获取指定时间范围内你 BytePlus 账号下所有直播间的直播质量数据。 |
|[GetActivityReservationAPIV2](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityreservationapiv2) |获取指定直播间的预约信息。 |


<span id="comments"></span>
## 评论


|**API** |**接口行为** |
|---|---|
|[PresenterChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-presenterchatapi-zh-CN) |以主播身份在直播间发送评论。 |
|[PollingChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-CN) |获取直播间的评论。 |
|[GetHotChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gethotchatapi-zh-CN) |获取直播间的优质评论。BytePlus Live 会将获得较多点赞的评论识别为优质评论。 |
|[GetTopChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-gettopchatapi-zh-CN) |获取置顶于聊天区域的评论。 |
|[DeleteChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletechatapi-zh-CN) |删除直播间中的部分评论。 |
|[LikeChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-likechatapi-zh-CN) |点赞评论。 |
|[TopChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-topchatapi-zh-CN) |将评论置顶于聊天区域。 |
|[EmptyChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-emptychatapi-zh-CN) |清空直播间的所有评论。 |
|[UpdateChatReviewStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatechatreviewstatusapi-zh-CN) |开启或关闭评论审核功能。 |
|[ConfirmReviewChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-confirmreviewchatapi-zh-CN) |审核通过评论。 |
|[SilenceUserAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-silenceuserapi-zh-CN) |禁止直播间内部分观众发送评论。 |
|[GetSilenceUserListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsilenceuserlistapi-zh-CN) |获取被禁止发送评论的观众列表。 |


<span id="menus"></span>
## 菜单


|**API** |**接口行为** |
|---|---|
|[GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-CN) |获取直播间的菜单列表。 |
|[UpdateActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitymenuapi-zh-CN) |更新直播间的菜单。 |
|[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN) |获取直播间内商品卡片的配置信息。 |
|[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN) |更新直播间内商品卡片的配置信息。 |
|[ExplainProduct](https://docs.byteplus.com/en/docs/byteplus-livesaas/explainproduct) |将商品置顶于菜单，并在观看页以悬浮窗形式展示，或将商品恢复至菜单原位置并从观看页悬浮窗移除。 |
|[CreateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/createactivityproductlibrary) |为指定直播间添加一个或多个商品库。然后，可在直播间中从 Shopify 或自有系统的商品库获取商品。 |
|[UpdateActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityproductlibrary) |更新指定直播间中商品库的信息，包括商品库的名称、类型及配置信息。 |
|[DeleteActivityProductLibrary](https://docs.byteplus.com/en/docs/byteplus-livesaas/deleteactivityproductlibrary) |删除指定直播间中的一个或多个商品库。 |
|[GetActivityProductCommonConfig](https://docs.byteplus.com/en/docs/byteplus-livesaas/getactivityproductcommonconfig) |获取指定直播间内商品的配置信息，包括商品库的 ID、名称、类型及配置信息。 |
|[ListActivityProductCommons](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityproductcommons) |一次性获取一个或多个直播间的商品库信息。 |
|[UpdatePresenterNameAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepresenternameapi-zh-CN) |更新发送评论时使用的主播昵称。 |
|[UpdateBulletScreensSwitchAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebulletscreensswitchapi-zh-CN) |配置是否在观看页显示弹幕开关。 |
|[ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-CN) |获取问答菜单中的问题，按点赞数或发送时间排序，优先返回最受欢迎或最新的问题。要获取问题的回复，可使用返回调用结果中的问题 ID 调用[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-CN)。 |
|[ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-CN) |获取问答菜单中某个问题的回复，按点赞数或发送时间排序，优先返回最受欢迎或最新的回复。 |


<span id="viewing-restrictions"></span>
## 观看限制


|**API** |**接口行为** |
|---|---|
|[UpdateCustomizationViewPermissionAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatecustomizationviewpermissionapi-zh-CN) |更新观看页和评论限制的登录链接。 |


<span id="promotion"></span>
## 推广


|**API** |**接口行为** |
|---|---|
|[ListLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listlivepromotionsapi-zh-CN) |获取直播间中已添加用于直播流推广的第三方平台列表。 |
|[AddLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi-zh-CN) |一次性为直播间添加多个第三方平台，将直播流推送多路视频流至这些平台。直播间开始直播流后，BytePlus Live 会将直播流推送至已开启直播流推广的平台。 |
|[UpdateLivePromotionsStatusAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatelivepromotionsstatusapi-zh-CN) |更新直播间中第三方平台的分发状态，以指定该平台是否已开启直播流推广。 |
|[DeleteLivePromotionsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-deletelivepromotionsapi-zh-CN) |删除直播间中的第三方直播流推广平台。 |
|[UpdateHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount) |新增主播账号或更新您账号下已有主播账号的信息。 |
|[DeleteHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/deletehostaccount) |删除您账号下的指定主播账号。 |
|[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts) |获取您账号下主播账号的 ID、名称和头像 URL 等信息。 |
|[UpdateActivityHostAccount](https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount) |更新与指定直播间关联的主播账号，并配置是否在直播间启用账号设置功能。 |
|[GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) |获取与指定直播间关联的主播账号的 ID、名称和头像 URL 等信息。 |


<span id="interaction-tools"></span>
## 互动工具


|**API** |**接口行为** |
|---|---|
|[GetVoteListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteListAPI-zh-CN) |调用 `GetVoteListAPI` 获取指定直播间的投票配置信息。 |
|[GetVoteStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetVoteStatisticsAPI-zh-CN) |调用 `GetVoteStatisticsAPI` 获取直播间的投票数据。 |
|[UpdatePresenterAwardConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateAwardConfig-zh-CN) |调用 `UpdatePresenterAwardConfigAPI` 新增、更新或删除直播间的实时抽奖。 |
|[ListAwardConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardConfigs-zh-CN) |调用 `ListAwardConfigsAPI` 获取抽奖的配置信息。 |
|[SendAward](https://docs.byteplus.com/docs/byteplus-livesaas/SendAward-zh-CN) |调用 `SendAward` 在直播间发起实时抽奖。 |
|[WithdrawAward](https://docs.byteplus.com/docs/byteplus-livesaas/WithdrawAward-zh-CN) |调用 `WithdrawAward` 撤回直播间中的实时抽奖。注意，已撤回的抽奖无法再次发送或更新。 |
|[UpdateActivityQuizConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateActivityQuizConfig-zh-CN) |调用 `UpdateActivityQuizConfigAPI` 更新指定直播间中未发送答题的配置信息。 |
|[ListActivityQuizConfigsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListActivityQuizConfigs-zh-CN) |调用 `ListActivityQuizConfigsAPI` 获取指定直播间的答题配置信息。 |
|[ListQuizStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListQuizStatisticsAPI-zh-CN) |调用 `ListQuizStatisticsAPI` 获取答题及其参与统计的分页列表。数据包括指定直播间的参与人数、答对人数及其他相关信息。 |
|[GetQuizDataAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetQuizDataAPI-zh-CN) |调用 `GetQuizDataAPI` 获取指定直播间中某次答题的详细信息。包括参与人数、答对人数及各选项内容。 |
|[GetCheckInListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInListAPI-zh-CN) |调用 `GetCheckInListAPI` 获取指定直播间的全部签到或指定签到信息，包括签到 ID、参与人数、签到时长等。 |
|[GetCheckInRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-CN) |调用 `GetCheckInRecordStatisticsAPI` 获取指定直播间的签到记录。 |
|[UpdateFloatingAdvertisementAPI](https://docs.byteplus.com/docs/byteplus-livesaas/UpdateFloatingAdvertisement-zh-CN) |调用 `UpdateFloatingAdvertisementAPI` 更新指定直播间内浮窗广告的状态、链接及其他配置信息。 |
|[GetTaskAwardItemListAPI](https://docs.byteplus.com/docs/byteplus-livesaas/GetTaskAwardItemListAPI-zh-CN) |调用 `GetTaskAwardItemListAPI` 获取直播间内已发送的按观看时长抽奖的奖品列表。 |
|[ListAwardRecordStatisticsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/ListAwardRecordStatisticsAPI-zh-CN) |调用 `ListAwardRecordStatisticsAPI` 获取指定直播间中某次抽奖的参与或中奖观众列表。 |


<span id="account-configurations"></span>
## 账号配置


|**API** |**接口行为** |
|---|---|
|[ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN) |获取您的 BytePlus 账号下直播间的标签列表。 |
|[UpdateSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2-zh-CN) |更新您的 BytePlus 账号下直播间的标签信息。 |


<span id="client-sdk"></span>
## 客户端 SDK


|**API** |**接口行为** |
|---|---|
|[GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN) |获取允许观众通过集成 Viewer SDK 的网页或应用进入直播间所需的授权令牌。 |
