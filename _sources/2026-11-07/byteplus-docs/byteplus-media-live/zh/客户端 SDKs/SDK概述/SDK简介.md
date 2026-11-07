---
title: "SDK简介"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction-zh-CN"
---

BytePlus MediaLive 提供适用于 Android、iOS、React Native 和 Flutter 的拉流 SDK。

BytePlus MediaLive SDK 提供三种类型的许可证：基础版、高级版和试用版。


* **基础版许可证**：适用于仅需基础拉流功能的直播场景，如体育赛事、娱乐、电商和教育。

* **高级版许可证**：适用于既需基础拉流功能，又需高级功能（如自适应码率（ABR）流、超分辨率（SR）和[实时媒体（RTM）](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction-to-real-time-media)）的直播场景。更多信息请参见[Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-zh-CN#b1681aaf)。

* **试用版许可证**：适用于测试等试用场景。包含所有 BytePlus MediaLive SDK 的全部功能。


<span id="2a8ebace"></span>
## 功能

拉流 SDK 支持的功能如下。


|功能 ||接口行为 |Android & iOS |Flutter |React Native |
|---|---|---|---|---|---|
|回放格式 |FLV |支持播放延迟为 6 至 10 秒的 FLV 流。 |支持 |支持 |支持 |
||FLV（低延迟） |支持播放延迟为 2 至 3 秒的 FLV 流。 |仅高级版或试用版许可证支持 |不支持 |不支持 |
||HLS |支持播放 HLS 流。 |支持 |支持 |支持 |
||RTM |支持播放高并发、低延迟的 RTM 流。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支持纯音频或纯视频流。</div><br> |仅高级版或试用版许可证支持 |支持 |支持 |
||RTMP |支持播放 RTMP 流。 |支持 |支持 |支持 |
||CMAF |支持播放 CMAF 流。 |* iOS：不支持<br><br>* Android：仅高级版或试用版许可证支持 |* iOS：不支持<br><br>* Android：支持 |* iOS：不支持<br><br>* Android：支持 |
|传输协议 |TCP |支持 TCP 协议。 |支持 |支持 |支持 |
||QUIC |支持 QUIC 协议，有效提升视频传输效率。 |仅高级版或试用版许可证支持 |支持 |支持 |
||TLS |支持 TLS 协议。 |支持 |支持 |支持 |
||HTTP 2.0 |支持 HTTP 2.0 协议。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">不支持 RTM 流。</div><br> |支持 |支持 |支持 |
||HTTP header |请求视频资源时支持自定义 HTTP header。 |支持 |不支持 |支持 |
|视频解码 |H.264 硬解 |支持 H.264 硬解。 |支持 |支持 |支持 |
||H.264 软解 |支持 H.264 软解。 |支持 |支持 |支持 |
||H.265 硬解 |支持 H.265 硬解。通过设备 blocklist 和智能回放策略等功能优化 H.265 硬解的使用，在配合 H.265 转码时降低直播流成本并提升转码档位。 |仅高级版或试用版许可证支持 |仅高级版或试用版许可证支持 |仅高级版或试用版许可证支持 |
||H.265 软解 |支持 H.265 软解，提高低端设备兼容性，帮助降低直播流成本并提升观看体验。 |仅高级版或试用版许可证支持 |仅高级版或试用版许可证支持 |仅高级版或试用版许可证支持 |
||H.265 降级 |当 H.265 硬解失败时，播放器会自动降级，优先尝试切换到配置的 H.264 备流，若无备流则尝试使用 H.265 软解。 |支持 |支持 |支持 |
||H.266 软解 |支持 H.266 软解，可提升低端设备的兼容性，帮助降低直播流成本并增强观看体验。 |* iOS：不支持<br><br>* Android：仅高级版或试用版许可支持 |不支持 |不支持 |
||AAC\-HE |支持 AAC\-HE 音频编码格式。 |支持 |支持 |支持 |
||AAC\-LC |支持 AAC\-LC 音频编码格式。 |支持 |支持 |支持 |
|回放控制 |开始与停止回放 |支持开始或停止回放。 |支持 |支持 |支持 |
||暂停与恢复回放 |支持暂停或恢复回放。 |支持 |支持 |支持 |
||获取当前回放状态 |支持获取当前回放状态。 |支持 |支持 |支持 |
||手动切换清晰度 |支持手动切换不同清晰度等级。 |支持 |不支持 |支持 |
||设置播放器缓冲时间 |播放器会预先下载一定量的数据，以确保回放的连续性和流畅性。缓冲时间越长，播放器在网络波动或延迟时越能保持视频或音频回放不中断。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需实现该功能，请联系 BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">技术支持</a>。</div><br> |支持 |不支持 |支持 |
|视频特效 |配置渲染视图 |配置渲染视图以显示播放器的视频。 |支持 |支持 |支持 |
||屏幕填充模式 |支持调整回放屏幕的填充模式。 |支持 |支持 |支持 |
||屏幕旋转角度 |支持配置回放屏幕的旋转角度，可顺时针旋转至 0°、90°、180° 和 270°。 |支持 |支持 |支持 |
||镜像 |支持配置回放屏幕的镜像模式，如水平和垂直镜像。 |支持 |不支持 |支持 |
||画中画回放 |通过最小化播放器窗口并将其置于界面角落，观众可在观看直播流的同时浏览其他内容或打开其他应用，提升用户体验。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如需实现该功能，请联系 BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">技术支持</a>。</div><br> |支持 |不支持 |支持 |
||SDR（标准动态范围）视频回放 |支持 SDR 视频回放。 |支持 |支持 |支持 |
||超分辨率 |超分辨率指从观测到的低分辨率图像重建高分辨率图像的过程。实时移动端超分辨率利用算法技术，在设备上实时重建低分辨率帧，生成高分辨率帧并显示于屏幕。此功能提升视频内容的细节和对比度，优化整体清晰度和观看体验。 |仅高级版或试用版许可支持 |不支持 |仅高级版或试用版许可支持 |
||视频锐化 |视频锐化是一种用于增强视频图像清晰度和细节的图像处理技术。通过锐化处理，视频中的边缘和细节更加突出，使画面更清晰、更鲜明。 |仅高级版或试用版许可支持 |不支持 |支持 |
|美声音效 |音量调节 |支持调整回放音量。 |支持 |支持 |支持 |
||静音 |支持静音回放。 |支持 |支持 |支持 |
||获取静音状态 |支持获取当前静音状态。 |支持 |支持 |支持 |
||后台音频回放 |应用切换至后台时，音频可继续播放。 |支持 |支持 |支持 |
||纯音频回放 |支持播放纯音频。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅适用于 FLV 流。</div><br> |支持 |支持 |支持 |
||立体声音频 |支持播放立体声音频。 |支持 |支持 |支持 |
|回放策略 |回放失败重试 |如因网络或其他问题导致直播流中断，播放器会尝试重试。 |支持 |支持 |支持 |
||本地 DNS 预解析 |启用本地 DNS 预解析可优化播放器的启动时间。 |支持 |支持 |支持 |
||配置一个或多个回放地址 |支持配置一个或多个回放地址。通过配置多个回放地址，可实现依赖多路流的功能，例如 ABR 流和主备流切换。 |支持 |支持 |支持 |
||ABR 流 |ABR 是一种流技术，通过一系列算法策略动态切换不同质量的媒体流。该技术可适应网络带宽变化，帮助防止直播流卡顿，并提升回放质量和观感体验。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅适用于 FLV 流。</div><br> |仅高级版或试用版授权支持 |支持 |支持 |
||IP 地址流 |支持直接使用回放域名的 IP 地址进行流播放，以减少首帧时间。 |支持 |不支持 |支持 |
||主备流切换 |当主流地址失效或出现回放错误时，播放器会自动切换到备流地址。当备流地址失效或出现回放错误时，播放器会切回主流地址。 |仅高级版或试用版授权支持 |支持 |支持 |
||多实例 |支持在同一界面添加多个播放器进行同时回放。 |支持 |支持 |支持 |
||动态追帧 |直播流过程中，视频流可能因网络波动或其他因素出现延迟或卡顿。动态追帧技术通过调整帧播放速度或跳过部分帧，使回放与直播流同步，降低延迟。 |支持 |支持 |支持 |
||即时回放优化 |减少首帧时间，实现即时回放。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">要实现此功能，请联系 BytePlus MediaLive <a href="https://console.byteplus.com/workorder/create">技术支持</a>。</div><br> |支持 |不支持 |支持 |
|附加功能 |截图 |支持在播放器内截取当前直播流画面。 |支持 |不支持 |支持 |
||SEI 消息接收 |SEI 在音视频流中嵌入文本数据，由主播发送，观众接收，实现文本与音视频内容的精准同步。 |仅高级版或试用版授权支持 |支持 |支持 |
||配置事件监听器 |通过配置事件监听器，可接收播放器内部状态信息，包括回放状态、错误信息、音视频首帧回调及周期性统计数据。 |支持 |支持 |支持 |
||订阅音视频数据 |订阅接收解码后的音视频帧，进行自定义处理或渲染。 |支持 |不支持 |不支持 |
|视频安全 |商用 DRM（数字版权管理） |支持播放 DRM 加密流，提供 Widevine、FairPlay、PlayReady 等 DRM 方案。 |仅高级版或试用版授权支持 |不支持 |不支持 |
|质量保障 |日志上报 |支持上报 SDK 日志，收集并分析与音视频直播流的回放追踪数据。 |支持 |支持 |支持 |


<span id="db2409b9"></span>
## 使用 SDK

下表列出了集成各 SDK 时可能有用的主题：


|**SDK** |**主题** |
|---|---|
|拉流 SDK for Android |* [集成 Android 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-android-zh-CN)<br><br>* [初始化 Android 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-android-zh-CN)<br><br>* [Player SDK for Android: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-2)<br><br>* [Player SDK for Android: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-2)<br><br>* [Player SDK for Android: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-android-api-overview) |
|拉流 SDK for iOS |* [集成 iOS 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-ios-zh-CN)<br><br>* [初始化 iOS 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-ios-zh-CN)<br><br>* [Player SDK for iOS: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-basic-features-3)<br><br>* [Player SDK for iOS: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-implementing-advanced-features-3)<br><br>* [Player SDK for iOS: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-ios-api-overview) |
|拉流 SDK for React Native |* [集成 React Native 的拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-integrating-the-broadcast-and-player-sdks-for-rn-zh-CN)<br><br>* [初始化 React Native 拉流 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-initializing-for-rn-zh-CN)<br><br>* [Player SDK for React Native: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-basic-features)<br><br>* [Player SDK for React Native: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/docs-rnplayer-advanced-features)<br><br>* [Player SDK for React Native: Overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-player-sdk-for-rn-api-overview) |
|拉流 SDK for Flutter |* [Integrating the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* [Initializing the Player SDK for Flutter](https://docs.byteplus.com/docs/byteplus-media-live/initializing-the-player-sdk-for-flutter)<br><br>* [Player SDK for Flutter: Basic features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-basic-features)<br><br>* [Player SDK for Flutter: Advanced features](https://docs.byteplus.com/docs/byteplus-media-live/player-sdk-for-flutter-advanced-features) |


<span id="f202fd8c"></span>
## 术语表

有关 SDK 相关术语的解释，请参见[Glossary](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary)。
