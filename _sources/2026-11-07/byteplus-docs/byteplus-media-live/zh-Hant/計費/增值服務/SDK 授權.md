---
title: "SDK 授權"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-licenses-zh-TW"
---

若要整合 BytePlus MediaLive SDK，您需要取得授權以管理功能存取。本主題詳細說明用於用戶端 SDK 及 Web 端 Player SDK 的可用授權類型及其相應價格，協助您為專案選擇最合適且具成本效益的方案。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需取得授權的詳細資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-sdk-management">Getting your SDK license</a>。</div>


<span id="74ff77ba"></span>
## 價格

<span id="9a8326b3"></span>
### 用戶端 SDK

用戶端 SDK（即 Android、iOS、React Native 及 Flutter 的 SDK）之計費包含以下兩部分。


|類型 |說明 |
|---|---|
|BytePlus MediaLive SDK 授權費用 |BytePlus MediaLive 用戶端 SDK 的授權費用。 |
|[其他雲端服務費用](https://docs.byteplus.com/docs/byteplus-media-live/docs-other-cloud-service-fees-zh-TW) |使用 BytePlus MediaLive SDK 搭配其他產品（如 BytePlus RTC 及 BytePlus Effects SDK）時產生的費用。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">高級授權於2026年1月9日進行升級。自該日期起，若需續約授權，請參考下表以了解各類授權所支援的最新功能。如需了解此次升級的更多資訊，請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/announcement_on_the_upgrade_of_the_client_sdk_premium_license">Announcement on the upgrade of the client SDK premium license</a>。</div>



|授權類型 |有效期限 |取得方式 |價格（美元） |說明 |
|---|---|---|---|---|
|基礎 |1年 |購買 |2,860 |可使用所有基礎功能，例如播放RTMP與HLS串流、使用TCP與TLS協議、啟動或停止播放，以及靜音播放。 |
|||綁定100 TB或以上的直播流量包 |0 ||
|高級 |1年 |購買 |28,600 |可使用所有基礎功能，以及以下功能。如需了解各SDK之間的差異，請參閱[SDK introduction](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)。<br><br><br>* QUIC協議<br><br>* 播放RTM串流<br><br>* 播放CMAF串流（目前僅支援Android SDK）<br><br>* 低延遲FLV拉流<br><br>* SEI訊息傳輸<br><br>* H.265硬體與軟體編碼<br><br>* H.265硬體與軟體解碼<br><br>* H.266軟體解碼（目前僅支援Android SDK）<br><br>* 自適應碼率（ABR）串流<br><br>* 商用DRM（數位版權管理）<br><br>* 超解析度（SR）<br><br>* 影片銳化<br><br>* 主備串流切換 |
|試用 |1個月 |透過控制台申請授權 |0 |試用期間可使用高級授權功能。 |


<span id="0c916d6b"></span>
### Web 端 Player SDK


|授權類型 |有效期限 |取得方式 |價格（美元） |說明 |
|---|---|---|---|---|
|基礎 |1年 |購買 |0 |可使用所有基礎功能，例如拉流與統計。 |
|高級 |1年 |購買 |8,300 |可使用所有基礎功能，以及以下功能：<br><br><br>* [ABR串流](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-adaptive-bitrate-streaming-abr)<br><br>* [自適應緩衝策略](https://docs.byteplus.com/en/docs/byteplus-media-live/adaptive-buffer-strategy)<br><br>* [低延遲FLV拉流](https://docs.byteplus.com/en/docs/byteplus-media-live/achieving_2-3s_live_stream_latency_with_low-latency_FLV_web)<br><br>* [播放RTM串流](https://docs.byteplus.com/en/docs/byteplus-media-live/RTM-Streaming-Integration) |
|試用 |1個月 |透過控制台申請授權 |0 |試用期間可使用高級授權功能。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus亦提供強大且適合AI的影片播放器解決方案，支援AI驅動功能，如影片摘要與物件識別，打造智慧化的客戶端觀看體驗。您可以<a href="https://demo.byteplus.com/aiexp/demo/ai-player">試用Demo</a>，並聯絡我們以獲取更多整合與計費資訊。</div>


<span id="55ec08cd"></span>
## 有效期計算方式

有效期的計算規則取決於操作類型。

<span id="1216336d"></span>
### 升級試用授權

此操作適用於將試用授權升級為基礎或高級授權時。


* **規則：**  升級後新的一年有效期將**立即**開始計算。試用授權剩餘的有效時間將會失效。

* **範例：** 

   * **試用授權開始時間**：2026 年 5 月 10 日 10:00

   * **試用授權到期時間**：2026 年 6 月 10 日 10:00

   * **升級為基礎授權**：2026 年 5 月 30 日 11:00

   * **新基礎授權開始時間**：2026 年 5 月 30 日 11:00

   * **新基礎授權到期時間**：2027 年 5 月 30 日 11:00


<span id="c766097e"></span>
### 續約授權

此操作適用於續約基礎或高級授權時。


* **規則**：有效期將**自現有授權原到期日順延一年**。您剩餘的有效期將被保留。

* **範例**：

   * **原基礎授權開始時間**：2026 年 5 月 12 日 10:00

   * **原基礎授權到期時間**：2027 年 5 月 12 日 10:00

   * **續約基礎授權**：2026 年 10 月 9 日 11:00

   * **新基礎授權到期時間**：2028 年 5 月 12 日 10:00


<span id="be926f57"></span>
## Note


* 授權的有效期僅於綁定至您的 SDK 應用程式後開始計算。試用授權自綁定日起有效期為一個月，基礎或高級授權自綁定日起有效期為一年。

* 您可於基礎或高級授權到期前或到期後進行續約。基礎授權僅能續約為基礎授權，高級授權僅能續約為高級授權。

* 試用授權無法續約。但您可以將其升級為基礎或高級授權。

* Android 應用程式（PackageName）、iOS 應用程式（BundleID）或 Web 應用程式的萬用字元網域，皆不可將基礎、高級或試用授權綁定至多個套件名稱、Bundle ID 或網域。若您有多個應用程式，則必須使用多份授權。

* 若您透過綁定 100 TB 或以上的直播流量包獲取授權，授權的有效期不受資源包影響。換言之，若資源包流量於授權到期前用盡，或您退訂或退款該資源包，只要授權仍在有效期內，您仍可繼續使用 SDK。
