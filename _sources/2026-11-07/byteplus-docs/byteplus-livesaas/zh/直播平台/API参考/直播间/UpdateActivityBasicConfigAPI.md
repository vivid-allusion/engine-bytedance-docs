---
title: "UpdateActivityBasicConfigAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN"
---

调用此 API 可更新直播间的基础配置，例如背景图片和预告。

在调用此 API 操作前，必须先调用 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)。根据需要更新 `GetActivityBasicConfigAPI` 的返回调用结果参数，并在调用此 API 操作时作为请求参数值传递。如有自定义需求，为防止参数值被默认值覆盖，即使该参数不是必填项，也必须传递对应的参数值。

<span id="requirement"></span>
## 需求

限速：每个账号每分钟最多 120 次请求

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=UpdateActivityBasicConfigAPI&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityBasicConfigAPI` |API操作。 |
|Version |String |是 |`2020-06-01` |此API操作的版本。当前版本：`2020-06-01`。 |


<span id="body"></span>
### 请求体


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该ID。 |
|Name |String |是 |`直播间A` |直播间名称，长度不得超过1950个字符。 |
|LiveTime |Long |否 |`1666258566` |直播流的开始时间，采用 Unix 时间戳格式。单位：秒。时间精确到分钟。<br><br>这是预定的开始时间。实际开始时间可能会根据主播开播的时间有所不同。<br><br><br>* `LiveTime`必须早于`EndTime`，最大时间差为259,200（72小时）。<br><br>* 在直播流过程中无法修改此参数值。 |
|IsBeginLiveEnable |Integer |否 |`0` |用于指定是否启用直播流开始时间功能。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。仅可在指定的开始时间后开播。<br><br><br>在直播流过程中无法修改此参数值。 |
|IsAutoEndEnable |Integer |否 |`0` |用于指定是否启用在指定结束时间自动结束直播流的功能。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。<br><br><br>在直播流过程中无法修改此参数值。 |
|EndTime |Long |否 |`1666358566` |直播流结束时间，Unix时间戳格式。单位：秒。时间可精确到分钟。<br><br>`EndTime`必须晚于`LiveTime`，最大差值为259,200（72小时）。<br><br><br>* 当`IsAutoEndEnable`的值为`1`时，此参数为必填项。<br><br>* 在直播流过程中无法修改此参数值。 |
|IsCoverImageEnable |Integer |否 |`0` |用于指定是否启用封面图。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：关闭封面图。<br><br>* `1`：启用封面图。 |
|CoverImageUrl |String |否 |`https://example.image` |横屏模式下封面图的URL。<br><br><br>* 通常情况下，参数值需为带协议头的URL。但如果你通过[BytePlus Live控制台](https://console.byteplus.com/livesaas/liveManagement/)上传图片获取URL（例如，通过调用[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)获取在直播间控制台上传的封面图URL），则参数值可以使用不带协议头的URL。<br><br>* 当`IsCoverImageEnable`的值为`1`时，必须填写该参数。 |
|VerticalCoverImageUrl |String |否 |`https://example.image` |竖屏模式下封面图的URL。<br><br>如未指定，则参数值为`CoverImageUrl`的值。<br><br><br>* 通常情况下，参数值需为带协议头的URL。但如果你通过[BytePlus Live控制台](https://console.byteplus.com/livesaas/liveManagement/)上传图片获取URL（例如，通过调用[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)获取在直播间控制台上传的封面图URL），则参数值可以使用不带协议头的URL。<br><br>* 当`IsCoverImageEnable`的值为`1`时，必须填写该参数。 |
|IsPcBackImageEnable |Integer |否 |`0` |用于指定是否启用PC端的背景图片或背景色。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：关闭背景图片。<br><br>* `1`：启用背景图片。<br><br>* `2`：启用背景色。 |
|PcBackImageUrl |String |否 |`//example.image` |PC端背景图片的URL。当`IsPcBackImageEnable`的值为`1`时，必须填写该参数。 |
|PcBackImageUrlDefault |String |否 |`https://example.image` |PC端默认背景图片的URL，需包含协议头。 |
|BackgroundColor |String |否 |`#060815` |PC端的背景色，采用RGB色彩模型。当`IsPcBackImageEnable`的值为`2`时，必须填写该参数。你需要设置与[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)返回调用结果中返回值一致。 |
|IsMobileBackImageEnable |Integer |否 |`0` |用于指定是否启用移动端的背景图片或背景色。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：关闭背景图片。<br><br>* `1`：启用背景图片。<br><br>* `2`：启用背景色。 |
|MobileBackImageUrl |String |否 |`//example.image` |移动端背景图片的URL。当`IsMobileBackImageEnable`的值为`1`时，必须填写该参数。 |
|MobileBackImageUrlDefault |String |否 |`https://example.image` |移动端默认背景图片的URL，需包含协议头。 |
|MobileBackgroundColor |String |否 |`#060815` |移动端的背景色，采用RGB色彩模型。当`IsMobileBackImageEnable`的值为`2`时，必须填写该参数。你需要设置与[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)返回调用结果中返回值一致。 |
|IsPreviewVideoEnable |Integer |否 |`0` |用于指定是否启用预告。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用预告。<br><br>* `1`：启用预告。 |
|PreviewVideoUrl |字符串 |否 |`-` |已废弃。 |
|PreviewVideoVid |字符串 |否 |`v03a49g10000ckkavibc77uejmsb****` |预告视频的 ID。当 `IsPreviewVideoEnable` 的值为 `1` 时，该参数为必填项。 |
|PreviewVideoVidDefault |字符串 |否 |`-` |已废弃。 |
|IsPeopleCountEnable |整数 |否 |`0` |用于指定是否在观看页显示观众人数。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不显示观众人数。<br><br>* `1`：显示观众人数。 |
|IsHeaderImageEnable |整数 |否 |`0` |用于指定是否启用移动端页头图。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用页头图。<br><br>* `1`：启用页头图。 |
|HeaderImageUrl |字符串 |否 |`//example.image` |移动端页头图的 URL。当 `IsHeaderImageEnable` 的值为 `1` 时，该参数为必填项。 |
|IsWatermarkImageEnable |整数 |否 |`0` |用于指定是否启用播放器 Logo。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用 Logo。<br><br>* `1`：启用 Logo。 |
|WatermarkImageUrl |字符串 |否 |`//example.image` |播放器 Logo 的 URL。当 `IsWatermarkImageEnable` 的值为 `1` 时，该参数为必填项。 |
|IsThumbUpEnable |整数 |否 |`0` |用于指定是否启用直播间点赞功能。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用该功能。<br><br>* `1`：启用该功能。 |
|ThumbUpUrl |字符串 |否 |`//example.image` |点赞图标的 URL。当 `IsThumbUpEnable` 的值为 `1` 时，该参数为必填项。 |
|ThumbUpUrlDefault |字符串 |否 |`https://example.image` |默认点赞图标的 URL，包含协议头。 |
|IsShareIconEnable |整数 |否 |`0` |用于指定是否启用分享图标。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用分享图标。<br><br>* `1`：启用分享图标。 |
|ShareIconUrl |字符串 |否 |`//example.image` |分享图标的 URL。当 `IsShareIconEnable` 的值为 `1` 时，该参数为必填项。 |
|ShareIconUrlDefault |字符串 |否 |`https://example.image` |默认分享图标的 URL，包含协议头。 |
|IsCommentTranslateEnable |整数 |否 |`-` |已废弃。 |
|IsAnnouncementEnable |整数 |否 |`0` |用于指定是否启用公告。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用公告。<br><br>* `1`：启用公告。 |
|Announcement |字符串 |否 |`公告` |公告。当 `IsAnnouncementEnable` 的值为 `1` 时，该参数为必填项。 |
|InteractionColor |字符串 |否 |`#202124` |PC 端交互区域的背景色，采用 RGB 色彩模型。必须设置为 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) 返回调用结果 中返回的相同值。 |
|FontColor |字符串 |否 |`#ffffff` |字体颜色，采用 RGB 色彩模型。必须设置为 [GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN) 返回调用结果 中返回的相同值。 |
|ColorThemeIndex |字符串 |否 |`dark` |主题。默认值：`dark`<br><br>可选值：<br><br><br>* `light`：浅色模式。<br><br>* `dark`：深色模式。<br><br>* `cold`：经典模式。<br><br>* `holiday`：节日模式。 |
|IsPCHeaderImageEnable |整数 |否 |`0` |用于指定是否启用 PC 页头图。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不启用页头图。<br><br>* `1`：启用页头图。 |
|PCHeaderImageUrl |字符串 |否 |`//example.image` |PC端页头图的URL。当`IsPCHeaderImageEnable`的值为`1`时，必须填写该参数。 |
|IsCountDownEnable |整数 |否 |`0` |指定是否启用倒计时。默认值：`0`<br><br>有效值：<br><br><br>* `0`：禁用倒计时。<br><br>* `1`：启用倒计时。 |
|IsAutoStartEnable |整数 |否 |`0` |指定是否自动启动直播流。默认值：`0`<br><br>有效值：<br><br><br>* `0`：不自动启动直播流。<br><br>* `1`：自动启动直播流。 |
|AutoStartType |整数 |否 |`0` |自动启动直播流的模式。当`IsAutoStartEnable`的值为`1`时，必须填写该参数。默认值：`0`<br><br>有效值：<br><br><br>* `0`：不自动启动直播流。<br><br>* `1`：自动启动预录视频。<br><br>* `2`：自动拉流。 |
|IsPageLimitEnable |整数 |否 |`0` |指定是否启用观看页限制。默认值：`0`<br><br>有效值：<br><br><br>* `0`：禁用限制。<br><br>* `1`：启用限制。 |
|PageLimitType |字符串 |否 |`pc` |观看页限制。当`IsPageLimitEnable`的值为`1`时，必须填写该参数。<br><br>有效值：<br><br><br>* `pc`：观众只能在PC端观看视频。<br><br>* `mobile`：观众只能在移动端观看视频。 |
|IsLanguageEnable |整数 |否 |`0` |指定是否在观看页启用语言选择器。默认值：`0`<br><br>有效值：<br><br><br>* `0`：禁用语言选择器。<br><br>* `1`：启用语言选择器。 |
|LanguageType |整数数组 |否 |`[0,1]` |观众可在观看页选择的语言。当`IsLanguageEnable`的值为`1`时，必须填写该参数。默认值：`0`。最多可选择13种语言。<br><br>有效值：<br><br><br>* `0`：简体中文。<br><br>* `1`：英文。<br><br>* `2`：日文。<br><br>* `3`：繁体中文。<br><br>* `4`：韩文。<br><br>* `5`：泰文。<br><br>* `6`：越南语。<br><br>* `7`：阿拉伯语。<br><br>* `8`：土耳其语。<br><br>* `9`：西班牙语。<br><br>* `10`：印尼语。<br><br>* `11`：葡萄牙语。<br><br>* `12`：俄语。<br><br>* `13`：塔加洛语。<br><br>* `14`：高棉语。<br><br>* `15`：老挝语。<br><br>* `16`：缅甸语。<br><br>* `17`：马来语。<br><br>* `18`：印地语。<br><br>* `19`：法语。<br><br>* `20`：德语。<br><br>* `21`：意大利语。 |
|SiteTags |数组[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |否 |`-` |直播间中的分类标签列表。 |
|TextSiteTags |数组[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |否 |`-` |直播间中的文本标签列表。 |
|PreviewVideoId |长整型 |否 |`431674` |预告的媒体库ID。当`IsPreviewVideoEnable`的值为`1`时，必须填写该参数。 |
|AccountId |长整型 |否 |`-` |已弃用。 |
|PreviewVideoReviewStatus |整数 |否 |`-` |已弃用。 |
|DefaultSubtitleLanguage |字符串 |否 |`-` |已弃用。 |
|SourceSubtitleLanguage |字符串 |否 |`-` |已弃用。 |
|OpenLiveAvextractorTask |整数 |否 |`-` |已弃用。 |
|IsTimeShift |整数 |否 |`0` |该功能当前不可用。固定值：`0` |
|PreviewVideoCoverImage |字符串 |否 |`https://example.image` |预告封面图的URL。 |
|PreviewVideoMediaName |字符串 |否 |`Video.mp4` |预告名称。 |
|IsPreviewPromptEnable |整数 |否 |`0` |指定是否启用预告文本。默认值：`0`<br><br>有效值：<br><br><br>* `0`：禁用预告文本。<br><br>* `1`：启用预告文本。 |
|PreviewPrompt |字符串 |否 |`直播流即将开始。` |预告文本。当`IsPreviewPromptEnable`的值为`1`时，必须填写该参数。 |
|IsReservationEnable |整数 |否 |`0` |指定是否开启预约功能。默认值：`0`<br><br>可选值：<br><br><br>* `0`：禁用该功能。<br><br>* `1`：启用该功能。 |
|IsReservationSmsEnable |整数 |否 |`1` |指定是否开启预约短信提醒。默认值：`1`。<br><br>可选值：<br><br><br>* `1`：开启短信提醒。<br><br>* `2`：关闭短信提醒。<br><br><br>仅当`IsReservationEnable`的值为`1`时，该参数有效。 |
|ReservationTime |整数 |否 |`300` |指定在直播流开始前多少秒向观众发送短信提醒。<br><br>单位：秒。<br><br>仅当`IsReservationSmsEnable`的值为`1`时，该参数有效。 |
|ReservationText |字符串 |否 |`-` |已废弃。 |
|WatermarkPosition |整数 |否 |`0` |播放器 Logo 的位置。默认值：`0`<br><br>可选值：<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：播放器右下角。 |
|IsReplayBulletChat |整数 |否 |`-` |已废弃。 |
|PresenterChatColor |字符串 |否 |`#FFD58B` |讲师聊天消息的字体颜色，采用 RGB 颜色模型。必须设置为与[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)返回调用结果中返回的值一致。 |
|IsLiveBulletChat |整数 |否 |`-` |已废弃。 |
|IsBackgroundBlur |整数 |否 |`0` |指定是否开启背景虚化。默认值：`0`<br><br>可选值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：在移动端开启该功能。<br><br>* `2`：在 PC 端开启该功能。<br><br>* `3`：在 PC 端和移动端均开启该功能。 |
|FeedbackMessage |字符串 |否 |`-` |已废弃。 |
|IsFeedbackEnable |整数 |否 |`-` |已废弃。 |
|IsThumbUpNumberEnable |整数 |否 |`0` |指定是否在观看页展示直播间点赞数。默认值：`0`<br><br>可选值：<br><br><br>* `0`：不展示点赞数。<br><br>* `1`：展示点赞数。 |
|SmsLanguage |整数 |否 |`0` |短信消息的语言。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：手机号以 +86 开头时为中文，其他情况为英文。<br><br>* `1`：中文。<br><br>* `2`：英文。<br><br>* `3`：中英文。 |
|MobileChatBackgroundColor |字符串 |否 |`#000000` |移动端评论区背景色，采用 RGB 颜色模型。必须设置为与[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)返回调用结果中返回的值一致。 |
|ConfigVersion |整数 |否 |`1` |配置版本。固定值：`1`。 |
|LiveZone |整数 |否 |`480` |时区。默认值：`480`。<br><br>可选值：<br><br><br>* `-60`：GMT\-01:00 Ponta del Gada（葡萄牙）。<br><br>* `-120`：GMT\-02:00 Fernando de Noronha（巴西）。<br><br>* `-180`：GMT\-03:00 Brasilia（巴西）。<br><br>* `-240`：GMT\-04:00 Santiago（智利）。<br><br>* `-300`：GMT\-05:00 Washington, D.C.（美国）。<br><br>* `-360`：GMT\-06:00 Mexico City（墨西哥）。<br><br>* `-420`：GMT\-07:00 Denver（美国）。<br><br>* `-480`：GMT\-08:00 Vancouver（加拿大）。<br><br>* `-540`：GMT\-09:00 Alaska（美国）。<br><br>* `-570`：GMT\-09:30 Teojae（法属波利尼西亚）。<br><br>* `-600`：GMT\-10:00 Hawaii（美国）。<br><br>* `-660`：GMT\-11:00 Alofi（纽埃）。<br><br>* `0`：GMT+00:00 伦敦（英国）。<br><br>* `60`：GMT+01:00 巴黎（法国）。<br><br>* `120`：GMT+02:00 大马士革（叙利亚）。<br><br>* `180`：GMT+03:00 莫斯科（俄罗斯）。<br><br>* `210`：GMT+03:30 德黑兰（伊朗）。<br><br>* `240`：GMT+04:00 迪拜（阿拉伯联合酋长国）。<br><br>* `300`：GMT+05:00 新德里（印度）。<br><br>* `330`：GMT+05:30 孟买（印度）。<br><br>* `360`：GMT+06:00 达卡（孟加拉国）。<br><br>* `390`：GMT+06:30 仰光（缅甸）。<br><br>* `420`：GMT+07:00 曼谷（泰国）。<br><br>* `480`：GMT+08:00 北京（中国）。<br><br>* `525`：GMT+08:45 Yukla（澳大利亚）。<br><br>* `540`：GMT+09:00 东京（日本）。<br><br>* `570`：GMT+09:30 达尔文（澳大利亚）。<br><br>* `600`：GMT+10:00 堪培拉（澳大利亚）。<br><br>* `630`：GMT+10:30 豪勋爵岛（澳大利亚）。<br><br>* `660`：GMT+11:00 悉尼（澳大利亚）。<br><br>* `720`：GMT+12:00 苏瓦（斐济）。<br><br>* `780`：GMT+13:00 凤凰群岛（基里巴斯）。<br><br>* `825`：GMT+13:45 查塔姆群岛（新西兰）。<br><br>* `840`：GMT+14:00 圣诞岛（基里巴斯）。 |
|RiskWarningSetting |RiskWarningSetting 对象[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |否 |`-` |观众进入直播间时弹出的提醒弹窗配置。 |
|IsColorSync |整数 |否 |`0` |指定是否将配色方案同步到竖屏模式。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：不同步到竖屏模式。<br><br>* `1`：同步到竖屏模式。 |
|IsPlayerTopEnable |整数 |否 |`0` |指定是否启用播放器置顶功能。默认值：`0`<br><br>可选值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。 |
|PlayerTopType |整数数组 |否 |`[1,2]` |播放器置顶显示的终端类型。默认值：`[1,2]`<br><br>当`IsPlayerTopEnable`的值为`1`时，该参数为必填。<br><br>可选值：<br><br><br>* `0`：已废弃。<br><br>* `1`：播放器在 PC 端页面置顶显示。<br><br>* `2`：播放器在移动端横屏模式页面置顶显示。 |
|IsReplayAutoOnlineEnable |整数 |否 |`0` |指定直播流结束后是否在观看页自动发布回放。<br><br>可选值：<br><br><br>* `0`：不自动发布回放。<br><br>* `1`：自动发布回放。 |
|IsSDKPlayEnable |整数 |否 |`1` |指定是否在集成了 Web 观播 SDK 的观看页上启用播放器播放直播视频。默认值：`1`。<br><br>可选值：<br><br><br>* `0`：禁止播放器播放直播视频。为避免不必要的播放，同时会关闭直播流。因此，无论观众是否在集成了 Web 观播 SDK 的观看页，均无法观看直播视频。<br><br>* `1`：允许播放器播放直播视频。 |
|SDKPlayStatus |整数 |否 |`2` |在集成了 Web 观播 SDK 的观看页上显示的直播间状态，可能与直播间的实际状态不同。<br><br>如果未指定，则显示直播间的实际状态。<br><br>仅当`IsSDKPlayEnable`的值为`0`时，该参数生效。<br><br>可选值：<br><br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：已结束。<br><br><br>如果将状态设置为`2`（预告）或`3`（回放），但对应内容不可用，页面将显示`已结束`状态。例如，将状态设置为`3`但未发布回放时，页面会显示`已结束`，而不是`回放`。 |
|IsVideoChatDisplayed |整数 |否 |`0` |指定是否在网页浏览器中的直播页面启用连麦（主播与主播）功能。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。 |
|IsSharedAddressDisplayed |整数 |否 |`0` |指定是否在网页端直播页面显示观看页地址。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：不显示地址。<br><br>* `1`：显示地址。 |
|IsReleaseNoticeDisplayed |整数 |否 |`0` |指定是否在网页端直播页面启用锁定预告功能。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。 |
|IsInteractiveEnable |整数 |否 |`0` |指定是否仅允许主播在网页端直播页面管理指定的互动工具。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播可以管理以下所有互动工具。<br><br>* 问卷<br><br>* 文档<br><br>* 签到<br><br>* 答题<br><br>* 抽奖<br><br>* 公告<br><br>* `1`：主播仅可管理指定的互动工具。 |
|InteractiveShowSetting |对象[UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi-zh-CN) |否 |`-` |主播可在网页端直播页面管理的互动工具。至少配置一个互动工具。<br><br>当`IsInteractiveEnable`的值为`1`时，该参数为必填项。 |


<span id="interactiveshowsetting"></span>
#### InteractiveShowSetting


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|IsQuestionnaireDisplayed |整数 |否 |`0` |指定是否允许主播在网页端直播页面管理问卷。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播无法管理问卷。<br><br>* `1`：主播可以管理问卷。 |
|IsDocDisplayed |整数 |否 |`0` |指定是否允许主播在网页端直播页面管理文档。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播无法管理文档。<br><br>* `1`：主播可以管理文档。 |
|IsCheckInDisplayed |整数 |否 |`0` |指定是否允许主播在网页端直播页面管理签到。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播无法管理签到。<br><br>* `1`：主播可以管理签到。 |
|IsQuizDisplayed |整数 |否 |`0` |指定是否允许主播在网页端直播页面管理答题。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播无法管理答题。<br><br>* `1`：主播可以管理答题。 |
|IsLuckDrawDisplayed |整数 |否 |`0` |指定是否允许主播在网页端直播页面管理抽奖。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播无法管理抽奖。<br><br>* `1`：主播可以管理抽奖。 |
|IsAnnouncementDisplayed |整数 |否 |`0` |指定是否允许主播在网页端直播页面管理公告。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：主播无法管理公告。<br><br>* `1`：主播可以管理公告。 |


<span id="sitetags"></span>
#### SiteTags


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|值 |字符串 |是 |`1` |分类标签值。 |
|索引 |整数 |是 |`0` |分类标签的索引，用于标识在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。<br><br>取值范围：[0,19]。 |


<span id="textsitetags"></span>
#### TextSiteTags


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|值 |字符串 |是 |`3` |文本标签值。 |
|Index |整数 |是 |`0` |文本标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。<br><br>取值范围：[0,4]。 |


<span id="riskwarningsetting"></span>
#### RiskWarningSetting


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|IsRiskWarningEnable |整数 |否 |`0` |指定是否启用提醒弹窗。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。 |
|RiskWarningButtonText |字符串 |否 |`知道了` |提醒弹窗的按钮名称。 |
|RiskWarningContent |字符串 |否 |`欢迎来到直播间！请遵守主办方及您所在国家的法律法规，勿发送色情、违法、低俗或诽谤性质的评论。做其他观众的榜样。请勿通过恶意行为（如恶意攻击）扰乱直播间的良好秩序。如遇到与主播之间的私人商品推介，请自行判断。` |提醒内容。 |
|RiskWarningTitle |字符串 |否 |`提醒` |提醒弹窗的标题。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |长整型 |`17218312****` |直播间的活动 ID。 |
|ActivityIdStr |字符串 |`-` |已弃用。 |
|状态 |整数 |`-` |已弃用。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityBasicConfigAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "IsSDKPlayEnable": 1,
    "SDKPlayStatus": 2,
    "Name": "Live Room A",
    "LiveTime": 1666258566,
    "IsBeginLiveEnable": 0,
    "IsCoverImageEnable": 0,
    "CoverImageUrl": "https://example.image",
    "VerticalCoverImageUrl": "https://example.image",
    "IsPcBackImageEnable": 0,
    "PcBackImageUrl": "//example.image",
    "PcBackImageUrlDefault": "https://example.image",
    "IsMobileBackImageEnable": 0,
    "MobileBackImageUrl": "//example.image",
    "MobileBackImageUrlDefault": "https://example.image",
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
    "IsPreviewPromptEnable": 0,
    "PreviewPrompt": "The live stream will start soon.",
    "IsReservationEnable": 0,
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
    "IsColorSync": 0,
    "IsVideoChatDisplayed": 0,
    "IsSharedAddressDisplayed": 0,
    "IsReleaseNoticeDisplayed": 0,
    "IsInteractiveEnable": 1,
    "InteractiveShowSetting": {
        "IsQuestionnaireDisplayed": 1,
        "IsDocDisplayed": 1,
        "IsCheckInDisplayed": 1,
        "IsQuizDisplayed": 0,
        "IsLuckDrawDisplayed": 0,
        "IsAnnouncementDisplayed": 0
        },
    "EndTime": 1666358566,
    "IsAutoEndEnable": 0
    "RiskWarningSetting": {
        "IsRiskWarningEnable": 0,
        "RiskWarningTitle": "",
        "RiskWarningContent": "",
        "RiskWarningButtonText": ""
    },
}
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "UpdateActivityBasicConfigAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656358566
  },
  "Result": {
    "ActivityId": 17218312****,
    "ActivityIdStr": "",
    "Status": 0
  }
}
```


<span id="error-codes"></span>
## 错误码

下表列出了此 API 操作的专用错误码。通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。


|状态码 |错误码 |错误信息 |接口行为 |
|---|---|---|---|
|200 |100000 |EndTime 不能早于当前时间。 |请修改 `EndTime` 参数值后重试。 |
|200 |100000 |EndTime 不能早于 LiveTime。 |请修改参数 `EndTime` 或 `LiveTime` 的值后重试。 |
|200 |100000 |EndTime 不能晚于 LiveTime 72 小时。 |参数 `EndTime` 与 `LiveTime` 的最大差值为 259,200（72 小时）。请修改参数值后重试。 |
|200 |100000 |直播流过程中无法修改 EndTime 或 IsAutoEndEnable。 |请先结束直播流，然后再修改参数 `EndTime` 或 `IsAutoEndEnable` 的值。 |
|200 |100000 |直播流过程中无法修改 LiveTime 或 IsBeginLiveEnable。 |请先结束直播流，然后再修改参数 `LiveTime` 或 `IsBeginLiveEnable` 的值。 |
|200 |100000 |无效的 %s |参数无效。请根据规范修改参数值后重试。 |
