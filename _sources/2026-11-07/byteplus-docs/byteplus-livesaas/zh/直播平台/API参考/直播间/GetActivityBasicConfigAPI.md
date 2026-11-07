---
title: "GetActivityBasicConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN"
---

调用此 API 获取指定直播间的完整基础配置集。

<span id="requirement"></span>
## 需求

限流：每个账号每分钟最多 120 次请求

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityBasicConfigAPI&Version=2020-06-01`

* 方法：GET


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityBasicConfigAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |Long |`17218312****` |直播间的活动 ID。 |
|Name |String |`直播间 A` |直播间名称。 |
|LiveTime |Long |`1666258566` |直播流开播时间的 Unix 时间戳格式。单位：秒。<br><br>该时间可能不是直播流实际开播的时间。 |
|IsBeginLiveEnable |Integer |`0` |指示是否启用直播流开播时间功能。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。只能在指定的开播时间后才能开播直播流。 |
|IsCoverImageEnable |Integer |`1` |指示是否启用封面图。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|CoverImageUrl |String |`//example.image` |横屏模式下封面图的 URL。<br><br>如果通过 API 调用配置，则 URL 包含协议头；如果通过控制台配置，则不包含协议头。 |
|CoverImageUrlDefault |String |`//example.image` |横屏模式下默认封面图的 URL，不包含协议头。 |
|VerticalCoverImageUrl |String |`//example.image` |竖屏模式下封面图的 URL。<br><br>如果未指定，则该参数值设置为`CoverImageUrl`的值。<br><br>如果通过调用 API 操作配置封面图，则 URL 包含协议头。但如果通过控制台配置封面图，则不包含协议头。 |
|IsPcBackImageEnable |Integer |`1` |表示是否已开启PC端背景图或背景色。<br><br>有效值：<br><br><br>* `0`：背景图未开启。<br><br>* `1`：已开启背景图片。<br><br>* `2`：已开启背景颜色。 |
|PcBackImageUrl |String |`//example.image` |PC端背景图的URL。仅当`IsPcBackImageEnable`的值为`1`时，该参数生效。 |
|PcBackImageUrlDefault |String |`https://example.image` |默认PC端背景图的URL，包含协议头。 |
|IsMobileBackImageEnable |Integer |`1` |表示是否已开启移动端背景图或背景色。<br><br>有效值：<br><br><br>* `0`：背景图未开启。<br><br>* `1`：背景图已开启。<br><br>* `2`：背景色已开启。 |
|MobileBackImageUrl |String |`//example.image` |移动端背景图的URL。仅当`IsMobileBackImageEnable`的值为`1`时，该参数生效。 |
|MobileBackImageUrlDefault |String |`https://example.image` |默认移动端背景图的URL，包含协议头。 |
|MobileBackgroundColor |String |`#060815` |移动端背景色，采用RGB色彩模型。<br><br>仅当`IsMobileBackImageEnable`的值为`2`时，该参数生效。 |
|IsPreviewVideoEnable |Integer |`0` |表示是否已开启预告。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|PreviewVideoUrl |String |`-` |已弃用。 |
|PreviewVideoVid |String |`v03a49g10000ckkavibc77uejmsb****` |预告视频的ID。仅当`IsPreviewVideoEnable`的值为`1`时，该参数生效。 |
|PreviewVideoVidDefault |String |`-` |已弃用。 |
|IsPeopleCountEnable |Integer |`0` |表示观看页是否显示观众人数。<br><br>有效值：<br><br><br>* `0`：不显示。<br><br>* `1`：显示。 |
|IsHeaderImageEnable |Integer |`0` |表示是否已开启移动端页头图。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|HeaderImageUrl |String |`//example.image` |移动端页头图的URL。仅当`IsHeaderImageEnable`的值为`1`时，该参数生效。 |
|IsWatermarkImageEnable |Integer |`0` |表示是否已开启播放器Logo。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|WatermarkImageUrl |String |`//example.image` |播放器Logo的URL。仅当`IsWatermarkImageEnable`的值为`1`时，该参数生效。 |
|IsThumbUpEnable |Integer |`0` |表示观众是否可以点赞直播间。有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|ThumbUpUrl |String |`//example.image` |点赞图标的URL。仅当`IsThumbUpEnable`的值为`1`时，该参数生效。 |
|ThumbUpUrlDefault |String |`https://example.image` |默认点赞图标的URL，包含协议头。 |
|IsShareIconEnable |Integer |`0` |表示是否已开启分享图标。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|ShareIconUrl |String |`//example.image` |分享图标的URL。仅当`IsShareIconEnable`的值为`1`时，该参数生效。 |
|ShareIconUrlDefault |String |`https://example.image` |默认分享图标的URL，包含协议头。 |
|IsCommentTranslateEnable |Integer |`-` |已弃用。 |
|IsAnnouncementEnable |Integer |`0` |表示是否已开启直播间描述。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|Announcement |String |`直播间描述` |直播间描述。仅当`IsAnnouncementEnable`的值为`1`时，该参数生效。 |
|BackgroundColor |String |`#060815` |PC端背景色，采用十六进制RGB格式。<br><br>仅当`IsPcBackImageEnable`的值为`2`时，该参数生效。 |
|InteractionColor |String |`#202124` |PC端交互区域背景色，采用RGB色彩模型。 |
|FontColor |String |`#ffffff` |字体颜色，采用RGB色彩模型。 |
|ColorThemeIndex |String |`dark` |主题。<br><br>有效值：<br><br><br>* `light`：明亮模式。<br><br>* `dark`：暗色模式。<br><br>* `cold`：经典模式。<br><br>* `holiday`：节日模式。 |
|IsPCHeaderImageEnable |Integer |`0` |表示是否已开启PC端页头图。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|PCHeaderImageUrl |String |`//example.image` |PC端页头图的URL。仅当`IsPCHeaderImageEnable`的值为`1`时，该参数生效。 |
|IsCountDownEnable |Integer |`0` |表示是否已开启倒计时。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|IsAutoStartEnable |Integer |`0` |表示是否已开启自动启动直播流功能。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|IsPageLimitEnable |Integer |`0` |表示是否已开启观看页限制。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|PageLimitType |String |`pc` |观看页限制。仅当`IsPageLimitEnable`的值为`1`时，该参数生效。<br><br>有效值：<br><br><br>* `pc`：观众仅可在PC端观看视频。<br><br>* `mobile`：观众仅可在移动端观看视频。 |
|IsLanguageEnable |Integer |`0` |表示是否已开启观看页语言选择器。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|LanguageType |Array of Integer |`[0,1]` |观众可在观看页选择的语言。仅当`IsLanguageEnable`的值为`1`时，该参数生效。<br><br>有效值：<br><br><br>* `0`：简体中文。<br><br>* `1`：英文。<br><br>* `2`：日文。<br><br>* `3`：繁体中文。<br><br>* `4`：韩文。<br><br>* `5`：泰文。<br><br>* `6`：越南文。<br><br>* `7`：阿拉伯文。<br><br>* `8`：土耳其文。<br><br>* `9`：西班牙文。<br><br>* `10`：印尼文。<br><br>* `11`：葡萄牙文。<br><br>* `12`：俄文。<br><br>* `13`：塔加洛语。<br><br>* `14`：高棉语。<br><br>* `15`：老挝语。<br><br>* `16`：缅甸语。<br><br>* `17`：马来语。<br><br>* `18`：印地语。<br><br>* `19`：法语。<br><br>* `20`：德语。<br><br>* `21`：意大利语。 |
|SiteTags |Array of[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |`-` |直播间分类标签列表。 |
|TextSiteTags |Array of[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |`-` |直播间文本标签列表。 |
|AutoStartType |Integer |`0` |自动启动直播流的模式。仅当`IsAutoStartEnable`的值为`1`时，该参数生效。<br><br>有效值：<br><br><br>* `0`：不自动启动直播流。<br><br>* `1`：自动启动预录视频。<br><br>* `2`：自动拉流启动。 |
|PreviewVideoId |Long |`431674` |预告的媒体库ID。仅当`IsPreviewVideoEnable`的值为`1`时，该参数生效。 |
|AccountId |Long |`-` |已弃用。 |
|PreviewVideoReviewStatus |Integer |`-` |已弃用。 |
|DefaultSubtitleLanguage |String |`-` |已弃用。 |
|SourceSubtitleLanguage |String |`-` |已弃用。 |
|OpenLiveAvextractorTask |Integer |`-` |已弃用。 |
|IsTimeShift |Integer |`0` |该功能当前不可用。固定值：`0` |
|PreviewVideoCoverImage |String |`https://example.image` |预告封面图的URL。 |
|PreviewVideoMediaName |String |`Video.mp4` |预告名称。 |
|IsPreviewPromptEnable |Integer |`1` |表示是否已开启预告文本。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|PreviewPrompt |String |`直播流即将开始。` |预告文本。仅当`IsPreviewPromptEnable`的值为`1`时，该参数生效。 |
|IsReservationEnable |Integer |`1` |指示预约功能是否已开启。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|IsReservationSmsEnable |Integer |`1` |指示预约短信提醒是否已开启。仅当`IsReservationEnable`的值为`1`时该参数有效。<br><br>有效值：<br><br><br>* `1`：已开启。<br><br>* `2`：未开启。 |
|ReservationTime |Integer |`300` |指定在直播流开始前多少秒发送短信提醒。<br><br>单位：秒。<br><br>仅当`IsReservationSmsEnable`的值为`1`时该参数有效。 |
|ReservationText |String |`-` |已弃用。 |
|WatermarkPosition |Integer |`0` |播放器logo位置。<br><br>有效值：<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：播放器右下角。 |
|IsReplayBulletChat |Integer |`-` |已弃用。 |
|PresenterChatColor |String |`#FFD58B` |主播字体颜色，采用RGB色彩模型。 |
|IsLiveBulletChat |Integer |`-` |已弃用。 |
|IsBackgroundBlur |Integer |`0` |指示是否启用背景虚化。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：移动端已开启。<br><br>* `2`：PC端已开启。<br><br>* `3`：PC端和移动端均已开启。 |
|FeedbackMessage |String |`-` |已弃用。 |
|IsFeedbackEnable |Integer |`-` |已弃用。 |
|IsThumbUpNumberEnable |Integer |`1` |指示直播间点赞数是否在观看页显示。<br><br>有效值：<br><br><br>* `0`：未显示。<br><br>* `1`：已显示。 |
|SmsLanguage |Integer |`0` |短信消息语言。<br><br>有效值：<br><br><br>* 手机号以+86开头默认使用中文，其他号码默认使用英文。<br><br>* `1`：中文。<br><br>* `2`：英文。<br><br>* `3`：中英文同时显示。 |
|MobileChatBackgroundColor |String |`#000000` |移动端评论背景色，采用RGB色彩模型。 |
|ConfigVersion |Integer |`1` |配置版本。固定值：`1` |
|LiveZone |Integer |`480` |时区。<br><br>有效值：<br><br><br>* `-60`：GMT\-01:00 Ponta del Gada（葡萄牙）。<br><br>* `-120`：GMT\-02:00 Fernando de Noronha（巴西）。<br><br>* `-180`：GMT\-03:00 Brasilia（巴西）。<br><br>* `-240`：GMT\-04:00 Santiago（智利）。<br><br>* `-300`：GMT\-05:00 Washington, D.C.（美国）。<br><br>* `-360`：GMT\-06:00 Mexico City（墨西哥）。<br><br>* `-420`：GMT\-07:00 Denver（美国）。<br><br>* `-480`：GMT\-08:00 Vancouver（加拿大）。<br><br>* `-540`：GMT\-09:00 Alaska（美国）。<br><br>* `-570`：GMT\-09:30 Teojae（法属波利尼西亚）。<br><br>* `-600`：GMT\-10:00 Hawaii（美国）。<br><br>* `-660`：GMT\-11:00 Alofi（纽埃）。<br><br>* `0`：GMT+00:00 London（英国）。<br><br>* `60`：GMT+01:00 Paris（法国）。<br><br>* `120`：GMT+02:00 Damascus（叙利亚）。<br><br>* `180`：GMT+03:00 Moscow（俄罗斯）。<br><br>* `210`：GMT+03:30 Tehran（伊朗）。<br><br>* `240`：GMT+04:00 Dubai（阿联酋）。<br><br>* `300`：GMT+05:00 New Delhi（印度）。<br><br>* `330`：GMT+05:30 Mumbai（印度）。<br><br>* `360`：GMT+06:00 Dhaka（孟加拉国）。<br><br>* `390`：GMT+06:30 Yangon（缅甸）。<br><br>* `420`：GMT+07:00 Bangkok（泰国）。<br><br>* `480`：GMT+08:00 Beijing（中国）。<br><br>* `525`：GMT+08:45 Yukla（澳大利亚）。<br><br>* `540`：GMT+09:00 Tokyo（日本）。<br><br>* `570`：GMT+09:30 Darwin（澳大利亚）。<br><br>* `600`：GMT+10:00 Canberra（澳大利亚）。<br><br>* `630`：GMT+10:30 Lord Howe Island（澳大利亚）。<br><br>* `660`：GMT+11:00 Sydney（澳大利亚）。<br><br>* `720`：GMT+12:00 Suva（斐济）。<br><br>* `780`：GMT+13:00 Phoenix Islands（基里巴斯）。<br><br>* `825`：GMT+13:45 Chatham Islands（新西兰）。<br><br>* `840`：GMT+14:00 Christmas Island（基里巴斯）。 |
|RiskWarningSetting |属于[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)的对象 |`-` |当观众进入直播间时显示的提醒弹窗配置。 |
|IsColorSync |Integer |`1` |表示颜色配置是否同步到竖屏模式。<br><br>有效值：<br><br><br>* `0`：不同步。<br><br>* `1`：同步。 |
|IsPlayerTopEnable |Integer |`0` |表示是否启用播放器置顶功能。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|PlayerTopType |Array of Integer |`[1,2]` |播放器置顶页面的终端类型。<br><br>有效值：<br><br><br>* `0`：已废弃。<br><br>* `1`：播放器在 PC 端页面置顶。<br><br>* `2`：播放器在移动端横屏模式页面置顶。 |
|IsReplayAutoOnlineEnable |Integer |`0` |表示直播流结束后是否自动将回放发布到观看页。<br><br>有效值：<br><br><br>* `0`：不自动发布。<br><br>* `1`：自动发布。 |
|IsSDKPlayEnable |Integer |`1` |表示观看页集成 Web 观播 SDK 的播放器是否启用直播视频播放。<br><br>有效值：<br><br><br>* `0`：未开启。为避免不必要的播放，直播流同时被禁用。因此，无论观众是否在集成 Web 观播 SDK 的观看页，均无法观看直播视频。<br><br>* `1`：已开启。 |
|SDKPlayStatus |Integer |`2` |在 Web 观播 SDK 观看页显示的直播间状态。该状态可能与实际房间状态不同。<br><br>仅当`IsSDKPlayEnable`的值为`0`时，该参数有效。<br><br>有效值：<br><br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：结束。 |
|IsVideoChatDisplayed |Integer |`1` |表示是否在网页端直播页启用连麦（主播与主播）功能。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|IsSharedAddressDisplayed |Integer |`1` |表示是否在网页端直播页显示观看页地址。<br><br>有效值：<br><br><br>* `0`：不显示。<br><br>* `1`：显示。 |
|IsReleaseNoticeDisplayed |Integer |`1` |表示是否在网页端直播页启用锁定预告功能。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|IsInteractiveEnable |Integer |`0` |表示主播是否只能在网页端直播页管理指定的互动工具。<br><br>有效值：<br><br><br>* `0`：主播可以管理以下所有互动工具。<br><br>* 问卷<br><br>* 文档<br><br>* 签到<br><br>* 答题<br><br>* 抽奖<br><br>* 公告<br><br>* `1`：主播只能管理指定的互动工具。 |
|InteractiveShowSetting |Object of[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) |`-` |主播可以在网页端直播页管理的互动工具。<br><br>仅当`IsInteractiveEnable`的值为`1`时，该参数生效。 |
|EndTime |Long |`1666358566` |直播流的结束时间，Unix 时间戳格式。单位：秒。 |
|IsAutoEndEnable |Integer |`1` |表示是否启用在指定结束时间自动结束直播流的功能。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |


<span id="interactiveshowsetting"></span>
#### InteractiveShowSetting


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|IsQuestionnaireDisplayed |Integer |`0` |表示主播是否可以在网页端直播页管理问卷。<br><br>有效值：<br><br><br>* `0`：主播无法管理问卷。<br><br>* `1`：主播可以管理问卷。 |
|IsDocDisplayed |整数 |`0` |指示主播是否可以在网页端直播页面管理文档。<br><br>有效值：<br><br><br>* `0`：主播无法管理文档。<br><br>* `1`：主播可以管理文档。 |
|IsCheckInDisplayed |整数 |`0` |指示主播是否可以在网页端直播页面管理签到。<br><br>有效值：<br><br><br>* `0`：主播无法管理签到。<br><br>* `1`：主播可以管理签到。 |
|IsQuizDisplayed |整数 |`0` |指示主播是否可以在网页端直播页面管理答题。<br><br>有效值：<br><br><br>* `0`：主播无法管理答题。<br><br>* `1`：主播可以管理答题。 |
|IsLuckDrawDisplayed |整数 |`0` |指示主播是否可以在网页端直播页面管理抽奖。<br><br>有效值：<br><br><br>* `0`：主播无法管理抽奖。<br><br>* `1`：主播可以管理抽奖。 |
|IsAnnouncementDisplayed |整数 |`0` |指示主播是否可以在网页端直播页面管理公告。<br><br>有效值：<br><br><br>* `0`：主播无法管理公告。<br><br>* `1`：主播可以管理公告。 |


<span id="sitetags"></span>
#### SiteTags


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Name |字符串 |`标签 A` |分类标签的名称。 |
|Value |字符串 |`1` |分类标签的值。 |
|Index |整数 |`0` |分类标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。<br><br>取值范围：[0,19]。 |
|DbIndex |整数 |`-` |已废弃。 |
|Show |整数 |`-` |已废弃。 |
|Id |整数 |`-` |已废弃。 |


<span id="textsitetags"></span>
#### TextSiteTags


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Name |字符串 |`标签 B` |文本标签的名称。 |
|Value |字符串 |`3` |文本标签的值。 |
|Index |整数 |`0` |文本标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。<br><br>取值范围：[0,4]。 |
|DbIndex |整数 |`-` |已废弃。 |
|Show |整数 |`-` |已废弃。 |
|Id |整数 |`-` |已废弃。 |


<span id="riskwarningsetting"></span>
#### RiskWarningSetting


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|IsRiskWarningEnable |整数 |`0` |指示提醒弹窗是否已开启。<br><br>有效值：<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|RiskWarningButtonText |字符串 |`已了解` |提醒弹窗的按钮名称。 |
|RiskWarningContent |字符串 |`欢迎来到直播间！请遵守主办方及您所在国家的法律法规，勿发送涉黄、违法、低俗或诽谤性质的评论。做其他观众的榜样。请勿通过恶意行为（如恶意刷屏等）扰乱直播间秩序。如遇到与主播之间的私人商品推介，请自行判断并谨慎处理。` |提醒的内容。 |
|RiskWarningTitle |字符串 |`提醒` |提醒弹窗的标题。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityBasicConfigAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="sample-response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityBasicConfigAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1666121102
    },
     "Result": {
        "ActivityId": 17218312****,
        "Name": "Live Room A",
        "LiveTime": 1666258566,
        "IsBeginLiveEnable": 0, 
        "IsCoverImageEnable": 1,
        "CoverImageUrl": "//example.image",
        "CoverImageUrlDefault": "//example.image",
        "VerticalCoverImageUrl": "//example.image",
        "IsPcBackImageEnable": 1,
        "PcBackImageUrl": "//example.image",
        "PcBackImageUrlDefault": "https://example.image",
        "IsMobileBackImageEnable": 1,
        "MobileBackImageUrl": "//example.image",
        "MobileBackImageUrlDefault": "https://example.imagee",
        "IsPreviewVideoEnable": 0,
        "PreviewVideoUrl": "",
        "PreviewVideoVid": "",
        "PreviewVideoVidDefault": "",
        "IsPeopleCountEnable": 0,
        "IsHeaderImageEnable": 0,
        "HeaderImageUrl": "",
        "IsWatermarkImageEnable": 0,
        "WatermarkImageUrl": "",
        "IsThumbUpEnable": 0,
        "ThumbUpUrl": "",
        "ThumbUpUrlDefault": "",
        "IsShareIconEnable": 0,
        "ShareIconUrl": "",
        "ShareIconUrlDefault": "https://example.image",
        "IsCommentTranslateEnable": 0,
        "Announcement": "",
        "IsAnnouncementEnable": 0,
        "BackgroundColor": "#060815",
        "InteractionColor": "#202124",
        "FontColor": "#ffffff",
        "ColorThemeIndex": "dark",
        "IsPCHeaderImageEnable": 0,
        "PCHeaderImageUrl": "",
        "IsCountdownEnable": 0,
        "IsAutoStartEnable": 0,
        "IsPageLimitEnable": 0,
        "PageLimitType": "",
        "IsLanguageEnable": 0,
        "LanguageType": [],
        "SiteTags": [],
        "TextSiteTags": [],
        "AutoStartType": 0,
        "IsPlayerTopEnable": 0,
        "PlayerTopType": [],
        "IsReplayAutoOnlineEnable": 0,
        "PreviewVideoId": 0,
        "AccountId": 0,
        "PreviewVideoReviewStatus": 0,
        "DefaultSubtitleLanguage": "",
        "SourceSubtitleLanguage": "",
        "OpenLiveAvextractorTask": 0,
        "IsTimeShift": 0,
        "PreviewVideoCoverImage": "",
        "PreviewVideoMediaName": "",
        "IsPreviewPromptEnable": 1,
        "PreviewPrompt": "The live stream will start soon.",
        "IsReservationEnable": 1,
        "IsReservationSmsEnable": 1,
        "ReservationTime": 300,
        "ReservationText": "",
        "WatermarkPosition": 0,
        "IsReplayBulletChat": 0,
        "PresenterChatColor": "#FFD58B",
        "IsLiveBulletChat": 0,
        "IsBackgroundBlur": 0,
        "FeedbackMessage": "",
        "IsFeedbackEnable": 0,
        "IsThumbUpNumberEnable": 1,
        "SmsLanguage": 0,
        "MobileChatBackgroundColor": "#000000",
        "MobileBackgroundColor": "#060815",
        "ConfigVersion": 1,
        "LiveZone": 480,
        "IsColorSync": 1,
        "RiskWarningSetting": {
            "IsRiskWarningEnable": 0,
            "RiskWarningTitle": "",
            "RiskWarningContent": "",
            "RiskWarningButtonText": ""
        },
        "IsSDKPlayEnable": 1,
        "SDKPlayStatus": 2,
        "IsVideoChatDisplayed": 1,
        "IsSharedAddressDisplayed": 1,
        "EndTime": 1666358566,
        "IsAutoEndEnable": 1,
        "IsReleaseNoticeDisplayed": 1,
        "IsInteractiveEnable": 1,
        "InteractiveShowSetting": {
            "IsQuestionnaireDisplayed": 1,
            "IsDocDisplayed": 1,
            "IsCheckInDisplayed": 1,
            "IsQuizDisplayed": 0,
            "IsLuckDrawDisplayed": 0,
            "IsAnnouncementDisplayed": 0
        }
    }
}
```


<span id="error-codes"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
