---
title: "Player SDK for Web：发布说明"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-changelog_2-zh-CN"
---

本主题是 Player SDK for Web 的官方变更日志。你可以在此查看所有版本更新的详细记录，包括新增功能、改进和缺陷修复。

|发布日期 |版本 |描述 |
|---|---|---|
|2026 年 10 月 19 日 |2.13.0 |在 [getRTMStats()](https://docs.byteplus.com/player-sdk-for-web-methods-and-properties-1789729567342#veplayerlive-getrtmstats) 和 [getFLVStats()](https://docs.byteplus.com/player-sdk-for-web-methods-and-properties-1789729567342#veplayerlive-getflvstats) 返回的播放信息中新增 SEI 延迟统计信息。由 [SEIDelayStats](https://docs.byteplus.com/player-sdk-for-web-options-1789729565231#seidelaystats) 类型定义的新字段 `delay_s2s` 和 `delay_s2e` 分别上报服务器到服务器延迟和服务器到端延迟。 |
|2026 年 6 月 23 日 |2.12.1 |优化海外地区的播放日志上报。建议中国大陆以外地区的应用升级到此版本。 |
|2026 年 6 月 08 日 |2.12.0 |* 新增在 Tizen 和 webOS 智能电视系统上集成 Player SDK for Web 的支持。创建 SDK 应用时，请在 **Wildcard domain** 字段中输入应用标识符。更多信息，请参见[集成 Player SDK for Web](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1)和[获取 SDK 许可证](https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management)。<br><br>* 启用严格的应用 ID 校验。集成 Player SDK for Web 时，必须同时配置应用 ID 和许可证。<br><br>* 新增 [isRTMSeiSupported](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178?lang=en#isrtmseisupported) 方法，用于检查当前浏览器是否支持从 RTM 流接收 SEI（Supplemental Enhancement Information）消息。<br><br>* 修复 HarmonyOS 上百度浏览器中的播放问题。在此场景下，播放现在默认降级为 M3U8。<br><br>* 调整 RTM 流播放实现，防止 `video` 元素的 `src` 被 HeyTap 浏览器错误拦截。 |
|2026 年 1 月 20 日 |2.11.2 |更新拉取 RTM 流的自动降级机制。目前，播放器仅在以下情况下自动触发降级：<br><br><br>* 浏览器或设备环境不支持 RTM 协议播放，或不支持播放 H.264 编码的 RTM 流。<br><br>* 播放过程中发生解码异常。<br><br><br>对于网络异常导致的 RTM 拉流失败，播放器会触发自动重试（默认为 3 次），不会直接降级。你可以使用 `retryCount` 参数自定义重试次数。 |
|2026 年 1 月 07 日 |2.11.0 |* 为进一步提升 Player SDK for Web 的功能和服务，BytePlus MediaLive 对 Player SDK for Web 启用许可证校验，并更新计费规则。更多信息，请参见 [Player SDK for Web 许可证校验公告](https://docs.byteplus.com/docs/byteplus-media-live/announcement_on_license_validation_for_player_sdk_for_web)。<br><br>* [RTM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#rtm)、[FLV](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#flv) 和 [HLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423?lang=en#hls) 流的 `retryCount` 默认值从 `0` 变更为 `3`。 |
|2025 年 11 月 27 日 |2.10.3 |* 支持通过 npm 导入单个插件以减小包体积。更多信息，请参见[步骤 1：导入依赖](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web_1#ceef554f)。<br><br>* 修复通过 `link` 标签预加载 JS 时导致报错的问题。 |
|2025 年 11 月 12 日 |2.10.2 |* 优化 RTM 和 FLV 流首帧时间的日志上报逻辑，支持上报各阶段的耗时明细。<br><br>* 修复 RTM 拉流错误后降级到其他协议时日志上报停止的问题。<br><br>* 修复 RTM 流断开后调用 [retry](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#retry) 导致重复报错的问题。<br><br>* 修复部分手机上非静音播放被浏览器劫持，导致有音频无视频的问题。 |
|2025 年 10 月 21 日 |2.10.0 |* 传入 `appId`（应用 ID）后支持配置下发。<br><br>* 修复以下场景中封面图无法隐藏的问题：设置 `poster` 参数、禁用自动播放（`autoplay: false`）且播放 RTM 流。 |
|2025 年 9 月 2 日 |2.9.2 |修复 HarmonyOS 中 RTM 流播放期间点击静音或取消静音不生效的问题。 |
|2025 年 8 月 6 日 |2.9.1 |修复 RTM 播放失败触发重复错误事件的问题。此问题仅影响 V2.8.2 到 V2.9.0 版本。 |
|2025 年 8 月 4 日 |2.9.0 |将 hls 插件替换为 hlsjs 插件。 |
|2025 年 7 月 24 日 |2.8.2 |处理不符合规范的 FLV，以缓解屏幕方向显示错误问题。 |
|2025 年 7 月 15 日 |2.8.1 |优化 RTM Jitterbuffer 播放策略，可根据实时网络状况动态调整缓冲时长，平衡延迟和播放流畅度。 |
|2025 年 7 月 8 日 |2.8.0 |* 新增 RTM 中的 SEI 数据支持，用于同步显示评论和标记。<br><br>* 启用商用 DRM（FairPlay、Widevine、PlayReady）以保护视频内容。<br><br>* 改进 RTM 卡顿日志，帮助诊断弱网环境中的问题。<br><br>* 实现 jitter buffer 策略，在较差网络条件下提供更流畅的 RTM 播放。 |
|2025 年 6 月 12 日 |2.7.1 |1. 修复 `userId` 未正确记录日志的问题（仅影响 V2.6.1 到 V2.7.0 版本）。这可确保日志信息准确记录用户标识符，便于问题跟踪和调试。<br><br>2. 修复 `controls` 设置为 `false` 时切换清晰度或线路不生效的问题。这可确保即使控件隐藏，切换清晰度或线路功能也能正常工作。<br><br>3. 优化部分 OPPO 移动设备上的 RTM 流播放。这解决了在特定 OPPO 移动设备上播放 RTM 流时报错的问题，确保更流畅的播放体验。 |
|2025 年 5 月 19 日 |2.7.0 |新增对多协议降级的支持，可指定多个协议 URL 和降级顺序。降级场景包括：<br><br><br>* 根据定义的降级顺序选择支持的协议。<br><br>* RTM 播放失败后按顺序自动降级。<br><br>* 支持基于错误码的失败降级。<br><br>* 支持针对不同协议的自定义降级策略。<br><br><br>更多信息，请参见[拉取 RTM 流](https://docs.byteplus.com/docs/byteplus-media-live/RTM-Streaming-Integration)和[拉取 FLV 流](https://docs.byteplus.com/docs/byteplus-media-live/docs-flv-streaming-integration)。 |
|2025 年 4 月 21 日 |\- |\*\*文档更新：\*\*新增 ABR（Adaptive Bitrate）播放集成指南，可根据实时网络状况动态调整画质，以改善观看体验。 |
|2025 年 3 月 10 日 |2.6.1 |新增支持通过新的 `mediaElement` 参数传入 `video` DOM 元素。这使多个播放器可以共享同一个视频源。 |
|2024 年 10 月 23 日 |2.5.1 |* isMseSupported、isMMSSupported 和 isFLVSupported 方法支持传入字符串类型的编码信息，用于判断浏览器对编解码信息的支持情况。<br><br>* 新增日志上传配置检查。未配置 AppID 时，将在浏览器开发者工具的控制台中报告错误，并使用默认 AppID 进行日志上报。 |
|2024 年 9 月 06 日 |2.5.0 |* 新增功能：<br><br>   * [RTM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1155423#rtm) 配置支持配置暂停播放后的断连时间，以及断连后重新拉流是否无缝。<br><br>   * 优化 LL\-HLS 的实现逻辑。<br><br>   * 新增用于检查 iOS 浏览器是否支持 FLV 格式流播放的方法，并支持在 iOS 17.1 及以上版本浏览器中播放 FLV。请参考 [isFLVSupported](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#isflvsupported) 和 [isMMSSupported](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#ismmssupported) 方法。 |
|2024 年 6 月 12 日 |2.4.0 |* 新增功能：<br><br>   * 播放器在拉取 RTM 流时新增 networkEvaluateInterval（网络评估时间间隔）设置。<br><br>   * 新增 [getRTMNetWorkInfo](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#getrtmnetworkinfo) 方法，支持获取 RTM 拉流的网络评估信息。<br><br>   * 新增 [getRTMStats](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#getrtmstats) 方法，支持获取 RTM 拉流的播放信息。<br><br>   * 新增 [getFLVStats](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-1156178#getflvstats) 方法，支持获取 FLV 拉流的播放信息。<br><br>   * FLV 拉流支持自适应码率（ABR）拉流。<br><br>   * 新增播放器的 playTime 属性，支持获取当前播放时长。 |
|2024 年 2 月 29 日 |2.3.0 |与 1.x 版本相比，2.x 版本有以下改进：<br><br><br>* 改进集成流程并减小包体积。<br><br>* 增强播放器创建流程。<br><br>* 优化播放器配置、方法、属性和事件格式。<br><br><br>> **说明**<br><br><br>> 2.x 版本引入了破坏性变更，且不兼容 Video\-on\-Demand（VOD）。如果要同时播放直播流和 VOD，请改用 SDK 的早期版本。详情请参见 [Player SDK for Web：1.x 版本](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-web-1-x-versions)。<br> |
|2023 年 10 月 16 日 |1.6.3 |* 改进：自 v1.6.3 起，SDK 使用新的地址导入 JS 和 CSS 文件。你无法使用新地址导入早期版本的 JS 和 CSS 文件。请参见[集成 Player SDK for Web](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-player-sdk-for-web)。<br><br>* 修复的问题：<br><br>   * SDK 播放 RTM 流时，部分日志信息无法上传。<br><br>   * 错误消息中的 `userId` 值与通过 [liveLogger](https://docs.byteplus.com/docs/byteplus-media-live/docs-api-reference#liveLogger) 传入的值不一致。 |
|2023 年 5 月 5 日 |1.0.1 |这是 BytePlus MediaLive Player SDK for Web 的首次发布。 |
