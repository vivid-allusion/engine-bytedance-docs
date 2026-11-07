---
title: "SDK 许可"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-licenses-zh-CN"
---

要集成 BytePlus MediaLive SDK，需要许可证来管理功能访问权限。本主题详细介绍了客户端 SDK 和 Web 拉流 SDK 可用的许可证类型及其对应的价格，帮助你为项目选择最合适且具成本效益的选项。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">关于如何获取许可证的更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management">Getting your SDK license</a>。</div>


<span id="74ff77ba"></span>
## 价格

<span id="9a8326b3"></span>
### 客户端 SDK

客户端 SDK（即 Android、iOS、React Native 和 Flutter 的 SDK）的计费情况包括以下两部分。


|类型 |接口行为 |
|---|---|
|BytePlus MediaLive SDK 许可费用 |BytePlus MediaLive 客户端 SDK 的许可费用。 |
|[其他云服务费用](https://docs.byteplus.com/docs/byteplus-media-live/docs-processing-of-overdue-payments-zh-CN) |使用 BytePlus MediaLive SDK 与其他产品（如火山引擎实时音视频和 BytePlus Effects SDK）结合时产生的费用。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">高级许可证已于2026年1月9日升级。从该日期起，如需续订许可证，请参考下表了解各类许可证支持的最新功能。有关此次升级的更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-media-live/announcement_on_the_upgrade_of_the_client_sdk_premium_license-zh-CN">关于客户端 SDK 高级版 License 升级的公告</a>。</div>



|许可证类型 |有效期 |获取方式 |刊例价（美元） |接口行为 |
|---|---|---|---|---|
|基础版 |1年 |购买 |2,860 |可使用所有基础功能，例如播放RTMP和HLS流、支持TCP和TLS协议、启动或停止回放，以及静音回放。 |
|||绑定100 TB及以上直播流量包 |0 ||
|高级版 |1年 |购买 |28,600 |可使用所有基础功能，以及以下功能。关于各SDK之间的差异，详见[SDK introduction](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)。<br><br><br>* QUIC协议<br><br>* 播放RTM流<br><br>* 播放CMAF流（目前仅适用于Android SDK）<br><br>* 低延迟FLV拉流<br><br>* SEI消息传输<br><br>* H.265硬件和软编码<br><br>* H.265硬件和软解解码<br><br>* H.266软解（目前仅适用于Android SDK）<br><br>* 自适应码率流<br><br>* 商业DRM（数字版权管理）<br><br>* 超分辨率（SR）<br><br>* 视频锐化<br><br>* 主/备流切换 |
|试用版 |1个月 |通过控制台申请许可证 |0 |试用期间可使用高级许可证功能。 |


<span id="0c916d6b"></span>
### Web 拉流 SDK


|许可证类型 |有效期 |获取方式 |刊例价（美元） |接口行为 |
|---|---|---|---|---|
|基础版 |1年 |购买 |0 |可使用所有基础功能，例如拉流和统计。 |
|高级版 |1年 |购买 |8,300 |可使用所有基础功能，以及以下功能：<br><br><br>* [自适应码率流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr)<br><br>* [自适应缓冲策略](https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy)<br><br>* [低延迟FLV拉流](https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web)<br><br>* [播放RTM流](https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration) |
|试用版 |1个月 |通过控制台申请许可证 |0 |试用期间可使用高级许可证功能。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus还提供强大的、适用于AI的播放器解决方案，支持视频摘要、目标识别等AI功能，实现智能的客户端观看体验。您可以<a href="https://demo.byteplus.com/aiexp/demo/ai-player">体验演示</a>，并联系我们获取更多关于集成和计费情况的信息。</div>


<span id="55ec08cd"></span>
## 有效期计算

有效期的计算规则取决于操作类型。

<span id="1216336d"></span>
### 升级试用许可证

该操作适用于将试用许可证升级为基础或高级许可证。


* **规则：** 新的一年有效期将在升级后**立即**开始。试用许可证剩余的时间将会失效。

* **示例：** 

   * **试用许可证开始时间**：2026 年 5 月 10 日 10:00

   * **试用许可证到期时间**：2026 年 6 月 10 日 10:00

   * **升级为基础许可证**：2026 年 5 月 30 日 11:00

   * **新基础许可证开始时间**：2026 年 5 月 30 日 11:00

   * **新基础许可证到期时间**：2027 年 5 月 30 日 11:00


<span id="c766097e"></span>
### 续订许可证

该操作适用于续订基础或高级许可证。


* **规则**：有效期通过**在当前许可证原到期日基础上延长一年**来延长。剩余有效期将被保留。

* **示例**：

   * **原基础许可证开始时间**：2026 年 5 月 12 日 10:00

   * **原基础许可证到期时间**：2027 年 5 月 12 日 10:00

   * **续订基础许可证**：2026 年 10 月 9 日 11:00

   * **新基础许可证到期时间**：2028 年 5 月 12 日 10:00


<span id="be926f57"></span>
## Note


* 许可证的有效期仅在绑定到你的 SDK 应用后开始计算。试用许可证自绑定日期起有效期为一个月，基础或高级许可证自绑定日期起有效期为一年。

* 你可以在基础或高级许可证到期前或到期后进行续订。基础许可证只能续订为基础许可证，高级许可证只能续订为高级许可证。

* 试用许可证无法续订。你可以将其升级为基础或高级许可证。

* 你无法将基础、高级或试用许可证绑定到多个 Android 应用的包名（PackageName）、iOS 应用的 BundleID 或 Web 应用的通配符域名。如果你有多个应用，则必须使用多个许可证。

* 若通过绑定 100 TB 或更大直播流量包获得许可证，许可证的有效期不会受资源包影响。换句话说，如果资源包中的流量在许可证到期前用完，或你退订或退款该资源包，只要许可证仍然有效，你仍可继续使用 SDK。
