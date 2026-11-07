---
title: "OpenAPI 概述"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-openapi-overview-zh-TW"
---

本主題列出了 BytePlus MediaLive 提供的所有 OpenAPI 端點。

<span id="a2c83367"></span>
## 網域


|API |說明 |
|---|---|
|[CreateDomainV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn) |呼叫 `CreateDomainV2` API 以新增一個或多個推流或拉流網域名稱。 |
|[UpdateDomainVhost](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatedomainvhost) |呼叫 `UpdateDomainVhost` API 以變更與網域名稱關聯的網域命名空間。 |
|[DeleteDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletedomain-2023) |呼叫 `DeleteDomain` 介面以刪除網域名稱。 |
|[DisableDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-disabledomain-2023) |呼叫 `DisableDomain` API 以停用網域名稱。網域名稱停用後，MediaLive 服務中的網域狀態將從 `0-Enabled` 變更為 `2-Disabled`。 |
|[EnableDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enabledomain-2023) |呼叫 `EnableDomain` API 以啟用已停用的網域名稱。網域名稱啟用後，MediaLive 服務中的網域狀態將從 `2-Disabled` 變更為 `0-Enabled`。 |
|[DescribeDomain](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describedomain-2023) |呼叫 `DescribeDomain` API 以查詢指定網域名稱的資訊，包括網域命名空間、CNAME 地址及網域狀態等。 |
|[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) |呼叫 `ListDomainDetail` API 以查詢帳戶下網域名稱的相關資訊。你可以依網域狀態、網域類型及其他維度篩選查詢結果。 |


<span id="58822a39"></span>
## 存取控制


|API |說明 |
|---|---|
|[UpdateClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateclusterratelimit) |呼叫 `UpdateClusterRateLimit` API 以新增或修改拉流請求的頻率限制。 |
|[DeleteClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteclusterratelimit) |呼叫 `DeleteClusterRateLimit` API 以刪除拉流請求的頻率限制。 |
|[DescribeClusterRateLimit](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclusterratelimit) |呼叫 `DescribeClusterRateLimit` API 以查詢拉流請求的頻率限制。 |
|[UpdateUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateuseragentaccessrule) |呼叫 `UpdateUserAgentAccessRule` API 以新增或更新 User\-Agent 限制規則。 |
|[DescribeUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeuseragentaccessrule) |呼叫 `DescribeUserAgentAccessRule` API 以查詢 User\-Agent 限制規則。 |
|[DeleteUserAgentAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteuseragentaccessrule_1) |呼叫 `DeleteUserAgentAccessRule` API 以刪除 User\-Agent 限制規則。 |
|[UpdateIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateipaccessrule) |呼叫 `UpdateIPAccessRule` API 以為指定網域名稱設定 IP 阻擋清單或允許清單。 |
|[DescribeIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeipaccessrule) |呼叫 `DescribeIPAccessRule` API 以查詢已建立的 IP 存取規則設定。 |
|[DeleteIPAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteipaccessrule) |呼叫 `DeleteIPAccessRule` API 以刪除指定網域名稱的 IP 阻擋清單或允許清單。 |
|[UpdateRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateregionaccessrule) |呼叫 `UpdateRegionAccessRule` API 以為指定網域名稱建立地理限制。 |
|[DescribeRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeregionaccessrule) |呼叫 `DescribeRegionAccessRule` API 以查詢指定網域名稱的地理限制。 |
|[DeleteRegionAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteregionaccessrule) |呼叫 `DeleteRegionAccessRule` API 以刪除指定網域名稱的地理限制。 |
|[UpdateFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateformataccessrule) |呼叫 `UpdateFormatAccessRule` API 以建立協議限制。 |
|[DescribeFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeformataccessrule) |呼叫 `DescribeFormatAccessRule` API 以查詢協議限制。 |
|[DeleteFormatAccessRule](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteformataccessrule) |呼叫 `DeleteFormatAccessRule` API 以刪除協議限制。 |
|[UpdateAuthKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateauthkey-2023) |呼叫 `UpdateAuthKey` API 以新增或更新推流與拉流地址的 URL 驗證設定。使用此 API 更新設定時，所有驗證參數都會被更新。 |
|[DescribeAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeauth-2023) |呼叫 `DescribeAuth` API 以查詢符合條件的 URL 驗證設定。 |
|[UpdateReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatereferer-2023) |呼叫 `UpdateReferer` API 以建立網域層級（Vhost + Domain）或應用層級（Vhost + App）的 Referer 阻擋清單或允許清單設定。 |
|[DeleteReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletereferer-2023) |呼叫 `DeleteReferer` API 以刪除 Referer 阻擋清單或允許清單設定。 |
|[DescribeReferer](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describereferer-2023) |呼叫 `UpdateReferer` API 以取得 Referer 阻擋清單或允許清單設定。 |
|[UpdateRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcerewrite) |設定源站地址重寫規則。原始地址重寫功能可根據預先定義的匹配規則，從新的地址獲取串流。詳情請參見[原始地址重寫](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite)。 |
|[DescribeRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dakt2mfojk) |查詢原始地址重寫規則。原始地址重寫功能可根據預先定義的匹配規則，從新的地址獲取串流。詳情請參見[原始地址重寫](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite)。 |
|[DeleteRelaySourceRewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-3nf0nln2b2) |刪除原始地址重寫規則。原始地址重寫功能可根據預先定義的匹配規則，從新的地址獲取串流。詳情請參見[原始地址重寫](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite)。 |
|[UpdateRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateremoteauth-2023) |調用`UpdateRemoteAuth` API，為拉流域名創建遠端驗證配置。創建成功後，使用者的拉流請求將會發送至指定的驗證伺服器，由該伺服器驗證使用者的拉流請求。 |
|[DescribeRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeremoteauth-2023) |調用`DescribeRemoteAuth` API，查詢拉流域名的遠端驗證配置。 |
|[DeleteRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleteremoteauth-2023) |調用`DeleteRemoteAuth` API，刪除已新增的遠端驗證配置。 |
|[ListVhostRemoteAuth](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostremoteauth-2023) |調用`ListVhostRemoteAuth` API，查詢該 Vhost 下所有拉流域名的遠端驗證配置。 |


<span id="29c6707d"></span>
## 延遲控制


|API |說明 |
|---|---|
|[UpdateLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig) |調用`UpdateLatencyConfig` API，通過配置伺服器 GOP 快取，降低指定拉流域名下串流的直播延遲。 |
|[DescribeLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig) |調用`DescribeLatencyConfig` API，查詢 GOP 的伺服器快取配置。 |
|[DeleteLatencyConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletelatencyconfig) |調用`DeleteLatencyConfig` API，刪除已建立的伺服器 GOP 快取配置。 |


<span id="ba30e946"></span>
## 封裝


|API |說明 |
|---|---|
|[UpdateHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig) |調用`UpdateHLSConfig` API，為指定域名空間新增或更新 HLS 配置，包括分段大小與分段數量，以有效降低延遲並提升直播相容性。在 HTTP Live Streaming（HLS）及低延遲 HLS（LL\-HLS）中，直播串流會被切分為 Transport Stream（TS）。每個 TS 都有對應的 URL，使用 HLS 協議拉直播流時，地址會不斷變化。 |
|[DescribeHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig) |調用`DescribeHLSConfig` API，查詢指定域名空間的 HLS 配置，包括分段大小、分段數量等。 |
|[DeleteHLSConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig) |調用`DeleteHLSConfig` API，將指定域名空間的 HLS 配置恢復為預設設定，包括分段大小、分段數量等。 |
|[UpdateCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig) |在 Dynamic Adaptive Streaming over HTTP（DASH）及低延遲 DASH（LL\-DASH）中，直播串流會被切分為 Common Media Application Format（CMAF）分段。調用`UpdateCMAFConfig` API，可調整分段時長與分段數量設定，以有效降低延遲並提升指定域名空間（Vhost）下直播的相容性。 |
|[DescribeCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig) |調用`DescribeCMAFConfig` API，查詢指定域名空間下串流的分段時長與分段數量設定。 |
|[DeleteCMAFConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/deletecmafconfig) |調用`DeleteCMAFConfig` API，刪除指定域名空間（Vhost）下串流的 DASH 設定，包括分段時長與分段數量。 |


<span id="418dfe8b"></span>
## 標頭


|API |說明 |
|---|---|
|[EnableHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-enablehttpheaderconfig) |調用`EnableHTTPHeaderConfig` API，啟用或停用 HTTP 標頭配置。 |
|[DeleteHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletehttpheaderconfig) |調用`DeleteHTTPHeaderConfig` API，刪除已透過 UpdateHTTPHeaderConfig 新增的指定域名 HTTP 標頭配置。 |
|[DescribeHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig) |呼叫 `DescribeHTTPHeaderConfig` API 以查詢指定網域名稱的 HTTP 標頭設定。 |
|[UpdateHTTPHeaderConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatehttpheaderconfig) |呼叫 `UpdateHTTPHeaderConfig` API，可在邊緣伺服器回應給用戶端時新增額外的 HTTP 標頭，或於回源任務期間，在發送至第三方源站伺服器的請求中新增額外的 HTTP 標頭。 |


<span id="20ae8318"></span>
## 憑證


|API |說明 |
|---|---|
|[CreateCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcert-2023) |呼叫 `CreateCert` API，將憑證新增或更新至 MediaLive，以便日後綁定至網域名稱並啟用 HTTPS。 |
|[DeleteCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecert-2023) |呼叫 `DeleteCert` API 以刪除已上傳至 MediaLive 的憑證。 |
|[BindCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-bindcert-2023) |呼叫 `BindCert` API，將已上傳的 HTTPS 憑證綁定至網域名稱，並啟用該網域名稱的 HTTPS 安全傳輸。 |
|[UnbindCert](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-unbindcert-2023) |呼叫 `UnbindCert` API 以解除憑證與網域名稱的綁定。 |
|[ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) |呼叫 `ListCertV2` API 以檢視當前帳號下的憑證清單。 |
|[DescribeCertDetailSecretV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdetailsecretv2-2023) |呼叫 `DescribeCertDetailSecretV2` API，透過憑證 ID 或憑證鏈 ID 檢視憑證詳細資訊。 |


<span id="015ee63e"></span>
## 加密


|API |說明 |
|---|---|
|[DescribeLicenseDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelicensedrm) |擷取 DRM 授權。播放器使用該授權來解密 DRM 加密的直播串流。 |
|[DescribeCertDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm) |擷取 FairPlay 憑證。播放器會結合 DRM 授權與該憑證，在 Apple 裝置上解密 DRM 加密的直播串流。 |
|[UpdateEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencryptdrm) |上傳 DRM API 金鑰及／或 FairPlay 憑證，或更新現有憑證或金鑰。 |
|[DescribeEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_2) |呼叫 `DescribeEncryptDRM` API 以檢視已設定的 DRM 憑證管理平台存取金鑰與 FairPlay 憑證資訊。 |
|[BindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1) |呼叫 `BindEncryptDRM` API，為直播串流新增或更新 DRM 加密設定。 |
|[UnBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_3) |呼叫 `UnBindEncryptDRM` API 以刪除已建立的加密設定。 |
|[ListBindEncryptDRM](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_4) |呼叫 `ListBindEncryptDRM` API，以查詢指定網域命名空間及應用名稱的加密設定，或檢視指定網域命名空間下的所有加密設定。 |
|[UpdateEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateencrypthls) |呼叫 `UpdateEncryptHLS` API，新增或更新用於 HLS 標準加密的自管金鑰管理服務位址，以及直播視訊串流的金鑰更新週期。 |
|[GetHLSEncryptDataKey](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-gethlsencryptdatakey) |呼叫 `GetHLSEncryptDataKey` API，以查詢由直播視訊服務伺服器產生、用於 HLS 標準加密的金鑰。 |
|[DescribeEncryptHLS](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeencrypthls) |呼叫 `DescribeEncryptHLS` API，查詢用於 HLS 標準加密的自管金鑰管理服務位址及金鑰更新週期。 |


<span id="7ed100d3"></span>
## 串流地址


|API |說明 |
|---|---|
|[GeneratePushURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023) |呼叫 `GeneratePushURL` API，以產生指定串流的推流位址。 |
|[GeneratePlayURL](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023) |呼叫 `GeneratePlayURL` API，以產生指定串流的拉流位址。 |


<span id="72ec9417"></span>
## 串流


|API |說明 |
|---|---|
|[DescribeLiveStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023) |呼叫 `DescribeLiveStreamGroupByPage` API，分頁檢索進行中的直播串流資訊。 |
|[DescribeClosedStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclosedstreaminfobypage-2023) |呼叫 `DescribeClosedStreamInfoByPage` API，分頁檢索已結束的直播串流資訊。 |
|[DescribeForbiddenStreamInfoByPage](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeforbiddenstreaminfobypage-2023) |呼叫 `DescribeForbiddenStreamGroupByPage` API，分頁檢索已停用的串流資訊。 |
|[ForbidStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-forbidstream-2023) |呼叫 `ForbidStream` API 以停用直播串流。 |
|[KillStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-killstream-2023) |呼叫 `KillStream` API 以終止推送直播串流。 |
|[DescribeLiveStreamState](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivestreamstate-2023) |呼叫 `DescribeLiveStreamState` API 以查詢直播串流狀態。 |
|[ResumeStream](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-resumestream-2023) |呼叫 `ResumeStream` 以恢復已停用串流的推送。 |


<span id="d8d7e0bb"></span>
## 轉碼


|API |說明 |
|---|---|
|[CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023) |呼叫 `CreateTranscodePreset` API 以建立轉碼設定，系統將根據您的轉碼設定，對符合條件的直播串流進行即時轉碼。 |
|[UpdateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1) |呼叫 `UpdateTranscodePreset` API 以更新已新增的轉碼設定。若非必要參數未填寫，對應的參數設定將不會變更。 |
|[DeleteTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetranscodepreset-2023) |呼叫 `DeleteTranscodePreset` API 以刪除已建立的轉碼設定。 |
|[ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) |呼叫 `ListVhostTransCodePreset` API 以查詢轉碼設定清單。 |
|[ListCommonTransPresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023) |呼叫 `ListCommonTransPresetDetail` API 以查詢預設轉碼設定的詳細資訊。 |
|[CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023) |呼叫 `CreateTranscodePresetBatch` API 以批次建立 ABR 子串流轉碼設定。 |
|[DeleteTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023) |呼叫 `DeleteTranscodePresetBatch` API 以批次刪除 ABR 子串流的轉碼設定。 |


<span id="3193eddd"></span>
## 錄製


|API |說明 |
|---|---|
|[CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023) |呼叫 `CreateRecordPresetV2` API 以建立錄製設定。系統將根據您的錄製設定，對符合條件的直播串流進行錄製。 |
|[UpdateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023) |呼叫 `UpdateRecordPresetV2` API 以更新已建立的錄製設定。 |
|[ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) |呼叫 `ListVhostRecordPresetV2` API 以查詢指定 Vhost 下所有錄製設定，包含 Vhost、Vhost + App、Vhost + App + Stream 三個層級的所有設定。 |
|[DescribeRecordTaskFileHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023) |查詢指定網域命名空間先前錄製的資訊，例如錄製時長、檔案格式、開始時間與結束時間。進行中的錄製將不會被查詢。 |
|[DeleteRecordPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterecordpreset-2023) |呼叫 `DeleteRecordPreset` API 以刪除已建立的錄製設定。 |
|[CreatePullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreatePullRecordTask) |呼叫 `CreatePullRecordTask` API 以建立在指定時間開始與結束的直播拉流錄製任務。建立成功後，直播期間可錄製任意時長的單一直播串流並保存為影片檔案。 |
|[StopPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppullrecordtask) |呼叫 `StopPullRecordTask` API 以停止尚未開始或正在進行的錄製任務。停止正在進行的錄製任務將會產生錄製檔案。 |
|[ListPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask) |此 API 用於查詢當前帳戶下建立的直播錄製任務清單，並支援依分頁、網域名稱、應用名稱、串流名稱等條件組合查詢。透過此 API，您可取得任務的具體資訊，例如錄製時段、任務狀態等，有助於追蹤錄製進度、監控任務狀態並支援後續資源管理作業。 |
|[GetPullRecordTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetPullRecordTask) |呼叫 `GetPullRecordTask` API 以查詢單一直播錄製任務的資訊。 |


<span id="6ae274dd"></span>
## 截圖擷取


|API |說明 |
|---|---|
|[CreateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/createsnapshotpresetv2) |新增截圖設定，當直播串流落在截圖設定的有效範圍內時，將進行截圖並保存。 |
|[UpdateSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2) |更新已新增的截圖設定。 |
|[DeleteSnapshotPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesnapshotpreset-2023) |呼叫 `DeleteRecordPreset` API 以刪除已建立的截圖設定。 |
|[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2) |取得指定網域命名空間下所有截圖設定資訊。 |
|[DescribeCDNSnapshotHistory](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023) |呼叫 `DescribeCDNSnapshotHistory` API 以查詢直播串流的截圖檔案資訊。 |


<span id="6ad08614"></span>
## 源站拉流


|API |說明 |
|---|---|
|[UpdateRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcev3-2023) |呼叫 `UpdateRelaySourceV3` API 以新增或更新播放觸發的源站拉流設定。播放觸發的源站拉流指的是只有在有觀眾觀看時才會觸發源站拉流，這可以節省源站伺服器的頻寬資源，並提升系統的整體效率。 |
|[DeleteRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterelaysourcev3-2023) |調用 `DeleteRelaySourceV3` API 以刪除播放觸發的源站拉流配置。 |
|[DescribeRelaySourceV3](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerelaysourcev3-2023) |調用 `DescribeRelaySourceV3` API 查詢播放觸發的源站拉流配置。 |


<span id="8f1b5c50"></span>
## 時移


|API |說明 |
|---|---|
|[CreateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createtimeshiftpresetv2-2023) |調用 `CreateTimeShiftPresetV2` API 創建直播時移配置。配置直播時移後，使用者可在直播過程中觀看先前已播出的內容。 |
|[UpdateTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetimeshiftpresetv2-2023) |調用 `UpdateTimeShiftPresetV2` API 更新已創建的時移配置。 |
|[DeleteTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetimeshiftpresetv2-2023) |調用 `DeleteTimeShiftPresetV2` API 刪除已創建的時移配置。 |
|[ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) |調用 `ListTimeShiftPresetV2` API 查詢指定域名空間下所有 appName 的時移配置。 |


<span id="dd457b9d"></span>
## 浮水印


|API |說明 |
|---|---|
|[CreateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023) |調用 `CreateWatermarkPreset` API 創建轉碼流的浮水印配置。 |
|[DeleteWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletewatermarkpreset-2023) |調用 `DeleteWatermarkPreset` API 刪除現有的浮水印配置。 |
|[UpdateWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023) |調用 `UpdateWatermarkPreset` API 更新現有的浮水印配置。 |
|[ListWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023) |調用 `ListWatermarkPreset` API 查詢指定 AppName 或 StreamName 的浮水印配置。 |
|[ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) |調用 `ListVhostWatermarkPreset` API 查詢指定域名空間下所有浮水印配置。 |


<span id="c5b62a66"></span>
## AI 配音與字幕


|API |說明 |
|---|---|
|[CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) |呼叫 `CreateSpeechTask` API 以建立 AI 配音任務。任務建立後，於從 `StartTime` 到 `EndTime` 的轉播時段開始推流時，任務會自動拉取直播流進行 AI 配音處理，並將處理後的直播流推送至指定的推流地址。例如，你可以使用 OBS 開啟直播，透過 AI 配音任務處理直播流，然後將處理後的內容在 TikTok 上進行直播。如需更多資訊，請參閱 [AI 配音](https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation)。 |
|[SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) |呼叫 `SearchSpeechTask` API 以搜尋符合特定條件的 AI 配音任務。 |
|[GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) |呼叫 `GetSpeechTask` API 以查詢特定 AI 配音任務的資訊。 |
|[UpdateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask) |呼叫 `UpdateSpeechTask` API 以更新 AI 配音任務的功能開關狀態。此 API 常用於直播過程中根據需求開啟或關閉翻譯功能。 |
|[DeleteSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask) |呼叫 `DeleteSpeechTask` API 以刪除不再需要的 AI 配音任務。若任務正在執行，MediaLive 會先停止任務再進行刪除。 |
|[RestartSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask) |呼叫 `RestartSpeechTask` API 以重新啟動正在執行或啟動中的 AI 配音任務。 |
|[GetSpeechConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechConfig) |呼叫 `GetSpeechConfig` API 以取得目前帳戶可用的 AI 配音配置，包括支援的字型與語言。 |
|[CreateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createsubtitletranscodepreset-2023) |呼叫 `CreateSubtitleTranscodePreset` API 以新增字幕配置。配置新增後，觀眾可透過拉取與字幕配置關聯的轉碼流，或拉取加上字幕後綴的原始流，觀看字幕效果。如需更多資訊，請參閱 [字幕配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-manage-subtitle-configuration)。 |
|[DeleteSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletesubtitletranscodepreset-2023) |呼叫 `DeleteSubtitleTranscodePreset` API 以刪除已新增的字幕配置。 |
|[UpdateSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatesubtitletranscodepreset-2023) |呼叫 `UpdateSubtitleTranscodePreset` API 以更新已新增的字幕配置。 |
|[ListVhostSubtitleTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostsubtitletranscodepreset-2023) |呼叫 `ListVhostSubtitleTranscodePreset` API 以查詢特定網域命名空間下的所有字幕配置。 |
|[GetSubtitleTranscodePresetConfig](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSubtitleTranscodePresetConfig) |呼叫 `GetSubtitleTranscodePresetConfig` API 以取得目前帳戶在字幕配置的 AI 配音模式下可用的字型與語言。 |
|[DescribeSubtitleTranscodePresetDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeSubtitleTranscodePresetDetail) |呼叫 `DescribeSubtitleTranscodePresetDetail` API 以查詢特定字幕配置的詳細資訊。 |


<span id="0cfcd58b"></span>
## 輪播任務


|API |說明 |
|---|---|
|[UpdateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecarouseltask) |調用 `UpdateCarouselTask` API 修改指定輪播任務配置，調整播放內容、播放規則或時間範圍，系統將於更新後依新配置執行輪播任務。 |
|[ListCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask) |調用 `ListCarouselTask` API 獲取所有當前輪播任務列表，包括任務 ID、狀態及創建時間，可用於任務管理及批次查詢。 |
|[DeleteCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask) |調用 `DeleteCarouselTask` API 刪除指定輪播任務。任務刪除後，系統將停止播放該任務的所有輪播內容並釋放相關資源。 |
|[CreateCarouselTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask) |調用 `CreateCarouselTask` API 創建輪播任務。直播過程中，視頻直播伺服器將依任務配置按設定順序循環播放指定視頻內容。 |
|[GetCarouselDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail) |調用 `GetCarouselDetail` API 查詢指定輪播任務的詳細資訊，包括播放狀態、視頻列表及當前播放進度，便於管理與監控任務執行情況。 |


<span id="3f683d7a"></span>
## 中繼


|API |說明 |
|---|---|
|[CreatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023) |調用 `CreatePullToPushTask` API 創建拉流轉推任務，從直播源或點播視頻拉取內容。 |
|[ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) |調用 `ListPullToPushTask` API 分頁查詢拉流轉推任務列表，支持依任務名稱模糊搜尋。 |
|[StopPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-stoppulltopushtask-2023) |調用 `StopPullToPushTask` API 停止狀態未終止的拉流轉推任務 |
|[DeletePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushtask-2023) |調用 `DeletePullToPushTask` API 刪除已創建的拉流轉推任務。 |
|[UpdatePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023) |呼叫 `UpdatePullToPushTask` API 以更新中繼任務的資訊。 |
|[CreatePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023) |呼叫 `CreatePullToPushGroup` API 以建立中繼任務群組並綁定至專案，透過配置群組可根據專案管理子帳戶權限。 |
|[DeletePullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletepulltopushgroup-2023) |呼叫 `DeletePullToPushGroup` API 以刪除群組名稱。 |
|[ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) |呼叫 `ListPullToPushGroup` API 以查詢群組名稱列表。 |
|[ListPullToPushTaskV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtaskv2-2023) |呼叫 `ListPullToPushTaskV2` API 以分頁查詢中繼任務列表，並支援依任務名稱模糊搜尋。 |
|[ContinuePullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/continuepulltopushtask) |呼叫 `ContinuePullToPushTask` API 以重新啟動處於停用狀態的中繼任務。 |
|[RelaunchPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relaunchpulltopushtask) |呼叫 `RelaunchPullToPushTask` API 以重新啟動處於停用狀態的中繼任務。 |


<span id="a506533a"></span>
## VQScore


|API |說明 |
|---|---|
|[CreateLiveVideoQualityAnalysisTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivevideoqualityanalysistask-2023) |呼叫 `CreateLiveVideoQualityAnalysisTask` API 以建立指定時長的影片品質分析任務。該任務會根據你設定的間隔取得每個分析點的即時位元率，並評分分析點的畫面品質。 |
|[ListLiveVideoQualityAnalysisTasks](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listlivevideoqualityanalysistasks-2023) |呼叫 `ListLiveVideoQualityAnalysisTasks` API 以查詢影片品質分析任務資訊列表。 |
|[GetLiveVideoQualityAnalysisTaskDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getlivevideoqualityanalysistaskdetail-2023) |呼叫 `GetLiveVideoQualityAnalysisTaskDetail` API 以查詢單一影片品質分析任務的詳細資訊，包括在指定分析點取得的影片位元率與品質分析分數。 |
|[DeleteLiveVideoQualityAnalysisTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletelivevideoqualityanalysistask-2023) |呼叫 `DeleteLiveVideoQualityAnalysisTask` API 以刪除影片品質分析任務。你可以刪除已完成及進行中的任務。 |


<span id="489d6079"></span>
## 用量查詢


|API |說明 |
|---|---|
|[DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata) |呼叫 `DescribeLiveTrafficData` API 以查詢指定直播網域在指定時間範圍內的流量使用情況。此外，包含推流網域的上行流量資料與拉流網域的下行流量資料。 |
|[DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) |呼叫 `DescribeLiveBandwidthData` API 以查詢指定直播網域在指定時間範圍內的頻寬使用情況，包括推流網域的上行峰值頻寬及拉流網域的下行峰值頻寬。 |
|[DescribeLiveSnapshotData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesnapshotdata) |呼叫 `DescribeLiveSnapshotData` API 以取得指定直播網域在指定時間範圍內由截圖功能產生的快照數量。 |
|[DescribeLiveRecordData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliverecorddata) |呼叫 `DescribeLiveRecordData` API 以查詢指定直播網域在指定時間範圍內的錄製使用情況，包括最大同時錄製數。 |
|[DescribeLivePullToPushData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushdata) |呼叫 `DescribeLivePullToPushData` API 以查詢群組在指定時間範圍內產生的所有中繼任務的時長使用情況。 |
|[DescribeLivePullToPushBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepulltopushbandwidthdata) |呼叫 `DescribeLivePullToPushBandwidthData` API 以查詢指定時間範圍內產生的中繼任務頻寬使用情況。 |
|[DescribeLiveTranscodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetranscodedata) |呼叫 `DescribeLiveTranscodeData` API 以查詢指定直播網域在指定時間範圍內的轉碼時長使用情況。 |
|[DescribeLiveStorageSpaceData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestoragespacedata) |呼叫 `DescribeLiveStorageSpaceData` API 以查詢指定時間範圍內直播時移功能每日的儲存空間使用情況。 |
|[DescribeLiveP95PeakBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata) |呼叫 `DescribeLiveP95PeakBandwidthData` API 以查詢指定直播網域在指定時間範圍內的第95百分位峰值頻寬使用情況，包括推流網域的上行第95百分位峰值頻寬及拉流網域的下行第95百分位峰值頻寬。 |
|[DescribeLiveASRDurationData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveasrdurationdata) |調用 `DescribeLiveASRDurationData` API 以查詢指定時間範圍內 AI 語音轉字幕的時長。 |


<span id="06af5ead"></span>
## 日誌


|API |說明 |
|---|---|
|[DescribeLiveLogData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivelogdata) |調用 `DescribeLiveLogData` API 以查詢該域名產生的日誌檔案資訊。 |


<span id="87d29bad"></span>
## 統計與分析


|API |說明 |
|---|---|
|[DescribeLivePushStreamInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreaminfodata) |調用 `DescribeLivePushStreamInfoData` API 以查詢推流資訊及斷流原因。 |
|[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata) |調用 `DescribeLiveISPData` API 以獲取為 BytePlus MediaLive 提供網路接入服務的網路服務供應商（ISP）識別碼。獲取 ISP 識別碼後，可於支援基於 ISP 查詢的 API 中，查詢特定 ISP 的維度資料。 |
|[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) |調用 `DescribeLiveRegionData` API 以獲取 MediaLive 覆蓋區域的識別碼。獲取區域識別碼後，可於支援按區域查詢資料的 API 中，查詢特定區域的資料。 |
|[DescribeLiveSourceTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata) |調用 `DescribeLiveSourceTrafficData` API 以查詢指定拉流域名或源流於指定時間範圍內產生的回源流量及頻寬監控資料。 |
|[DescribeLiveStreamCountData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata) |獲取指定推流、回源拉流或轉碼流於特定時間範圍內的峰值數量。 |
|[DescribeLivePushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreammetrics) |調用 `DescribeLivePushStreamMetrics` API 以查詢指定時間範圍內單路推流的音視頻幀率、碼率等監控資料，用於評估直播流的健康狀態。 |
|[DescribeLivePlayStatusCodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata) |調用 `DescribeLivePlayStatusCodeData` API 以查詢指定時間範圍內對域名發起的請求（包括推流、拉流及回源請求）的狀態碼佔比。 |
|[DescribeLiveStreamSessionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata) |調用 `DescribeLiveStreamSessionData` API 以查詢指定域名下所有或指定直播流於指定時間範圍內的請求數及最大在線觀看人數。 |
|[DescribeLiveSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics) |調用 `DescribeLiveSourceStreamMetrics` API 以查詢指定時間範圍內單路回源流的音視頻幀率、碼率等監控資料，用於評估回源流的健康狀態。 |
|[DescribeCDNTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdntrafficdata) |調用 `DescribeCDNTrafficData` API 以查詢指定時間範圍內存取直播錄製檔案及快照時所產生的 CDN 流量。 |
|[DescribeLiveBatchPushStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023) |調用 `DescribeLiveBatchPushStreamMetrics` API 以查詢某個推流域名下單路或多路推流的統計資料，包括幀率、碼率、展示時間戳（PTS）等。可利用這些統計資料監控推流會話的健康狀態。可查詢已刪除域名的資料。 |
|[DescribeLiveTranscodeInfoData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetranscodeinfodata-2023) |調用 `DescribeLiveTranscodeInfoData` API 以查詢指定時間範圍內，特定直播域名或直播流的轉碼任務 ID、流名稱、轉碼字尾、轉碼開始及結束時間等詳細資料。 |
|[DescribeLiveTopPlayData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivetopplaydata-2023) |調用 `DescribeLiveTopPlayData` API 以查詢指定時間範圍內，熱門直播流或熱門域名的流量及頻寬明細。 |
|[DescribeLiveBatchStreamTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtrafficdata-2023) |調用 `DescribeLiveBatchStreamTrafficData` API 以查詢指定時間範圍內的上下行流量及其詳細資料。 |
|[DescribeLiveBatchStreamTranscodeData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtranscodedata-2023) |調用 `DescribeLiveBatchStreamTranscodeData` API，以查詢指定網域下所有串流在特定時間範圍內的轉碼資料。資料包含轉碼時長、解析度等級以及編碼方式等指標。 |
|[DescribeLiveEdgeStatData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023) |調用 `DescribeLiveEdgeStatData` 介面，以查詢指定協議、ISP、區域及時間範圍下，直播串流產生的上下行流量、上下行峰值頻寬，以及請求數等資料。 |
|[DescribeLiveBatchSourceStreamMetrics](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics) |取得特定網域下所有或指定原始拉流串流在特定時間範圍內的監控資料，例如音視頻的幀率與碼率。可利用監控資料評估原始拉流串流的健康狀態。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">可取得已刪除網域產生的歷史原始拉流串流資料。</div><br> |


<span id="c7ad7b5e"></span>
## 回調


|API |說明 |
|---|---|
|[UpdateCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatecallback-2023) |調用 `UpdateCallback` API，以新增或更新串流推送、錄製與截圖事件的回調配置。 |
|[DescribeCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecallback-2023) |調用 `DescribeCallback` API，以獲取應用程式的回調配置。 |
|[DeleteCallback](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecallback-2023) |調用 `DeleteCallback` API，以刪除回調配置。 |
|[DescribeLiveCallbackData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata) |此 API 可查詢與直播相關的回調紀錄，包括事件類型、狀態、請求與回應資料。有助於排查回調異常，並驗證回調是否成功送達。 |


<span id="57297203"></span>
## 儲存空間


|API |說明 |
|---|---|
|[ListStorageSpace](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespace) |調用 `ListStorageSpace` API，以查詢帳戶下所有可用儲存空間的清單。可在配置錄製與截圖設定時參考此清單。 |
|[ListStorageSpaceDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-liststoragespacedetail) |調用 `ListStorageSpaceDetail` API，以查詢帳戶下指定儲存空間的詳細資訊。 |
