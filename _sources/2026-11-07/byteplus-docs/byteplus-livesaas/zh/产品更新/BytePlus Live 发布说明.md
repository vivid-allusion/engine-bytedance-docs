---
title: "BytePlus Live 发布说明"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-product-updates-zh-CN"
---

在此处可查阅 BytePlus Live 控制台、API 和 SDK 的所有变更。

## 2026年10月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|iOS 观播 SDK |新增支持通过 Swift Package Manager（SPM）集成 SDK。 |2026\-10\-23 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|AI Live |新增支持通过 RTMP 将 AI Live 直播流推送至 Shopee。使用 Live Connector 浏览器插件，还可以将 Shopee 直播间的观众评论同步至 BytePlus AI 直播间，由 AI 主播根据已配置的知识库和提示词生成并播报回复。 |2026\-10\-10 |[通过 RTMP 在 Shopee 上开启直播](https://docs.byteplus.com/docs/byteplus-livesaas/going-live-on-shopee-via-rtmp-zh-CN) |
|AI 直播 |新增支持使用 AI 生成直播脚本。你可以在脚本编辑区通过 AI 脚本生成，根据交互式提示创建文本脚本或商品脚本，并将生成内容应用到直播间。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2935c7392c634a4f851c4dc8e5dd754a~tplv-goo7wpa0wc-image.image) |2026\-10\-01 |[生成直播脚本](https://docs.byteplus.com/docs/byteplus-livesaas/generating-ai-live-scripts-zh-CN) |

## 2026年9月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|AI 直播 |形象复刻新增支持绿幕抠像模式。提交绿幕背景视频，并在复刻时选择**绿幕抠像**，即可获得透明背景的虚拟形象。同时，直播间装修新增支持静态图片、GIF、贴片视频和切镜视频，用户可根据场景维度更换直播间装修，使画面随不同脚本话术同步调整。 |2026\-09\-23 |* [管理素材库](https://docs.byteplus.com/docs/byteplus-livesaas/manage-live-room-visual-materials-zh-CN)<br><br>* [装饰直播间](https://docs.byteplus.com/docs/byteplus-livesaas/decorating-a-live-room-zh-CN)<br><br>* [训练虚拟形象和声音](https://docs.byteplus.com/docs/byteplus-livesaas/train-a-digital-human-and-voice-zh-CN) |
|AI Live |新增对通过 iframe 将 AI Live 控制台嵌入您自己网页的支持。借助 STS 临时凭证，您可以嵌入 AI Live 控制页、直播间列表、模型训练、商品库、知识库和服务中心等页面，让您的用户无需离开您的平台即可使用 AI Live 能力。 |2026\-09\-18 |[使用 iframe 嵌入 AI Live 控制台](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-ai-live-console-zh-CN) |

## 2026年8月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|AI Live |新增对以下功能的支持：<br><br><br>* **AI Rewrite**：开启后，在原始脚本被读完后，BytePlus Live 会利用 AI 扩展内容，并自动保存生成的内容，使 AI 主播能够持续输出新内容，避免重复。<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50421a278e504c74bbe9278872e30b0c~tplv-goo7wpa0wc-image.image)<br><br>* **Audience interaction**：AI 主播可主动响应观众的活动，例如加入直播、点赞、分享和关注。<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4b36f2893864a29a0ada23a1ee55070~tplv-goo7wpa0wc-image.image)<br><br>* **Pre\-live content check**：在开播前，BytePlus Live 支持检查您的内容并确保其已准备好进行直播。<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c18cb9f094484693b43c0e6359c3f601~tplv-goo7wpa0wc-image.image)<br><br>* **LIVE hours**：您可以设置直播时长，达到该时长后，直播将自动结束。 |2026\-08\-28 |[启动AI直播](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN) |
|Web 观播 SDK |发布了 2.0.31 版本，更新了 CSS 样式。 |2026\-08\-12 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2026年7月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|AI Live |AI Live 让你能够为你的电商店铺运行全天候、无人值守的直播流，从而实现 24/7 不间断销售并持续与购物者互动。它使用从真人克隆的 AI 形象作为主播，主持流，展示来自 TikTok Shop 或 Shopify 等渠道的商品，并实时回答观众的问题。你现在可以享受**免费试用**。 |2026\-07\-31 |[AI Live 概览](https://docs.byteplus.com/docs/byteplus-livesaas/digital-human-overview-zh-CN) |
|商品卡片 |新增对多环境直达链接功能的支持。现在可以配置最多5个环境，每个环境通过 User Agent 标识，并且可以在每个商品卡片上为每个环境设置独立的直达链接。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a82ea836309945ee9a64e8b27890db2a~tplv-goo7wpa0wc-image.image) |2026\-07\-23 |[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN) |
|直播模板 |新增支持在直播模板中配置商品卡片多UA、点赞和热门展示。 |2026\-07\-23 |[创建和使用直播模板](https://docs.byteplus.com/docs/byteplus-livesaas/docs-create-and-use-template-zh-CN) |
|服务端 OpenAPI |在[GetActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN)和[UpdateActivityProductAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN)中新增`UAInfo`和`DirectUrls`参数，以支持商品卡片多环境直达链接功能。 |2026\-07\-23 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Web 观播 SDK |发布了 2.0.30 版本，新增商品卡片多环境直达链接功能，并支持在直播模板中配置点赞和热门展示。从该版本开始，资源域名已更改为`https://res.gcloudcache.com/bp-fe`。 |2026\-07\-23 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|API 接口地址 |推荐的 BytePlus Live API 接口地址已更新为`https://livesaas.byteplusapi.com`。原接口地址`https://open.byteplusapi.com`仍可用。 |2026\-07\-10 |* [API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN)<br><br>* [关于 BytePlus Live API Endpoint 更新的公告](https://docs.byteplus.com/docs/byteplus-livesaas/endpoint-update-zh) |
|AI 直播分析 |新增支持通过 AI 分割、转录、分析标签和分段级优化建议对直播视频进行分析。 |2026\-07\-03 |[AI直播分析](https://docs.byteplus.com/docs/byteplus-livesaas/AI-Live-analysis-zh-CN) |

## 2026年4月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|iOS 观播 SDK |发布版本 1.66.1。 |2026\-04\-28 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 观播 SDK |发布版本 1.66.3。 |2026\-04\-28 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|BytePlus Live 应用 |优化了账号登录页。 |2026\-04\-16 |* [从 iOS 手机进行直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone-zh-CN)<br><br>* [使用 Android 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone-zh-CN) |
|服务端 OpenAPI |新增对部分互动工具的管理支持。 |2026\-04\-01 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |

## 2026年2月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Web 观播 SDK |发布版本 2.0.27\-beta.4。 |2026\-02\-02 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2026年1月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|服务端 OpenAPI |新增支持在[ActivityAutoReplayCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityautoreplaycallback-zh-CN)中展示与回放视频对应的直播流开始时间和结束时间。 |2026\-01\-27 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|服务端 OpenAPI |弃用ForbidLiveStreamAPI，该接口用于禁止直播间内特定直播源的流。 |2026\-01\-14 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Web 观播 SDK |发布版本 2.0.27\-beta.2 和 2.0.27\-beta.3。 |2026\-01\-12 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Web 观播 SDK |发布版本 2.0.27。 |2026\-01\-06 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2025年12月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Web 观播 SDK |发布版本 2.0.25，新增部分参数和事件，帮助你实现自定义的人气展示和商品逻辑。 |2025\-12\-10 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2025年11月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|iOS 观播 SDK |发布版本 1.65.2。 |2025\-11\-25 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布版本 1.65.2。 |2025\-11\-25 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布版本 1.65.1。 |2025\-11\-17 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布版本 1.65.1。 |2025\-11\-17 |iOS 开播 SDK 版本发布说明 |
|奖品库 |新增**奖品库**页面用于奖品管理。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39c6f735aa444d16a949a6ee7d9cbd8d~tplv-goo7wpa0wc-image.image) |2025\-11\-12 |[在奖品库中管理奖品](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-prizes-in-prize-library-zh-CN) |
|角色 |* 新增**媒体库** \> **奖品库** \> **仅查看**或**编辑**权限。<br><br>* 新增角色可访问或管理奖品的用户范围。 |2025\-11\-12 |[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN) |
|多语言 |观看页支持更多语言类型：<br><br><br>* 塔加拉语<br><br>* 高棉语<br><br>* 老挝语<br><br>* 缅甸语<br><br>* 马来语<br><br>* 印地语<br><br>* 法语<br><br>* 德语<br><br>* 意大利语 |2025\-11\-12 |* [为观看页配置多语言](https://docs.byteplus.com/docs/byteplus-livesaas/docs-configuring-multiple-languages-for-the-viewing-page-zh-CN)<br><br>* [管理聊天区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area-zh-CN) |
|礼物奖励 |各语言礼物名称的最大字符限制更新为50。 |2025\-11\-12 |[通过礼物奖励主播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts-zh-CN) |
|回放 |可发布的回放视频最大数量更新为200。 |2025\-11\-12 |[回放管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploading-a-video-on-demand-vod-zh-CN) |
|服务端 OpenAPI |* 直播间支持更多语言类型。<br><br>* 新增对账号下奖品管理的支持，包括新增、更新、删除和获取奖品信息。 |2025\-11\-12 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Web 观播 SDK |发布版本 2.0.24，新增对更多语言类型的支持。 |2025\-11\-12 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布版本 1.65.0，新增对更多语言类型的支持。 |2025\-11\-12 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Flutter 观播 SDK |发布版本 1.65.0\-1，新增对 Flutter 组件显示的支持。 |2025\-11\-12 |[Flutter 观众 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-building-viewer-sdk-for-flutter-zh-CN) |
|Android 开播 SDK |发布版本 1.65.0。 |2025\-11\-12 |Android 开播 SDK 更新日志 |
|iOS 观播 SDK |发布版本 1.65.0，新增悬浮窗图片视图配置、首选语言设置及更多语言类型。 |2025\-11\-12 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布版本 1.65.0。 |2025\-11\-12 |iOS 开播 SDK 版本发布说明 |

## 2025年10月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Android 观播 SDK |发布版本 1.64.1。 |2025\-10\-28 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Web 观播 SDK |发布了 2.0.23 版本，新增在观看页自定义商品信息和回放列表的支持。 |2025\-10\-16 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|演示 |新增支持主动开启画中画（PiP）功能、更新画中画中的 URL、静音和取消静音直播视频，以及调整画中画窗口大小。 |2025\-10\-16 |[将直播间 H5 页面嵌入到您的移动端 React Native 应用](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-react-zh-CN) |

## 2025年9月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|iOS 观播 SDK |发布了 1.64.0 版本，支持回放日志上报。 |2025\-09\-25 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.64.0 版本，支持推流日志上报。 |2025\-09\-25 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.64.0 版本，适配 Android 16 KB 特性，并支持回放日志上报。 |2025\-09\-25 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.64.0 版本，兼容 BytePlus Effects SDK v4.7.2，适配 Android 16 KB 特性，并支持推流日志上报。 |2025\-09\-25 |Android 开播 SDK 更新日志 |
|Web 观播 SDK |发布了 2.0.22 版本。 |2025\-09\-18 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|iOS 观播 SDK |发布了 1.63.0 版本，优化了中奖用户需填写信息的类型定义。 |2025\-09\-09 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.63.0 版本。 |2025\-09\-09 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.63.0 版本。 |2025\-09\-09 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.63.0 版本。 |2025\-09\-09 |Android 开播 SDK 更新日志 |
|Web 观播 SDK |发布了 2.0.21 版本。 |2025\-09\-05 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2025年8月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|快速开始 |新增 3 步快速入门指南，帮助新用户创建并开启直播。 |2025\-08\-28 |[开始直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-live-stream-zh-CN) |
|直播模板 |新增 3 个系统直播模板，每个模板包含不同场景的典型配置，包括电商、直播营销和在线教育。 |2025\-08\-28 |[创建和使用直播模板](https://docs.byteplus.com/docs/byteplus-livesaas/docs-create-and-use-template-zh-CN) |
|Web 观播 SDK |发布了 2.0.20 版本，新增部分事件，帮助你实现自定义礼物逻辑。 |2025\-08\-28 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|iOS 观播 SDK |发布了 1.62.1 版本，优化了商品卡片点击回调逻辑。 |2025\-08\-26 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.62.1 版本。 |2025\-08\-26 |iOS 开播 SDK 发布说明 |
|商品卡片 |商品卡片中商品名称和描述的字符限制提升至每种语言 255 个字符。 |2025\-08\-12 |[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN) |
|服务端 OpenAPI |商品卡片中 `Title` 和 `Remark` 的字符限制提升至 3315 个字符。 |2025\-08\-12 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Android 观播 SDK |发布了 1.62.0 版本。 |2025\-08\-12 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.62.0 版本，商品卡片中商品名称和描述的字符限制提升至每种语言 255 个字符。 |2025\-08\-12 |Android 开播 SDK 发行说明 |
|iOS 观播 SDK |发布了 1.62.0 版本。 |2025\-08\-12 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.62.0 版本，商品卡片中商品名称和描述的字符限制提升至每种语言 255 个字符。 |2025\-08\-12 |iOS 开播 SDK 发布说明 |
|Web 观播 SDK |发布了 2.0.19 版本，新增 `shareUrl` 参数，支持自定义直播间分享链接。 |2025\-08\-12 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|BytePlus Live 应用 |优化了商品卡片功能的用户体验。 |2025\-08\-12 |* [使用 iOS 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone-zh-CN)<br><br>* [使用 Android 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone-zh-CN) |

## 2025年7月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Android 观播 SDK |发布了 1.61.4 版本。 |2025\-07\-30 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.61.4 版本。 |2025\-07\-30 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.61.3 版本，支持自定义置顶评论和评论的行间距、圆角和文字颜色等属性。 |2025\-07\-28 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.61.3 版本。 |2025\-07\-28 |Android 开播 SDK 发行说明 |
|iOS 观播 SDK |发布了 1.61.2 版本，支持自定义置顶评论和评论的属性，如行间距、圆角和文字颜色。 |2025\-07\-28 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.61.2 版本。 |2025\-07\-28 |iOS 开播 SDK 发布说明 |
|计费情况 |支持在控制台订阅功能版本和资源包。 |2025\-07\-17 |[Subscription method](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods-zh-CN#48f4bdcd) |
|服务端 OpenAPI |支持获取指定账号创建的直播间、直播间竖屏模式下封面图的 URL，以及创建直播间的账号。 |2025\-07\-17 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|iframe |支持使用 iframe 嵌入控制台。 |2025\-07\-15 |[使用 iframe 嵌入控制台](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-iframe-to-embed-the-console-zh-CN) |
|媒体库 |* 支持将视频存储在视频库的指定分类下。<br><br>* 支持不同 IAM 用户上传或创建的视频和云剪项目的数据隔离。 |2025\-07\-15 |* [在视频库中管理视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-video-in-the-media-library-zh-CN)<br><br>* [管理临时存储中的视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-videos-in-the-media-library-zh-CN)<br><br>* [管理回放](https://docs.byteplus.com/docs/byteplus-livesaas/docs-uploading-a-video-on-demand-vod-zh-CN)<br><br>* [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN) |
|服务端 OpenAPI |* 支持获取 BytePlus Live 中指定账号的 STS 签名，然后可使用 iframe 将 BytePlus Live 控制台的功能模块嵌入到自己的页面。<br><br>* 支持获取媒体库下视频库或临时存储的视频信息，包括视频 ID 和名称。<br><br>* 支持将临时存储的视频转移到视频库的指定分类，实现永久存储。<br><br>* 支持获取账号下默认分类或指定分类及其子分类的信息。 |2025\-07\-15 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Android 观播 SDK |发布了 1.60.0 版本，优化了观看页实时抽奖功能的 UI 样式。 |2025\-07\-15 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.60.0 版本。 |2025\-07\-15 |Android 开播 SDK 发行说明 |
|iOS 观播 SDK |发布了 1.60.0 版本，包含对观看页实时抽奖功能 UI 样式的优化。 |2025\-07\-15 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.60.0 版本。 |2025\-07\-15 |iOS 开播 SDK 发布说明 |
|Web 观播 SDK |发布了 2.0.17 版本，新增部分参数和事件，帮助你实现礼物和商品的自定义逻辑。 |2025\-07\-15 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Demo |简化了开发流程，在移动端 Native 和 React Native 应用中自动实现画中画、自动播放等功能，无需手动触发 Web 事件。 |2025\-07\-01 |* [将直播间H5页面嵌入你的移动React Native应用](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-react-zh-CN)<br><br>* [将直播间H5页面嵌入到你的移动原生应用中](https://docs.byteplus.com/docs/byteplus-livesaas/docs-entering-a-live-room-to-live-stream-via-your-app-zh-CN) |
|Web 观播 SDK |发布了 2.0.16 版本。 |2025\-07\-01 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布了 1.59.0 版本。 |2025\-07\-01 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.59.0 版本。 |2025\-07\-01 |Android 开播 SDK 发行说明 |
|iOS 观播 SDK |发布了 1.59.0 版本。 |2025\-07\-01 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.59.0 版本。 |2025\-07\-01 |iOS 开播 SDK 发布说明 |

## 2025年6月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Viewer SDK for Flutter |发布了 1.58.0\-1 版本，移除了 iOS 部分依赖，新增支持配置是否启用自动播放功能，并新增画中画功能支持。 |2025\-06\-23 |[Flutter 观众 SDK 发行说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-building-viewer-sdk-for-flutter-zh-CN) |
|Web 观播 SDK 演示 |新增了 PC 端演示。观众打开网页时，视频列表中的第一个播放器自动播放视频。当观众鼠标悬停在其他播放器上时，该播放器自动播放视频。观众停止悬停所有播放器后，最后悬停的播放器视频继续播放。 |2025\-06\-16 |[Web 观播 SDK 的自动播放演示](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos-zh-CN) |
|Android 观播 SDK |发布了 1.58.0 版本，支持设置画中画窗口在锁屏时是否暂停播放视频。 |2025\-06\-04 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.58.0 版本，优化了部分泰语 UI 文本。 |2025\-06\-04 |Android 开播 SDK 发行说明 |
|iOS 观播 SDK |发布了 1.58.0 版本。 |2025\-06\-04 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.58.0 版本，优化了部分泰语 UI 文本。 |2025\-06\-04 |iOS 开播 SDK 发布说明 |

## 2025年5月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|iOS 开播 SDK |发布了 1.57.0 版本，优化了 SDK 日志上报能力，提升故障排查效率。 |2025\-05\-20 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布了 1.57.0 版本，优化了 SDK 日志上报能力，提升故障排查效率。 |2025\-05\-20 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 开播 SDK |发布了 1.57.0 版本，优化了 SDK 日志上报能力，提升故障排查效率。 |2025\-05\-20 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.57.1 版本，优化了 SDK 日志上报能力，提升故障排查效率。 |2025\-05\-20 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Web 观播 SDK |发布了 2.0.15 版本，新增支持自定义错误页：当账号下所有状态为**直播**的直播间总峰值并发用户数（PCU）超出并发上限时，可展示自定义错误页。 |2025\-05\-15 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|BytePlus Live 应用 |* 支持切换应用语言为以下选项：<br><br>   * 简体中文<br><br>   * 英文<br><br>   * 日文<br><br>   * 繁体中文<br><br>   * 韩文<br><br>   * 泰文<br><br>   * 越南文<br><br>   * 阿拉伯文<br><br>   * 土耳其文<br><br>   * 西班牙文<br><br>   * 印尼文<br><br>   * 葡萄牙文<br><br>   * 俄文<br><br>* 已开启多语言及评论翻译功能后，主播可发送多语言评论，提升主播评论在多语言环境下的准确传达。<br><br>* 已开启多语言功能后，支持为以下内容设置多语言版本，在观看页中以对应语言展示。<br><br>   * 直播间名称<br><br>   * 直播间描述<br><br>   * 主播账号名称<br><br>   * 商品名称<br><br>   * 现价<br><br>   * 原价<br><br>   * 商品 URL |2025\-05\-12 |* [使用 iOS 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone-zh-CN)<br><br>* [使用 Android 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone-zh-CN) |
|iOS 开播 SDK |发布了 1.56.1 版本。 |2025\-05\-06 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布了 1.56.1 版本。 |2025\-05\-06 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |

## 2025年4月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|多平台推流 |预录制视频不支持多平台推流功能。 |2025\-04\-29 |* [将 BytePlus Live 的直播流同步到第三方平台](https://docs.byteplus.com/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms-zh-CN)<br><br>* [启动预录制视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-the-carousel-zh-CN) |
|iOS 开播 SDK |发布了 1.56.0 版本，新增支持设置 SDK 语言类型及自定义 SDK 展示文本。 |2025\-04\-29 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布了 1.56.0 版本，初始化方法有变更。 |2025\-04\-29 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 开播 SDK |发布了 1.56.0 版本，新增支持设置 SDK 语言类型及自定义 SDK 展示文本。 |2025\-04\-29 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.56.0 版本。 |2025\-04\-29 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.55.1 版本。 |2025\-04\-16 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布了 1.55.1 版本。 |2025\-04\-16 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 开播 SDK |发布了 1.55.2 版本。 |2025\-04\-15 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.55.2 版本，新增支持将观众踢出直播间及封禁观众 IP 地址。 |2025\-04\-15 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.55.0 版本。 |2025\-04\-15 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布了 1.55.0 版本，新增支持将观众踢出直播间及封禁观众 IP 地址。 |2025\-04\-15 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 开播 SDK |发布了 1.54.2 版本。<br><br>> **注意**<br><br><br>> Android 开播 SDK 1.49.0 \- 1.54.1 版本存在日志事件上报问题。为避免影响线上问题排查，请将这些版本升级至 1.54.2。<br> |2025\-04\-07 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.54.2 版本。<br><br>> **注意**<br><br><br>> Android 观播 SDK 1.49.0 \- 1.54.1 版本存在日志事件上报问题。为避免影响线上问题排查，请将这些版本升级至 1.54.2。<br> |2025\-04\-07 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.54.1 版本。 |2025\-04\-03 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.54.1 版本。 |2025\-04\-03 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |本次版本修改了导入开播 SDK 时的 SDK 版本后缀。 |2025\-04\-01 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布了 1.54.0 版本，该版本在导入 Android 观播 SDK 时修改了 SDK 版本后缀，并支持设置评论输入框允许输入的最大字符数。 |2025\-04\-01 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.54.0 版本。 |2025\-04\-01 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布了 1.54.0 版本，支持设置评论输入框允许输入的最大字符数，以及设置评论输入框内输入文字的颜色。 |2025\-04\-01 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |

## 2025年3月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Web 观播 SDK 演示 |在手机端左右滑动场景下，新增了当播放器完全展示时自动播放视频的演示。 |2025\-03\-28 |[Web 观播 SDK 自动播放演示](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos-zh-CN) |
|Web 观播 SDK |发布了 2.0.13 版本，支持设置是否禁用评论输入框、指定禁用评论输入框的占位符文本，以及自定义禁用评论输入框的样式。 |2025\-03\-19 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 开播 SDK |发布了 1.53.0 版本。 |2025\-03\-18 |Android 开播 SDK 更新日志 |
|Android 观播 SDK |发布了 1.53.0 版本，支持自定义评论输入框和评论区样式。 |2025\-03\-18 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.53.0 版本。 |2025\-03\-18 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.53.0 版本，支持自定义评论输入框和评论区样式。 |2025\-03\-18 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 观播 SDK |发布了 1.52.1 版本，支持关注主播，并新增韩语、泰语、越南语、阿拉伯语、土耳其语、西班牙语、印尼语、葡萄牙语和俄语的语言支持。 |2025\-03\-04 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.52.0 版本。 |2025\-03\-04 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.52.0 版本，支持关注主播，并新增韩语、泰语、越南语、阿拉伯语、土耳其语、西班牙语、印尼语、葡萄牙语和俄语的语言支持。 |2025\-03\-04 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |

## 2025年2月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|BytePlus Live 应用 |新增支持在控制台和其他页面同步删除评论。 |2025\-02\-26 |* [从 iOS 手机进行直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone-zh-CN)<br><br>* [使用 Android 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone-zh-CN) |
|服务端 OpenAPI |支持根据特定规则和顺序对直播间进行排序，并根据分类标签值对直播间进行筛选。 |2025\-02\-25 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Android 开播 SDK |发布了 1.51.1 版本，支持在控制台和其他页面同步删除评论。 |2025\-02\-24 |Android 开播 SDK 更新日志 |
|Android 观播 SDK |发布了 1.51.1 版本。 |2025\-02\-24 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.51.1 版本，支持在控制台和其他页面同步删除评论。 |2025\-02\-24 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.51.1 版本。 |2025\-02\-24 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|服务端 OpenAPI |* 支持将商品置顶到菜单顶部并在观看页以悬浮窗形式展示，或将商品恢复到菜单下原位置并从观看页悬浮窗移除。<br><br>* 新增回调 `ActivityExplainProductCallBack`，当你的直播间中的商品出现以下任一情况时触发：<br><br>   * 置顶到菜单顶部并在观看页以悬浮窗形式展示。<br><br>   * 已恢复至菜单下的原始位置，不再在观看页以悬浮窗形式显示。 |2025\-02\-20 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Android 观播 SDK |发布了 1.51.0 版本，新增支持设置是否在刊例价上显示删除线。 |2025\-02\-18 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.51.0 版本。 |2025\-02\-18 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.51.0 版本，新增支持设置是否在刊例价上显示删除线。 |2025\-02\-18 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |

## 2025年1月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|免费试用版 |将免费试用期由 14 天调整为 1 个月，观看时长由 120 分钟调整为 3000 分钟。 |2025\-01\-24 |* [订阅计费方式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods-zh-CN)<br><br>* [开启直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-live-stream-zh-CN) |
|BytePlus Live 应用 |* 优化了应用的登录页。<br><br>* 修复了部分问题。 |2025\-01\-23 |* [从 iOS 手机进行直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone-zh-CN)<br><br>* [使用 Android 手机进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone-zh-CN) |
|Android 开播 SDK |发布了 1.50.0 版本。 |2025\-01\-21 |Android 开播 SDK 更新日志 |
|Android 观播 SDK |发布了 1.50.0 版本，支持设置热度标签文本的字体大小和颜色。 |2025\-01\-21 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.50.0 版本。 |2025\-01\-21 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.50.0 版本，支持配置热度图标，以及热度标签文本的字体、字体大小和颜色。 |2025\-01\-21 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|服务端 OpenAPI |支持根据外部平台 ID 筛选主播账号。 |2025\-01\-16 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Android 开播 SDK |发布了 1.49.0 版本，包含加入直播间方法的参数修改。 |2025\-01\-08 |Android 开播 SDK 更新日志 |
|Android 观播 SDK |发布了 1.49.0 版本。 |2025\-01\-08 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.49.0 版本，包含 SDK 导入 URL 和集成 SDK 时需添加的 BPLive 依赖项的变更。 |2025\-01\-08 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.49.0 版本，包含 SDK 导入 URL 和集成 SDK 时需添加的 BPLive 依赖项的变更。 |2025\-01\-08 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |

## 2024年12月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|服务开通 |优化了 BytePlus Live 服务的开通流程。 |2024\-12\-24 |[Step 1: Activate the BytePlus Live service](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-live-stream-zh-CN) |
|商品卡片菜单 |当 BytePlus Live 调用你的自有 API 后返回错误信息（即你的自有 API 中 `Message` 参数的值），该错误信息会显示在集成了 iOS 或 Android 开播 SDK 的应用上。 |2024\-12\-24 |[Response parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN) |
|Android 开播 SDK |发布了 1.48.0 版本。 |2024\-12\-24 |Android 开播 SDK 更新日志 |
|Android 观播 SDK |发布了 1.48.0 版本。 |2024\-12\-24 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK |发布了 1.48.0 版本。 |2024\-12\-24 |iOS 开播 SDK 版本发布说明 |
|iOS 观播 SDK |发布了 1.48.0 版本。 |2024\-12\-24 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 观播 SDK |发布了 1.47.3 版本，支持在直播间右上角显示自定义悬浮视图组件。 |2024\-12\-10 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK |发布了 1.47.3 版本，支持在直播间右上角显示自定义悬浮视图。 |2024\-12\-10 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.47.3 版本。 |2024\-12\-10 |iOS 开播 SDK 版本发布说明 |
|Web 观播 SDK |发布了 2.0.11 版本，提升了表情显示速度。 |2024\-12\-10 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|商品卡片菜单 |更新了自有商品库的功能。<br><br><br>* 为防止由于系统中的产品数量超过指定上限而导致无法返回产品的问题，您可以联系 BytePlus Live 技术支持，将您的 BytePlus 账号添加至 allowlist。随后，您可以基于自研 API 中新增的参数 `FilterName` 返回筛选后的产品。更多信息，请参见 [Process](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN#32f5a471)。<br><br>* 若 BytePlus Live 调用您的自研 API 后返回错误信息（即自研 API 中 `Message` 参数的值），该错误信息会在控制台显示。更多信息，请参见 [Response parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。 |2024\-12\-05 |[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN) |
|Web 观播 SDK 演示 |优化了自动播放演示，支持观众在观看页点击标签时加载对应分类标签值的直播间。您可以通过完成以下步骤实现该功能：<br><br><br>1. 在控制台为直播间添加分类标签值。<br><br>2. 调用 `ListActivityFeedInfosAPI`。现在，您可以通过调用该 API 获取每个直播间的分类标签列表。<br><br>3. 当观众在观看页点击标签时，调用您的自研 API，并将 `ActivityTag` 参数设置为该标签对应的分类标签值。 |2024\-12\-05 |* [Classifying live rooms](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos-zh-CN)<br><br>* [ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi) |
|iframe |* 新增参数以自定义嵌入页面。<br><br>* 新增事件。检测到特定事件后，您可以执行自定义后续操作。 |2024\-12\-05 |* [使用 iframe 嵌入观看页](https://docs.byteplus.com/docs/byteplus-livesaas/docs-docs-embedding-a-viewing-page-with-iframe-zh-CN)<br><br>* [参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-parameter-zh-CN)<br><br>* [事件](https://docs.byteplus.com/docs/byteplus-livesaas/docs-embedding-a-viewing-page-with-iframe-zh-CN)<br><br>* [类型详情](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-zh-CN) |
|iOS 观播 SDK |发布了 1.47.2 版本，支持使用 TTSDK 的静态库版本。 |2024\-12\-03 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.47.2 版本，支持使用 TTSDK 的静态库版本。 |2024\-12\-03 |iOS 开播 SDK 版本发布说明 |

## 2024年11月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Flutter 观播 SDK |发布了 Flutter 观播 SDK 的首个版本。 |2024\-11\-29 |* [集成 Flutter 观众 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-flutter-zh-CN)<br><br>* [功能实现](https://docs.byteplus.com/docs/byteplus-livesaas/docs-feature-the-viewer-sdk-for-flutter-zh-CN)<br><br>* [类型详情](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-flutter-zh-CN) |
|Android 观播 SDK |发布了 1.47.2 版本，支持设置浮标广告是否显示白色边框和背景。 |2024\-11\-26 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.47.1 版本。 |2024\-11\-26 |Android 开播 SDK 更新日志 |
|iOS 观播 SDK |发布了 1.47.1 版本。 |2024\-11\-26 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.47.1 版本。 |2024\-11\-26 |iOS 开播 SDK 版本发布说明 |
|服务端 OpenAPI |支持一次获取一个或多个直播间的商品库信息。 |2024\-11\-21 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|服务端 OpenAPI |* 支持设置返回直播间的排序规则和顺序。<br><br>* 支持新增主播账号、更新已有主播账号信息、删除主播账号，以及获取账号下的主播账号信息。<br><br>* 支持更新直播间关联的主播账号，并配置是否在直播间启用账号设置功能。<br><br>* 获取特定直播间关联的主播账号信息时，新增返回参数用于指示观众是否允许在观看页关注主播。 |2024\-11\-07 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|直播间排序 |控制台现已支持以下规则对直播间进行排序：<br><br><br>* 创建时间升序<br><br>* 创建时间降序<br><br>* 开始时间升序<br><br>* 开始时间降序<br><br>* 直播优先<br><br>* 结束优先<br><br><br>默认顺序为先按直播间状态升序（直播、预告、回放、结束）排序，再在每个状态内按开始时间降序排序。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be866e8d50ae44b08f6d26ffd022b991~tplv-goo7wpa0wc-image.image) |2024\-11\-07 |\- |
|Android 观播 SDK |发布了 1.46.3 版本，支持设置是否在竖屏模式下直播间顶部显示渐变遮罩。如果你的视频背景为白色，显示渐变遮罩可以让直播间顶部的白色文字更加清晰可见。 |2024\-11\-07 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |

## 2024年10月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|Android 观播 SDK |发布了 1.46.2 版本，现已兼容 Android 15。 |2024\-10\-31 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.46.2 版本，现已兼容 Android 15。 |2024\-10\-31 |Android 开播 SDK 更新日志 |
|iOS 观播 SDK |发布了 1.46.1 版本，现已兼容 iOS 18。 |2024\-10\-31 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.46.1 版本，现已兼容 iOS 18。 |2024\-10\-31 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.46.1 版本。 |2024\-10\-28 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.46.1 版本。 |2024\-10\-28 |Android 开播 SDK 更新日志 |
|iOS 观播 SDK |发布了 1.46.0 版本，包含以下新功能：<br><br><br>* 新增支持自定义正在播放信息。<br><br>* 新增支持设置是否响应正在播放信息区域的用户操作。<br><br><br>如下所示，正在播放信息区域适用于你的应用播放的媒体。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/431054e406a74ac2bbe857ece5b7af0a~tplv-goo7wpa0wc-image.image) |2024\-10\-24 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.46.0 版本。 |2024\-10\-24 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.46.0 版本。 |2024\-10\-24 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Web 观播 SDK 演示 |优化了演示，包括：<br><br><br>* 新增支持观众在观看页点击标签时加载指定直播间。<br><br>* 在自研 API 中新增请求参数 `ActivityTag`，用于观众在观看页点击标签时加载指定直播间。<br><br>* 新增支持自定义是否隐藏观看页所有标签并在列表中展示所有直播间。<br><br>* 新增支持观众从视频详情页返回直播间列表时，在你的应用中以画中画模式播放视频。<br><br>* 减少从直播间列表跳转到视频详情页时的空白屏时长。 |2024\-10\-21 |[Web 观播 SDK 自动播放演示](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos-zh-CN) |
|观看页多语言 |新增支持观看页以下语言，以及观看页支持的所有语言之间的评论翻译。<br><br><br>* 泰语<br><br>* 越南语<br><br>* 阿拉伯语<br><br>* 土耳其语<br><br>* 西班牙语<br><br>* 印尼语<br><br>* 葡萄牙语<br><br>* 俄语 |2024\-10\-15 |* [为观看页配置多语言](https://docs.byteplus.com/docs/byteplus-livesaas/docs-configuring-multiple-languages-for-the-viewing-page-zh-CN)<br><br>* [管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)<br><br>* [管理聊天区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area-zh-CN) |
|Web 观播 SDK |发布了 2.0.6 版本，包含以下新功能：<br><br><br>* 新增支持观看页以下语言：<br><br>   * 泰语<br><br>   * 越南语<br><br>   * 阿拉伯语<br><br>   * 土耳其语<br><br>   * 西班牙语<br><br>   * 印尼语<br><br>   * 葡萄牙语<br><br>   * 俄语<br><br>* 新增支持配置观看页默认语言。观众加入直播间时，无论 PC 浏览器默认语言或移动设备系统语言如何，页面将设置为配置的默认语言。<br><br>* 新增方法获取观看页支持的语言，并在你有自定义切换语言按钮时切换到指定语言。 |2024\-10\-15 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布了 1.45.0 版本，包含竖屏模式下直播间 UI 样式优化。 |2024\-10\-15 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK |发布了 1.45.0 版本，包含竖屏模式下直播间 UI 样式优化。 |2024\-10\-15 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.45.0 版本。启用 BytePlus Live 控制台的直播流开播时间功能或调用服务端 API 后，主播只能在指定的开播时间之后开播。 |2024\-10\-15 |iOS 开播 SDK 版本发布说明 |
|Android 开播 SDK |发布了 1.45.0 版本。启用 BytePlus Live 控制台的直播流开播时间功能或调用服务端 API 后，主播只能在指定的开播时间之后开播。 |2024\-10\-15 |Android 开播 SDK 更新日志 |
|开播 |新增开播时间开关。开启开关后，只能在指定的开播时间之后开播。 |2024\-10\-10 |[仅在指定时间后开始直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-an-auto-start-zh-CN) |
|通过网页浏览器开播 |支持配置主播可在直播间观看页管理的互动工具。 |2024\-10\-10 |[通过网页浏览器进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser-zh-CN) |
|服务端 OpenAPI |* 支持配置是否启用直播流开播时间功能。启用后，只能在指定的开播时间之后开播。<br><br>* 支持配置是否允许主播仅在网页浏览器的直播间观看页管理指定的互动工具。<br><br>* 支持配置主播可在网页浏览器的直播间观看页管理哪些互动工具。<br><br>* 支持获取上述所有配置。<br><br>* 新增错误码 `200027`。 |2024\-10\-10 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |

## 2024年9月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|商品卡片菜单 |支持在 Shopify 商品库中不展示指定商品。 |2024\-09\-26 |[Not displaying specific products in Shopify product library](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN#bd977a0e) |
|服务端 OpenAPI |新增 [ListActivityFeedInfosAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi)，用于获取 BytePlus 账号及 IAM 用户下所有现有直播间的基本信息，包括封面图、虚拟热度、主播账号和创建时间。 |2024\-09\-26 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Web 观播 SDK 演示 |运行自动播放演示后，可在手机上上下滑动观看页。播放器完全展示时，直播视频、预告或回放会自动播放。 |2024\-09\-26 |[Web 观播 SDK 自动播放演示](https://docs.byteplus.com/docs/byteplus-livesaas/docs-running-the-demos-zh-CN) |
|签到 |* 签到时长单位由分钟改为秒。<br><br>* 新增支持按计划时间发送签到。<br><br>* 支持将未按时签到的观众踢出。 |2024\-09\-12 |[发送签到](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-questionnaire-zh-CN) |
|Web 观播 SDK |发布了 2.0.5 版本，优化签到功能，包括将签到时长单位由分钟改为秒，以及将未按时签到的观众踢出。 |2024\-09\-12 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布了 1.44.0 版本，支持签到功能。 |2024\-09\-12 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK |发布了 1.44.0 版本，支持签到功能。 |2024\-09\-12 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.44.0 版本。 |2024\-09\-12 |iOS 开播 SDK 版本发布说明 |
|Web 观播 SDK |发布了 2.0.4 版本。 |2024\-09\-05 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|iOS 观播 SDK |发布了 1.43.3 版本。 |2024\-09\-04 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.43.3 版本。 |2024\-09\-04 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.43.4 版本。 |2024\-09\-04 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |

## 2024年8月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|多平台推流 |【文档更新】新增如何同步直播流到 Instagram 的章节。 |2024\-08\-28 |[Instagram](https://docs.byteplus.com/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms-zh-CN) |
|Android 观播 SDK |发布了 1.43.3 版本。 |2024\-08\-28 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Web 观播 SDK |发布了 2.0.3 版本，支持自定义竖屏模式下直播间图标的样式和背景色。 |2024\-08\-23 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|iOS 观播 SDK |发布了 1.43.2 版本，新增用于配置在清屏时是否显示关闭直播间按钮的属性。 |2024\-08\-22 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.43.2 版本。 |2024\-08\-22 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.43.2 版本，新增用于配置在清屏时是否显示关闭直播间按钮的方法。 |2024\-08\-22 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 观播 SDK |发布了 1.43.1 版本。 |2024\-08\-20 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|商品卡片菜单 |* 支持管理商品库并从商品库添加商品。<br><br>* 在移动设备横屏模式下新增购物车图标。 |2024\-08\-15 |[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN) |
|服务端 OpenAPI |新增和更新了部分 OpenAPI。 |2024\-08\-15 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|iOS 观播 SDK |发布了 1.43.0 版本，支持在横屏模式下显示购物车图标。 |2024\-08\-15 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.43.0 版本，支持从商品库添加商品和自定义美颜、滤镜、贴纸。 |2024\-08\-15 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.43.0 版本，支持在横屏模式下显示购物车图标。 |2024\-08\-15 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.43.0 版本，支持从商品库添加商品和自定义美颜、滤镜、贴纸。 |2024\-08\-15 |Android 开播 SDK 更新日志 |
|Web 观播 SDK |发布了 2.0.2 版本，支持在移动设备横屏模式下显示购物车图标。 |2024\-08\-15 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|iOS 观播 SDK |发布了 1.42.1 版本。 |2024\-08\-06 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.42.1 版本。 |2024\-08\-06 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.42.1 版本。 |2024\-08\-06 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|连麦（主播与主播） |* 优化了 UI。<br><br>* 默认视图由画廊视图改为主讲人视图。 |2024\-08\-06 |[与嘉宾开启连麦（主播与主播）](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-a-video-chat-zh-CN) |
|iOS 观播 SDK |发布了 1.42.0 版本。 |2024\-08\-01 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.42.0 版本。 |2024\-08\-01 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.42.0 版本。 |2024\-08\-01 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |

## 2024年7月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|BytePlus Live 控制台 |优化了聊天互动菜单、**安全控制**页面和**直播控制**页面的 UI。 |2024\-07\-23 |* [管理聊天区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area-zh-CN)<br><br>* [配置安全控制](https://docs.byteplus.com/docs/byteplus-livesaas/docs-configuring-security-control-zh-CN)<br><br>* [管理直播源](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming-zh-CN)<br><br>* [为直播间点赞](https://docs.byteplus.com/docs/byteplus-livesaas/docs-liking-a-live-stream-or-comment-zh-CN)<br><br>* [将所有观众静音](https://docs.byteplus.com/docs/byteplus-livesaas/docs-muting-viewers-zh-CN)<br><br>* [将观众踢出或屏蔽观众的 IP 地址](https://docs.byteplus.com/docs/byteplus-livesaas/docs-kick-out-or-block-zh-CN)<br><br>* [超低延时直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-ultra-low-latency-zh-CN)<br><br>* [通过网页浏览器进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser-zh-CN) |
|服务端 OpenAPI |* 新增回调 `ActivityClickReservationCallBack`。<br><br>* 新增接口 `GetActivityReservationAPIV2`。 |2024\-07\-23 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|iOS 观播 SDK |发布了 1.41.0 版本。 |2024\-07\-23 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.41.0 版本。 |2024\-07\-23 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.41.0 版本。 |2024\-07\-23 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Web 观播 SDK |发布了 2.0.1 版本。 |2024\-07\-23 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Web 观播 SDK |发布了 2.0.0 版本。 |2024\-07\-09 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2024年6月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|iOS 观播 SDK |发布了 1.40.1 版本。 |2024\-06\-28 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.40.1 版本。 |2024\-06\-28 |iOS 开播 SDK 版本发布说明 |
|Android 观播 SDK |发布了 1.40.0 版本，包含新增部分回调、优化 UI 风格及部分方法参数变更。 |2024\-06\-27 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布了 1.40.0 版本，支持根据 BytePlus Live 服务端配置自动结束直播流。 |2024\-06\-27 |Android 开播 SDK 更新日志 |
|云剪辑 |新增云剪辑功能支持。 |2024\-06\-26 |* [在云剪辑中编辑视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-edit-videos-in-the-cloud-zh-CN)<br><br>* [编辑直播视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-edit-video-zh-CN) |
|媒体库 |* 支持批量上传多个视频。<br><br>* 优化了 UI。 |2024\-06\-26 |* [在视频库中管理视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-video-in-the-media-library-zh-CN)<br><br>* [管理临时存储中的视频](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-videos-in-the-media-library-zh-CN) |
|iOS 观播 SDK |发布了 1.40.0 版本，支持在竖屏模式下显示图形菜单、优化 UI 风格并新增部分属性和方法。 |2024\-06\-26 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.40.0 版本，支持根据 BytePlus Live 服务端配置自动结束直播流。 |2024\-06\-26 |iOS 开播 SDK 版本发布说明 |
|服务端 OpenAPI |新增参数 `EndTime` 和 `IsAutoEndEnable`。 |2024\-06\-25 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|自动结束直播流 |新增对自动结束直播流的支持。 |2024\-06\-25 |[自动结束直播流](https://docs.byteplus.com/docs/byteplus-livesaas/automatically-ending-a-live-stream-zh-CN) |
|Web 观播 SDK |发布 1.3.8 版本，支持在引入 CSS 和 JS 资源时，移除 URL 中 `byteplus` 紧跟在 `mobile/` 或 `pc/` 后的部分。 |2024\-06\-25 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布 1.39.3 版本。 |2024\-06\-18 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|服务端 OpenAPI |将 `ForbidTime` 参数的最大值和默认值由 7 × 24 × 60 × 60 修改为 31 × 24 × 60 × 60。 |2024\-06\-12 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Android 观播 SDK |发布 1.39.2 版本。 |2024\-06\-12 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK |发布 1.39.1 版本，支持优化 SDK 包体积、配置是否显示指定按钮、设置评论区自定义回调，以及设置是否支持在横屏模式下编辑封面图和直播间标题。 |2024\-06\-11 |Android 开播 SDK 更新日志 |
|Android 观播 SDK |发布 1.39.1 版本，新增部分方法。 |2024\-06\-11 |[Android 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK |发布 1.39.0 版本，更新集成 SDK 时需添加的 BPLive 依赖。 |2024\-06\-07 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布 1.39.0 版本，更新集成 SDK 时需添加的 BPLive 依赖，并支持配置是否显示指定按钮、是否支持编辑直播间信息，以及自定义评论单元格。 |2024\-06\-07 |iOS 开播 SDK 版本发布说明 |
|计费情况 |* 新增直播并发观众套餐。<br><br>* 支持查看超低延迟相关资源用量。 |2024\-06\-07 |* [订阅计费方式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods-zh-CN)<br><br>* [查看资源使用情况和购买记录](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewing-resource-usage-zh-CN) |
|超低延迟 |支持超低延迟功能。 |2024\-06\-07 |* [超低延时直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-ultra-low-latency-zh-CN)<br><br>* [管理直播源](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming-zh-CN)<br><br>* [推流（以 OBS 为例）](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pushing-streams-zh-CN)<br><br>* [查看直播间数据](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics-zh-CN)<br><br>* [在数据中心查看数据](https://docs.byteplus.com/docs/byteplus-livesaas/docs-checking-your-streaming-statistics-zh-CN) |
|Web 观播 SDK |发布 1.3.3 版本，支持超低延迟功能。 |2024\-06\-07 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|服务端 OpenAPI |新增回调 [ActivityQuestionChatCallBack](https://docs.byteplus.com/docs/byteplus-livesaas/activityquestionchatcallback-zh-CN) 及以下 API 操作。<br><br><br>* [ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN)<br><br>* [GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-CN)<br><br>* [ListQuestionChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listquestionchatapi-zh-CN)<br><br>* [ListAnswerChatAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listanswerchatapi-zh-CN) |2024\-06\-06 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Web 观播 SDK |发布 1.3.2 版本。 |2024\-06\-06 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2024年5月

|功能 |接口行为 |发布日期 |相关文档 |
|---|---|---|---|
|网页端开播 |支持配置是否在直播页显示连麦（主播与主播）功能、观看页地址或锁定预告功能。 |2024\-05\-31 |[通过网页浏览器进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser-zh-CN) |
|服务端 OpenAPI |* 新增 [GetWebPushLiveClientWithExpiryAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-CN)。<br><br>* 新增部分请求和返回调用结果参数。 |2024\-05\-31 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|iOS 观播 SDK |发布 1.35.0 版本，增强兼容性。 |2024\-05\-30 |[iOS 观播 SDK 版本更新说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布 1.35.0 版本。 |2024\-05\-30 |iOS 开播 SDK 版本发布说明 |
|网页端开播 |* 支持白板共享。<br><br>* 支持文档和图片共享。 |2024\-05\-20 |* [共享白板](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sharing-documents-and-pictures-zh-CN)<br><br>* [共享文档和图片](https://docs.byteplus.com/docs/byteplus-livesaas/share-doc-and-pic)<br><br>* [通过网页浏览器进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser-zh-CN) |
|网页端开播 |* 支持选择 OBS 虚拟摄像头。<br><br>* 新增问答菜单。 |2024\-05\-11 |[通过网页浏览器进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser-zh-CN) |
|BytePlus Live 控制台 |* 新增以下功能：<br><br>   * 答题<br><br>   * 公告<br><br>   * 奖品库<br><br>   * 频道<br><br>   * 试看<br><br>   * 二次观看限制<br><br>   * 观众列表<br><br>   * 内嵌链接菜单<br><br>   * 白名单观看限制<br><br>   * 主播账号库<br><br>   * 匿名评论<br><br>   * 重复登录防护<br><br>   * 评论举报<br><br>* 支持踢出观众并拉黑观众 IP 地址。<br><br>* 支持在网页端直播页发送问卷、签到等互动内容。<br><br>* 优化实时抽奖，支持配置参与条件、白名单、黑名单等功能。<br><br>* 支持观众关注主播账号。<br><br>* 支持发送非匿名问卷。<br><br>* 支持配置轮播视频播放次数。<br><br>* 支持配置 PC 端观看页商品浮窗的展示位置。<br><br>* 支持为商品卡片添加商品备注，并将商品卡片置顶于商品卡片菜单。 |2024\-05\-10 |* [发送答题](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-vote-zh-CN)<br><br>* [发送公告](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-graphic-message-zh-CN)<br><br>* [管理互动区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area-zh-CN)<br><br>* [通过网页浏览器进行直播流](https://docs.byteplus.com/docs/byteplus-livesaas/docs-live-streaming-from-your-web-browser-zh-CN)<br><br>* [管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)<br><br>* [管理聊天区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-chat-area-zh-CN)<br><br>* [配置安全控制](https://docs.byteplus.com/docs/byteplus-livesaas/docs-configuring-security-control-zh-CN)<br><br>* [将观众踢出或屏蔽观众的 IP 地址](https://docs.byteplus.com/docs/byteplus-livesaas/docs-kick-out-or-block-zh-CN)<br><br>* [将主播账号关联到直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN)<br><br>* [在数据中心查看数据](https://docs.byteplus.com/docs/byteplus-livesaas/docs-checking-your-streaming-statistics-zh-CN)<br><br>* [查看直播间数据](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics-zh-CN)<br><br>* [查看数据看板](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewing-data-of-a-live-room-zh-CN)<br><br>* [OAuth 2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-oauth-2-0-zh-CN) |
|服务端 OpenAPI |新增部分请求和返回调用结果参数。 |2024\-05\-10 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-release-notes-zh-CN) |
|Web 观播 SDK |发布了 1.3.1 版本。 |2024\-05\-10 |[Web 观播 SDK 更新日志](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2024年4月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|礼物奖励 |优化了礼物奖励功能，包括：<br><br><br>* 调整了默认礼物。<br><br>* 优化了礼物效果。<br><br>* 观众现在可以在直播间处于**直播**、**回放**或**结束**状态时发送礼物，而不仅限于直播期间。 |2024\-04\-29 |[通过礼物奖励主播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-rewarding-hosts-with-gifts-zh-CN) |
|Web 观播 SDK |发布了 1.1.22 版本，优化了礼物奖励功能，包括：<br><br><br>* 调整了默认礼物。<br><br>* 优化了礼物效果。<br><br>* 允许观众在直播间处于**直播**、**回放**或**结束**状态时发送礼物，而不仅限于**直播**状态。 |2024\-04\-29 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布了 1.32.0 版本，新增礼物奖励功能。 |2024\-04\-29 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK |发布了 1.34.0 版本，新增礼物奖励功能。 |2024\-04\-29 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布了 1.34.0 版本。 |2024\-04\-29 |iOS 开播 SDK 发布说明 |
|观看限制 \> 自定义认证登录 |支持在你的 Cookie 中添加`Sign`、`Nickname`、`UserId`和`Timestamp`参数，用于用户登录你自有账号系统后避免二次登录的方案。 |2024\-04\-28 |[Solution B](https://docs.byteplus.com/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions-zh-CN) |
|计费情况 |如需除[BytePlus Live 控制台](https://console.byteplus.com/livesaas/product)所列之外的更多自定义功能和更大套餐，请联系销售代表协助。 |2024\-04\-23 |[订阅计费方法](https://docs.byteplus.com/docs/byteplus-livesaas/docs-billing-methods-zh-CN) |
|数据看板 |支持在数据看板的**用户画像**板块按省份和城市维度展示数据。 |2024\-04\-22 |[Data dashboard](https://docs.byteplus.com/docs/byteplus-livesaas/docs-data-statistics-zh-CN) |
|互动工具菜单 |优化了控制台互动工具菜单的 UI 和体验。 |2024\-04\-18 |* [管理互动区域](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-the-interaction-area-zh-CN)<br><br>* [发送投票](https://docs.byteplus.com/docs/byteplus-livesaas/docs-initiating-a-vote-zh-CN)<br><br>* [发送签到](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-questionnaire-zh-CN)<br><br>* [发送实时抽奖](https://docs.byteplus.com/docs/byteplus-livesaas/docs-sending-a-real-time-lucky-draw-zh-CN)<br><br>* [发送问卷](https://docs.byteplus.com/docs/byteplus-livesaas/docs-send-questionnaire-zh-CN) |
|Android 观播 SDK |发布了 1.31.1 版本，支持优化 SDK 包体大小。 |2024\-04\-15 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK 和 iOS 开播 SDK |发布了 1.33.0 版本，支持优化 SDK 包体大小。 |2024\-04\-15 |* [iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN)<br><br>* iOS 开播 SDK 发布说明 |
|Web 观播 SDK |发布了 1.1.21 版本。 |2024\-04\-09 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2024年3月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|Android 观播 SDK |发布了 1.30.6 版本。 |2024\-03\-28 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 观播 SDK 和 iOS 开播 SDK |发布了 1.32.2 版本。 |2024\-03\-27 |* [iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN)<br><br>* iOS 开播 SDK 发布说明 |
|Android 观播 SDK |发布了 1.30.5 版本。 |2024\-03\-27 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|主/备流 |支持主/备流功能。 |2024\-03\-27 |[管理直播源](https://docs.byteplus.com/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming-zh-CN) |
|敏感词 |在开启**模糊匹配**开关时，支持在评论和昵称匹配敏感词时忽略空格和指定特殊字符。 |2024\-03\-14 |[屏蔽敏感词](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-sensitive-words) |
|轮播 |支持一次性开启或结束所有频道的轮播。 |2024\-03\-14 |[开启轮播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-starting-the-carousel) |
|商品卡片 |支持一次性添加多个商品卡片，导出所有商品卡片信息，并批量更改商品卡片菜单中已添加及待添加商品卡片的跳转图片。 |2024\-03\-14 |[商品卡片管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|回放 |回放最长时长提升至 12 小时。 |2024\-03\-14 |[为什么回放内容不完整？](https://docs.byteplus.com/docs/byteplus-livesaas/docs-playback-faq#45baa631) |
|iOS 观播 SDK 和 iOS 开播 SDK |发布了 1.32.1 版本。 |2024\-03\-11 |* [iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN)<br><br>* iOS 开播 SDK 发布说明 |
|Android 观播 SDK |发布了 1.30.4 版本。 |2024\-03\-11 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |

## 2024年2月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|商品卡片 |支持在商品卡片中添加商品分类。 |2024\-02\-29 |[商品卡片管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream) |
|服务端 OpenAPI |* 新增获取 BytePlus 账号下直播间模版列表的 API 操作。<br><br>* 新增参数 `TagName`。 |2024\-02\-29 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|iOS 开播 SDK |发布 1.32.0 版本，支持修改直播间基础信息、管理商品及其他功能。 |2024\-02\-29 |iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布 1.32.0 版本，支持在竖屏模式下展示直播间描述。 |2024\-02\-29 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 开播 SDK |发布 1.30.0 版本，支持修改直播间基础信息、管理商品及其他功能。 |2024\-02\-29 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布 1.30.3 版本，支持在竖屏模式下展示直播间描述。 |2024\-02\-29 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |

## 2024年1月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|iOS 观播 SDK |发布 1.26.0 版本，包含以下新功能及其他优化：<br><br><br>* 自定义分享地址<br><br>* 倒计时<br><br>* 预约直播流<br><br>* 场馆切换<br><br>* 邀请海报<br><br>* 系统通知<br><br>* 欢迎语<br><br>* 风险提示<br><br>* 全屏水印<br><br>* 问卷<br><br>* 投票<br><br>* 实时抽奖 |2024\-01\-24 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|iOS 开播 SDK |发布 1.26.0 版本。 |2024\-01\-24 |iOS 开播 SDK 发布说明 |
|Android 观播 SDK |发布 1.30.0 版本，包含以下新功能及其他优化：<br><br><br>* 自定义分享地址<br><br>* 倒计时<br><br>* 预约直播流<br><br>* 场馆切换<br><br>* 邀请海报<br><br>* 系统通知<br><br>* 欢迎语<br><br>* 风险提示<br><br>* 全屏水印<br><br>* 问卷<br><br>* 投票<br><br>* 实时抽奖 |2024\-01\-23 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|服务端 OpenAPI |新增获取直播流质量数据的 API 操作。 |2024\-01\-23 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|播放器 Logo |支持在移动设备竖屏模式下展示播放器 Logo。 |2024\-01\-18 |*  |
|Web 观播 SDK |发布 1.1.14 版本，支持在移动设备竖屏模式下展示播放器 Logo。 |2024\-01\-18 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2023年12月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|品牌账号 |支持在配置品牌账号信息时添加外部平台 ID。 |2023\-12\-21 |[添加品牌账号](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account) |
|服务端 OpenAPI |新增更新及获取直播间品牌账号信息的 API 操作。 |2023\-12\-21 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web 观播 SDK |发布 1.1.13 版本，支持在移动设备横屏模式下展示播放器 Logo。 |2023\-12\-14 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2023年11月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|直播间装饰 |支持在直播间配置竖屏封面。 |2023\-11\-30 |[装饰素材规范](https://docs.byteplus.com/docs/byteplus-livesaas/docs-graphics-guide-for-live-streaming) |
|直播间数据 |优化直播间数据的 UI 和逻辑。 |2023\-11\-30 |[数据统计](https://docs.byteplus.com/en/byteplus-livesaas/docs/data-statistics?version=v1.0#3c85b475) |
|服务端 OpenAPI |* 新增获取 BytePlus 账号下直播间数据的 API 操作。<br><br>* 新增参数 `VerticalCoverImageUrl`。 |2023\-11\-30 |[API 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-api-release-notes) |
|Web 观播 SDK |发布 1.1.12 版本，支持在移动设备横屏和竖屏模式下展示不同封面。 |2023\-11\-30 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|敏感词 |* 支持屏蔽新加坡、日本、韩国、印尼和泰国的手机号。<br><br>* 支持敏感词不区分大小写。 |2023\-11\-27 |[屏蔽敏感词](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-sensitive-words) |
|URL 屏蔽 |支持屏蔽评论和昵称中的 URL。 |2023\-11\-27 |[屏蔽 URL](https://docs.byteplus.com/docs/byteplus-livesaas/docs-blocking-urls) |
|竖屏模式 |支持将 BytePlus Live 控制台的配色同步到竖屏模式直播间。 |2023\-11\-16 |[竖屏模式常见问题](https://docs.byteplus.com/docs/byteplus-livesaas/docs-portrait-mode-faqs) |
|投票 |优化观看页的投票样式。 |2023\-11\-16 |[发起投票](https://docs.byteplus.com/docs/byteplus-livesaas/docs-initiating-a-vote) |
|Web 观播 SDK |发布版本 1.1.11。 |2023\-11\-16 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 观播 SDK |发布版本 1.10.9，兼容 Android 14。 |2023\-11\-13 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |

## 2023年10月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|计费情况拆分 |支持计费情况拆分。 |2023\-10\-31 |按组织查看用量和账单 |
|授权 |支持在**授权**模块中管理组织。 |2023\-10\-31 |[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles) |
|Web 观播 SDK |发布版本 1.1.10。 |2023\-10\-16 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Web 观播 SDK |发布版本 1.1.8。 |2023\-10\-10 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |

## 2023年9月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|Android 开播 SDK |发布版本 1.26.0，支持在默认帧率和高帧率模式间切换，并可设置高帧率模式为默认。 |2023\-09\-27 |Android 开播 SDK 发行说明 |

## 2023年8月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|Web 观播 SDK |发布版本 1.1.7。 |2023\-08\-24 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Go 语言 SDK |Go 语言 SDK 首次发布。 |2023\-08\-11 |[服务端 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-server-side_SDK_changelog) |
|Android 开播 SDK 和 iOS 开播 SDK |发布版本 1.25.2，支持删除直播页和观看页上的所有评论。 |2023\-08\-04 |* Android 开播 SDK 发行说明<br><br>* iOS 开播 SDK 发布说明 |
|iOS 观播 SDK |发布版本 1.25.2。 |2023\-08\-04 |[iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Android 观播 SDK |发布版本 1.10.7。 |2023\-08\-04 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|Android 开播 SDK 和 iOS 开播 SDK |发布版本 1.25.1。 |2023\-08\-01 |* Android 开播 SDK 发行说明<br><br>* iOS 开播 SDK 发布说明 |

## 2023年7月

|**功能** |**接口行为** |**发布日期** |**相关文档** |
|---|---|---|---|
|Web 观播 SDK |发布版本 1.1.6。 |2023\-07\-31 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
|Android 开播 SDK |发布版本 1.25.0。 |2023\-07\-20 |Android 开播 SDK 发行说明 |
|Android 观播 SDK |发布版本 1.10.6。 |2023\-07\-20 |[Android 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-android-zh-CN) |
|iOS 开播 SDK 和 iOS 观播 SDK |发布版本 1.25.0。 |2023\-07\-20 |* iOS 开播 SDK 发布说明<br><br>* [iOS 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-viewer-sdk-for-ios-zh-CN) |
|Web 观播 SDK |发布版本 1.1.5。 |2023\-07\-20 |[Web 观播 SDK 发布说明](https://docs.byteplus.com/docs/byteplus-livesaas/docs-changelog-zh-CN) |
